---
title: 高度な URL 設定
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
ht-degree: 97%

---


# 高度な URL 設定 {#url}

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、製品ページとカテゴリページの URL をカスタマイズする高度な設定を提供します。多くの実装では、検索エンジン最適化（SEO）用にこれらの URL をカスタマイズします。  次のビデオでは、`UrlProvider` サービスと [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)の機能を設定して、製品ページとカテゴリページの URL をカスタマイズする方法について詳しく説明します。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

SEO 要件と必要性に従って `UrlProvider` サービスを設定するには、プロジェクトで「CIF URL Provider configuration」設定用の OSGI 設定を提供し、以下の説明に従ってサービスを設定する必要があります。

>[!NOTE]
>
> 下記の [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトには、製品ページとカテゴリページでのカスタム URL の使用方法を示す設定例が含まれています。

### 製品ページの URL テンプレート {#product}

次のプロパティを使用して製品ページの URL を設定します。

* **製品 URL テンプレート**：一連のプレースホルダーを使用して URL の形式を定義します。デフォルト値は `{{page}}.{{url_key}}.html#{{variant_sku}}` で、最終的に `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange` のような URL が生成されます。
   * `{{page}}` は `/content/venia/us/en/products/product-page` で置き換えられています。
   * `{{url_key}}` は、Magento の製品の `url_key` プロパティに置き換えられています（ここでは `chaz-kangeroo-hoodie`）。
   * `{{variant_sku}}` は、現在選択されているバリアントに置き換えられています（ここでは `MH01-M-Orange`）。
* **製品識別子の場所**：製品データの取得に使用される識別子の場所を定義します。デフォルト値は `SELECTOR` です。もう 1 つの有効な値は `SUFFIX` です。前の例の URL では、ID `chaz-kangeroo-hoodie` を使用して製品データを取得します。
* **製品識別子の種類**：製品データを取得する際に使用する識別子のタイプを定義します。デフォルト値は `URL_KEY` です。もう 1 つの有効な値は `SKU` です。前の例の URL では、`filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}` のような Magento GraphQL フィルターを使用して製品データを取得します。

### 製品リストページの URL テンプレート {#product-list}

次のプロパティを使用して、カテゴリページまたは製品リストページの URL を設定します。

* **カテゴリ URL テンプレート**：一連のプレースホルダーを使用して URL の形式を定義します。デフォルト値は `{{page}}.{{id}}.html` で、最終的に `/content/venia/us/en/products/category-page.3.html` のような URL が生成されます。
   * `{{page}}` は `/content/venia/us/en/products/category-page` で置き換えられています。
   * `{{id}}` は、カテゴリの Magento の `id` プロパティ（ここでは `3`）に置き換えられています。
* **カテゴリ識別子の場所**：製品データの取得に使用される識別子の場所を定義します。デフォルト値は `SELECTOR` です。もう 1 つの有効な値は `SUFFIX` です。前の例の URL では、ID `3` を使用して製品データを取得します。
* **カテゴリ識別子の種類**：製品データを取得する際に使用する識別子のタイプを定義します。`ID` はデフォルト値であり、現在サポートされている唯一の値です。前の例の URL では、`category(id:3)` のような Magento GraphQL フィルターを使用してカテゴリデータを取得します。

コンポーネントが `UrlProvider` を使用して対応するデータを設定している限り、各テンプレートにカスタムプロパティを追加できます。`ProductListItemImpl` クラスのコード例を調べて、この実装方法を確認してください。

また、`UrlProvider` サービスを完全にカスタムの OSGi サービスで置き換えることもできます。この場合、デフォルトの実装を置き換えるには、`UrlProvider` インターフェイスを実装し、それをより高いサービスランクに登録する必要があります。

## Sling マッピングとの結合 {#sling-mapping}

`UrlProvider` に加え、URL の書き換えと処理をおこなうために、[Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)を設定することもできます。AEM アーキタイププロジェクトでは、ポート 4503（パブリッシュ）および 80（ディスパッチャー）の Sling マッピングを設定する[設定例](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)も提供されています。

## AEM Dispatcher との統合 {#dispatcher}

URL の書き換えは、AEM Dispatcher HTTP サーバーで `mod_rewrite` モジュールを使用しておこなうこともできます。[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)には、生成されたサイズに対する基本的な[書き換えルール](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)が含まれている参照用 AEM Dispatcher 設定が用意されています。

## 例

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトには、製品ページとカテゴリページでのカスタム URL を使用方法を示す設定例が含まれています。これにより、各プロジェクトで、SEO のニーズに応じて、製品ページとカテゴリページの個々の URL パターンを設定できます。上記の CIF `UrlProvider` と Sling マッピングの組み合わせが使用されます。

>[!NOTE]
>
>この設定は、プロジェクトで使用する外部ドメインで調整する必要があります。Sling マッピングは、ホスト名とドメインに基づいて動作します。したがって、この設定はデフォルトで無効になっており、デプロイ前に有効にする必要があります。これをおこなうには、使用されているドメイン名に従って `ui.content/src/main/content/jcr_root/etc/map.publish/https` の Sling マッピング `hostname.adobeaemcloud.com` フォルダーの名前を変更し、`resource.resolver.map.location="/etc/map.publish"` をプロジェクトの `JcrResourceResolver` 設定に追加してこの設定を有効にします。

## その他のリソース

* [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [AEM リソースマッピング](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/deploying/configuring/resource-mapping.translate.html)
* [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
