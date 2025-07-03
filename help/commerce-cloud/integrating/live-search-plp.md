---
title: '[!DNL Live Search] 製品リストページのCIFコンポーネント'
description: CIF コンポーネントを使用して AEM サイトで [!DNL Live Search] 製品リストページコンポーネントを有効にします
exl-id: 7f2d9a43-a7cb-4d9d-a108-b016cd1ff81e
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 98%

---

# [!DNL Live Search] CIF コンポーネント {#live-search-cif-component}

Adobe Commerce の Live Search では、追加費用なしで、高速で関連性の高い直感的な検索エクスペリエンスを実現します。Adobe Sensei を活用した Live Search では、人工知能と機械学習アルゴリズムを使用して、集計された訪問者データの詳細な分析を実行します。このデータを Adobe Commerce カタログと組み合わせると、関連性の高いパーソナライズされたショッピングエクスペリエンスが実現します。

このトピックでは、AEM CIF コンポーネントを使用して[!DNL Live Search]製品リストページ（PLP）ウィジェットを AEM サイトに実装する方法について説明します。

## 前提条件 {#prerequisites}

このトピックでは、ローカル [AEM 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=ja)が設定されていることを前提としています。

PLP コンポーネントには、[[!DNL Live Search]  ポップオーバー CIF コンポーネント](live-search-popover.md)をインストールする必要があります。PLP ウィジェットには、ポップオーバーによって生成されるブラウザーセッション変数が必要です。

## コンポーザーを更新 {#update-composer}

イベントモジュールを `ui.frontend/package.json` に追加します。

27 行目で、次の内容を変更します。

```json
...
  },

  "devDependencies": {

    "@babel/core": "^7.3.4",
...
```

変更後は次のとおりです。

```json
...
  },
  "type": "module",
  "devDependencies": {
    "@adobe/magento-storefront-event-collector": "^1.5.4",
    "@adobe/magento-storefront-events-sdk": "^1.5.4",
    "@babel/core": "^7.3.4",
...
```

## ファイルの変更 {#files-changes}

[!DNL Live Search] 機能を有効にするには、複数のファイルを更新する必要があります。次のファイルを編集します。行番号は、次に示されているものと少し異なる場合があります。

* ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-cif/.content.xml

  `core.cif.productlist.v1` を `embed` 行に追加します。

  ```
  embed="[core.cif.components.common,core.cif.components.product.v3,core.cif.components.productcarousel.v1,core.cif.components.productcollection.v2,core.cif.components.productteaser.v1,core.cif.components.searchbar.v2,core.cif.components.header.v1,core.cif.components.carousel.v1,core.cif.components.categorycarousel.v1,core.cif.components.featuredcategorylist.v1,core.cif.components.storefront-events.v1,core.cif.components.extensions.product-recs.storefront-events-collector.v1,core.wcm.components.commons.site.link,core.cif.productlist.v1]"
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/.content.xml

  `.content.xml` ファイルを作成します。

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:ClientLibraryFolder"
    allowProxy="{Boolean}true"
    categories="[core.cif.productlist.v1]"
    jsProcessor="[default:none,min:none]"/>
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/css.txt

  `css.txt` ファイルを作成します。

  ```text
  #base=css
  
  productlist.css
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/css/productlist.css

  `productlist.css` ファイルを作成します。

  ```css
    /* #search-plp-root */
  
  html {
    font-size: 62.5% !important;
  }
  
  body {
    font-size: 1.6rem;
  }
  
  .root.container {
    max-width: inherit;
  }
  
  .container {
    margin-left: auto;
    margin-right: auto;
  }
  
  div.ds-sdk-sort-dropdown {
    z-index: 9;
  }
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/js.txt

  `js.txt` ファイルを作成します。

  ```text
  js/productlist.js
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/js/productlist.js

  `productlist.js` ファイルを作成します。

  ```javascript
  /*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  ~ Copyright 2023 Adobe
  ~
  ~ Licensed under the Apache License, Version 2.0 (the "License");
  ~ you may not use this file except in compliance with the License.
  ~ You may obtain a copy of the License at
  ~
  ~     http://www.apache.org/licenses/LICENSE-2.0
  ~
  ~ Unless required by applicable law or agreed to in writing, software
  ~ distributed under the License is distributed on an "AS IS" BASIS,
  ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  ~ See the License for the specific language governing permissions and
  ~ limitations under the License.
  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
  "use strict";
  
  class ProductList {
    constructor() {
      const stateObject = {
        categoryName: null,
        currentCategoryUrlPath: null,
      };
      this._state = stateObject;
      this._init();
    }
  
    _init() {
      this._initWidgetPLP();
    }
  
    _injectStoreScript(src) {
      const script = document.createElement("script");
      script.type = "text/javascript";
      script.src = src;
  
      document.head.appendChild(script);
    }
  
    async _getStoreData() {
      // get from session storage
      const sessionData = sessionStorage.getItem(
        "WIDGET_STOREFRONT_INSTANCE_CONTEXT"
      );
      // WIDGET_STOREFRONT_INSTANCE_CONTEXT is set from searchbar/clientlibs/js/searchbar.js
      // if not, we will need to retrieve from graphql separately here.
  
      if (sessionData) {
        this._state.dataServicesSessionContext = JSON.parse(sessionData);
        return;
      }
    }
  
    getStoreConfigMetadata() {
      const storeConfig = JSON.parse(
        document
          .querySelector("meta[name='store-config']")
          .getAttribute("content")
      );
  
      const { storeRootUrl } = storeConfig;
      const redirectUrl = storeRootUrl.split(".html")[0];
      return { storeConfig, redirectUrl };
    }
  
    async _initWidgetPLP() {
      if (!window.LiveSearchPLP) {
        const liveSearchPlpSrc =
          "https://plp-widgets-ui.magento-ds.com/v1/search.js";
        this._injectStoreScript(liveSearchPlpSrc);
        // wait until script is loaded
        await new Promise((resolve) => {
          const interval = setInterval(() => {
            if (window.LiveSearchPLP && window.LiveSearchAutocomplete) {
              // Widget expects LiveSearchAutocomplete already loaded to rely on data-service-graphql
              clearInterval(interval);
              resolve();
            }
          }, 200);
        });
      }
      await this._getStoreData();
      const { dataServicesSessionContext } = this._state;
      if (!dataServicesSessionContext) {
        console.log("no dataServicesSessionContext");
        return;
      }
  
      const root = document.getElementById("search-plp-root");
      if (!root) {
        console.log("plp root not found.");
        return;
      }
      // get dataset from root
      const categoryUrlPath = root.getAttribute("data-plp-urlPath") || "";
      const categoryName = root.getAttribute("data-plp-title") || "";
      const storeDetails = {
        environmentId: dataServicesSessionContext.environment_id,
        environmentType: dataServicesSessionContext.environment,
        apiKey: dataServicesSessionContext.api_key,
        websiteCode: dataServicesSessionContext.website_code,
        storeCode: dataServicesSessionContext.store_code,
        storeViewCode: dataServicesSessionContext.store_view_code,
        config: {
          pageSize: dataServicesSessionContext.page_size,
          perPageConfig: {
            pageSizeOptions: dataServicesSessionContext.page_size_options,
            defaultPageSizeOption:
              dataServicesSessionContext.default_page_size_option,
          },
          minQueryLength: dataServicesSessionContext.min_query_length,
          currencySymbol: dataServicesSessionContext.currency_symbol,
          currencyRate: dataServicesSessionContext.currency_rate,
          displayOutOfStock: dataServicesSessionContext.display_out_of_stock,
          allowAllProducts: dataServicesSessionContext.allow_all_products,
          locale: dataServicesSessionContext.locale,
          currentCategoryUrlPath: categoryUrlPath,
          categoryName,
          displayMode: "", // "" for plp || "PAGE" for category/catalog
        },
        context: {
          customerGroup: dataServicesSessionContext.customer_group,
        },
        route: ({ sku }) => {
          return `${
            this.getStoreConfigMetadata().redirectUrl
          }.cifproductredirect.html/${sku}`;
        },
        searchQuery: "search_query",
      };
      setTimeout(() => {
        console.log("init PLP");
        window.LiveSearchPLP({ storeDetails, root });
      }, 0);
    }
  }
  
  (function () {
    function onDocumentReady() {
      new ProductList({});
    }
  
    if (document.readyState !== "loading") {
      onDocumentReady();
    } else {
      document.addEventListener("DOMContentLoaded", onDocumentReady);
    }
  })();
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/productlist.html

  `productlist.html` ファイルを作成します。

  ```html
  <div
  data-sly-use.productList="com.adobe.cq.commerce.core.components.models.productlist.ProductList"
  id="search-plp-root"
  class="productlist__root"
  data-plp-urlPath="${productList.storefrontContext.urlPath}"
  data-plp-title="${productList.title}">
  </div>
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/searchresults/.content.xml

  `.content.xml` の 6 行目を編集します。

  ```xml
  sling:resourceSuperType="venia/components/commerce/productlist"
  ```

* ui.content/src/main/content/jcr_root/content/venia/language-masters/en/search/.content.xml

  `.content.xml` の 21～22 行目を編集します。

  ```xml
  sling:resourceType="venia/components/commerce/productlist"
  ```

* ui.content/src/main/content/jcr_root/content/venia/us/en/search/.content.xml

  `.content.xml` の 26 行目を編集します。

  ```xml
  sling:resourceType="venia/components/commerce/productlist"
  ```

* ui.frontend/src/main/components/App/App.js

  `../../site/main.scss` のすぐ上にある、`App.js` の 47 行目を編集します。

  ```javascript
  import '@adobe/magento-storefront-event-collector';
  ```

* ui.tests/test-module/specs/venia/productlist-dialog.js

  `productlist-dialog.js` の 20 行目を編集し、`describe` を `describe.skip` に変更します。

  ```javascript
  describe.skip('Product List Component Dialog', function () {
  ```

## 非 PLP ページ {#non-plp-pages}

カテゴリによっては、PLP ウィジェットを使用するのではなく、デフォルトのカテゴリまたはカタログページが必要な場合があります。AEM では、これらのカテゴリページを手動で設定する必要があります。

1. 作成者ページから、カテゴリページテンプレートを選択します。_Venia ストア - ホーム_／_カタログページ_／_Venia ストア - カテゴリページ_&#x200B;に移動し、「商品の陳列」を選択するか、新しいページテンプレートを作成します。

![テンプレートの選択](../assets/cif-widget-1.jpg)

1. 「_プロパティ_」セクションをクリックし、「_コマース_」タブを選択します。

![プロパティの選択](../assets/cif-widget-2.jpg)

1. 選択したカテゴリページテンプレートで表示するカテゴリを選択します。

![カテゴリの選択](../assets/cif-widget-3.jpg)
