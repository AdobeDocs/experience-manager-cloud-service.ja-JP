---
title: 高度な URL 設定
description: 製品ページとカテゴリページの URL をカスタマイズする方法について説明します。このカスタマイズにより、実装で URL を検索エンジン向けに最適化し、検出を促進できます。
sub-product: Commerce
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: 92cb864f71b5e98bf98519a3f5be6469802be0e4
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 40%

---

# 高度な URL 設定 {#url}

>[!NOTE]
>
> 検索エンジン最適化（SEO）は、多くのマーケティング担当者にとって重要な課題となっています。その結果、多くの Adobe Experience Manager（AEM）as a Cloud Service プロジェクトで SEO の懸念に対処する必要があります。詳しくは、[SEO と URL 管理のベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html?lang=ja)を参照してください。

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、製品ページとカテゴリページの URL をカスタマイズする高度な設定を提供します。多くの実装では、検索エンジン最適化（SEO）用にこれらの URL をカスタマイズします。次のビデオでは、`UrlProvider` サービスと [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)の機能を設定して、製品ページとカテゴリページの URL をカスタマイズする方法について詳しく説明します。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

次の手順で `UrlProvider` SEO 要件と必要に応じたサービスでは、プロジェクトで _CIF URL プロバイダーの設定_.

>[!NOTE]
>
> AEM CIF コアコンポーネントのリリース 2.0.0 以降、URL プロバイダー設定では、1.x リリースで知られている自由テキスト設定可能な形式の代わりに、事前に定義された URL 形式のみが提供されます。 さらに、セレクターを使用して URL 内のデータを渡すことはなくなり、代わりにサフィックスが使用されます。

### 製品ページの URL 形式 {#product}

製品ページの URL を設定するもので、次のオプションをサポートしています。

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（デフォルト）
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)の場合は次のとおりです。

* `{{page}}` は `/content/venia/us/en/products/product-page` に置き換えられます
* `{{sku}}` は製品の SKU（例：`VP09`）に置き換えられます
* `{{url_key}}` は製品の `url_key` プロパティ（例：`lenora-crochet-shorts`）に置き換えられます
* `{{url_path}}` は製品の `url_path`（例：`venia-bottoms/venia-pants/lenora-crochet-shorts`）に置き換えられます
* `{{variant_sku}}` は、現在選択されているバリアント（例：`VP09-KH-S`）に置き換えられます

`url_path` が非推奨になったため、あらかじめ定義された製品のURLフォーマットは製品の `url_rewrites` を使用し、`url_path` が利用できない場合は最もパスセグメントが多いものを代替手段として選択します。

上記のサンプルデータでは、デフォルトの URL 形式を使用して設定された製品バリアント URL は `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S` のようになります。

### カテゴリページの URL 形式 {#product-list}

カテゴリページまたは製品リストページの URL を設定するもので、次のオプションをサポートしています。

* `{{page}}.html/{{url_path}}.html`（デフォルト）
* `{{page}}.html/{{url_key}}.html`

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)の場合は次のとおりです。

* `{{page}}` は `/content/venia/us/en/products/category-page` に置き換えられます
* `{{url_key}}` はカテゴリの `url_key` プロパティに置き換えられます
* `{{url_path}}` はカテゴリの `url_path` に置き換えられます

上記のサンプルデータでは、デフォルトの URL 形式を使用して設定されたカテゴリページ URL は `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html` のようになります。

>[!NOTE]
> 
> `url_path` は、製品またはカテゴリの上位層の `url_keys` と製品またはカテゴリの `url_key` をスラッシュ `/` で区切って連結したものです。各 `url_key` は、特定のストア内で一意と見なされます。

### ストア固有の設定 {#store-specific-urlformats}

システム全体のカテゴリおよび製品ページの URL 形式を、 _CIF URL プロバイダーの設定_ は、各ストアに対して変更できます。

CIF 設定では、エディターが別の製品またはカテゴリページの URL 形式を選択できます。 何も選択されていない場合、実装はシステム全体の設定にフォールバックします。

