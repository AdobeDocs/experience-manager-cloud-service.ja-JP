---
title: '[!DNL Live Search] ポップオーバーCIFコンポーネント'
description: CIFコンポーネントを使用した有効化 [!DNL Live Search] AEMサイトのポップオーバーコンポーネント
exl-id: 9dac6693-fe87-4a47-a920-2cf788933499
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# [!DNL Live Search] ポップオーバーCIFコンポーネント {#live-search-popover}

The [!DNL Live Search] ポップオーバーは、 [!DNL Live Search] 検索フィールドに入力した結果。
ここでは、このコンポーネントをAEMサイトに統合する方法について説明します。

## ファイル構造 {#file-strucure}

CIFコンポーネントを有効にするには、ファイルを編集して作成する必要があります。

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/searchbar/clientlibs/.content.xml

  を作成します。 `.content.xml` ファイル：

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:ClientLibraryFolder"
    allowProxy="{Boolean}true"
    categories="[venia.cif]"
    jsProcessor="[default:none,min:none]"/>
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/searchbar/clientlibs/css.txt

  を作成します。 `css.txt` ファイル：

  ```text
  #base=css
  
  searchbar.css
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/searchbar/clientlibs/css/searchbar.css

  を作成します。 `searchbar.css` ファイル：


  ```css
  .searchbar__root .action.search:before {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-size: 16px;
    line-height: 32px;
    color: #757575;
    /* content: "\e615"; */
    font-family: "luma-icons";
    margin: 0;
    vertical-align: top;
    display: inline-block;
    font-weight: normal;
    overflow: hidden;
    speak: none;
    text-align: center;
  }
  .searchbar__label {
    display: none;
  }
  
  .searchbar__root .action.search > span {
    border: 0;
    clip: rect(0, 0, 0, 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
  }
  input.searchbar__input::placeholder {
    font-size: 14px;
  }
  input.searchbar__input {
    background: #fff;
    background-clip: padding-box;
    border: 1px solid #c2c2c2;
    border-radius: 1px;
    font-family: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 16px;
    height: 32px;
    line-height: 1.42857143;
    padding: 0 9px;
    vertical-align: baseline;
    width: 100%;
    max-width: 200px;
    box-sizing: border-box;
    cursor: text;
  }
  .search-autocomplete {
    position: absolute;
  }
  div.searchbar {
    width: 100% !important;
  }
  div.searchbar__fields.search {
    display: flex;
    justify-content: center;
  }
  .searchbar__form {
    justify-items: center !important;
  }
  @media all and (min-width: 769px) {
    .searchbar__form {
      justify-items: stretch !important;
    }
    div.searchbar {
      width: 8.333333% !important;
      margin: 0;
    }
    .searchbar__root {
      position: relative;
      z-index: 4;
    }
    .searchbar__root .searchbar__control {
      border-top: 0;
      margin: 0;
      padding: 0.75em 0;
    }
    .searchbar__root .searchbar__input {
      margin: 0;
      padding-right: 12px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
  }
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/searchbar/clientlibs/js.txt

  を作成します。 `js.txt` ファイル：

  ```text
  js/searchbar.js
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/searchbar/clientlibs/js/searchbar.js

  を作成します。 `searchbar.js` ファイル：

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
  
  const dataServicesStorefrontInstanceContextQuery = `
      query DataServicesStorefrontInstanceContext {
        dataServicesStorefrontInstanceContext {
          customer_group
          environment_id
          environment
          store_id
          store_view_id
          store_code
          store_view_code
          website_id
          website_name
          website_code
          store_url
          api_key
          store_name
          store_view_name
          base_currency_code
          store_view_currency_code
          catalog_extension_version
        }
        storeConfig {
          base_currency_code
          store_code
        }
      }
    `;
  
  const dataServicesMagentoExtensionContextQuery = `
      query DataServicesStorefrontInstanceContext {
        dataServicesMagentoExtensionContext {
          magento_extension_version
        }
      }
    `;
  
  const dataServicesStoreConfigurationContextQuery = `
      query DataServicesStoreConfigurationContext {
        dataServicesStoreConfigurationContext {
          currency_symbol
          currency_rate
          page_size
          page_size_options
          default_page_size_option
          display_out_of_stock
          allow_all_products
          locale
          min_query_length
        }
      }
    `;
  
  const getCookie = (cookieName) => {
    const cookie = document.cookie.match(
      `(^|[^;]+)\\s*${cookieName}\\s*=\\s*([^;]+)`
    );
    return cookie ? cookie.pop() : "";
  };
  
  const getLoginToken = () => {
    const key = "M2_VENIA_BROWSER_PERSISTENCE__signin_token";
    let token = getCookie("cif.userToken") || "";
  
    try {
      const lsToken = JSON.parse(localStorage.getItem(key));
      if (lsToken && lsToken.value) {
        const timestamp = new Date().getTime();
        if (timestamp - lsToken.timeStored < lsToken.ttl * 1000) {
          token = lsToken.value.replace(/"/g, "");
        }
      }
    } catch (e) {
      console.error(`Login token at ${key} is not valid JSON.`);
    }
    return token;
  };
  
  async function getGraphQLQuery(query, variables = {}) {
    const graphqlEndpoint = `/api/graphql`;
    const headers = {
      "Content-Type": "application/json",
    };
  
    const loginToken = getLoginToken();
    if (loginToken) {
      headers["Authorization"] = `Bearer ${loginToken}`;
    }
  
    const response = await fetch(graphqlEndpoint, {
      method: "POST",
      headers,
      body: JSON.stringify({
        query,
        variables,
      }),
    }).then((res) => res.json());
  
    return response.data;
  }
  
  class SearchBar {
    constructor() {
      const stateObject = {
        dataServicesStorefrontInstanceContext: null,
        dataServicesStoreConfigurationContext: null,
        magentoExtensionVersion: null,
        storeConfig: null,
      };
      this._state = stateObject;
      this._init();
    }
    _init() {
      this._initLiveSearch();
    }
  
    _injectStoreScript(src) {
      const script = document.createElement("script");
      script.type = "text/javascript";
      script.src = src;
  
      document.head.appendChild(script);
    }
  
    async _getStoreData() {
      const { dataServicesStorefrontInstanceContext, storeConfig } =
        (await getGraphQLQuery(dataServicesStorefrontInstanceContextQuery)) || {};
      const { dataServicesStoreConfigurationContext } =
        (await getGraphQLQuery(dataServicesStoreConfigurationContextQuery)) || {};
      this._state.dataServicesStorefrontInstanceContext =
        dataServicesStorefrontInstanceContext;
      this._state.dataServicesStoreConfigurationContext =
        dataServicesStoreConfigurationContext;
      this._state.storeConfig = storeConfig;
  
      if (!dataServicesStorefrontInstanceContext) {
        console.log("no dataServicesStorefrontInstanceContext");
        return;
      }
      // set session storage to expose for widget
      sessionStorage.setItem(
        "WIDGET_STOREFRONT_INSTANCE_CONTEXT",
        JSON.stringify({
          ...dataServicesStorefrontInstanceContext,
          ...dataServicesStoreConfigurationContext,
        })
      );
    }
  
    async _getMagentoExtensionVersion() {
      const { dataServicesMagentoExtensionContext } =
        (await getGraphQLQuery(dataServicesMagentoExtensionContextQuery)) || {};
      this._state.magentoExtensionVersion =
        dataServicesMagentoExtensionContext?.magento_extension_version;
      if (!dataServicesMagentoExtensionContext) {
        console.log("no magentoExtensionVersion");
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
  
    async _initLiveSearch() {
      await Promise.all([
        this._getStoreData(),
        this._getMagentoExtensionVersion(),
      ]);
      if (!window.LiveSearchAutocomplete) {
        const liveSearchSrc =
          "https://livesearch-autocomplete.magento-ds.com/v0/LiveSearchAutocomplete.js";
  
        this._injectStoreScript(liveSearchSrc);
        // wait until script is loaded
        await new Promise((resolve) => {
          const interval = setInterval(() => {
            if (window.LiveSearchAutocomplete) {
              clearInterval(interval);
              resolve();
            }
          }, 200);
        });
      }
  
      const {
        dataServicesStorefrontInstanceContext,
        dataServicesStoreConfigurationContext,
      } = this._state;
      if (!dataServicesStorefrontInstanceContext) {
        console.log("no dataServicesStorefrontInstanceContext");
        return;
      }
  
      // initialize live-search
      new window.LiveSearchAutocomplete({
        environmentId: dataServicesStorefrontInstanceContext.environment_id,
        websiteCode: dataServicesStorefrontInstanceContext.website_code,
        storeCode: dataServicesStorefrontInstanceContext.store_code,
        storeViewCode: dataServicesStorefrontInstanceContext.store_view_code,
        config: {
          pageSize: dataServicesStoreConfigurationContext.page_size,
          minQueryLength: dataServicesStoreConfigurationContext.min_query_length,
          currencySymbol: dataServicesStoreConfigurationContext.currency_symbol,
          currencyRate: dataServicesStoreConfigurationContext.currency_rate,
          displayOutOfStock:
            dataServicesStoreConfigurationContext.display_out_of_stock,
          allowAllProducts:
            dataServicesStoreConfigurationContext.allow_all_products,
        },
        context: {
          customerGroup: dataServicesStorefrontInstanceContext.customer_group,
        },
        route: ({ sku }) => {
          return `${
            this.getStoreConfigMetadata().redirectUrl
          }.cifproductredirect.html/${sku}`;
        },
        searchRoute: {
          route: `${this.getStoreConfigMetadata().redirectUrl}/search.html`,
          query: "search_query",
        },
      });
  
      const formEle = document.getElementById("search_mini_form");
  
      formEle.setAttribute(
        "action",
        `${dataServicesStorefrontInstanceContext.store_url}catalogsearch/result`
      );
      // initialize store event after live-search
      this._initMetrics();
    }
  
    async _initMetrics() {
      //  Magento Store event
  
      // wait until script is magentoStorefrontEvents is found
      await new Promise((resolve) => {
        const interval = setInterval(() => {
          if (window.magentoStorefrontEvents) {
            clearInterval(interval);
            resolve();
          }
        }, 200);
      });
  
      const mse = window.magentoStorefrontEvents;
  
      const { dataServicesStorefrontInstanceContext, storeConfig } = this._state;
  
      const {
        base_currency_code,
        catalog_extension_version,
        environment,
        environment_id,
        store_code,
        store_id,
        store_name,
        store_url,
        store_view_code,
        store_view_id,
        store_view_name,
        store_view_currency_code,
        website_code,
        website_id,
        website_name,
      } = dataServicesStorefrontInstanceContext;
  
      console.log("initializing magento extension");
      mse.context.setMagentoExtension({
        magentoExtensionVersion: this._state.magentoExtensionVersion,
      });
  
      mse.context.setPage({
        pageType: "pdp",
        maxXOffset: 0,
        maxYOffset: 0,
        minXOffset: 0,
        minYOffset: 0,
        ping_interval: 5,
        pings: 1,
      });
  
      mse.context.setStorefrontInstance({
        environmentId: environment_id,
        environment: environment,
        storeUrl: store_url,
        websiteId: website_id,
        websiteCode: website_code,
        storeId: store_id,
        storeCode: store_code,
        storeViewId: store_view_id,
        storeViewCode: store_view_code,
        websiteName: website_name,
        storeName: store_name,
        storeViewName: store_view_name,
        baseCurrencyCode: base_currency_code,
        storeViewCurrencyCode: store_view_currency_code,
        catalogExtensionVersion: catalog_extension_version,
      });
    }
  }
  
  (function () {
    function onDocumentReady() {
      new SearchBar({});
    }
  
    if (document.readyState !== "loading") {
      onDocumentReady();
    } else {
      document.addEventListener("DOMContentLoaded", onDocumentReady);
    }
  })();
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/searchbar/searchbar.html

  を作成します。 `searchbar.html` ファイル：

  ```html
  <!-- Livesearch popover -->
  <div
    data-sly-use.storeconfig="com.adobe.cq.commerce.core.components.models.storeconfigexporter.StoreConfigExporter"
    class="searchbar__root widget-search"
  >
    <div class="block-title" style="display: none">
      <strong>Search</strong>
    </div>
    <div class="live-search-popover block-content">
      <form
        class="searchbar__form"
        id="search_mini_form"
        method="get"
        style="width: auto"
      >
        <div class="searchbar__fields">
          <label
            class="searchbar__label"
            for="search"
            data-role="minisearch-label"
          >
            <span>Search</span>
          </label>
          <div class="searchbar__control">
            <input
              id="search"
              type="text"
              name="q"
              value=""
              placeholder="Search entire store here..."
              class="searchbar__input"
              maxlength="128"
              role="combobox"
              aria-haspopup="false"
              aria-autocomplete="both"
              autocomplete="off"
              aria-expanded="false"
              onchange=""
            />
            <div id="search_autocomplete" class="search-autocomplete"></div>
          </div>
        </div>
        <div class="actions" style="display: none">
          <button
            type="submit"
            title="Search"
            class="action search"
            aria-label="Search"
          >
            <span>Search</span>
          </button>
        </div>
      </form>
    </div>
  </div>
  ```

* ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.core.components.internal.servlets.ProductPageRedirectServlet.cfg.json

  を作成します。 `com.adobe.cq.commerce.core.components.internal.servlets.ProductPageRedirectServlet.cfg.json` ファイル：

  ```json
  {
    "sling.servlet.resourceTypes": [
        "core/cif/components/structure/page/v1/page",
        "core/cif/components/structure/page/v2/page",
        "core/cif/components/structure/page/v3/page"
    ]
  }
  ```

   * ui.tests/test-module/specs/venia/searchbar.js

     を編集します。 `searchbar.js` ファイル、19～20 行目、変更 `describe` から `describe.skip`:

     ```javascript
     describe.skip('Venia Searchbar Component', () => {
     ```
