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
source-git-commit: dadf4f21ebaac12386153b2a9c69dc8f10951e9c
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 63%

---

# 高度な URL 設定 {#url}

>[!NOTE]
>
> 検索エンジン最適化（SEO）は、多くのマーケティング担当者にとって重要な課題となっています。その結果、多くの Adobe Experience Manager（AEM）as a Cloud Service プロジェクトで SEO の懸念に対処する必要があります。詳しくは、[SEO と URL 管理のベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html?lang=ja)を参照してください。

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、製品ページとカテゴリページの URL をカスタマイズする高度な設定を提供します。多くの実装では、検索エンジン最適化（SEO）用にこれらの URL をカスタマイズします。次のビデオでは、`UrlProvider` サービスと [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)の機能を設定して、製品ページとカテゴリページの URL をカスタマイズする方法について詳しく説明します。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

次の手順で `UrlProvider` SEO 要件と必要に応じて、サービスで「CIF URL Provider configuration」の OSGI 設定をプロジェクトで提供する必要があります。

>[!NOTE]
>
> AEM CIF コアコンポーネントのリリース 2.0.0 以降、URL プロバイダー設定では、1.x リリースで知られているフリーテキスト設定可能な形式の代わりに、事前に定義された URL 形式のみが提供されます。 さらに、セレクターを使用して URL 内のデータを渡すことはなくなり、代わりにサフィックスが使用されます。

### 製品ページの URL 形式 {#product}

製品ページの URL を設定するもので、次のオプションをサポートしています。

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（デフォルト）
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)の場合は次のとおりです。

* `{{page}}` は `/content/venia/us/en/products/product-page` に置き換えられます
* `{{sku}}` は製品の SKU（例：`VP09`）に置き換えられます
* `{{url_key}}` は製品の `url_key` プロパティ（例：`lenora-crochet-shorts`）に置き換えられます
* `{{url_path}}` は製品の `url_path`（例：`venia-bottoms/venia-pants/lenora-crochet-shorts`）に置き換えられます
* `{{variant_sku}}` は、現在選択されているバリアント（例：`VP09-KH-S`）に置き換えられます

以降 `url_path` 廃止されました。事前定義済みの製品 URL 形式では、製品の `url_rewrites` を選択し、最もパスセグメントが多いセグメントを選択します。 `url_path` は使用できません。

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
> `url_path` は、製品またはカテゴリの上位層の `url_keys` と製品またはカテゴリの `url_key` をスラッシュ `/` で区切って連結したものです。

### 特定のカテゴリ/製品ページ {#specific-pages}

次を作成できます。 [複数のカテゴリページと製品ページ](../authoring/multi-template-usage.md) カタログの特定のカテゴリまたは製品のサブセットのみ。

この `UrlProvider` は、オーサー層インスタンスでこのようなページへのディープリンクを生成するように事前に設定されています。 これは、編集者がプレビューモードでサイトを参照し、特定の製品またはカテゴリのページに移動して、ページを編集するために編集モードに戻るのに役立ちます。

一方、パブリッシュ層インスタンスでは、例えば検索エンジンのランキングで得られる結果が失われないように、カタログページの URL を安定させる必要があります。 そのパブリッシュ層のインスタンスは、デフォルトでは特定のカタログページへのディープリンクをレンダリングしません。 この動作を変更するには、 _CIF URL プロバイダー固有のページ戦略_ は、常に特定のページ url を生成するように設定できます。

## カスタム URL 形式 {#custom-url-format}

プロジェクトで実装できるカスタム URL 形式を指定するには、 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) または [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) サービスインターフェイスを使用し、実装を OSGi サービスとして登録します。 これらの実装がある場合、設定済みの事前定義済みの形式が置き換えられます。 複数の実装が登録されている場合、サービスランキングが高い実装は、低いサービスランキングで置き換えられます。

カスタム URL 形式の実装では、指定されたパラメーターから URL を作成し、それぞれ同じパラメーターを返す URL を解析するために、メソッドのペアを実装する必要があります。

## Sling マッピングとの結合 {#sling-mapping}

`UrlProvider` に加え、URL の書き換えと処理を行うために、[Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)を設定することもできます。AEM アーキタイププロジェクトでは、ポート 4503（パブリッシュ）および 80（ディスパッチャー）の Sling マッピングを設定する[設定例](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)も提供されています。

## AEM Dispatcher との統合 {#dispatcher}

URL の書き換えは、AEM Dispatcher HTTP サーバーを `mod_rewrite` モジュール。 [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)には、生成されたサイズに対する基本的な[書き換えルール](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)が含まれている参照用 AEM Dispatcher 設定が用意されています。

## 例 {#example}

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトには、製品ページとカテゴリページでのカスタム URL を使用方法を示す設定例が含まれています。これにより、各プロジェクトで、SEO のニーズに応じて、製品ページとカテゴリページの個々の URL パターンを設定できます。上記の CIF `UrlProvider` と Sling マッピングの組み合わせが使用されます。

>[!NOTE]
>
>この設定は、プロジェクトで使用する外部ドメインで調整する必要があります。Sling マッピングは、ホスト名とドメインに基づいて動作します。したがって、この設定はデフォルトで無効になっており、デプロイ前に有効にする必要があります。これを行うには、使用されているドメイン名に従って `ui.content/src/main/content/jcr_root/etc/map.publish/https` の Sling マッピング `hostname.adobeaemcloud.com` フォルダーの名前を変更し、`resource.resolver.map.location="/etc/map.publish"` をプロジェクトの `JcrResourceResolver` 設定に追加してこの設定を有効にします。

## その他のリソース {#additional}

* [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [AEM リソースマッピング](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html?lang=ja)
* [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