ライブ Web サイトの URL 形式を変更すると、サイトのオーガニックトラフィックに悪影響を与える可能性があります。 詳しくは、 [ベストプラクティス](#best-practices) を参照し、事前に URL 形式の変更を慎重に計画します。

![CIF 設定での URL 形式](assets/store-specific-url-formats.png)

>[!NOTE]
>
> ストア固有の URL 形式の設定には、次が必要です [CIF コアコンポーネント 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) およびAdobe Experience Manager Content and Commerce アドオンの最新バージョン。

## カテゴリ対応製品ページの URL {#context-aware-pdps}

製品 URL 内のカテゴリ情報をエンコードできるので、複数のカテゴリに属する製品に対しても、複数の製品 URL で指定できます。

デフォルトの URL 形式では、次のスキームを使用して、考えられる代替方法の 1 つを選択します。

* ( `url_path` は e コマースバックエンドによって定義され、それを使用します（廃止）
* から `url_rewrites` 製品の `url_key` 代替案として
* これらの代替手段では、最も多くのパスセグメントを使用します
* 複数ある場合は、e コマースバックエンドで指定された順序で最初のを使用します。

このスキームは、 `url_path` 子カテゴリが親カテゴリよりも具体的であるという前提に基づいて、上位カテゴリと共に使用されます。 選択した `url_path` 考慮される _標準_ とは、常に製品ページの正規リンクまたは製品サイトマップで使用されます。

ただし、買い物客がカテゴリページから製品ページに、または同じカテゴリ内のある製品ページから別の関連製品ページに移動する場合、現在のカテゴリのコンテキストを維持することをお勧めします。 この場合、 `url_path` 選択では、現在のカテゴリのコンテキスト内にある代替オプションを、 _標準_ 上記の選択。

この機能は、 _CIF URL プロバイダーの設定_. 有効にした場合、選択範囲は、

* 特定のカテゴリの一部と一致する `url_path` 先頭から（ファジープレフィックスの一致）
* または指定されたカテゴリの `url_key` anywhere （完全な部分一致）

例えば、 [製品クエリ](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 下 ユーザーが「New Products / New in Summer 2022」カテゴリページに移動し、ストアがデフォルトのカテゴリページ URL 形式を使用している場合、代替「new-products/new-in-summer-2022/gold-cirque-earrings.html」は、最初からのコンテキストのパスセグメントの 2 と一致します。「new-products」と「new-in-summer-2022」の 2 つのリストが追加されました。 ストアが、カテゴリのみを含むカテゴリページの URL 形式を使用している場合 `url_key`の場合、同じ代替案が、コンテキストの `url_key` どこでも どちらの場合も、製品ページの URL は「new-products/new-in-summer-2022/gold-cirque-earrings.html」 `url_path`.

```
{
  "data": {
    "products": {
      "items": [
        {
          "sku": "VA18-GO-NA",
          "url_key": "gold-cirque-earrings",
          "url_rewrites": [
            {
              "url": "gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/venia-jewelry/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/new-in-summer-2022/gold-cirque-earrings.html"
            }
          ]
        }
      ]
    }
  }
}
```

>[!NOTE]
>
> カテゴリ対応の製品 URL にはが必要です [CIF コアコンポーネント 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 以降

## 特定のカテゴリおよび製品ページ {#specific-pages}

カタログのカテゴリーまたは製品の特定のサブセットに対してのみ、[複数のカテゴリーページおよび製品ページ](../authoring/multi-template-usage.md)を作成することができます。

### 選択条件 {#specific-pages-selection}

特定のカテゴリページの選択は、そのカテゴリの `url_path` または `url_key`. サブカテゴリの一致は、完全なカテゴリを含む URL 形式でのみサポートされます `url_path`. それ以外の場合は、 `url_key` が可能です。

特定の製品ページは、製品の sku またはカテゴリで選択されます。 後で、製品 URL で一部のカテゴリ情報をエンコードする必要があります。 これは、一部のデフォルトの URL 形式でのみ使用できます。 sku またはカテゴリ別の特定のページ選択をサポートする URL 形式の比較については、以下の表を参照してください。


| URL 形式 | sku 別 | カテゴリ別 |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` |  no |  no |
| `{{page}}.html/{{category}}/{{url_key}}.html` |  no | 完全一致のみ |
| `{{page}}.html/{{url_path}}.html` |  no | ○ |
| `{{page}}.html/{{sku}}.html` | ○ |  no |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | ○ |  no |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | ○ | 完全一致のみ |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | ○ | ○ |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> カテゴリ別に特定の製品ページを選択するには、 [CIF コアコンポーネント 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 以降

### デップリンク {#specific-pages-deep-linking}

この `UrlProvider` は、オーサー層インスタンス上の特定のカテゴリおよび製品ページへのディープリンクを生成するように事前に設定されています。 これは、編集者がプレビューモードでサイトを閲覧し、特定の製品ページまたはカテゴリーページに移動したあと編集モードに切り替えてページを編集する場合に便利な機能です。

一方、パブリッシュ層インスタンスでは、検索エンジンのランキングでの利益を失わないように、カタログページの URL を安定させる必要があります。 そのため、パブリッシュ層インスタンスは、デフォルトでは特定のカタログページへのディープリンクをレンダリングしません。 この動作を変更するには、 _CIF URL プロバイダー固有のページ戦略_ は、常に特定のページ URL を生成するように設定できます。

## カスタマイズ {#customization}

### カスタム URL 形式 {#custom-url-format}

カスタム URL 形式を指定するには、プロジェクトで [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) または [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) サービスインターフェイスを実装し、その実装を OSGi サービスとして登録します。 これらの実装が用意されている場合は、設定されている事前定義済み形式の代わりに、その実装が使用されます。 複数の実装が登録されている場合は、サービスランキングの高い実装が、サービスランキングの低い実装と入れ替わります。

カスタム URL 形式の実装では、指定されたパラメーターから URL を作成するメソッドと URL を解析して同じパラメーターを返すメソッドのペアを実装する必要があります。

### Sling マッピングとの結合 {#sling-mapping}

`UrlProvider` に加え、URL の書き換えと処理を行うために、[Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)を設定することもできます。AEM アーキタイププロジェクトでは、ポート 4503（パブリッシュ）および 80（ディスパッチャー）の Sling マッピングを設定する[設定例](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)も提供されています。

### AEM Dispatcher との統合 {#dispatcher}

URL の書き換えは、AEM Dispatcher HTTP サーバーを `mod_rewrite` モジュール。 [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)には、生成されたサイズに対する基本的な[書き換えルール](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)が含まれている参照用 AEM Dispatcher 設定が用意されています。

## ベストプラクティス {#best-practices}

### 最適な URL 形式を選択 {#choose-url-format}

使用可能なデフォルトの形式の 1 つを選択する前に述べたように、カスタム形式を実装する場合も、ストアのニーズと要件に大きく依存します。 以下の提案は、教育を受けた意思決定を行うのに役立ちます。

_**sku を含む製品ページ URL 形式を使用します。**_

CIF コアコンポーネントでは、すべてのコンポーネントで sku をプライマリ識別子として使用します。 製品ページの URL 形式に sku が含まれていない場合、それを解決するには GraphQL クエリが必要です。 これは、最初のバイトまでの時間に影響を与える可能性があります。 また、買い物客が検索エンジンを使用して sku で製品を見つけることが望ましい場合もあります。

_**カテゴリコンテキストを含む製品ページの URL 形式を使用します。**_

CIF URL プロバイダーの一部の機能は、カテゴリなど、カテゴリコンテキストをエンコードする製品 URL 形式を使用する場合にのみ使用できます `url_key` またはカテゴリ `url_path`. 新しいストアでこれらの機能が必要でない場合でも、最初にこれらの URL 形式のいずれかを使用すると、将来の移行作業を減らすことができます。

_**URL の長さとエンコードされた情報のバランス。**_

カタログのサイズ、特にカテゴリツリーのサイズと深さに応じて、完全にエンコードするのは適切でない場合があります `url_path` 」と入力します。 その場合、カテゴリの `url_key` 代わりに、 これは、カテゴリを使用する際に使用できる機能のほとんどをサポートします `url_path`.

また、 [Sling マッピング](#sling-mapping) sku を製品と組み合わせるために `url_key`. ほとんどの e コマースシステムでは、sku は特定の形式に従い、sku を `url_key` を使用すると、受信リクエストが簡単に可能になります。 そのため、製品ページの URL を `/p/{{category}}/{{sku}}-{{url_key}}.html`、およびカテゴリ URL を `/c/{{url_key}}.html` 専門的に この `/p` および `/c` 製品ページとカテゴリページを他のコンテンツページと区別するために、引き続きプレフィックスが必要です。

### 新しい URL 形式への移行 {#migrate-url-formats}

デフォルトの URL 形式の多くは、互いに何らかの互換性があり、ある形式で書き出された URL は別の形式で解析される場合があることを意味します。 これは、URL 形式間の移行に役立ちます。

一方、検索エンジンでは、すべてのカタログページを新しい URL 形式で再クロールするのにしばらく時間が必要になります。 このプロセスをサポートし、エンドユーザーエクスペリエンスを向上させるために、古い URL から新しい URL にユーザーを転送するリダイレクトを提供することをお勧めします。

その 1 つのアプローチは、ステージ環境を実稼動 e コマースバックエンドに接続し、新しい URL 形式を使用するように設定することです。 その後、 [CIF 製品サイトマップジェネレーターで生成された製品サイトマップ](../../overview/seo-and-url-management.md) ステージ環境と実稼動環境の両方で使用し、 [Apache httpd 書き換えマップ](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). この書き換えマップは、新しい URL 形式のロールアウトと共に Dispatcher にデプロイすることはできません。

## 例 {#example}

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトには、製品ページとカテゴリページでのカスタム URL を使用方法を示す設定例が含まれています。これにより、各プロジェクトで、SEO のニーズに応じて、製品ページとカテゴリページの個々の URL パターンを設定できます。上記の CIF `UrlProvider` と Sling マッピングの組み合わせが使用されます。

>[!NOTE]
>
>この設定は、プロジェクトで使用する外部ドメインで調整する必要があります。Sling マッピングは、ホスト名とドメインに基づいて動作します。したがって、この設定はデフォルトで無効になっており、デプロイ前に有効にする必要があります。これを行うには、使用されているドメイン名に従って `ui.content/src/main/content/jcr_root/etc/map.publish/https` の Sling マッピング `hostname.adobeaemcloud.com` フォルダーの名前を変更し、`resource.resolver.map.location="/etc/map.publish"` をプロジェクトの `JcrResourceResolver` 設定に追加してこの設定を有効にします。

## その他のリソース {#additional}

* [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [AEM リソースマッピング](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html?lang=ja)
* [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
