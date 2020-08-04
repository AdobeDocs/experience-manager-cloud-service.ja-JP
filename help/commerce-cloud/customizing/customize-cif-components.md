---
title: CIFコアコンポーネントのカスタマイズ
description: CIFコアコンポーネントのカスタマイズ
translation-type: tm+mt
source-git-commit: c3cf472f5e207e7ca0788dc3e42105868d9bdf00
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 3%

---


# AEM CIFコアコンポーネントのカスタマイズ {#customize-cif-components}

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) （CIFコアコンポーネント）は、Adobe Experience Manager(AEM)とMagentoソリューションを統合するプロジェクトの迅速化に役立つ、標準的なコマースコンポーネントのセットを提供します。 これらのコンポーネントは、運用に対応しており、CSSを [使用して簡単にスタイル設定できます](style-cif-component.md)。 多くの実装では、ビジネス固有の要件を満たすために、これらのコンポーネントを拡張する必要があります。

このチュートリアルでは、AEM CIFコアコンポーネントとAEMが提供する一般的な拡張機能ポイントのいくつかを確認します。 これを行うには、 [Product Teaserコンポーネントの機能を拡張して、「New」バナーのレンダリング機能を含めます](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) 。 コンテンツ作成者は、このバナーを切り替えて、バナーの表示期間を指定できます。 商品の「年齢」は、Magentoカタログの作成日に基づきます。 製品が一定日数経過したら、「新規」バナーは自動的に消えます。

![新しいバナー拡張](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## 前提条件 {#prerequisites}

次のツールとテクノロジーが必要です。

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) （3.3.9以降）
* [AEM Cloud SKDとCIFアドオン](../develop.md)
* CIFコアコンポーネントと互換性のあるMagento

このチュートリアルに進む前に、次の内容を確認することをお勧めします。

* [Cloud ServiceとしてのAEM上でのCommerce Integration Frameworkの概要](/help/commerce-cloud/overview.md)
* [スタイルAEM CIFコアコンポーネント — チュートリアル](style-cif-component.md)

## スタータープロジェクト

