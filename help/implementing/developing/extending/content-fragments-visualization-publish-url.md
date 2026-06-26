---
title: ビジュアルコンテンツフラグメント – 公開URLを使用した配信
description: 公開URLを使用して、ビジュアルコンテンツフラグメントを配信します。
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: 733e7a8c497fcffdfadd22c2abd3323d35d54e3e
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# ビジュアルコンテンツフラグメント – 公開URLを使用した配信 {#visual-content-fragments-deliver-with-the-publish-url}

添付されたHTML テンプレートを含むモデルに基づくコンテンツフラグメントが公開されると、そのフラグメントのレンダリングされたHTMLは、次の構造を持つURLのAdobe Experience Manager（AEM）as a Cloud Service パブリッシュ層を介して利用できるようになります。

```html
https://publish-p<programId>-e<envId>.adobeaemcloud.com/adobe/stable/previewtemplates/contentFragments/<templateId>/<fragmentId>/<variation>.html
```

このURLは、任意のweb コンテキストに埋め込むことができる&#x200B;*自己完結型のHTML ドキュメント* （インライン CSSと構造を含む）を返します。

## テクニックの埋め込み – 概要 {#embedding-techniques-overview}

ホストページ上のビジュアルコンテンツフラグメントからHTMLを使用するには、3つの異なるアプローチがあります。 それぞれ、スタイルの分離、レイアウト動作、アクセシビリティ、複雑さなどの特徴が異なります。

| | インライン要素 | iframe | カスタム要素+ シャドウ DOM |
|--- |--- |--- |--- |
| メカニズム | `fetch()`のURLを入力し、`innerHTML`経由で`<div>`に応答HTMLを挿入します | `<iframe src="publishURL">` | カスタム要素を定義し、HTMLを`fetch()`し、添付されたShadow DOM ルートに挿入します |
| スタイルの分離 | なし – フラグメント CSSがホストページにリークし、ホスト CSSがフラグメントに影響する | フル – 個別のブラウジングコンテキスト、完全なCSS分離 | 強力 – シャドウ DOM境界ブロックはCSS カスケードをホストします。フラグメントスタイルはカプセル化されたままです |
| レイアウト参加 | フル – コンテンツは通常のドキュメントフローの一部で、flexbox/grid/containerのサイズに対応します | なし – iframeに固定ディメンションがあります。明示的な`width`/`height`またはJS ベースの自動サイズ変更が必要です | フル – カスタム要素は、他のDOM要素と同様に、ホスト文書の通常のフローに参加します |
| アクセシビリティ （a11y） | ベスト – コンテンツはメインのDOM ツリーにあり、スクリーンリーダーと支援テクノロジーによって完全にトラバース可能です | 中程度：個別の閲覧コンテキストは、スクリーンリーダーのナビゲーションを混乱させる可能性があります。`title`属性が必要です | 良い – コンテンツは同じドキュメント内にあります。シャドウ DOMは最新の支援テクノロジーでトラバース可能です |
| SEO | 悪い – JS `fetch()`を介して読み込まれたコンテンツは、ほとんどのweb クローラーでインデックスが作成されていません | 悪い – iframe コンテンツは通常、親ページコンテキストではインデックス化されません | 悪い – インラインと同じ。JSで取得されたコンテンツはクロールできません |
| JavaScript runtime | 共有：同じウィンドウ/ドキュメントコンテキスト。フラグメントに`<script>`個のタグが含まれる場合、スクリプトが競合するリスクがあります | 分離 – ウィンドウのコンテキストを分離します。競合のリスクはありません | Shared – 同じウィンドウのコンテキストだがDOMのスコープが設定されている場合、シャドウルート内のスクリプトはホストコンテキストで実行される |
| クロスオリジンサポート | 公開URLにCORS ヘッダーが必要です（サービスはこれらのヘッダーを設定します） | ネイティブに機能 – IFRAMEはCORSを使用せずにクロスオリジンのコンテンツを読み込みます | パブリッシュ URL （インラインと同じ）にCORS ヘッダーが必要です |
| 実装の複雑さ | 最小限 – JSの数行 | Trivial — JSは必要ありません。純粋なHTML | 低 – カスタム要素の定義に20行のJSを含め、ページ全体で再利用 |
| 最適な用途 | プロトタイピング、信頼できる同一生成元コンテンツ、レイアウト統合が重要でCSSの競合が管理可能なコンテキスト | クイック埋め込み、サンドボックス化されたコンテンツ、CORSが利用できないクロスオリジンのシナリオ、完全に分離する必要があるコンテンツ | 実稼動環境での使用：分離、レイアウトへの参加、およびアクセシビリティのバランス調整（AEM コアコンポーネントと外部サイトに推奨） |

