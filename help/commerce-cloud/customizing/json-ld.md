---
title: JSON-LD メタデータ
description: AEM CIFで JSON+LD 機能を有効にし検証する方法を説明します。
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 5fef97e5c0963529aac6d210cb17326864e6d248
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 5%

---


# JSON-LD メタデータ {#json-ld}

このガイドでは、AEM CIFで JSON+LD 機能を有効にし検証する方法について説明します。

## CIF設定で JSON+LD を有効にする {#enabling}

デフォルトでは、「**JSON+LD を有効にする**」チェックボックスはCIF設定に表示されません。 この機能を有効にするには、必要な OSGi 設定がプロジェクトに含まれている必要があります。これにより、チェックボックスを表示できます。 この設定により、ユーザーは製品ページで JSON+LD スクリプトのサポートを切り替えることができます。
**JSON+LD を有効にする** チェックボックスをCIF設定で使用できるようにするには、次の OSGi 設定をプロジェクトに追加します：`
com.adobe.cq.cif.components.models.JsonLdFeatureEnable`。
この設定の追加について詳しくは、公開 aem-cif-guides-venia リポジトリの [Json-Ld の設定を追加 ](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.cif.components.models.JsonLdFeatureEnable.cfg.json) を参照してください。

この設定を追加してデプロイすると、CIFの設定に「」チェックボックスが表示されます。**JSON+LD** を有効にする手順は次のとおりです。

1. AEMのCIF設定に移動します。
1. 継承をキャンセルします。
1. 「**JSON+LD を有効にする**」チェックボックスをオンにします。
1. 設定を保存します。

## 製品詳細ページ（PDP）での JSON+LD の確認 {#verify}

JSON+LD を検証する手順を説明するために、必要な JSON+LD 設定が既に追加されている場合の例として、Venia プロジェクトを使用して機能を有効にします。 手順は次のとおりです。

1. ローカルのAEM インスタンスに移動し、製品詳細ページ（PDP）を開きます。http://localhost:4502/editor.html/content/venia/us/en/products/product-page.html
1. 製品詳細ページ（PDP）で製品を作成します。
1. **公開として表示** モードに切り替えます。
1. ブラウザーで **ページを表示Source** を開きます。
1. ページソースで JSON+LD を検索します。

正しく設定されている場合は、ページに挿入された製品に関連付けられた JSON+LD スクリプトが見つかります。

## 製品の JSON+LD 構造のサンプル {#sample}

以下は、Venia プロジェクトの PDP ページで作成された、Agatha スカートの **JSON+LD** 構造の例です。

```
<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@type": "Product",
  "sku": "VSK05",
  "name": "Agatha Skirt",
  "image": "https://mcstaging.catalogservice4commerce.fun/media/catalog/product/cache/926ea6fc2ad48a7202ff4587b6c2768e/v/s/vsk05-pe_main_2.jpg",
  "description": "The Agatha Skirt has a large circumference that lends itself to all sorts of drama...",
  "@id": "product-ef4fa1dc72",
  "offers": [
    {
      "@type": "Offer",
      "sku": "VSK05-KH-S",
      "url": "/content/venia/us/en/products/product-page.html/agatha-skirt.html",
      "priceCurrency": "USD",
      "price": 78.0
    },
    {
      "@type": "Offer",
      "sku": "VSK05-RN-XS",
      "availability": "InStock",
      "priceSpecification": {
        "@type": "UnitPriceSpecification",
        "priceType": "https://schema.org/ListPrice",
        "price": 18.0,
        "priceCurrency": "USD"
      },
      "price": 46.0
    }
  ]
}
</script>
```

## JSON+LD 属性のGraphQLへのマッピング {#mapping}

JSON+LD 属性はAEM CIFのGraphQL クエリにマッピングでき、構造化データはGraphQLで取得された商品情報を動的に反映します。

### 製品マッピングの例 {#example}

| JSON+LD 属性 | Magento GraphQL属性 | 必須（Y/N） |
|---------------------------------|-------------------|---|
| sku | sku | × |
| offers.url | カスタムロジック | × |
| offers.SpecialPricedate | special_to_date | × |
| offers.sku | sku | × |
| offers.priceSpecification.priceCurrency | 通貨 | ○ |
| offers.priceSpecification.price | regular_price | × |
| offers.priceCurrency | 通貨 | ○ |
| offers.price | special_price | ○ |
| offers.image | media_gallery.url | × |
| offers.availability | stock_status | × |
| name | name | ○ |
| 画像 | media_gallery.url | ○ |
| 説明 | 説明 | × |
| aggregateRating.reviewCount | review_count | × |
| aggregateRating.ratingValue | rating_summary | × |
| @id | id | × |

このマッピングにより、GraphQL クエリを使用して取得した商品データに基づいて、JSON+LD スクリプトが動的に入力されます。

JSON+LD 構造をテストするには、[ リッチ結果テスト - Google Search Console](https://search.google.com/test/rich-results/result?id=wtU3LVIEM8H7Aaf5qqK9qw) を使用します。 このツールは、必要な属性が存在するかどうかなど、詳細なフィードバックを提供し、構造化データが正しく実装されていることを確認するのに役立ちます。
