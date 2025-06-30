---
title: アセットセレクターと  [!DNL Adobe]  アプリケーションの統合
description: アセットセレクターを様々なアドビ、アドビ以外、サードパーティのアプリケーションと統合します。
role: Admin, User
exl-id: a0c030e2-2213-406b-ad92-4761f1e2ee9f
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 100%

---

# アセットセレクターとアドビアプリケーションの統合 {#integrate-asset-selector-with-adobe-app}

アセットセレクターを使用すると、様々なアドビアプリケーションを統合して、シームレスに連携できます。

## 前提条件{#prereqs-adobe-app}

アセットセレクターを [!DNL Adobe] アプリケーションと統合する場合は、次の前提条件を使用しまず。

* [通信方法](/help/assets/overview-asset-selector.md#prereqs)
* imsOrg
* imsToken
* apikey

## アセットセレクターと [!DNL Adobe] アプリケーションの統合 {#adobe-app-integration-vanilla}

次の例では、統合シェルの下で [!DNL Adobe] アプリケーションを実行している場合、または認証用に生成された `imsToken` が既にある場合に、アセットセレクターの使用方法を示します。

以下の例の _6～15 行目_&#x200B;に示されているように、`script` タグを使用してアセットセレクターパッケージをコードに含めます。スクリプトが読み込まれると、`PureJSSelectors` グローバル変数を使用できるようになります。_16～23 行目_&#x200B;に示されているように、アセットセレクターの[プロパティ](/help/assets/asset-selector-properties.md)を定義します。`imsOrg` プロパティと `imsToken` プロパティは、いずれもアドビアプリケーションでの認証に必要です。`handleSelection` プロパティは、選択したアセットを処理するために使用されます。_17 行目_&#x200B;で示されているように、アセットセレクターをレンダリングするには `renderAssetSelector` 関数を呼び出します。_21～22 行目_&#x200B;に示されているように、アセットセレクターが `<div>` コンテナ要素に表示されます。

これらの手順に従うことで、[!DNL Adobe] アプリケーションでアセットセレクターを使用できます。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const assetSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderAssetSelector` available in PureJSSelectors globals to render AssetSelector
        PureJSSelectors.renderAssetSelector(container, assetSelectorProps);
    </script>
</head>

<body>
    <div id="asset-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

<!--For detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

### ImsAuthProps {#ims-auth-props}

`ImsAuthProps` プロパティは、アセットセレクターが `imsToken` を取得するのに使用する認証情報とフローを定義します。これらのプロパティを設定すると、認証フローの動作を制御し、様々な認証イベントのリスナーを登録できます。

| プロパティ名 | 説明 |
|---|---|
| `imsClientId` | 認証目的で使用される IMS クライアント ID を表す文字列値。この値はアドビが指定し、アドビの AEM CS 組織に固有です。 |
| `imsScope` | 認証で使用されるスコープについて説明します。スコープは、組織のリソースに対するアプリケーションのアクセスレベルを決定します。複数のスコープは、コンマで区切ることができます。 |
| `redirectUrl` | 認証後にユーザーがリダイレクトされる URL を表します。この値は通常、アプリケーションの現在の URL に設定されます。`redirectUrl` を指定していない場合、`ImsAuthService` は `imsClientId` の登録に使用した redirectUrl を使用します。 |
| `modalMode` | 認証フローをモーダル（ポップアップ）に表示するかどうかを示すブール値。`true` に設定すると、認証フローがポップアップで表示されます。`false` に設定すると、認証フローはページ全体をリロードして表示されます。_メモ：_ UX を向上させるために、ユーザーがブラウザーのポップアップを無効にしている場合は、この値を動的に制御できます。 |
| `onImsServiceInitialized` | Adobe IMS 認証サービスを初期化する際に呼び出されるコールバック関数。この関数は、Adobe IMS サービスを表すオブジェクトである `service` という 1 つのパラメーターを受け取ります。詳しくは、[`ImsAuthService`](#imsauthservice-ims-auth-service) を参照してください。 |
| `onAccessTokenReceived` | Adobe IMS 認証サービスから `imsToken` を受信する際に呼び出されるコールバック関数。この関数は、アクセストークンを表す文字列である `imsToken` という 1 つのパラメーターを受け取ります。 |
| `onAccessTokenExpired` | アクセストークンの有効期限が切れる際に呼び出されるコールバック関数。この関数は通常、新しい認証フローをトリガーして新しいアクセストークンを取得するために使用されます。 |
| `onErrorReceived` | 認証中にエラーが発生する際に呼び出されるコールバック関数。この関数は、エラータイプとエラーメッセージという 2 つのパラメーターを受け取ります。エラータイプはエラータイプを表す文字列で、エラーメッセージはエラーメッセージを表す文字列です。 |

### ImsAuthService {#ims-auth-service}

`ImsAuthService` クラスは、アセットセレクターの認証フローを処理します。これは、Adobe IMS 認証サービスから `imsToken` を取得する役割を果たします。`imsToken` は、ユーザーを認証し、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] アセットリポジトリへのアクセスを認証するために使用されます。ImsAuthService は、`ImsAuthProps` プロパティを使用して認証フローを制御し、様々な認証イベントのリスナーを登録します。便利な [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) 関数を使用して、_ImsAuthService_ インスタンスをアセットセレクターに登録できます。`ImsAuthService` クラスでは、次の関数を使用できます。ただし、_registerAssetsSelectorsAuthService_ 関数を使用している場合は、これらの関数を直接呼び出す必要はありません。

| 関数名 | 説明 |
|---|---|
| `isSignedInUser` | ユーザーが現在サービスにログインしているかどうかを判断し、それに応じてブール値を返します。 |
| `getImsToken` | 現在ログインしているユーザーの認証 `imsToken` を取得します。これは、asset _rendition の生成など、他のサービスへのリクエストを認証するために使用できます。 |
| `signIn` | ユーザーのログインプロセスを開始します。この関数は、`ImsAuthProps` を使用して、ポップアップまたはページ全体のリロードで認証を表示します。 |
| `signOut` | ユーザーをサービスからログアウトし、認証トークンを無効にし、保護されたリソースにアクセスするには再度ログインするようにリクエストします。この関数を呼び出すと、現在のページがリロードされます。 |
| `refreshToken` | 現在ログインしているユーザーの認証トークンを更新して、トークンの有効期限切れを防ぎ、保護されたリソースに中断なくアクセスできるようになります。後続のリクエストに使用できる新しい認証トークンを返します。 |

### 提供された IMS トークンによる検証 {#validation-ims-token}

```
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected asset: ", selection);
    };
    function renderAssetSelectorInline() {
    console.log("initializing Asset Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('asset-selector-container');
    PureJSSelectors.renderAssetSelector(container, props);
    }
    $(document).ready(function() {
    renderAssetSelectorInline();
    });
</script>
```

### IMS サービスへのコールバックの登録 {#register-callback-ims-service}

```
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

>[!MORELIKETHIS]
>
>* [アセットセレクターと様々なアプリケーションの統合](/help/assets/integrate-asset-selector.md)
>* [アセットセレクターのプロパティ](/help/assets/asset-selector-properties.md)
>* [OpenAPI 機能を備えた Dynamic Media とのアセットセレクターの統合](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [アセットセレクターのカスタマイズ](/help/assets/asset-selector-customization.md)
