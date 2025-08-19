---
title: CIF 製品カルーセルに対するカスタム属性
description: Sling モデルを更新し、マークアップをカスタマイズして、AEM CIF 製品カルーセルコンポーネントを拡張する方法について説明します。
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 758e0e13-c4d8-4d32-bcc9-91a36b3ffa98
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 76%

---


# CIF 製品カルーセルに対するカスタム属性 {#product-carousel}

Sling モデルを更新し、マークアップをカスタマイズして、AEM CIF 製品カルーセルコンポーネントを拡張する方法について説明します。

## はじめに {#intro}

このチュートリアルでは、全体を通じて、製品カルーセルコンポーネントの拡張を行います。最初の手順として、製品カルーセルのインスタンスをホームページに追加し、ベースライン機能を理解します。

1. サイトのホームページ（例：[http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)）に移動します
1. 新しい製品カルーセルコンポーネントをページのメインのレイアウトコンテナに挿入します。

   ![製品カルーセルコンポーネント](/help/commerce-cloud/cif-storefront/assets/product-carousel-component.png)

1. サイドパネルを展開し（まだ切り替えていない場合）、アセットファインダードロップダウンを **製品** に切り替えます。

   ![ カルーセル製品 ](/help/commerce-cloud/cif-storefront/assets/carousel-products.png)

1. 接続された Adobe Commerce インスタンスから使用可能な製品のリストが表示されます。

   ![接続済みインスタンス](/help/commerce-cloud/cif-storefront/assets/connected-instance.png)

1. 製品は、以下のようにデフォルトのプロパティで表示されます。

   ![プロパティで表示される製品](/help/commerce-cloud/cif-storefront/assets/discount.png)

## Sling モデルの更新 {#update-sling-model}

Sling モデルを実装して、製品カルーセルのビジネスロジックを拡張できます。

1. IDE で、コアモジュールの下にある `core/src/main/java/com/venia/core/models/commerce` に移動し、CIF ProductCarousel インターフェイスを拡張する CustomCarousel インターフェイスを作成します。

   ```text
   package com.venia.core.models.commerce;
   import com.adobe.cq.commerce.core.components.models.productcarousel.ProductCarousel;
   public interface CustomCarousel extends ProductCarousel {
   }
   ```

1. 次に、`CustomCarouselImpl.java` に実装クラス `core/src/main/java/com/venia/core/models/commerce/CustomCarouselImpl.java` を作成します。

   Sling モデルのデリゲーションパターンを使用すると、`CustomCarouselImpl` は `sling:resourceSuperType` プロパティを介して `ProductCarousel` モデルを参照できます。

   ```text
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductCarousel productCarousel;
   ```

1. `@PostConstruct` 注釈により、Sling モデルの初期化時にこのメソッドが確実に呼び出されます。 製品の GraphQL クエリは、属性を取得するために extendProductQueryWith メソッドを使用して既に拡張されています。GraphQL クエリを更新して、部分的なクエリに属性を含めます。

   ```javascript
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

   上記のコードでは、`accessory_gemstone_addon` 属性を取得するために `addCustomSimpleField` が使用されます。

## マークアップのカスタマイズ {#customize-markup}

マークアップをさらにカスタマイズするには：

1. `/apps/core/cif/components/commerce/productcarousel/v1/productcarousel`（コアコンポーネントの crxde パス）から ui.apps モジュール `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productcarousel/productcard.html` に `productcard.html` のコピーを作成します。

1. `productcard.html` を編集して、実装クラスに記載されているカスタム属性を呼び出します。

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

1. 変更を保存し、コマンドラインターミナルから Maven コマンドを使用して、AEM にアップデートをデプロイします。ページで選択した製品のカスタム属性 `accessory_gemstone_addon` 値を確認できます。
