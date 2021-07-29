---
title: 高度な URL 設定
description: 製品ページとカテゴリページの URL をカスタマイズする方法について説明します。このカスタマイズにより、実装で URL を検索エンジン向けに最適化し、検出を促進できます。
sub-product: コマース
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: コマース統合フレームワーク
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: dbf32230042f39760733b711ffe8b5b4143e0544
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 48%

---

# 高度な URL 設定 {#url}

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、製品ページとカテゴリページの URL をカスタマイズする高度な設定を提供します。多くの実装では、検索エンジン最適化（SEO）用にこれらの URL をカスタマイズします。次のビデオでは、`UrlProvider` サービスと [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)の機能を設定して、製品ページとカテゴリページの URL をカスタマイズする方法について詳しく説明します。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

SEO要件と必要に応じて`UrlProvider`サービスを設定するには、プロジェクトで「CIF URL Provider configuration」のOSGI設定を提供する必要があります。

>[!NOTE]
>
> AEM CIFコアコンポーネントのリリース2.0.0以降、URLプロバイダー設定では、1.xリリースで提供されていたフリーテキスト設定可能な形式の代わりに、事前に定義されたURL形式のみが提供されます。 さらに、URL内のデータを渡すためのセレクターの使用は、サフィックスに置き換えられました。

### 製品ページのURL形式 {#product}

製品ページのURLを設定し、次のオプションをサポートします。

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（デフォルト）
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

ここで、[Venia参照用ストア](https://github.com/adobe/aem-cif-guides-venia)の場合は

* `{{page}}` は、  `/content/venia/us/en/products/product-page`
* `{{sku}}` は、製品のskuに置き換えられます（例： ）。  `VP09`
* `{{url_key}}` は、製品のプロパティに置 `url_key` き換えられます(例：  `lenora-crochet-shorts`
* `{{url_path}}` は製品のに置き換えら `url_path`れます（例： ）。  `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` は、現在選択されているバリアントに置き換えられます(例：  `VP09-KH-S`

上記の例のデータでは、デフォルトのURL形式を使用して書式設定された製品バリアントURLは`/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`のようになります。

### カテゴリページのURL形式 {#product-list}

カテゴリまたは製品リストページのURLを設定し、次のオプションをサポートします。

* `{{page}}.html/{{url_path}}.html`（デフォルト）
* `{{page}}.html/{{url_key}}.html`

ここで、[Venia参照用ストア](https://github.com/adobe/aem-cif-guides-venia)の場合は

* `{{page}}` は、  `/content/venia/us/en/products/category-page`
* `{{url_key}}` は、カテゴリのプロパティに置き換えられま `url_key` す。
* `{{url_path}}` は、カテゴリの  `url_path`

上記の例のデータでは、デフォルトのURL形式を使用して書式設定されたカテゴリページのURLは`/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`のようになります。

>[!NOTE]
> 
> `url_path`は、製品またはカテゴリの上位層の`url_keys`と、製品またはカテゴリの`url_key`を`/`スラッシュで区切った連結です。

## カスタムUrl形式 {#custom-url-format}

カスタムURL形式をプロジェクトに提供するには、[`UrlFormat`インターフェイス](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/UrlFormat.html)を実装し、asカテゴリページまたは製品ページのURL形式を使用してOSGIサービスとして実装を登録します。 `UrlFormat#PROP_USE_AS`サービスプロパティは、置き換える設定済みの事前定義済み形式ので示します。

* `useAs=productPageUrlFormat`は、設定済みの製品ページのurl形式を置き換えます。
* `useAs=categoryPageUrlFormat`は、設定済みのカテゴリページのurl形式を置き換えます。

OSGIサービスとして登録されている`UrlFormat`の実装が複数ある場合、サービスランキングの高い実装が、サービスランキングの低い実装に置き換えられます。

`UrlFormat`は、指定されたパラメーターのマップからURLを作成し、同じパラメーターのマップを返すURLを解析するメソッドのペアを実装する必要があります。 パラメーターは前述と同じです。カテゴリに対してのみ、追加の`{{uid}}`パラメーターが`UrlFormat`に提供されます。

## Sling マッピングとの結合 {#sling-mapping}

`UrlProvider` に加え、URL の書き換えと処理を行うために、[Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)を設定することもできます。AEM アーキタイププロジェクトでは、ポート 4503（パブリッシュ）および 80（ディスパッチャー）の Sling マッピングを設定する[設定例](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)も提供されています。

## AEM Dispatcher との統合 {#dispatcher}

URL の書き換えは、AEM Dispatcher HTTP サーバーで `mod_rewrite` モジュールを使用して行うこともできます。[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)には、生成されたサイズに対する基本的な[書き換えルール](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)が含まれている参照用 AEM Dispatcher 設定が用意されています。

## 例

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトには、製品ページとカテゴリページでのカスタム URL を使用方法を示す設定例が含まれています。これにより、各プロジェクトで、SEO のニーズに応じて、製品ページとカテゴリページの個々の URL パターンを設定できます。上記の CIF `UrlProvider` と Sling マッピングの組み合わせが使用されます。

>[!NOTE]
>
>この設定は、プロジェクトで使用する外部ドメインで調整する必要があります。Sling マッピングは、ホスト名とドメインに基づいて動作します。したがって、この設定はデフォルトで無効になっており、デプロイ前に有効にする必要があります。これを行うには、使用されているドメイン名に従って `ui.content/src/main/content/jcr_root/etc/map.publish/https` の Sling マッピング `hostname.adobeaemcloud.com` フォルダーの名前を変更し、`resource.resolver.map.location="/etc/map.publish"` をプロジェクトの `JcrResourceResolver` 設定に追加してこの設定を有効にします。

## その他のリソース

* [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [AEM リソースマッピング](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