このチュートリアルで使用するスタータープロジェクトを用意しました。 プロジェクトは、CIFプロジェクトアーキタイプ [のv0.7.0](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) を使用して生成されました。 新しいプロジェクトを開始する際は、常に [最新リリースのアーキタイプを使用することをお勧めします](https://github.com/adobe/aem-cif-project-archetype/releases/latest) 。

1. スタータープロジェクト [**acme-store.zipをデスクトップにダウンロードします&#x200B;**](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip)。

1. 「 **acme-store.zip** 」を解凍すると、次のフォルダー構造が表示されます。

   ```plain
   /acme-store
      /ui.content
      /ui.apps
      /samplecontent
      /core
      /all
      + pom.xml
      + README.md
   ```

1. 新しいターミナルウィンドウを開き、プロジェクトを構築し、AEMのローカルインスタンスに展開します。

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. AEMインスタンス追加をMagentoインスタンスに接続したり、新しく作成したプロジェクトに設定を追加したりするために必要なOSGi設定。

1. この時点で、Magentoインスタンスに接続されたストアフロントの作業バージョンが必要です。 次の場所にある `US` / `Home` ページに移動します。 [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   現在、店頭ではベニアのテーマが使用されていることがわかります。 ストアフロントのメインメニューを展開すると、様々なカテゴリが表示され、接続Magentoが機能していることが示されます。

   ![ベニアテーマで構成されたストアフロント](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## Product Teaserの作成 {#author-product-teaser}

このチュートリアル全体で、Product Teaserコンポーネントの拡張を行います。 最初の手順として、Product Teaserの新しいインスタンスをホームページに追加し、ベースライン機能を理解します。

1. サイトの **ホームページ** : [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. ページのメインレイアウトコンテナに新しい **製品Teaser** コンポーネントを挿入します。

   ![Product Teaserの挿入](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. サイドパネルを展開し（まだ切り替えていない場合）、アセットファインダードロップダウンを **製品に切り替えます**。 これにより、接続されたMagentoインスタンスから使用可能な商品のリストが表示されます。 製品を選択し、ページ上の **製品ティーザー****(Product Teaser** )コンポーネントにドラッグ&amp;ドロップします。

   ![Product Teaserをドラッグ&amp;ドロップ](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > 注意：ダイアログ( *レンチ* アイコンをクリック)を使用してコンポーネントを設定することで、表示された製品を設定することもできます。

1. これで、Product Teaserによって製品が表示されます。 製品の名前と製品の価格は、表示されるデフォルトの属性です。

   ![製品ティーザー — デフォルトスタイル](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## Product Teaserのマークアップのカスタマイズ {#customize-markup-product-teaser}

AEMコンポーネントの一般的な拡張機能は、コンポーネントによって生成されたマークアップを変更することです。 これは、コンポーネントがマークアップのレンダリングに使用する [HTLスクリプトを上書きすることで行われます](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/overview.html) 。 HTML Template Language(HTL)は、AEMコンポーネントがオーサリングされたコンテンツに基づいて動的にマークアップをレンダリングし、コンポーネントを再利用する際に使用する、軽量なテンプレート言語です。 例えば、Product Teaserを何度も繰り返し使用して、異なる製品を表示できます。

この例では、テーザーの上にバナーをレンダリングして、製品が「新規」で、最近カタログに追加されたことを示します。 コンポーネントのマークアップを [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) カスタマイズするデザインパターンは、AEM CIFコアコンポーネントだけでなく、すべてのAEMコンポーネントに対して実際に標準です。

選択したIDEを使用して、チュートリアルの最初にダウンロードしたスタータープロジェクト [を](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) 開きます。

1. ui.apps **** モジュールに移動して展開し、フォルダー階層を展開して次の操作を行います。 `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` ファイルを検査し `.content.xml` ます。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   上記は、プロジェクトのProduct Teaserコンポーネントのコンポーネント定義です。 プロパティに注目し `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`ます。 これは、 [プロキシコンポーネントの作成例です](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)。 AEM CIFコアコンポーネントからすべてのProduct Teaser HTLスクリプトをコピー&amp;ペーストする代わりに、を使用してすべての機能を継承す `sling:resourceSuperType` ることができます。

1. 新しいブラウザーを開き、AEMの [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) に移動します。 ツリーを展開して、次の下のコンポー `productteaser` ネントを表示します。 `/apps/core/cif/components/commerce/productteaser/v1/productteaser`:

   ![CRXDE Lite製品ティーザー](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   これは、Product Teaserコンポーネントの完全なコンポーネント定義です。

1. IDEとAcme Storeプロジェクトに戻ります。 Create a new file named `productteaser.html` beneath `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. CRXDE-Lite `productteaser.html` の内容を [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)`productteaser.html` からコピーし、新しく作成したファイルのAcme-Storeプロジェクトに貼り付けます。

   ![Product Teaserのhtml上書き](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. Acme-Storeプロジェクトで、 `productteaser.html` ファイルを変更し、製品の画像マークアップの上にバッジを表す新しいdivを挿入します。

   ```html
   ...
   <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
       <!-- Add Badge -->
       <div class="item__badge">
           <span>New</span>
       </div>
       <!-- end add badge -->
       <a class="item__images" href=${product.url}>
           <img class="item__image" width="100%" height="100%"
                   src="${product.image}" alt="${product.image}"/>
       </a>
       <a class="item__name" href=${product.url}><span>${product.name}</span></a>
       <div class="item__price">
           <span> ${product.formattedPrice} </span>
       </div>
       <sly data-sly-call="${actionsTpl.actions @ product=product}"></sly>
   </div>
   ```

1. Mavenのスキルを使用するか、IDEの機能を使用して、更新したコードをAEMのローカルインスタンス [にデプロイします](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)。

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. ブラウザーで、AEMの店頭の [ホームページに戻ります](http://localhost:4502/editor.html/content/acme/us/en.html) 。 更新すると、コンポーネントの右上隅に「新しい」バナーが表示されます。

   ![新しいバナー拡張](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   現在のところ、バナーを表示するロジックはありません。 次の練習では、それを修正します。

   > バナーをレンダリングするCSSは、スタータープロジェクトの一部として提供されており、次の場所にあります。 `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. 詳しくは、「CIFコアコンポーネントの [スタイル設定](style-cif-component.md)」チュートリアルを参照してください。

## 製品テーザーのダイアログのカスタマイズ {#customize-dialog-product-teaser}

次に、「新規」と見なされる製品の日付範囲や、バナーを表示する必要があるかどうかを作成者が決定できるように、製品のTeaserコンポーネントのダイアログをカスタマイズします。 これを行うには、Acme Storeプロジェクトの一部としてProduct Teaserのダイアログを [カスタマイズします](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) 。

1. 任意のIDEでAcme Storeプロジェクトを開き、に移動し `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`ます。

1. Beneath the `productteaser` folder, add a new folder named `_cq_dialog`. 追加という名前の `_cq_dialog` フォルダーに新しいファイル `.content.xml`。 これで、次のファイル構造になります。

   ```plain
   ../acme
       /components
           /commerce
               /productteaser
                  /_cq_dialog
                     + .content.xml
                  /_cq_template
                  + .content.xml
                  + productteaser.html
   ```

1. 次 `_cq_dialog/.content.xml` のXMLで更新：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
       xmlns:cq="http://www.day.com/jcr/cq/1.0" 
       xmlns:jcr="http://www.jcp.org/jcr/1.0" 
       xmlns:nt="http://www.jcp.org/jcr/nt/1.0" 
       jcr:primaryType="nt:unstructured" 
       jcr:title="My Product Teaser" 
       sling:resourceType="cq/gui/components/authoring/dialog" 
       trackingFeature="cif-core-components:productteaser:v1">
       <content jcr:primaryType="nt:unstructured" 
           sling:resourceType="granite/ui/components/coral/foundation/container">
           <items jcr:primaryType="nt:unstructured">
               <tabs jcr:primaryType="nt:unstructured" 
                   sling:resourceType="granite/ui/components/coral/foundation/tabs" 
                   maximized="{Boolean}true">
                   <items jcr:primaryType="nt:unstructured">
                       <badge jcr:primaryType="nt:unstructured" 
                           jcr:title="Badge" 
                           sling:resourceType="granite/ui/components/coral/foundation/container" 
                           margin="{Boolean}true">
                           <items jcr:primaryType="nt:unstructured">
                               <columns jcr:primaryType="nt:unstructured" 
                                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns" 
                                   margin="{Boolean}true">
                                   <items jcr:primaryType="nt:unstructured">
                                       <column jcr:primaryType="nt:unstructured" 
                                           sling:resourceType="granite/ui/components/coral/foundation/container">
                                           <items jcr:primaryType="nt:unstructured">
                                               <badge jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/checkbox" 
                                                   text="Display 'New' badge" 
                                                   value="true" 
                                                   uncheckedValue="false" 
                                                   name="./badge" />
                                               <age jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield" 
                                                   fieldDescription="The maximum age in days the 'new' badge should be shown" 
                                                   fieldLabel="Max Product Age" 
                                                   name="./age"
                                                   min="{Long}0" 
                                                   value="10" />
                                               <ageTypeHint jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/foundation/form/hidden" 
                                                   ignoreData="{Boolean}true" 
                                                   name="./age@TypeHint" 
                                                   value="Long" />
                                           </items>
                                       </column>
                                   </items>
                               </columns>
                           </items>
                       </badge>
                   </items>
               </tabs>
           </items>
       </content>
   </jcr:root>
   ```

   上記では、新しいタブと1つの非表示フィールドの一部として、さらに2つのフィールドを追加しました。

   1. 「新規」バッジを表示するチェックボックス
   2. 製品の最大年齢を定義する数値フィールド
   3. 製品の最大期間が長く保存されるように非表示にするフィールドです(詳しくは、 [@TypeHint](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) を参照)。

   プロキシコンポーネントの一部として定義されたダイアログは、 [Sling Resource Margeと呼ばれる機能を持つ既存のすべてのダイアログフィールドを継承します](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/sling-resource-merger.html)。 したがって、Product Teaserの一部である既存のフィールドを再定義する必要はありません。

1. を更新 `productteaser.html` し、バッジ `data-sly-test` のにを追加 `<div>` します。 これは、ユーザーが「true」をチェックした場合にバッジを表示するかどうかを決定する簡単なテストです。

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. IDEの機能を使用するか、mavenスキルを使用して、更新したコードをAEMのローカルインスタンスにデプロイします。

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. 製品ティーザーコンポーネントに戻り、 *レンチ* アイコンをクリックしてダイアログを開きます。 これで、 **バッジのタブが表示され** 、さらに2つのフィールドが表示されます。 これらのフィールドを更新すると、値がAEMに保持されます。 次のチェックボックスを使用して、バッジのオン/オフを切り替えることができます。

   ![バッジの切り替え](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   これにより、バッジの表示タイミングを作成者が制御できるようになります。 ただし、製品の **最大使用期間のエントリに基づいて、製品が特定の年齢に達したら、バッジが自動的に消えるのが最適です**。 この場合、いくつかのバックエンドロジックを実装する必要があります。

## 製品ティーザーのSlingモデルの更新 {#updating-sling-model-product-teaser}

次に、Slingモデルを導入して、製品Teaserのビジネスロジックを拡張します。 [Slingモデル](https://sling.apache.org/documentation/bundles/models.html)(Sling Models)は、コンポーネントで必要なビジネスロジックを実装する注釈駆動の「POJO」(Plain Old Java Objects)です。 Slingモデルは、コンポーネントの一部としてHTLスクリプトと組み合わせて使用されます。 既存のProduct Teaserモデルの一部を拡張できるように、Slingモデルの [委任パターンに従います](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 。

SlingモデルはJavaとして実装され、生成されたプロジェクトの **コア** モジュールにあります。

1. 任意のIDEでAcme Storeプロジェクトを開き、 **core** モジュールの下で次の操作を行います。 `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java** は、CIF **** ProductTeaserインターフェイスを拡張する、事前に作成したJavaインターフェイスです。

1. 次に、次の場所にあるMyProductTeaserImpl.java **ファイルを開きます** 。 `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` は、インターフェイスの実装クラスで `MyProductTeaser`す。

   Slingモデルに対する [委任パターンを使用して](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 、次の `ProductTeaser` プロパティを使用して `sling:resourceSuperType` クラスを参照できます。

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   上書きや変更を望まないメソッドの場合は、単に次の値を返すことができ `ProductTeaser` ます。

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

1. AEM CIFコアコンポーネントが提供する拡張ポイントの1つに、特定の製品属性にアクセス `AbstractProductRetriever` できる拡張ポイントがあります。 次追加のメソッドを使用して、メソッド `AbstractProductRetriever` 内のを初期化し `init()` ます。

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
   
       }
   ...
   ```

1. フォーマットされた価格を変更し、のロジックを上書きして、これらの変更をテストし `getFormattedPrice()`ます。 ドイツ語のロケールに基づいて価格を明示的にフォーマットするように、次の更新を行います。 （または別の国を選ぶ！）

   ```java
           import java.util.Locale;
           import java.text.NumberFormat;
            ...
   
               @Override
                   public String getFormattedPrice() 
                   {
                   //return productTeaser.getFormattedPrice();
                   NumberFormat germanCurrencyFormat = NumberFormat.getCurrencyInstance(Locale.GERMANY);
                   Double price =  productRetriever.fetchProduct().getPrice().getRegularPrice().getAmount().getValue();
                       if(price != null) 
                       {
                           return germanCurrencyFormat.format(price);
                       }
                   return null;
                   }
   ```

   この `productRetriever` オブジェクトが、この `ProductInterface``fetchProduct()` メソッドを使用してオブジェクトにアクセスする方法を示します。 使用可能なすべての [メソッドは、ここで確認できます](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)。

   > 注意*ロケールをドイツ語に変更するのは、オーバーライドを見る楽しい例です。 実際、ProductTeaserは [ページのロケールを使用して形式を決定します](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173)。

1. 次に、 **ui.apps****** モジュールのproducteaser.htmlを更新して、次の場所で新しいSlingモデルを参照する必要があります。 `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
      ...
   ```

   に変更を保存し `productteaser.html`ます。

1. コードベースをAEMのローカルインスタンスにデプロイします。 ui.apps **と** コア **** モジュールの両方に変更が加えられたので、ルートからプロジェクトを構築しデプロイします。

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. ブラウザーを開き、次の場所に移動します。 [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels). このコンソールには、システムに登録されているSlingモデルがすべて表示されます。 MyTeaserModelImplがデプロイされ、正しくマッピングされていることを確認する重複チェック。 次のような表示が可能です。

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. 最後に、Product Teaserコンポーネントを作成した場所に移動し、次のようにドイツの通貨形式で価格が表示されます。

   ![価格の形式が更新されました](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## isShowBadgeロジックの実装 {#implement-isshowbadge}

これで、Slingモデルのメソッドの上書きを試す機会ができたので、「新しい」バッジを表示するタイミングのロジックを実装します。

1. IDEに戻り、次の場所にあるMyProductTeaser.java **** ファイルを開きます。 `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`.

1. 新し追加いメソッド、インターフェイス `isShowBadge()` への

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   }
   ```

   これは、バッジを表示するかどうかのロジックをカプセル化するために導入する新しい方法です。

1. 次に、MyProductTeaserImpl.java **をで再度開き**`core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`ます。

1. 「新しい」バッジを表示する期間のロジックは、製品の `created_at` 属性に基づきます。 この属性にアクセスするには、ProductTeaserで実行する **GraphQL** クエリを拡張する必要があります。 これを行うには、MyProductTeaserImpl.javaの `init()` メソッドを更新し **ます**。

   ```java
   //MyProductTeaserImpl.java
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           // Pass your custom partial query to the ProductRetriever. This class will
           // automatically take care of executing your query as soon
           // as you try to access any product property.
           productRetriever.extendProductQueryWith(p ->
               p.addCustomSimpleField("created_at")
           );
       }
   }
   ```

   この `extendProductQueryWith` 方法を追加すると、他の製品属性を確実にモデルの残りの部分で使用できるようになります。 また、実行されるクエリの数も最小限に抑えられます。

   >[!NOTE]
   >上記のコードでは`addCustomSimpleField` 、を使用して `created_at` プロパティを取得しています。 この例では、Magentoスキーマの一部であるカスタム属性をクエリする方法を説明します。
   >
   > ただし、この `created_at` プロパティは実際に [製品インターフェイスの一部として実装されているので](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) 、次のようにメソッドを再使用する方がよい方法です。 `productRetriever.extendProductQueryWith(p -> p.createdAt());`. 最も一般的に見つかるスキーマ属性のほとんどは実装されているので、真のカスタム属性 `addCustomSimpleField` に対してのみを使用します。

1. 次に、次の `isShowBadge()` メソッドを実装します。

   ```java
   import java.time.format.DateTimeFormatter;
   import java.util.Locale;
   import java.time.temporal.ChronoUnit;
   
   ...
   
   @Override
   public Boolean isShowBadge() {
        final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
   
        //Look at the checkbox from the dialog to see if we should even attempt to show the badge
        final boolean showBadge = properties.get("badge", false);
        if (showBadge) {
   
            //Look at the numberfield set from the dialog to determine the max "age" in days to compare too
            final int maxAgeProp = properties.get("age", 0);
   
           String createdAtString;
           try {
               //Grab the created_at property from the product
               //Here we show the example of retrieving the attribute as if it was a custom attribute
               // an alternative that would work is productRetriever.fetchProduct().getCreatedAt()
               createdAtString = productRetriever.fetchProduct().getAsString("created_at");
               log.info("***CREATED_AT**** " + createdAtString);
           } catch (SchemaViolationError e) {
               //it is possible that a schema error could be thrown if the attribute is not part of the schema
               log.error("Error determining to showBadge" , e);
               return false;
           }
   
            // Custom code to calc the date difference of the product creation
            // compared to today
           final LocalDate createdAt = LocalDate.parse(createdAtString, formatter);
            if (createdAt != null) {
   
                final long ageInDays = ChronoUnit.DAYS.between(createdAt, LocalDate.now());
                if (ageInDays < maxAgeProp) {
                    return true;
                }
            }
        }
        return false;
    }
   ```

   上記の方法では、まず、作成者がチェックボックスを使用してバッジ機能を有効にしたかどうかを確認します。 次に、ダイアログの一部として設定され `age` 、製品の保存日数を表すプロパティの値を読み取り、バナーが消えるまでの長さを表します。 最後に、その `created_at` 日付に基づいて、商品の古さを計算します。 2つの値を比較した後、バッジ `true` を表示します。他の場合 `false` も同様です。

1. 最後に、このメソッドを呼び出すには、 `productteaser.html` スクリプトにもう1つ追加する必要があり `isShowBadge()` ます。 のファイルを開き `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`ます。 次の更新を行います。

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. コードベースをAEMのローカルインスタンスにデプロイします。 ui.apps **と** コア **** モジュールの両方に変更が加えられたので、ルートからプロジェクトを構築しデプロイします。

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. AEMとProductTeaserコンポーネントに戻り、異なる数値を試して製品の最大経過時間を表示します。 製品の古さに応じて、バッジを表示するには、非常に大きな数値を入力する必要があります。

   ![製品の最大年齢999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. 最後に、AEMログを検索して、上記の手順5で入力したログ文を確認します。 これは、Magentoから取得される `created_at` プロパティの値を出力する必要があります。 ファイルを開いてAEMのログを表示でき `error.log` ます。 このファイルは、AEM jarがインストールされ `crx-quickstart/logs/error.log` ている場所の下にあります。 次のような行項目が表示されます。

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   これで、実装したロジックが正しいことを確認できます。

### Congratulations {#congratulations}

最初のAEM CIFコンポーネントをカスタマイズしただけです。 Download the [finished solution package here](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip).

## その他のリソース {#additional-resources}

* [AEMアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)
* [AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)
* [AEM CIFコアコンポーネントのカスタマイズ](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [コアコンポーネントのカスタマイズ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
