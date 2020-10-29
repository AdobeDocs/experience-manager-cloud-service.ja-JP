---
title: 高度なURL設定
description: 商品ページとカテゴリページのURLをカスタマイズする方法について説明します。 これにより、導入で検索エンジンのURLを最適化し、検出を促進できます。
sub-product: Commerce
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 4%

---


# 高度なURL設定 {#url}

[AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components) ：製品ページとカテゴリページのURLをカスタマイズする高度な設定を提供します。 多くの実装では、検索エンジン最適化(SEO)用にこれらのURLをカスタマイズします。  次のビデオでは、Sling Mappingの `UrlProvider` サービスと機能を設定して、製品ページとカテゴリページのURLをカスタマイズする方法について詳しく説明し [](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) ます。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

SEO要件に従って `UrlProvider` サービスを設定し、プロジェクトが必要になるには、「CIF URL Provider設定」設定用のOSGI設定を提供し、以下の説明に従ってサービスを設定する必要があります。

>[!NOTE]
>
> 下記の [ベニアリファレンスストア](https://github.com/adobe/aem-cif-guides-venia) プロジェクトには、製品ページとカテゴリページでのカスタムURLの使用方法を示すサンプル設定が含まれています。

### 製品ページのURLテンプレート {#product}

これにより、次のプロパティを使用して製品ページのURLが設定されます。

* **製品URLテンプレート**:は、一連のプレースホルダーを使用してURLの形式を定義します。 デフォルト値 `{{page}}.{{url_key}}.html#{{variant_sku}}``/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange` はです。最終的にURLが生成されます。例えば、
   * `{{page}}` が `/content/venia/us/en/products/product-page`
   * `{{url_key}}` は、Magentoの製品の `url_key` プロパティ（ここ）に置き換えられました。 `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` は、現在選択されているバリアントに置き換えられました。 `MH01-M-Orange`
* **製品識別子の場所**:製品データの取得に使用される識別子の場所を定義します。 デフォルト値はで `SELECTOR`す。もう1つの有効な値は `SUFFIX`です。 前の例のURLでは、このIDを使用して製品データ `chaz-kangeroo-hoodie` を取得します。
* **製品識別子の種類**:製品データを取得する際に使用する識別子のタイプを定義します。 デフォルト値はで `URL_KEY`す。もう1つの有効な値は `SKU`です。 前の例のURLでは、のようなMagentoGraphQLフィルタを使用して製品データが取得され `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`ます。

### 製品リストページのURLテンプレート {#product-list}

これにより、次のプロパティを使用して、カテゴリページまたは製品リストページのURLが設定されます。

* **カテゴリURLテンプレート**:は、一連のプレースホルダーを使用してURLの形式を定義します。 デフォルト値 `{{page}}.{{id}}.html``/content/venia/us/en/products/category-page.3.html` はです。最終的にURLが生成されます。例えば、
   * `{{page}}` が `/content/venia/us/en/products/category-page`
   * `{{id}}` ここ、カテゴリのMagentoの `id` 財産に取って代わられた `3`
* **カテゴリ識別子の場所**:製品データの取得に使用される識別子の場所を定義します。 デフォルト値はで `SELECTOR`す。もう1つの有効な値は `SUFFIX`です。 前の例のURLでは、このIDを使用して製品データ `3` を取得します。
* **カテゴリ識別子の種類**:製品データを取得する際に使用する識別子のタイプを定義します。 デフォルト値であり、現在サポートされている値のみ `ID`です。 前の例のURLでは、カテゴリデータは、のようなMagentoGraphQLフィルタを使用して取得され `category(id:3)`ます。

を使用するコンポーネントによって対応するデータが設定されている限り、各テンプレートにカスタムプロパティを追加でき `UrlProvider`ます。 クラスのコード例を調べて、この実装方法を調べ `ProductListItemImpl` ます。

また、完全にカスタムのOSGiサービスで `UrlProvider` サービスを置き換えることもできます。 この場合、デフォルトの実装を置き換えるには、インター `UrlProvider` フェイスを実装し、それをより高いサービスランクに登録する必要があります。

## Slingマッピングとの結合 {#sling-mapping}

さらに、URLの書き換え `UrlProvider`と処理を行うために、 [Sling Mappings](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) を設定することもできます。 AEM Archetypeプロジェクト [](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) では、ポート4503（発行）および80（ディスパッチャー）のSling Mappingsを設定する設定例も提供されています。

## AEM Dispatcherとの統合 {#dispatcher}

URLの書き換えは、モジュールと共にAEM Dispatcher HTTPサーバーを使用して行うこともでき `mod_rewrite` ます。 AEM [プロジェクトのアーキタイプ](https://github.com/adobe/aem-project-archetype) には、生成されたサイズに対する基本的な [](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 書き換えルールが既に含まれている、参照AEMディスパッチャー設定が用意されています。

## 例

Venia Reference Store [](https://github.com/adobe/aem-cif-guides-venia) Projectには、製品ページとカテゴリページでのカスタムURLの使用を示すサンプル設定が含まれています。 これにより、各プロジェクトで、SEOのニーズに応じて、商品ページとカテゴリページの個々のURLパターンを設定できます。 上記のCIF `UrlProvider` とSlingのマッピングの組み合わせが使用されます。

>[!NOTE]
>
>この設定は、プロジェクトで使用される外部ドメインで調整する必要があります。 Slingマッピングは、ホスト名とドメインに基づいて動作します。 したがって、この設定はデフォルトで無効になっており、展開前に有効にする必要があります。 これを行うには、使用されているドメイン名に `hostname.adobeaemcloud.com` 従ってのSling Mapping `ui.content/src/main/content/jcr_root/etc/map.publish/https` フォルダーの名前を変更し、プロジェクトの `resource.resolver.map.location="/etc/map.publish"``JcrResourceResolver` configに追加してこの設定を有効にします。

## その他のリソース

* [ベニアリファレンスストア](https://github.com/adobe/aem-cif-guides-venia)
* [AEMリソースマッピング](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling Mappings](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
