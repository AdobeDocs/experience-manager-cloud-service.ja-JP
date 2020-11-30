---
title: CIF コアコンポーネントのカスタマイズ
description: AEM CIF コアコンポーネントをカスタマイズする方法を説明します。このチュートリアルでは、ビジネス固有の要件を満たすために、CIF コアコンポーネントを安全に拡張する方法について説明します。GraphQL クエリを拡張してカスタム属性を返し、新しい属性を CIF コアコンポーネントに表示する方法を説明します。
sub-product: Commerce
topics: Development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '2550'
ht-degree: 100%

---


# AEM CIF コアコンポーネントのカスタマイズ {#customize-cif-components}

[CIF Venia プロジェクト](https://github.com/adobe/aem-cif-guides-venia)は、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)を使用するための参照用コードベースです。このチュートリアルでは、[製品ティーザー](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser)コンポーネントをさらに拡張して、Magento のカスタム属性を表示します。また、AEM と Magento 間の GraphQL 統合、および CIF コアコンポーネントによって提供される拡張フックについても学習します。

>[!TIP]
>
> 独自のコマース実装を開始する際に [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)を使用します。

## 作成する内容

Venia ブランドは最近、持続可能な資材を使用して一部の製品を製造し始めました。同社は、**エコフレンドリー**&#x200B;バッジを製品ティーザーの一部として表示したいと考えています。製品が&#x200B;**エコフレンドリー**&#x200B;な資材を使用しているかどうかを示す新しいカスタム属性が Magento で作成されます。次に、このカスタム属性が GraphQL クエリの一部として追加され、特定の製品の製品ティーザーに表示されます。

![エコフレンドリーバッジの最終実装](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 前提条件 {#prerequisites}

このチュートリアルを完了するには、ローカルの開発環境が必要です。これには、Magento インスタンスに設定および接続された AEM の実行インスタンスが含まれます。[AEM as a Cloud Service SDK を使用してローカル開発をセットアップする](../develop.md)ための要件と手順を確認します。このチュートリアルを完全に実行するには、[属性を Magento 内の製品に追加](https://docs.magento.com/user-guide/catalog/product-attributes-add.html)する権限が必要になります。

また、コード例やチュートリアルを実行するには、[GraphiQL ](https://github.com/graphql/graphiql) またはブラウザー拡張機能などの GraphQL IDE が必要です。ブラウザー拡張機能をインストールする場合は、その拡張機能にリクエストヘッダーを設定できることを確認してください。Google Chrome の [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) は、ジョブを実行できる拡張機能の 1 つです。

## Venia プロジェクトのクローン {#clone-venia-project}

Venia プロジェクト[のクローンを作成して](https://github.com/adobe/aem-cif-guides-venia)、デフォルトのスタイルを上書きします。

>[!NOTE]
>
> （CIF を含む AEM プロジェクトアーキタイプに基づく）**既存のプロジェクトを使用**&#x200B;する場合、このセクションをスキップできます。

1. 次の git コマンドを実行して、プロジェクトのクローンを作成します。

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. プロジェクトをビルドしてローカル AEM インスタンスにデプロイします。

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. AEM インスタンスを Magento インスタンスに接続するために必要な OSGi 構成を追加するか、新しく作成されたプロジェクトに構成を追加します。

1. この時点で、Magento インスタンスに接続されたストアフロントの作業用のバージョンが必要です。`US`／`Home` ページ（[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)）にアクセスします。

   ストアフロントは現在 Venia テーマを使用しています。ストアフロントのメインメニューを展開すると、様々なカテゴリが表示され、接続 Magento が機能していることが示されます。

   ![Venia テーマで構成されたストアフロント](../assets/customize-cif-components/venia-store-configured.png)

## 製品ティーザーの作成 {#author-product-teaser}

製品ティーザーコンポーネントは、このチュートリアル全体で拡張されます。最初の手順として、製品ティーザーの新しいインスタンスをホームページに追加し、ベースライン機能を理解します。

1. サイトの&#x200B;**ホームページ**（[http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)）に移動します。

2. ページのメインレイアウトコンテナに新しい&#x200B;**製品ティーザー**&#x200B;コンポーネントを挿入します。

   ![製品ティーザーの挿入](../assets/customize-cif-components/product-teaser-add-component.png)

3. サイドパネルを展開し（まだ切り替えていない場合）、アセットファインダードロップダウンを「**製品**」に切り替えます。接続された Magento インスタンスから使用可能な製品のリストが表示されます。製品を選択し、ページ上の&#x200B;**製品ティーザー**&#x200B;コンポーネントに&#x200B;**ドラッグ＆ドロップ**&#x200B;します。

   ![製品ティーザーのドラッグ＆ドロップ](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > ダイアログ（*レンチ*&#x200B;アイコンをクリック）を使用してコンポーネントを設定することで、表示された製品を設定することもできます。

4. これで、製品ティーザーによって製品が表示されます。製品名と製品の価格は、表示されるデフォルトの属性です。

   ![製品ティーザー - デフォルトスタイル](../assets/customize-cif-components/product-teaser-default-style.png)

## Magento カスタム属性の追加 {#add-custom-attribute}

AEM に表示された製品と製品データは Magento に格納されます。次に、Magento UI を使用して設定する製品属性の一部として、新しい&#x200B;**エコフレンドリー**&#x200B;属性を追加します。

>[!TIP]
>
> 製品属性セットの一部として、既にカスタムの&#x200B;**はい／いいえ**&#x200B;属性がある場合は、それを使用して、この節をスキップしてください。

1. Magento インスタンスにログインします。
1. **カタログ**／**製品**&#x200B;に移動します。
1. 検索フィルターをアップデートして、前の練習でティーザーコンポーネントに追加した場合に使用する&#x200B;**構成可能な製品**&#x200B;を見つけます。製品を編集モードで開きます。

   ![Valeria 製品の検索](../assets/customize-cif-components/search-valeria-product.png)

1. 製品の表示で、**属性を追加**／**新しい属性を作成**&#x200B;をクリックします。
1. 次の値を使用して&#x200B;**新規属性**&#x200B;フォームに入力します（他の値はデフォルト設定のままにします）。

   | フィールドセット | フィールドラベル | 値 |
   |-----------|-------------|---------|
   | 属性プロパティ | 属性ラベル | **エコフレンドリー** |
   | 属性プロパティ | カタログ入力タイプ | **はい／いいえ** |
   | 高度な属性プロパティ | 属性コード | **eco_friendly** |

   ![新規属性フォーム](../assets/customize-cif-components/attribute-new-form.png)

   終了したら「**属性を保存**」をクリックします。

1. 製品の下部までスクロールし、「**属性**」見出しを展開します。新しい「**エコフレンドリー**」フィールドが表示されます。切り替えボタンを「**はい**」に切り替えます。

   ![「はい」に切り替える](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   変更内容を製品に&#x200B;**保存**&#x200B;します。

   >[!TIP]
   >
   > 製品属性の管理の詳細については、『[Magento ユーザーガイド](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)』を参照してください。

1. **システム**／**ツール**／**キャッシュ管理**&#x200B;に移動します。データスキーマはアップデートされたので、Magento 内のキャッシュタイプの一部を無効にする必要があります。
1. 「**設定**」の横のチェックボックスをオンにして、**更新**&#x200B;用にキャッシュタイプを送信します。

   ![構成キャッシュタイプの更新](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > キャッシュ管理の詳細については、『[Magento ユーザーガイド](https://docs.magento.com/user-guide/system/cache-management.html)』を参照してください。

## GraphQL IDE を使用した属性の検証 {#use-graphql-ide}

AEM コードを始める前に、GraphQL IDE を使用して [Magento GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) を調べてみると役に立ちます。AEM との Magento 統合は、主に一連の GraphQL クエリを介して実行されます。GraphQL クエリを理解し変更することは、CIF コアコンポーネントを拡張するのに重要なことの 1 つです。

次に、GraphQL IDE を使用して、`eco_friendly` 属性が製品属性セットに追加されたことを確認します。このチュートリアルのスクリーンショットは、[Altair GraphQL クライアント](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)を使用しています。

1. GraphQL IDE を開き、IDE または拡張機能の URL バーに URL `http://<magento-server>/graphql` を入力します。
2. 次の[製品クエリ](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html)を追加します。ここで、`YOUR_SKU` は、前の演習で使用した製品の **SKU** です。

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. クエリを実行すると、次のような応答が返されます。

   ```json
   {
   "data": {
       "products": {
           "items": [
               {
               "name": "Valeria Two-Layer Tank",
               "sku": "VT11",
               "eco_friendly": 1
               }
           ]
           }
       }
   }
   ```

   ![GraphQL の応答例](../assets/customize-cif-components/sample-graphql-query.png)

   「**はい**」の値は整数 **1** です。これは、GraphQL クエリを Java で記述する場合に役立ちます。

   >[!TIP]
   >
   > Magento GraphQL に関する詳細なドキュメントは、[こちら](https://devdocs.magento.com/guides/v2.4/graphql/index.html)を参照してください。

## 製品ティーザーの Sling モデルのアップデート {#updating-sling-model-product-teaser}

次に、Sling モデルを実装して、製品ティーザーのビジネスロジックを拡張します。[Sling モデル](https://sling.apache.org/documentation/bundles/models.html)は、コンポーネントで必要なビジネスロジックを実装する注釈駆動型の「POJO」（Plain Old Java Objects）です。Sling モデルは、コンポーネントの一部として HTL スクリプトと組み合わせて使用されます。既存の製品ティーザーモデルの一部を拡張できるように、[Sling モデルの委任パターン](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)に従います。

Sling モデルは Java として実装され、生成されたプロジェクトの&#x200B;**コア**&#x200B;モジュールにあります。

[任意の IDE](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) を使用して、Venia プロジェクトをインポートします。使用したクリーンショットは、[Visual Studio Code IDE](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code) からのものです。

1. IDE で、**コア**&#x200B;モジュールの下に移動して、次の操作をおこないます。`core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`

   ![コアのロケーション IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` は、CIF [製品ティーザー](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java)インターフェイスを拡張する Java インターフェイスです。

   製品が「新規」と見なされた場合にバッジを表示するための新しい `isShowBadge()` メソッドが既に追加されています。

1. 新しい `isEcoFriendly()` メソッドをインターフェイスに追加します。

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   これは、製品の `eco_friendly` 属性が「**はい**」と「**いいえ**」のどちらに設定されているかを示すロジックをカプセル化する新しいメソッドです。

1. 次に、`core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java` で `MyProductTeaserImpl.java` を検査します。

   [Sling モデルの委任パターン](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)を使用すると、`MyProductTeaserImpl` は `sling:resourceSuperType` プロパティを介して `ProductTeaser` モデルを参照できます。

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   上書きや変更を望まないすべてのメソッドに対しては、単に `ProductTeaser` の戻り値を返すだけです。次に例を示します。

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   これにより、実装で記述する必要のある Java コードの量を最小限に抑えることができます。

1. AEM CIF コアコンポーネントが提供する拡張ポイントの 1 つに、特定の製品属性へのアクセスを提供する `AbstractProductRetriever` があります。`initModel()` メソッドを検査します。

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   `@PostConstruct` 注釈により、Sling モデルが初期化されるとすぐにこのメソッドが呼び出されます。

   製品の GraphQL クエリは、追加の `created_at` 属性を取得するために `extendProductQueryWith` メソッドを使用して既に拡張されています。この属性は、後で `isShowBadge()` メソッドの一部として使用されます。

1. GraphQL クエリをアップデートし、`eco_friendly` 属性を部分クエリに含めます。

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p ->
                productRetriever.extendProductQueryWith(p -> p
                   .createdAt()
                   .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
               );
           );
       }
   }
   ```

   `extendProductQueryWith` メソッドに追加すると、他の製品属性を確実にモデルの残りの部分で使用できるようになります。また、実行されるクエリの数も最小限に抑えられます。

   上記のコードでは、`eco_friendly` 属性を取得するために `addCustomSimpleField` が使用されます。この例では、Magento スキーマの一部であるカスタム属性をクエリする方法を説明します。

   >[!NOTE]
   >
   > `createdAt()` メソッドは、[製品インターフェイス](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)の一部として実装されています。一般的なスキーマ属性のほとんどは実装されているので、真のカスタム属性に対してのみ `addCustomSimpleField` を使用します。

1. Java コードのデバッグに役立つロガーを追加します。

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 次に、`isEcoFriendly()` メソッドを実装します。

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   上記のメソッドでは、`productRetriever` が製品の取得に使用され、`getAsInteger()` メソッドが `eco_friendly` 属性の値の取得に使用されます。先ほど実行した GraphQL クエリに基づいて、 `eco_friendly` 属性が「**はい**」に設定された場合の期待値は、実際には整数 **1** であることがわかっています。

   Sling モデルがアップデートされたので、Sling モデルに基づいて&#x200B;**エコフレンドリー**&#x200B;という指標を実際に表示するには、コンポーネントマークアップをアップデートする必要があります。

## 製品ティーザーのマークアップのカスタマイズ {#customize-markup-product-teaser}

AEM コンポーネントの一般的な拡張機能は、コンポーネントによって生成されたマークアップを変更することです。これは、コンポーネントがマークアップのレンダリングに使用する [HTL スクリプト](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/overview.html)を上書きすることでおこなわれます 。HTML Template Language（HTL）は、AEM コンポーネントがオーサリングされたコンテンツに基づいて動的にマークアップをレンダリングし、コンポーネントを再利用する際に使用する、軽量なテンプレート言語です。例えば、製品ティーザーを何度も繰り返し使用すれば、異なる製品を表示できます。

この例では、ティーザーの上にバナーをレンダリングして、カスタム属性に基づいて製品が「エコフレンドリー」であることを示します。コンポーネントの[マークアップをカスタマイズ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup)するデザインパターンは、AEM CIF コアコンポーネントだけでなく、すべての AEM コンポーネントに対して実際に標準です。

1. IDE で、`ui.apps` モジュールに移動して展開し、フォルダー階層を `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` まで展開し、`.content.xml` ファイルを検査します。

   ![製品ティーザー ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   上記は、プロジェクトの製品ティーザーコンポーネントのコンポーネント定義です。`sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"` プロパティに注目してください。これは、[プロキシコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/get-started/using.html#create-proxy-components)の作成例です。AEM CIF コアコンポーネントからすべての製品ティーザー HTL スクリプトをコピー＆ペーストする代わりに、`sling:resourceSuperType` を使用してすべての機能を継承することができます。

1. `productteaser.html` ファイルを開きます。これは、[CIF 製品ティーザー](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)からの `productteaser.html` ファイルのコピーです。

   ```html
   <!--/* productteaser.html */-->
   <sly data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
       data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
       data-sly-use.actionsTpl="actions.html"
       data-sly-test.isConfigured="${properties.selection}"
       data-sly-test.hasProduct="${product.url}">
   ```

   `MyProductTeaser` の Sling モデルが使用され、 `product` 変数に割り当てられていることに注意してください。

1. `productteaser.html` を変更して、前の演習で実装した `isEcoFriendly` メソッドを呼び出します。

   ```html
   ...
   <div data-sly-test="${isConfigured && hasProduct}" class="item__root" data-cmp-is="productteaser" data-virtual="${product.virtualProduct}">
       <div data-sly-test="${product.showBadge}" class="item__badge">
           <span>${properties.text || 'New'}</span>
       </div>
       <!--/* Insert call to Eco Friendly here */-->
       <div data-sly-test="${product.ecoFriendly}" class="item__eco">
           <span>Eco Friendly</span>
       </div>
   ...
   ```

   Sling モデルメソッドを HTL で呼び出すと、メソッドの `get` および `is` 部分が削除され、最初の文字が小文字に変換されます。`isShowBadge()` は `.showBadge` となり、`isEcoFriendly` は `.ecoFriendly` となります。`.isEcoFriendly()` から返されるブール値に基づいて、`<span>Eco Friendly</span>` が表示されるかどうかを決定します。

   `data-sly-test` などの HTL ブロック文の詳細については、[こちら](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/htl/block-statements.translate.html#test)を参照してください。

1. 変更を保存し、コマンドラインターミナルから Maven を使用して AEM にアップデートをデプロイします。

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 新しいブラウザーウィンドウを開いて AEM に移動し、**OSGi コンソール**／**ステータス**／**Sling モデル**：[http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels) に移動します。

1. `MyProductTeaserImpl` を検索すると、次のような行が表示されます。

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   これは、Sling モデルが正しくデプロイされ、正しいコンポーネントにマッピングされていることを示します。

1. **Venia ホームページ**（[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)）を更新します。製品ティーザーが追加されています。

   ![エコフレンドリーメッセージの表示](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   製品の `eco_friendly` 属性が「**はい**」に設定されている場合、ページに「エコフレンドリー」というテキストが表示されます。異なる製品に切り替えて、動作の変更を確認してください。

1. 次に AEM `error.log` を開き、追加したログ文を確認します。`error.log` は、`<AEM SDK Install Location>/crx-quickstart/logs/error.log` にあります。

   AEM ログを検索して、Sling モデルに追加されたログ文を確認します。

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > また、ティーザーで使用される製品が属性セットの一部としての `eco_friendly` 属性を持たない場合は、スタックトレースが表示されることがあります。

## エコフレンドリーバッジにスタイルを追加 {#add-styles}

この時点で、**エコフレンドリー**&#x200B;バッジを表示するタイミングのロジックは機能していますが、プレーンテキストなのでスタイルを設定できます。次に、`ui.frontend` モジュールにアイコンとスタイルを追加し、実装を完了します。

1. [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) ファイルをダウンロードします 。これは、**エコフレンドリー**&#x200B;バッジとして使用されます。
1. IDE に戻り、`ui.frontend` フォルダーに移動します。
1. `eco_friendly.svg` ファイルを `ui.frontend/src/main/resources/images` フォルダーに格納します。

   ![エコフレンドリー SVG の追加](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. `productteaser.scss`（`ui.frontend/src/main/styles/commerce/_productteaser.scss`）ファイルを開きます。
1. 次の Sass ルールを `.productteaser` クラス内に追加します。

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg'); 
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > フロントエンドワークフローに関する詳細については、「[CIF コアコンポーネントのスタイル設定](./style-cif-component.md)」を参照してください。

1. 変更を保存し、コマンドラインターミナルから Maven を使用して AEM にアップデートをデプロイします。

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. **Venia ホームページ**（[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)）を更新します。製品ティーザーが追加されています。

   ![エコフレンドリーバッジの最終実装](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## これで完了です。{#congratulations}

最初の AEM CIF コンポーネントをカスタマイズしました。完成したソリューションファイルを[こちら](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip)からダウンロードしてください。

## ボーナスチャレンジ {#bonus-challenge}

製品ティーザーに既に実装されている&#x200B;**新規**&#x200B;バッジの機能を確認します。作成者が&#x200B;**エコフレンドリー**&#x200B;バッジをいつ表示するかを制御するためのチェックボックスを追加してみます。`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml` でコンポーネントダイアログをアップデートする必要があります。

![新しいバッジの実装の課題](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## その他のリソース {#additional-resources}

* [AEM アーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)
* [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)
* [AEM CIF コアコンポーネントのカスタマイズ](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [コアコンポーネントのカスタマイズ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/customizing.html)
* [AEM Sites 使用の手引き](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
