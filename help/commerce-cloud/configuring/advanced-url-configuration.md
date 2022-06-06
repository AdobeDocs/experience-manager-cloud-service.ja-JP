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
source-git-commit: af07bce8618c7b13b4dc5e287c7218316029f565
workflow-type: ht
source-wordcount: '2039'
ht-degree: 100%

---

# 高度な URL 設定 {#url}

>[!NOTE]
>
> 検索エンジン最適化（SEO）は、多くのマーケティング担当者にとって重要な課題となっています。その結果、多くの Adobe Experience Manager（AEM）as a Cloud Service プロジェクトで SEO の懸念に対処する必要があります。詳しくは、[SEO と URL 管理のベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html?lang=ja)を参照してください。

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、製品ページとカテゴリページの URL をカスタマイズする高度な設定を提供します。多くの実装では、検索エンジン最適化（SEO）用にこれらの URL をカスタマイズします。次のビデオでは、`UrlProvider` サービスと [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)の機能を設定して、製品ページとカテゴリページの URL をカスタマイズする方法について詳しく説明します。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

SEO の要件とニーズに応じて `UrlProvider` サービスを設定するには、プロジェクトで&#x200B;_CIF URL プロバイダーの設定_&#x200B;の OSGI 設定を指定する必要があります。

>[!NOTE]
>
> AEM CIF コアコンポーネントのリリース 2.0.0 以降では、URL プロバイダーの設定には、1.x リリースで提供されていた設定可能なフリーテキスト形式ではなく、事前に定義された URL 形式のみが使用されます。さらに、セレクターを使用して URL 内のデータを渡すことはなくなり、代わりにサフィックスが使用されます。

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

_CIF URL プロバイダーの設定_ で設定したシステム全体のカテゴリおよび製品ページの URL 形式は、各ストアに対して変更できます。

CIF 設定では、エディターが別の製品またはカテゴリページの URL 形式を選択できます。何も選択されていない場合、実装はシステム全体の設定にフォールバックします。