### インライン要素（fetch + innerHTML） {#inline-element-fetch-and-innerhtml}

最も単純なアプローチ：

1. 公開URLを取得
1. HTMLをコンテナ要素に挿入する

インライン要素の埋め込みの例：

```html
<div id="cf-container"></div>
<script>
  fetch("<publish-url>")
    .then(r => r.ok ? r.text() : Promise.reject(r.status))
    .then(html => {
      document.getElementById("cf-container").innerHTML = html;
    })
    .catch(err => console.error("Failed to load fragment", err));
</script>
```

使用するタイミング：

* 迅速なプロトタイピングや概念実証のページ
* ホストページとフラグメントスタイルの両方を制御する同一オリジンのコンテキスト
* スタイルのカプセル化よりもレイアウトの柔軟性が重要な場合

>[!CAUTION]
>
>**CSS コリジョン リスク**
>
>フラグメントのインラインスタイル（その`<style>` ブロック、フォントフェイス宣言、および要素セレクターを含む）は、ホストページのカスケードに結合されます。
>
>これにより、両方の方向で意図しないスタイルの上書きが発生する可能性があります。
>
>この手法を使用するのは、このような競合を許容できる場合か、積極的に管理できる場合のみです。

### iframe {#iframe}

公開URLを`<iframe>`の`src`として直接読み込みます。 JavaScriptは必要ありません。

iframe埋め込みの例：

```iframe
<iframe
  src="<publish-url>"
  title="Content Fragment Preview"
  width="100%"
  height="600"
  frameborder="0"
  style="border: none;"
></iframe>
```

また、iframeのサイズを自動的に変更することもできます（これはオプションです）。

コンテンツの高さに合わせてiframeのサイズを動的に変更するには、`postMessage` パターンまたは適切なライブラリを使用します。

軽量化アプローチの例を次に示します。

```iframe
<iframe id="cf-iframe" src="<publish-url>" title="Content Fragment Preview"
  width="100%" frameborder="0" style="border:none; overflow:hidden;"
  onload="this.style.height = this.contentDocument.documentElement.scrollHeight + 'px';"
></iframe>
```

>[!WARNING]
>
>上記の`onload`自動サイズ変更アプローチは、**same-origin** iframeでのみ機能します。
>
>**クロスオリジン**&#x200B;公開URLの場合、`postMessage` ベースのソリューションまたは固定高さを設定する必要があります。

使用するタイミング：

* Edge Delivery Services埋め込みブロック（デフォルトの統合 – 以下の節を参照）
* CSS/JSの完全な分離が重要なコンテキスト
* CORSが設定されていないクロスオリジン埋め込み
* 迅速なゼロコード統合（URLを貼り付けるだけです）

### カスタム要素+ シャドウ DOM （推奨） {#custom-element-and-shadow-dom-recommended}

パブリッシュ URLを取得し、カプセル化されたシャドウ DOM ルートにHTMLを挿入する再利用可能な`<cf-visualization>` カスタム要素を定義します。

この要素は次の機能を提供します。

* シャドウ DOMの分離
   * フラグメントのマークアップとスタイルはシャドウルートにカプセル化され、ホストページのCSS カスケードとの競合を防ぎます。
* インラインレイアウトへの参加
   * レンダリングされたコンテンツは、ホストドキュメントの通常のフローに参加し、コンテナサイズとフレックスボックス/グリッドコンテキストに対応します。手動ディメンション管理は必要ありません。
* 単一のブラウジングコンテキスト
   * セカンダリドキュメントのコンテキストは作成されません。フラグメントコンテンツは、ページのJavaScript ランタイムを共有し、支援テクノロジーによって完全にトラバーサル可能です。
* 最小限のオーバーヘッド
   * 1回の`fetch`呼び出しでは、パブリッシュ層から事前レンダリングされたHTMLが取得されます。 クライアントサイドのレンダリングフレームワークは必要ありません。

>[!IMPORTANT]
>
>これは、実稼動環境での使用に推奨されるアプローチであり、AEM コアコンポーネントで使用される手法です。

カスタム要素を定義するには、ページごとに次のスクリプトを1回含めます。 ページ上のすべての`<cf-visualization>` インスタンスでは、次の定義が使用されます。

