---
title: CIF Product Carousel のカスタム属性
description: Sling モデルを更新し、マークアップをカスタマイズして、AEM CIF Product Carousel コンポーネントを拡張する方法を説明します。
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 594f0e6ec88851c86134be8d5d7f1719f74ddf4f
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# CIF Product Carousel のカスタム属性 {#product-carousel}

## はじめに {#intro}

製品カルーセルコンポーネントは、このチュートリアル全体を通して拡張されています。 最初の手順として、製品カルーセルのインスタンスをホームページに追加して、ベースライン機能を理解します。

1. サイトのホームページ（例：）に移動します。 [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)
1. 新しい製品カルーセルコンポーネントをページのメインのレイアウトコンテナに挿入します。
   ![製品カルーセルコンポーネント](/help/commerce-cloud/assets/product-carousel-component.png)
1. サイドパネルを展開し（まだ切り替えていない場合）、アセットファインダードロップダウンをに切り替えます。 **製品**.
     ![カルーセル製品](/help/commerce-cloud/assets/carousel-products.png)    
1. 接続されたAdobe Commerce インスタンスから使用可能な製品のリストが表示されます。
   ![接続されたインスタンス](/help/commerce-cloud/assets/connected-instance.png)
1. 製品は、デフォルトのプロパティを使用して以下のように表示されます。
   ![プロパティと共に表示される製品](/help/commerce-cloud/assets/discount.png)

## Sling モデルを更新する {#update-sling-model}

Sling モデルを実装して、製品カルーセルのビジネスロジックを拡張できます。

1. IDE で、コア モジュールの下に移動して、次の操作を行います。 `core/src/main/java/com/venia/core/models/commerce` さらに、CIF ProductCarousel インターフェイスを拡張する CustomCarousel インターフェイスを作成します。

   ```
   package com.venia.core.models.commerce;
   import com.adobe.cq.commerce.core.components.models.productcarousel.ProductCarousel;
   public interface CustomCarousel extends ProductCarousel {
   }
   ```
1. 次に、実装クラスを作成します `CustomCarouselImpl.java` 時刻 `core/src/main/java/com/venia/core/models/commerce/CustomCarouselImpl.java`.
Sling モデルの委任パターンでは、次のことが可能です `CustomCarouselImpl` 参照 `ProductCarousel` を使用したモデル `sling:resourceSuperType` プロパティ：

   ```
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductCarousel productCarousel;
   ```

1. @PostConstruct 注釈により、Sling モデルの初期化時にこのメソッドが確実に呼び出されます。 製品GraphQL クエリは、属性を取得するために extendProductQueryWith メソッドを使用して既に拡張されています。 GraphQL クエリを更新して、部分的なクエリに属性を含めます。

   ```
   @PostConstruct
   private void initModel() {
   productsRetriever = productCarousel.getProductsRetriever();
   
   if(productCarousel.getProductsRetriever() != null)
   productCarousel.getProductsRetriever().extendProductQueryWith(p -> p
   .createdAt()
   .addCustomSimpleField("accessory_gemstone_addon")
   );
   }
   ```

   上記のコードでは、 `addCustomSimpleField` は、を取得するために使用されます。 `accessory_gemstone_addon` 属性。

## マークアップのカスタマイズ {#customize-markup}

マークアップをさらにカスタマイズするには：

1. のコピーを作成 `productcard.html` から `/apps/core/cif/components/commerce/productcarousel/v1/productcarousel` （コアコンポーネントの crxde パス） ui.apps モジュールへ `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productcarousel/productcard.html`.

1. 編集 `productcard.html` 実装クラスに記載されているカスタム属性を呼び出すには、次の手順を実行します。

   ```xml
   ..
   <div
       data-product-sku="${product.commerceIdentifier.value}"
       data-product-base-sku="${product.combinedSku.baseSku}"
       id="${product.id}"
       data-cmp-data-layer="${product.data.json}"
       class="card product__card">
       <span>${product.product.responseData['accessory_gemstone_addon']}</span>
       <a href="${product.URL}"
           target="${productCarousel.linkTarget}"
   ..
   ```

1. コマンドラインターミナルから Maven コマンドを使用して、変更を保存し、更新をAEMにデプロイします。 カスタム属性を確認できます `accessory_gemstone_addon` ページで選択した製品の値。