ライブ Web サイトの URL 形式を変更すると、サイトのオーガニックトラフィックに悪影響を与える可能性があります。以下の [ベストプラクティス](#best-practices) を参照し、事前に URL 形式の変更を慎重に計画してください。

![CIF 設定での URL 形式](assets/store-specific-url-formats.png)

>[!NOTE]
>
> URL 形式のストア固有の設定には、 [CIF コアコンポーネント 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) と最新バージョンの Adobe Experience Manager コンテンツおよび Commerce アドオンが必要です。

## カテゴリ対応の製品ページ URL {#context-aware-pdps}

製品 URL にカテゴリ情報をエンコードできるので、複数のカテゴリに属する製品に対しても、複数の製品 URL でアドレス指定できます。

デフォルトの URL 形式では、次のスキームを使用した代替値の 1 つが選択されます。

* `url_path` が e コマースバックエンドによって定義されている場合は、それを使用します（非推奨）
* `url_rewrites` から、製品の `url_key` で終わる URL を代替値として使用します
* これらの代替値から、パスセグメントが最も多いものを使用します
* 複数ある場合は、e コマースバックエンドで指定された順序で最初の 1 つを使用します

このスキームは、子カテゴリが親カテゴリよりも具体的であるという前提に基づいて上位カテゴリが最も上位にある `url_path` を選択します。そのように選択された `url_path` は _正規_ と見なされ製品ページまたは製品サイトマップの正規リンクに常に使用されます。

ただし、買い物客がカテゴリページから製品ページに移動する場合、またはある製品ページから同じカテゴリ内の別の関連製品ページに移動する場合は、現在のカテゴリのコンテキストを維持することをお勧めします。この場合、`url_path` の選択は、上記の _正規_ の選択よりも現在のカテゴリのコンテキスト内にある代替値を優先する必要があります。


この機能は、 _CIF URL プロバイダーの設定_ に組み込まれている必要があります。有効にすると、次の場合に、選択により代替値のスコアが高くなります。

* 最初から特定のカテゴリの `url_path` の一部に一致する（ファジープレフィックスの一致）
* または、任意の場所で特定のカテゴリの `url_key` と一致する（完全な部分一致）

例えば、以下の [製品クエリ](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) に対する応答について考えてみます。ユーザーが「New Products / New in Summer 2022」カテゴリページを表示していて、ストアがデフォルトのカテゴリページの URL 形式を使用している場合、代替値の「new-products/new-in-summer-2022/gold-cirque-earrings.html」は、最初の「new-products」と「new-in-summer-2022」からのコンテキストのパスセグメントの 2 つと一致します。ストアがカテゴリ `url_key` のみを含んだカテゴリページ URL 形式を使用している場合でも、コンテキストの `url_key` と一致するため、同じ代替値が選択されます。どちらの場合も、製品ページの URL は「new-products/new-in-summer-2022/gold-cirque-earrings.html」の `url_path` に対して作成されます。

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
> カテゴリ対応製品 URL には、 [CIF コアコンポーネント 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 以降が必要です。

## 特定のカテゴリおよび製品ページ {#specific-pages}

カタログのカテゴリまたは製品の特定のサブセットに対してのみ、 [複数のカテゴリおよび製品ページ](../authoring/multi-template-usage.md) を作成することができます。

### 選択条件 {#specific-pages-selection}

特定のカテゴリページの選択はカテゴリの `url_path` または `url_key` に基づいて簡単に行えます。一致するサブカテゴリは、完全なカテゴリ `url_path` を含む URL 形式でのみサポートされます。それ以外の場合は、`url_key` の完全一致のみが可能です。

特定の製品ページは、製品の SKU またはカテゴリのいずれかによって選択されます。後者の場合は、一部のカテゴリ情報を製品 URL にエンコードする必要があります。これは、一部のデフォルト URL 形式でのみ使用できます。SKU またはカテゴリによる特定のページ選択をサポートする URL 形式の比較については、以下の表を参照してください。


| URL 形式 | SKU 別 | カテゴリ別 |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | いいえ | いいえ |
| `{{page}}.html/{{category}}/{{url_key}}.html` | いいえ | 完全一致のみ |
| `{{page}}.html/{{url_path}}.html` | いいえ | はい |
| `{{page}}.html/{{sku}}.html` | はい | いいえ |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | はい | いいえ |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | はい | 完全一致のみ |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | はい | はい |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> カテゴリ別に特定の製品ページを選択するには、 [CIF コアコンポーネント 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 以降が必要です。

### ディープリンク {#specific-pages-deep-linking}

`UrlProvider` は、特定のカテゴリおよび製品ページへのディープリンクをオーサー層インスタンスで生成するように事前に設定されています。これは、編集者がプレビューモードでサイトを閲覧し、特定の製品ページまたはカテゴリページに移動したあと編集モードに切り替えてページを編集する場合に便利な機能です。

一方、パブリッシュ層インスタンスでは、例えば検索エンジンのランキングを落とさないように、カタログページの URL を安定した状態に保つ必要があります。そのため、パブリッシュ層インスタンスは、デフォルトでは特定のカタログページへのディープリンクをレンダリングしません。この動作を変更するには、常に特定のページの URL を生成するように _CIF URL プロバイダー固有のページ戦略_ を設定します。

## カスタマイズ {#customization}

### カスタム URL 形式 {#custom-url-format}

カスタム URL 形式を指定するには、プロジェクトで [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) または [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) サービスインターフェイスを実装し、その実装を OSGi サービスとして登録します。これらの実装が用意されている場合は、設定されている事前定義済み形式の代わりに、その実装が使用されます。複数の実装が登録されている場合は、サービスランキングの高い実装が、サービスランキングの低い実装と入れ替わります。

カスタム URL 形式の実装では、指定されたパラメーターから URL を作成するメソッドと URL を解析して同じパラメーターを返すメソッドのペアを実装する必要があります。

### Sling マッピングとの結合 {#sling-mapping}

`UrlProvider` に加え、URL の書き換えと処理を行うために、[Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)を設定することもできます。AEM アーキタイププロジェクトでは、ポート 4503（パブリッシュ）および 80（ディスパッチャー）の Sling マッピングを設定する[設定例](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)も提供されています。

### AEM Dispatcher との統合 {#dispatcher}

URL の書き換えは、`mod_rewrite` モジュールを備えた AEM Dispatcher HTTP サーバーを使用して実行することもできます。[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype) は、既に生成されたサイズに対する基本的な [書き換えルール](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) が含まれている、参照用 AEM Dispatcher 設定を提供します。

## ベストプラクティス {#best-practices}

### 最適な URL 形式を選択 {#choose-url-format}

前述したように、使用可能なデフォルト形式の 1 つを選択するか、カスタム形式を実装するかさえ、ストアのニーズと要件に大きく依存します。次の提案は、知識に基づいた決定を下すのに役立つ場合があります。

_**SKU を含む製品ページの URL 形式を使用します。**_

CIF コアコンポーネントでは、すべてのコンポーネントで SKU をプライマリ識別子として使用します。製品ページの URL 形式に SKU が含まれていない場合、URL を解決するには GraphQL クエリが必要です。これは、最初のバイトを取得するまでの時間に影響を及ぼす可能性があります。また、買い物客が検索エンジンを使用して SKU で製品を見つけることができる方が望ましい場合もあります。

_**カテゴリコンテキストを含む製品ページの URL 形式を使用します。**_

CIF URL プロバイダーの一部の機能は、カテゴリ `url_key` やカテゴリ `url_path` など、カテゴリコンテキストをエンコードする製品 URL 形式を使用する場合にのみ使用できます。これらの機能が新しいストアに必要ない可能性がある場合でも、最初にこれらの URL 形式のいずれかを使用すると、将来の移行作業を軽減するのに役立ちます。

_**URL の長さとエンコードされた情報のバランス。**_

カタログのサイズ、特にカテゴリツリーのサイズと深さによっては、カテゴリの完全な `url_path` を URL にエンコードすることが合理的でない場合があります。その場合、代わりにカテゴリの `url_key` のみを含めることで、URL の長さを短くすることができます。これにより、カテゴリ `url_path` を使用する際に利用できるほとんどの機能がサポートされるようになります。

さらに、 [Sling マッピング](#sling-mapping) を使用して、SKU を製品 `url_key` と組み合わせます。ほとんどの e コマースシステムでは、SKU は特定の形式に従っており、受信リクエストのために SKU と `url_key` を分離することは簡単にできます。そのことを念頭に置くと、製品ページの URL を `/p/{{category}}/{{sku}}-{{url_key}}.html` に、カテゴリ URL を `/c/{{url_key}}.html` にそれぞれ書き換えることができます。`/p` および `/c` プレフィックスは、製品ページとカテゴリページを他のコンテンツページと区別するために、引き続き必要です。

### 新しい URL 形式への移行 {#migrate-url-formats}

デフォルトの URL 形式の多くは、何らかの形で相互に互換性があります。つまり、ある形式の URL が別の形式の URL で解析される可能性があります。これは、URL 形式間の移行に役立ちます。

一方、検索エンジンでは、すべてのカタログページを新しい URL 形式で再度クロールするのにしばらく時間が必要になります。このプロセスをサポートし、エンドユーザーエクスペリエンスを向上させるために、古い URL から新しい URL にユーザーを転送するリダイレクトを提供することをお勧めします。

その 1 つのアプローチとして考えられるのは、ステージング環境を実稼動 e コマースバックエンドに接続し、新しい URL 形式を使用するように設定することです。その後、ステージング環境と実稼動環境の両方で [CIF 製品サイトマップジェネレーターで生成された製品サイトマップ](../../overview/seo-and-url-management.md) を取得し、それらを使用して [Apache httpd 書き換えマップ](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html) を作成します。この書き換えマップは、新しい URL 形式のロールアウトと共に Dispatcher にデプロイすることはできません。

## 例 {#example}

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトには、製品ページとカテゴリページでのカスタム URL を使用方法を示す設定例が含まれています。これにより、各プロジェクトで、SEO のニーズに応じて、製品ページとカテゴリページの個々の URL パターンを設定できます。上記の CIF `UrlProvider` と Sling マッピングの組み合わせが使用されます。

>[!NOTE]
>
>この設定は、プロジェクトで使用する外部ドメインで調整する必要があります。Sling マッピングは、ホスト名とドメインに基づいて動作します。したがって、この設定はデフォルトで無効になっており、デプロイ前に有効にする必要があります。これを行うには、使用されているドメイン名に従って `ui.content/src/main/content/jcr_root/etc/map.publish/https` の Sling マッピング `hostname.adobeaemcloud.com` フォルダーの名前を変更し、`resource.resolver.map.location="/etc/map.publish"` をプロジェクトの `JcrResourceResolver` 設定に追加してこの設定を有効にします。

## その他のリソース {#additional}

* [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [AEM リソースマッピング](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html?lang=ja)
* [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