```javascript
<script>
  class CfVisualization extends HTMLElement {
    connectedCallback() {
      const src = this.getAttribute("src");
      if (!src) return;

      const shadow = this.attachShadow({ mode: "open" });

      fetch(src)
        .then((r) => (r.ok ? r.text() : Promise.reject(r.status)))
        .then((html) => {
          shadow.innerHTML = html;
        })
        .catch((err) => {
          console.error("cf-visualization: failed to load", src, err);
        });
    }
  }

  if (!customElements.get("cf-visualization")) {
    customElements.define("cf-visualization", CfVisualization);
  }
</script>
```

カスタム要素を使用するには：

```html
<cf-visualization src="<publish-url>"></cf-visualization>
```

使用するタイミング：

* コアコンポーネントを使用したAEM Sites ページ（これが組み込みのビヘイビアー）
* クリーンで再利用可能な統合を必要とする外部/サードパーティのweb サイト
* スタイルの分離とレイアウトフローへの参加の両方が必要なコンテキスト

## Edge Delivery Servicesとの統合（埋め込みブロック） {#integration-with-edge-services-embed-block}

Edge Delivery Servicesでは、公開URLは&#x200B;**[埋め込みブロック &#x200B;](https://sidekick-library--aem-block-collection--adobe.aem.page/tools/sidekick/library.html?plugin=blocks&path=/block-collection/embed&index=0)**&#x200B;を通じて消費され、`<iframe>`としてレンダリングされます。

1. 埋め込みブロックがプロジェクトに存在することを確認します。

   EDS プロジェクトに埋め込みブロックが含まれていない場合は、aem-block-collection リポジトリからコピーします。

   ```cmdline
   # From the aem-block-collection repo, copy blocks/embed/ into your project's blocks/ directory
   cp -r aem-block-collection/blocks/embed/ your-eds-project/blocks/embed/
   ```

1. ドキュメント作成エディター（Edge Delivery Services）で埋め込みを作成する

   文書オーサリングでは、ブロックは表として表されます。 ビジュアルコンテンツフラグメント埋め込みを追加するには：

   | 埋める |
   |--- |
   | （公開URLをハイパーリンクとしてペースト） |

   または、プロジェクトまたはSidekickがブロックライブラリ内の埋め込みブロックで設定されている場合は、スラッシュメニューを使用して埋め込みブロックを挿入し、パブリッシュ URLをブロックコンテンツに貼り付けることができます。

1. 結果

   埋め込みブロックは、`<iframe>`内の公開URLをレンダリングします。 フラグメントコンテンツは、EDS ページレイアウト内で完全なCSS分離で読み込まれます。

## 統合 – コアコンポーネントを備えたAEM Sites {#integration-aem-sites-with-core-components}

