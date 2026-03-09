---
title: コンテンツフラグメントセレクターとAdobe アプリケーションの統合
description: コンテンツフラグメントセレクターを様々なAdobe アプリケーションと統合します。
role: Admin, User, Developer
source-git-commit: a16d9e9fa6483a89283c595372abcc437d1d962e
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 20%

---

# コンテンツフラグメントセレクターとAdobe アプリケーションの統合 {#integrate-content-fragment-selector-with-adobe-application}

コンテンツフラグメントセレクターを使用すると、様々なAdobe アプリケーションと統合し、シームレスに連携できるようになります。

## 前提条件 {#prerequisites}

コンテンツフラグメントセレクターをAdobe アプリケーションと統合する場合は、次の前提条件を使用してください。

* [前提条件](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsOrg
* imsToken
* apikey

## コンテンツフラグメントセレクターとAdobe アプリケーションの統合 {#integrate-content-fragment-selector-with-an-adobe-application}

次の例は、統合シェルの下でAdobe アプリケーションを実行している場合、または認証用に生成された `imsToken` が既にある場合に、コンテンツフラグメントセレクターの使用を示しています。

以下の例に示すように、`script` タグを使用して、コンテンツフラグメントセレクターパッケージをコードに含めます。

* スクリプトが読み込まれると、`PureJSContentFragmentSelectors` グローバル変数を使用できるようになります。
* コンテンツフラグメントセレクターを定義します [ プロパティ ](/help/headless/content-fragment-selector/properties.md)。

   * `imsOrg` プロパティと `imsToken` プロパティは、どちらもAdobe アプリケーションでの認証に必要です
   * `handleSelection` プロパティは、選択したフラグメントを処理するために使用されます。

* コンテンツフラグメントセレクターをレンダリングするには、`renderFragmentSelector` 関数を呼び出します。
* コンテンツフラグメントセレクターが `<div>` コンテナ要素に表示されます。

このような手順に従うと、コンテンツフラグメントセレクターをAdobe アプリケーションと連携して使用できます。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Fragment Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-fragmentss-selectors/static-fragments/resources/fragments-selectors.js"></script>
    <script>
        // get the container element in which we want to render the FragmentSelector component
        const container = document.getElementById('fragment-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const fragmentSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (fragmentss: SelectedFragmentType[]) => {},
        };
        // Call the `renderFragmentSelector` available in PureJSContentFragmentSelectors globals to render FragmenttSelector
        PureJSContentFragmentSelectors.renderFragmentSelector(container, fragmentSelectorProps);
    </script>
</head>

<body>
    <div id="fragment-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

### ImsAuthProps {#imsauthprops}

`ImsAuthProps` プロパティは、コンテンツフラグメントセレクターが `imsToken` を取得するのに使用する認証情報とフローを定義します。これらのプロパティを設定すると、認証フローの動作を制御し、様々な認証イベントのリスナーを登録できます。

プロパティの詳細については、「[ImsAuthProps プロパティ ](/help/headless/content-fragment-selector/properties.md#imsauthprops-properties)」を参照してください。

### ImsAuthService {#imsauthservice}

クラス `ImsAuthService`、フラグメントセレクターの認証フローを処理します。 これは、Adobe IMS 認証サービスから `imsToken` を取得する役割を果たします。`imsToken` を使用して、ユーザーを認証し、AEM as a Cloud Service リポジトリへのアクセスを認証します。 `ImsAuthService` は `ImsAuthProps` のプロパティを使用して認証フローを制御し、様々な認証イベントのリスナーを登録します。 `registerFragmentsSelectorsAuthService` 関数を使用してフラグメントセレクターで `ImsAuthService` インスタンスを登録できます。 `ImsAuthService` クラスでは、次の関数を使用できます。ただし、`registerFragmentsSelectorsAuthService` 関数を使用している場合は、これらの関数を直接呼び出す必要はありません。

プロパティの詳細については、「[ImsAuthService プロパティ ](/help/headless/content-fragment-selector/properties.md#imsauthservice-properties)」を参照してください。

### 提供された IMS トークンによる検証 {#validation-with-provided-ims-token}

```javascript
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected fragment: ", selection);
    };
    function renderFragmentSelectorInline() {
    console.log("initializing Fragment Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('fragment-selector-container');
    PureJSContentFragmentSelectors.renderFragmentSelector(container, props);
    }
    $(document).ready(function() {
    renderFragmentSelectorInline();
    });
</script>
```

### IMS サービスへのコールバックの登録 {#register-callbacks-to-ims-service}

```java
// object `imsProps` to be defined as below 
let imsProps = {
    imsClientId: <IMS Client Id>,
        imsScope: "openid",
        redirectUrl: window.location.href,
        modalMode: true,
        adobeImsOptions: {
            modalSettings: {
            allowOrigin: window.location.origin,
},
        useLocalStorage: true,
},
onImsServiceInitialized: (service) => {
            console.log("onImsServiceInitialized", service);
},
onAccessTokenReceived: (token) => {
            console.log("onAccessTokenReceived", token);
},
onAccessTokenExpired: () => {
            console.log("onAccessTokenError");
// re-trigger sign-in flow
},
onErrorReceived: (type, msg) => {
            console.log("onErrorReceived", type, msg);
},
}
```
