---
title: JSON-LD メタデータ
description: AEM CIF で JSON+LD 機能を有効にして検証する方法を説明します。
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 547d3721-e094-4a42-8a7c-27e4ef97ea9c
source-git-commit: 6ee09ab274e26f6972a81e662b78030a71b3fc9b
workflow-type: ht
source-wordcount: '451'
ht-degree: 100%

---

# JSON-LD メタデータ {#json-ld}

このガイドでは、AEM CIF で JSON+LD 機能を有効にし検証する方法について説明します。

>[!NOTE]
>
> この機能は実験段階です。

## CIF 設定で JSON+LD を有効にする {#enabling}

デフォルトでは、「**JSON+LD を有効にする**」チェックボックスは CIF 設定に表示されません。この機能を有効にするには、チェックボックスを表示するために必要な OSGi 設定がプロジェクトに含まれている必要があります。この設定により、ユーザーは製品ページで JSON+LD スクリプトのサポートを切り替えることができます。
「**JSON+LD を有効にする**」チェックボックスを CIF 設定で使用できるようにするには、次の OSGi 設定 `
com.adobe.cq.cif.components.models.JsonLdFeatureEnable` をプロジェクトに追加します。
この設定の追加について詳しくは、パブリック aem-cif-guides-venia リポジトリの [Json-Ld の設定を追加](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.cif.components.models.JsonLdFeatureEnable.cfg.json)を参照してください。

この設定を追加して展開すると、CIF の設定にチェックボックスが表示されます。**JSON+LD** を有効にする手順は次のとおりです。

1. AEM の CIF 設定に移動します。
1. 継承をキャンセルします。
1. 「**JSON+LD を有効にする**」チェックボックスをオンにします。
1. 設定を保存します。

## 製品詳細ページ（PDP）での JSON+LD の検証 {#verify}

JSON+LD を検証する手順を説明するために、必要な JSON+LD 設定が既に追加されている場合の例として、Venia プロジェクトを使用して機能を有効にします。手順は次のとおりです。

1. ローカルの AEM インスタンスに移動し、製品詳細ページ（PDP）：http://localhost:4502/editor.html/content/venia/us/en/products/product-page.html を開きます
1. 製品詳細ページ（PDP）で製品を作成します。
1. **公開として表示**&#x200B;モードに切り替えます。
1. ブラウザーで&#x200B;**ページソースを表示**&#x200B;を開きます。
1. ページソースで JSON+LD を検索します。

正しく設定されている場合は、製品に関連付けられた JSON + LD スクリプトがページに挿入されます。

## 製品の JSON+LD 構造のサンプル {#sample}

以下は、Venia プロジェクトの PDP ページで作成された、Agatha Skirt の **JSON+LD** 構造の例です。

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

## JSON+LD 属性の GraphQL へのマッピング {#mapping}

JSON+LD 属性は AEM CIF の GraphQL クエリにマッピングでき、構造化データは GraphQL で取得された製品情報を動的に反映します。

### 製品マッピングの例 {#example}

| JSON+LD 属性 | Magento GraphQL 属性 | 必須（Y/N） |
|---------------------------------|-------------------|---|
| SKU | SKU | N |
| offers.url | Custom Logic | N |
| offers.SpecialPricedate | special_to_date | N |
| offers.sku | SKU | N |
| offers.priceSpecification.priceCurrency | currency | Y |
| offers.priceSpecification.price | regular_price | N |
| offers.priceCurrency | currency | Y |
| offers.price | special_price | Y |
| offers.image | media_gallery.url | N |
| offers.availability | stock_status | N |
| name | name | Y |
| 画像 | media_gallery.url | Y |
| description | description | N |
| aggregateRating.reviewCount | review_count | N |
| aggregateRating.ratingValue | rating_summary | N |
| @id | id | N |

このマッピングにより、GraphQL クエリを使用して取得した製品データに基づいて、JSON+LD スクリプトが動的に入力されます。

JSON+LD 構造をテストするには、[リッチ結果テスト - Google Search Console](https://search.google.com/test/rich-results/result?id=wtU3LVIEM8H7Aaf5qqK9qw) を使用します。このツールは、必要な属性が存在するかどうかなど、詳細なフィードバックを提供し、構造化データが正しく実装されていることを確認するのに役立ちます。