コンテンツフラグメントコアコンポーネント （`core/wcm/components/contentfragment/v1/contentfragment`）には、[顧客要素+ シャドウ DOM](#custom-element-and-shadow-dom-recommended)手法を使用したビジュアルコンテンツフラグメントのレンダリングが組み込まれています。

仕組み：

* 作成者モード：

  コンポーネントの`displayMode`が`vcf`に設定されている場合、オーサリング clientlib （`vcfRenderer.js`）はプレビューAPIからフラグメント HTMLを取得し、オーサリングキャンバスでインラインでレンダリングします。

  オーサープレビューエンドポイントの例を次に示します。

  ```html
  GET /adobe/sites/cf/fragments/{fragmentId}/preview?templateId={templateId}&variation={variation}
  ```

* 公開モード：

  公開されたページ （`wcmmode.disabled`）で、HTL テンプレートは、公開URLから取得したインラインスクリプトをレンダリングし、HTMLをShadow DOM ルートに挿入します。

  コアコンポーネントのビジュアルコンテンツフラグメント（templates.html）の例：

  ```html
  <div class="cmp-contentfragment cmp-contentfragment--vcf"
     data-cmp-contentfragment-id="{fragmentId}"
     data-cmp-contentfragment-vcf-template="{templateId}"
     data-cmp-contentfragment-variation="{variation}">
    <!-- Only rendered when wcmmode.disabled (publish) -->
    <div data-vcf-url="{vcfPublishUrl}" class="cmp-contentfragment__vcf-loader" style="display:none"></div>
    <script>
        (function() {
            var script = document.currentScript;
            var loader = script.previousElementSibling;
            var el = script.parentElement;
            if (!el || !loader) return;
            var url = loader.dataset.vcfUrl;
            if (!url) return;
            loader.remove();
            var shadow = el.attachShadow({ mode: "open" });
            var body = document.createElement("body");
            body.style.display = "none";
            shadow.appendChild(body);
            fetch(url)
                .then(function(r) { return r.ok ? r.text() : Promise.reject(r.status); })
                .then(function(html) {
                    body.innerHTML = html;
                    body.style.display = "";
                });
        })();
    </script>
  </div>
  ```

  URL形式を公開：

  Sling モデル （`ContentFragmentImpl`）は、次のパターンを使用して公開URLを構築します。

  ```html
  /adobe/experimental/previewtemplates-expires-20260301/contentFragments/{templateId}/{fragmentId}/{variation}.html
  ```

  この相対URLは、実行時にパブリッシュホストに対して解決されます。

## 外部サイトとの統合 {#integration-with-external-sites}

AEM以外のweb サイトの場合は、[Customer Element + Shadow DOM](#custom-element-and-shadow-dom-recommended)手法を使用します。 これにより、フレームワークに依存することなく、クリーンで宣言的な統合を実現できます。

例えば、次のようになります。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Product Page</title>
</head>
<body>
  <h1>Product Details</h1>
  <p>Some host-page content here...</p>

  <!-- Embed the Content Fragment visualization -->
  <cf-visualization
    src="https://publish-p12345-e67890.adobeaemcloud.com/adobe/experimental/previewtemplates-expires-20260301/contentFragments/product_template/abc-123/master.html"
  ></cf-visualization>

  <p>More host-page content below the fragment...</p>

  <!-- Custom Element definition (include once) -->
  <script>
    class CfVisualization extends HTMLElement {
      connectedCallback() {
        const src = this.getAttribute("src");
        if (!src) return;
        const shadow = this.attachShadow({ mode: "open" });
        fetch(src)
          .then(r => r.ok ? r.text() : Promise.reject(r.status))
          .then(html => { shadow.innerHTML = html; })
          .catch(err => console.error("cf-visualization: failed to load", src, err));
      }
    }
    if (!customElements.get("cf-visualization")) {
      customElements.define("cf-visualization", CfVisualization);
    }
  </script>
</body>
</html>
```

>[!NOTE]
>
>異なる`src`URLを持つ複数の`<cf-visualization>`要素を同じページに配置できます。 カスタム要素の定義は、1回だけ含める必要があります。

## CORSとセキュリティの考慮事項 {#cors-and-security-considerations}

| 懸念材料 | 詳細 |
|--- |--- |
| CORS | コンテンツフラグメント視覚化サービスは、設定可能な許可されたオリジンを使用して、`/adobe/**` パス上のCORSを設定します。<br> インライン要素（取得+ innerHTML） [&#128279;](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#inline-element-fetch-and-innerhtml) 1および[顧客要素+ シャドウ DOM](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#custom-element-and-shadow-dom-recommended)手法（`fetch()`を使用）では、ホストページの生成元を許可リストに配置する必要があります。 <br>[iFrame](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#iframe)手法にはCORSは必要ありません。 |
| CSP/X-Frame-Options | サービスは、公開されたHTMLに`Content-Security-Policy`または`X-Frame-Options`個のヘッダーを設定しません。 CDNまたはDispatcherがこれらのヘッダーを追加する場合は、ホストのオリジンからフレーム化（[iFrame](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#iframe)の場合）または`fetch()` アクセス権（インライン/シャドウ DOMの場合）を許可していることを確認します。 |
| コンテンツの信頼 | 公開されたHTMLは、サービスによって管理される[Handlebars テンプレート &#x200B;](/help/implementing/developing/extending/content-fragments-visualization-templates.md)を使用して、オーサリングされたコンテンツフラグメントデータから事前にレンダリングされます。 これには、ユーザー生成スクリプトは含まれません。 ただし、他のinnerHTML インジェクションと同様に、ソースオリジンを信頼してください。 |

### 適切な手法の選択 {#choose-the-appropriate-technique}

適切な手法を選択する際に役立つ意思決定ガイドとして、次の手順を使用します。

| シナリオ | ソリューション |
|--- |--- |
| JavaScript不要、完全な分離が必要ですか？ | Iframe |
| スタイルの分離にレイアウトフローの参加が必要ですか？ | カスタム要素+ シャドウ DOM （推奨） |
| 最速のプロトタイプ、同一生成元、CSSの競合は許容されますか？ | インライン要素 |
| Edge Delivery Servicesに埋め込む？ | 埋め込みブロック（フードの下のiframe） |
| AEM Sites ページに埋め込む | コアコンポーネント（Shadow DOM、組み込み） |


## その他のリソース {#additional-resources}

次のその他のリソースを使用できます。

* [AEM コンテンツフラグメントのドキュメント](/help/sites-cloud/administering/content-fragments/overview.md)

<!-- CQDOC-23650 - add link when docs are stable; not experimental -->

<!--
* [Content Fragment Visualization Templates APIs (experimental)](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/cvt/#)
-->
