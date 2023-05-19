---
title: のアセットセレクター [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: アセットセレクターを使用して、アプリケーション内のアセットのメタデータとレンディションを検索、検索、取得します。
contentOwner: Adobe
role: Admin,User
source-git-commit: af36101d8fecd7fab2300f93d40bba4c92f8eafe
workflow-type: tm+mt
source-wordcount: '2378'
ht-degree: 4%

---


# マイクロフロントエンドアセットセレクター {#Overview}

マイクロフロントエンドアセットセレクターは、 [!DNL Experience Manager Assets as a Cloud Service] リポジトリーを使用して、リポジトリーで使用可能なデジタルアセットを参照または検索し、アプリケーションオーサリングエクスペリエンスで使用できるようにします。

Micro-Frontend ユーザーインターフェイスは、アセットセレクターパッケージを使用して、アプリケーションエクスペリエンスで使用できるようになります。 パッケージの更新は自動的に読み込まれ、最新でデプロイされたアセットセレクターがアプリケーション内に自動的に読み込まれます。

![概要](assets/overview.png)

アセットセレクターには、次のような多くの利点があります。

* Vanilla JavaScript ライブラリを使用した、任意のAdobeまたは非Adobeアプリケーションとの簡単な統合。
* アセットセレクターパッケージの更新が、アプリケーションで使用可能なアセットセレクターに自動的にデプロイされるので、管理が容易です。 最新の変更を読み込むためにアプリケーション内で必要な更新はありません。
* アプリケーション内のアセットセレクター表示を制御するプロパティを利用できるので、カスタマイズが容易です。

* フルテキスト検索、標準でカスタマイズされたフィルターを使用して、オーサリングエクスペリエンス内で使用するアセットにすばやく移動できます。

* IMS 組織内のリポジトリを切り替えて、アセットを選択できるようになりました。

* 名前、サイズ、サイズでアセットを並べ替え、リスト、グリッド、ギャラリー、ウォーターフォールの各表示でアセットを表示できます。

この記事の範囲は、アセットセレクターを [!DNL Adobe] 統合シェルの下のアプリケーション、または認証用に生成された imsToken が既にある場合。 この記事では、これらのワークフローを非 SUSI フローと呼びます。

アセットセレクターを [!DNL Experience Manager Assets as a Cloud Service] リポジトリ：

* [Vanilla JS を使用したアセットセレクターの統合](#integration-with-vanilla-js)
* [アセットセレクター表示プロパティの定義](#asset-selector-properties)
* [アセットセレクターを使用する](#using-asset-selector)

## Vanilla JS を使用したアセットセレクターの統合 {#integration-with-vanilla-js}

任意の [!DNL Adobe] または、 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] リポジトリーを作成し、アプリケーション内からアセットを選択します。

統合は、アセットセレクターパッケージを読み込み、Vanilla JavaScript ライブラリを使用してas a Cloud Serviceに接続することでおこなわれます。 次を編集する必要があります： `index.html` またはアプリケーション内の適切なファイルを次の場所に置き換えます。
* 認証の詳細を定義
* Assets as a Cloud Serviceリポジトリへのアクセス
* アセットセレクターの表示プロパティの設定

<!--
Asset Selector supports authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS) properties such as `imsScope` or `imsClientID`. Authentication using these IMS properties is referred to as SUSI (Sign Up Sign In) flow in this article.

You can perform authentication without defining some of the IMS properties, such as `imsScope` or `imsClientID`, if:

*   You are integrating an [!DNL Adobe] application on [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
*   You already have an IMS token generated for authentication.

Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining `imsScope` or `imsClientID` IMS properties is referred to as a non-SUSI flow in this article.
-->

次の場合、一部の IMS プロパティを定義せずに認証を実行できます。

* 統合中の [!DNL Adobe] 適用対象 [統合シェル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
* 認証用に既に IMS トークンが生成されています。

## 前提条件 {#prerequisites}

<!--
If your application requires user based authentication, out-of-the-box Asset Selector also supports a flow for authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS.)

You can use properties such as `imsScope` or `imsClientID` to retrieve `imsToken` automatically. You can use SUSI (Sign Up Sign In) flow and IMS properties. Also, you can obtain your own imsToken and pass it to Asset Selector by integrating within [!DNL Adobe] application on Unified Shell or if you already have an imsToken obtained via other methods (for example, using technical account). Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining IMS properties (For example, `imsScope` and `imsClientID`) is referred to as a non-SUSI flow.
-->

前提条件を `index.html` ファイル、またはアプリケーション実装内の類似のファイル。 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] リポジトリ。 前提条件は次のとおりです。
* imsOrg
* imsToken
* apikey

<!--
The prerequisites vary if you are authenticating using a SUSI flow or a non-SUSI flow.

**Non-SUSI flow**

*   imsOrg
*   imsToken
*   apikey

For more information on these properties, refer to [Asset Selector Properties](#asset-selector-properties).

**SUSI flow**

*   imsClientId
*   imsScope
*   redirectUrl
*   imsOrg
*   apikey

For more information on these properties, refer to [Example for the SUSI flow](#susi-vanilla) and [Asset Selector Properties](#asset-selector-properties).
-->

## インストール {#installation}

Assets セレクターは、両方の ESM CDN から使用できます ( 例： [esm.sh](https://esm.sh/)/[スキーパック](https://www.skypack.dev/)) および [UMD](https://github.com/umdjs/umd) バージョン。

を使用しているブラウザーでは、 **UMD バージョン** （推奨）:

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

ブラウザーで `import maps` を使用したサポート **ESM CDN バージョン**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

次を使用して Deno/Webpack Module Federation に **ESM CDN バージョン**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### 選択したアセットタイプ {#selected-asset-type}

選択されたアセットタイプは、 `handleSelection`, `handleAssetSelection`、および `onDrop` 関数

**スキーマ構文**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

次の表に、 Selected Asset オブジェクトの重要なプロパティの一部を示します。

| プロパティ | タイプ | 説明 |
|---|---|---|
| *repo:repositoryId* | 文字列 | アセットが保存されるリポジトリの一意の識別子。 |
| *repo:id* | 文字列 | アセットの一意の ID。 |
| *repo:assetClass* | 文字列 | アセットの分類（例：画像、ビデオ、ドキュメント）。 |
| *repo:name* | 文字列 | アセットの名前（ファイル拡張子を含む）。 |
| *repo:size* | 数値 | アセットのサイズ（バイト単位）。 |
| *repo:path* | 文字列 | リポジトリ内のアセットの場所。 |
| *repo:incestors* | `Array<string>` | リポジトリ内のアセットの上位項目の配列。 |
| *repo:state* | 文字列 | リポジトリ内のアセットの現在の状態（アクティブ、削除など）。 |
| *repo:createdBy* | 文字列 | アセットを作成したユーザーまたはシステム。 |
| *repo:createDate* | 文字列 | アセットが作成された日時。 |
| *repo:modifiedBy* | 文字列 | アセットを最後に変更したユーザーまたはシステム。 |
| *repo:modifyDate* | 文字列 | アセットが最後に変更された日時。 |
| *dc:format* | 文字列 | アセットの形式 ( ファイルタイプ (JPEG、PNG など )。 |
| *tiff:imageWidth* | 数値 | アセットの幅。 |
| *tiff:imageLength* | 数値 | アセットの高さ。 |
| *computedMetadata* | `Record<string, any>` | あらゆる種類（リポジトリー、アプリケーションまたは埋め込みメタデータ）のすべてのアセットのメタデータのバケットを表すオブジェクト。 |
| *_links* | `Record<string, any>` | 関連付けられたアセットのハイパーメディアリンク。 メタデータやレンディションなどのリソースへのリンクが含まれます。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition* | `Array<Object>` | アセットのレンディションに関する情報を含むオブジェクトの配列。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].href* | 文字列 | レンディションの URI。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].type* | 文字列 | レンディションの MIME タイプ。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].`repo:size&#39;* | 数値 | レンディションのサイズ（バイト単位）。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].width* | 数値 | レンディションの幅。 |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].height* | 数値 | レンディションの高さ。 |

プロパティの完全なリストと詳細な例については、 [アセットセレクターのコード例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

<!--
### ImsAuthProps {#ims-auth-props}

The `ImsAuthProps` properties define the authentication information and flow that the Asset Selector uses to obtain an `imsToken`. By setting these properties, you can control how the authentication flow should behave and register listeners for various authentication events.

| Property Name | Description|
|---|---|
| `imsClientId`| A string value representing the IMS client ID used for authentication purposes. This value is provided by Adobe and is specific to your Adobe AEM CS organization.|
| `imsScope`| Describes the scopes used in authentication. The scopes determine the level of access that the application has to your organization resources. Multiple scopes can be separated by commas.|
| `redirectUrl` | Represents the URL where the user is redirected after authentication. This value is typically set to the current URL of the application. If a `redirectUrl` is not supplied, `ImsAuthService` will use the redirectUrl used to register the `imsClientId`|
| `modalMode`| A boolean indicating whether the authentication flow should be displayed in a modal (pop-up) or not. If set to `true`, the authentication flow is displayed in a pop-up. If set to `false`, the authentication flow is displayed in a full page reload. _Note:_ for better UX, you can dynamically control this value if the user has browser pop-up disabled. |
| `onImsServiceInitialized`| A callback function that is called when the Adobe IMS authentication service is initialized. This function takes one parameter, `service`, which is an object representing the Adobe IMS service. See [`ImsAuthService`](#imsauthservice-ims-auth-service) for more details.|
| `onAccessTokenReceived`| A callback function that is called when an `imsToken` is received from the Adobe IMS authentication service. This function takes one parameter, `imsToken`, which is a string representing the access token. |
| `onAccessTokenExpired`| A callback function that is called when an access token has expired. This function is typically used to trigger a new authentication flow to obtain a new access token. |
| `onErrorReceived`| A callback function that is called when an error occurs during authentication. This function takes two parameters: the error type and error message. The error type is a string representing the type of error and the error message is a string representing the error message. |

### ImsAuthService {#ims-auth-service}

`ImsAuthService` class handles the authentication flow for the Asset Selector. It is responsible for obtaining an `imsToken` from the Adobe IMS authentication service. The `imsToken` is used to authenticate the user and authorize access to the Adobe Experience Manager (AEM) CS Assets repository. ImsAuthService uses the `ImsAuthProps` properties to control the authentication flow and register listeners for various authentication events. You can use the convenient [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) function to register the _ImsAuthService_ instance with the Asset Selector. The following functions are available on the `ImsAuthService` class. However, if you're using the _registerAssetsSelectorsAuthService_ function, you do not need to call these functions directly.

| Function Name | Description |
|---|---|
| `isSignedInUser` | Determines whether the user is currently signed in to the service and returns a boolean value accordingly.|
| `getImsToken`    | Retrieves the authentication `imsToken` for the currently signed-in user, which can be used to authenticate requests to other services such as generating asset _rendition.|
| `signIn`| Initiates the sign-in process for the user. This function uses the `ImsAuthProps` to show authentication in either a pop-up or a full page reload |
| `signOut`| Signs the user out of the service, invalidating their authentication token and requiring them to sign in again to access protected resources. Invoking this function will reload the current page.|
| `refreshToken`| Refreshes the authentication token for the currently signed-in user, preventing it from expiring and ensuring uninterrupted access to protected resources. Returns a new authentication token that can be used for subsequent requests. |
-->

### 非 SUSI フローの例 {#non-susi-vanilla}

この例では、 [!DNL Adobe] 統合シェルの下のアプリケーション、または既に `imsToken` 認証用に生成されました。

を使用して、コードにアセットセレクターパッケージを含めます。 `script` タグ、 _6～15 行目_ 以下の例の スクリプトが読み込まれると、 `PureJSSelectors` グローバル変数は使用できます。 アセットセレクターの定義 [プロパティ](#asset-selector-properties) に示すように _16～23 行_. この `imsOrg` および `imsToken` プロパティは、どちらも非 SUSI フローでの認証に必要です。 この `handleSelection` プロパティは、選択したアセットを処理するために使用されます。 アセットセレクターをレンダリングするには、 `renderAssetSelector` ～で述べられているように機能する _17 行目_. アセットセレクターが `<div>` コンテナ要素 ( _行 21 および 22_.

以下の手順に従うことで、非 SUSI フローでアセットセレクターを使用できます [!DNL Adobe] アプリケーション。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
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

詳細な例は、次を参照してください： [アセットセレクターのコード例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

<!--
### Example for the SUSI flow {#susi-vanilla}

Use this example `index.html` file for authentication if you are integrating your application using SUSI flow.

Access the Asset Selector package using the `Script` Tag, as shown in *line 9* to *line 11* of the example `index.html` file.

*Line 14* to *line 38* of the example describes the IMS flow properties, such as `imsClientId`, `imsScope`, and `redirectURL`. The function requires that you define at least one of the `imsClientId` and `imsScope` properties. If you do not define a value for `redirectURL`, the registered redirect URL for the client ID is used.

As you do not have an `imsToken` generated, use the `registerAssetsSelectorsAuthService` and `renderAssetSelectorWithAuthFlow` functions, as shown in line 40 to line 50 of the example `index.html` file. Use the `registerAssetsSelectorsAuthService` function before `renderAssetSelectorWithAuthFlow` to register the `imsToken` with the Asset Selector. [!DNL Adobe] recommends to call `registerAssetsSelectorsAuthService` when you instantiate the component.

Define the authentication and other Assets as a Cloud Service access-related properties in the `const props` section, as shown in *line 54* to *line 60* of the example `index.html` file.

The `PureJSSelectors` global variable, mentioned in *line 65*, is used to render the Asset Selector in the web browser.

Asset Selector is rendered on the `<div>` container element, as mentioned in *line 74* to *line 81*. The example uses a dialog to display the Asset Selector.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8">
    <title>Asset Selectors</title>
    <link rel="stylesheet" href="index.css">
    <script id="asset-selector"
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/asset-selectors.js"></script>
    <script>

        const imsProps = {
            imsClientId: "<obtained from IMS team>",
            imsScope: "openid, <other scopes>",
            redirectUrl: window.location.href,
            modalMode: true, // false to open in a full page reload flow
            onImsServiceInitialized: (service) => {
                // invoked when the ims service is initialized and is ready
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

        function load() {
            const registeredTokenService = PureJSSelectors.registerAssetsSelectorsAuthService(imsProps);
            imsInstance = registeredTokenService;
        };

        // initialize the IMS flow before attempting to render the asset selector
        load();
        

        //function that will render the asset selector
            const otherProps = {
            // any other props supported by asset selector
            }
            const assetSelectorProps = {
                "imsOrg": "imsorg",
                ...otherProps
            }
             // container element on which you want to render the AssetSelector/DestinationSelector component
            const container = document.getElementById('asset-selector');

            /// Use the PureJSSelectors in globals to render the AssetSelector/DestinationSelector component
            PureJSSelectors.renderAssetSelectorWithAuthFlow(container, assetSelectorProps, () => {
                const assetSelectorDialog = document.getElementById('asset-selector-dialog');
                assetSelectorDialog.showModal();
            });
        }
    </script>

</head>
<body class="asset-selectors">
    <div>
        <button onclick="renderAssetSelectorWithAuthFlowFlow()">Asset Selector - Select Assets with Ims Flow</button>
    </div>
        <dialog id="asset-selector-dialog">
            <div id="asset-selector" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
            </div>
        </dialog>
    </div>
</body>

</html>

```
-->

## Use Asset Selector プロパティ {#asset-selector-properties}

アセットセレクターのプロパティを使用して、アセットセレクターのレンダリング方法をカスタマイズできます。 次の表に、アセットセレクターをカスタマイズして使用できるプロパティを示します。

| プロパティ | タイプ | 必須 | デフォルト | 説明 |
|---|---|---|---|---|
| *パネル* | ブール値 | いいえ | false | マークされている場合 `true`の場合、アセットセレクターが左側のパネル表示でレンダリングされます。 マークが付いている場合 `false`を指定した場合、アセットセレクターがモーダルビューでレンダリングされます。 |
| *imsOrg* | 文字列 | はい |  | プロビジョニング中に割り当てられるAdobeIdentity Management System(IMS)ID [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 組織の この `imsOrg` キーは、アクセスしようとしている組織がAdobe IMS中かどうかを認証するために必要です。 |
| *imsToken* | 文字列 | いいえ |  | 認証に使用される IMS ベアラートークン。 `imsToken` 非 SUSI フローを使用する場合は必須です。 |
| *apiKey* | 文字列 | いいえ |  | AEM Discovery サービスへのアクセスに使用する API キー。 `apiKey` 非 SUSI フローを使用する場合は必須です。 |
| *rootPath* | 文字列 | いいえ | /content/dam/ | アセットセレクターにアセットを表示するフォルダーパス。 `rootPath` また、カプセル化の形で使用することもできます。 例えば、次のパスを指定すると、 `/content/dam/marketing/subfolder/`の場合、アセットセレクターを使用すると、親フォルダーをトラバースできず、子フォルダーのみが表示されます。 |
| *パス* | 文字列 | いいえ |  | アセットセレクターがレンダリングされる際に、アセットの特定のディレクトリに移動するために使用されるパス。 |
| *filterSchema* | 配列 | いいえ |  | フィルタープロパティの設定に使用するモデル。 これは、アセットセレクターで特定のフィルターオプションを制限する場合に便利です。 |
| *filterFormProps* | オブジェクト | いいえ |  | 検索を絞り込むために使用する必要があるフィルタープロパティを指定します。 例えば、MIME タイプのJPG、PNG、GIF。 |
| *selectedAssets* | 配列 `<Object>` | いいえ |  | アセットセレクターがレンダリングされる際に、「選択したアセット」を指定します。 アセットの id プロパティを含むオブジェクトの配列が必要です。 例： `[{id: 'urn:234}, {id: 'urn:555'}]` アセットは、現在のディレクトリに存在する必要があります。 別のディレクトリを使用する必要がある場合は、 `path` プロパティも同様に使用します。 |
| *acvConfig* | オブジェクト | いいえ |  | デフォルトを上書きするカスタム設定を含むオブジェクトを含むアセットコレクション表示プロパティ。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | いいえ |  | OOTB 翻訳がアプリケーションのニーズに合わない場合は、独自のカスタムローカライズされた値を `i18nSymbols` prop. このインターフェイスに値を渡すと、提供されたデフォルトの翻訳が上書きされ、代わりに独自の翻訳が使用されます。  上書きを実行するには、有効な [メッセージ記述子](https://formatjs.io/docs/react-intl/api/#message-descriptor) ～の鍵に対して異議を唱える `i18nSymbols` 上書きする値を指定します。 |
| *intl* | オブジェクト | いいえ |  | アセットセレクターは、デフォルトの標準翻訳を提供します。 翻訳言語を選択するには、 `intl.locale` prop. 例： `intl={{ locale: "es-es" }}` </br></br> サポートされるロケール文字列は、 [ISO 639 — コード](https://www.iso.org/iso-639-language-codes.html) 言語標準の名前を表すための </br></br> サポートされているロケールの一覧：英語 — 「en-us」（デフォルト）スペイン語 — 「es-es」ドイツ語 — 「de-de」フランス語 — 「fr-fr」イタリア語 — 「it-it」日本語 — 「ja-jp」韓国語 — 「ko-kr」ポルトガル語 — 「pt-br」中国語（繁体字） — 「zh-cn」中国語（台湾） — 「zh-tw」 |
| *repositoryId* | 文字列 | いいえ | &quot; | アセットセレクターがコンテンツを読み込む元のリポジトリ。 |
| *additionalAemSolutions* | `Array<string>` | いいえ | [ ] | 追加のAEMリポジトリのリストを追加できます。 このプロパティで情報が提供されない場合、メディアライブラリまたはAEM Assetsリポジトリのみが考慮されます。 |
| *hideTreeNav* | ブール値 | いいえ |  | アセットツリーのナビゲーションサイドバーを表示するか非表示にするかを指定します。 このプロパティはモーダルビューでのみ使用されるので、レールビューではこのプロパティの効果はありません。 |
| *onDrop* | 関数 | いいえ |  | プロパティは、アセットのドロップ機能を許可します。 |
| *dropOptions* | `{allowList?: Object}` | いいえ |  | 「設許可リスト定」を使用してドロップオプションを設定します。 |
| *colorScheme* | 文字列 | いいえ |  | テーマの設定 (`light` または `dark`) をクリックします。 |
| *handleSelection* | 関数 | いいえ |  | アセットが選択され、 `Select` 」ボタンがクリックされました。 この関数は、モーダルビューでのみ呼び出されます。 パネル表示の場合は、 `handleAssetSelection` または `onDrop` 関数 例： <pre>handleSelection=(assets:アセット[])=> {...}</pre> 詳しくは、 [選択したアセットタイプ](#selected-asset-type) 」を参照してください。 |
| *handleAssetSelection* | 関数 | いいえ |  | アセットが選択または選択解除されているので、項目の配列を使用して呼び出されます。 これは、ユーザーがアセットを選択したときにアセットをリッスンする場合に役立ちます。 例： <pre>handleSelection=(assets:アセット[])=> {...}</pre> 詳しくは、 [選択したアセットタイプ](#selected-asset-type) 」を参照してください。 |
| *onClose* | 関数 | いいえ |  | 次の場合に呼び出し `Close` モーダルビューのボタンが押された。 これは、 `modal` ～に対する見解と無視 `rail` 表示 |
| *onFilterSubmit* | 関数 | いいえ |  | ユーザーが異なるフィルター条件を変更したときに、フィルター項目を使用して呼び出されました。 |
| *selectionType* | 文字列 | いいえ | 1 人 | の設定 `single` または `multiple` 一度に選択したアセット。 |

## アセットセレクタープロパティの使用例 {#usage-examples}

アセットセレクター [プロパティ](#asset-selector-properties) 内 `index.html` ファイルを編集して、アプリケーション内のアセットセレクター表示をカスタマイズします。

### 例 1:パネル表示のアセットセレクター

![rail-view-example](assets/rail-view-example-vanilla.png)

AssetSelector の値が `rail` が `false` またはがプロパティで指定されていない場合、アセットセレクターはデフォルトでモーダルビューに表示されます。

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### 例 2:メタデータポップオーバー

様々なプロパティを使用して、情報アイコンを使用して表示するアセットのメタデータを定義します。 情報ポップオーバーは、アセットまたはフォルダーに関する情報のコレクションを提供します。この情報には、タイトル、ディメンション、変更日、場所、アセットの説明などが含まれます。 次の例では、様々なプロパティを使用してアセットのメタデータを表示します。例えば、 `repo:path` プロパティは、アセットの場所を指定します。 <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)


### 例 3:パネル表示のカスタムフィルタープロパティ

アセットセレクターを使用すると、ファセット検索に加えて、様々な属性をカスタマイズして、検索を絞り込むことができます。 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] アプリケーション。 次のコードを追加して、カスタマイズした検索フィルターをアプリケーションに追加する必要があります。 次の例では、 `Type Filter` 「画像」、「ドキュメント」、「ビデオ」の中からアセットタイプをフィルタリングする検索、または検索に追加したフィルタータイプ。

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

<!-- Property details to be added here. Referred the ticket https://jira.corp.adobe.com/browse/ASSETS-19023-->

<!--
## Asset Selector Object Schema {#object-schema}

Schema describes the object properties associated with an asset selected using Asset Selector. It uses the combination of data types and their values to validate the object describing the selected Asset using an Asset Selector.

**Schema Syntax**
````
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
````

**Query Parameters**

| Parameter | Type | Description |
|---|---|---|
| repo:id | string | ID of an Asset |
| repo:name | string | The name of an Asset |
| repo:path | string | The path of an Asset |
| repo:size | number | Size of an Asset (in bytes) |
| repo:createdBy | string | ID of a user who created an Asset |
| repo: createdDate | string | The timestamp when an asset was created |
| repo:modifiedBy | string | ID of a user who modified the asset recently |
| repo:modifyDate | string | The timestamp when the asset was last modified |
| dc:format | string | MIME type of an Asset |
| tiff:imageWidth | number | The width of an image type of Asset |
| tiff:imageLength | number | The height of an image type of Asset |
| repo:state | string | The `Approved`, `Rejected`, or `Expired`state of an Asset |
| computedMetadata | string | It is an object that represents a bucket for all the Asset's metadata of all kinds (repository, application or embedded metadata) |
| _links | string | It represents the collection of links used in the Asset Selector. The links are represented in the form of an array. The parameters of an array include: `href`, `type`, `repo:size`, `width`, `height`, etc.  |

For the detailed example of Object Schema, click 
-->

## オブジェクトスキーマを使用したアセットの選択の処理 {#handling-selection}

この `handleSelection` プロパティは、アセットセレクターで 1 つまたは複数のアセットを選択した場合に処理するために使用されます。 次の例に、の使用構文を示します。 `handleSelection`.

![handle-selection](assets/handling-selection.png)

## アセットセレクターの使用 {#using-asset-selector}

アセットセレクターを設定し、アセットセレクターを [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] アプリケーションでは、アセットを選択したり、様々な操作を実行してリポジトリ内のアセットを検索したりできます。

![using-asset-selector](assets/using-asset-selector.png)

* **A**: [パネルを非表示/表示](#hide-show-panel)
* **B**: [リポジトリスイッチャー](#repository-switcher)
* **C**: [Assets](#repository)
* **D**: [フィルター](#filters)
* **E**: [検索バー](#search-bar)
* **金**: [並べ替え](#sorting)
* **G**: [昇順または降順での並べ替え](#sorting)
* **H**: [表示](#types-of-view)

### パネルを非表示/表示 {#hide-show-panel}

左側のナビゲーションでフォルダーを非表示にするには、 **[!UICONTROL フォルダーを非表示]** アイコン 変更を元に戻すには、 **[!UICONTROL フォルダーを非表示]** アイコンを再度クリックします。

### リポジトリスイッチャー {#repository-switcher}

また、アセットセレクターでは、アセット選択用にリポジトリを切り替えることもできます。 左側のパネルにあるドロップダウンから、目的のリポジトリを選択できます。 ドロップダウンリストで使用できるリポジトリオプションは、 `repositoryId` プロパティが `index.html` ファイル。 ログインしたユーザーがアクセスする、選択した IMS 組織の環境に基づきます。 消費者は優先 `repositoryID` その場合、アセットセレクターはリポジトリのレンダリングを停止し、特定のリポジトリからのみアセットをレンダリングします。
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### Assets リポジトリ

操作を実行する際に使用できるアセットフォルダーの集まりです。

### 標準のフィルター {#filters}

アセットセレクターには、検索結果を絞り込むための標準のフィルターオプションも用意されています。 次のフィルターを使用できます。

* `File type`:フォルダー、ファイル、画像、ドキュメント、ビデオが含まれます
* `MIME type`:JPG、GIF、PPTX、PNG、MP4、DOCX、TIFF、PDF、XLSX を含む
* `Image Size`:画像の最小/最大の幅、最小/最大の高さを含む

![rail-view-example](assets/filters-asset-selector.png)

### カスタム検索

アセットセレクターでは、フルテキスト検索以外にも、カスタマイズされた検索を使用してファイル内のアセットを検索することができます。 カスタム検索フィルターは、モーダル表示モードとレール表示モードの両方で使用できます。

![カスタム検索](assets/custom-search.png)

また、デフォルトの検索フィルターを作成して、頻繁に検索するフィールドを保存し、後で使用することもできます。 アセットのカスタム検索を作成するには、 `filterSchema` プロパティ。

### 検索バー {#search-bar}

アセットセレクターを使用すると、選択したリポジトリ内のアセットに対して全文検索を実行できます。 例えば、次のようなキーワードを入力した場合、 `wave` 検索バーで、 `wave` キーワードが表示されます。

### 並べ替え {#sorting}

アセットセレクター内のアセットを、名前、サイズまたはアセットのサイズで並べ替えることができます。 アセットを昇順または降順で並べ替えることもできます。

### ビューのタイプ {#types-of-view}

アセットセレクターを使用すると、次の 4 つの異なるビューでアセットを表示できます。

* **![リスト表示](assets/do-not-localize/list-view.png) [!UICONTROL リスト表示]**:リスト表示では、スクロール可能なファイルとフォルダが 1 列に表示されます。
* **![グリッド表示](assets/do-not-localize/grid-view.png) [!UICONTROL グリッド表示]**:グリッド表示では、スクロール可能なファイルとフォルダが行と列のグリッドに表示されます。
* **![ギャラリー表示](assets/do-not-localize/gallery-view.png) [!UICONTROL ギャラリー表示]**:ギャラリー表示では、中央にロックされた水平リストにファイルやフォルダが表示されます。
* **![滝ビュー](assets/do-not-localize/waterfall-view.png) [!UICONTROL ウォーターフォール表示]**:ウォーターフォールビューには、ファイルやフォルダが Bridge の形式で表示されます。

<!--
### Modes to view Asset Selector

Asset Selector supports two types of out of the box views:

**  Modal view or Inline view:** The modal view or inline view is the default view of Asset Selector that represents Assets folders in the front area. The modal view allows users to view assets in a full screen to ease the selection of multiple assets for import. Use `<AssetSelector rail={false}>` to enable modal view.

    ![modal-view](assets/modal-view.png)

**  Rail view:** The rail view represents Assets folders in a left panel. The drag and drop of assets can be performed in this view. Use `<AssetSelector rail={true}>` to enable rail view.

    ![rail-view](assets/rail-view.png)
-->
<!--

### Application Integration

Asset Selector is flexible and can be integrated within your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application. It is accessible and localized to add, search, and select assets in your application. With Asset Selector you can:
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It allows you to control the display of various text or symbols as per your choice.
*   **Perfect fit** Asset selector easily fits in your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application and choose the way you want to view. The mode of view can be inline, rail, or modal view.
*   **Accessible** With Asset Selector, you can reach the desired asset in an easy manner.
*   **Localize** Assets can be availed for the various locales available as per Adobe's localization standards.
-->
<!--

### Support for multiple instances

The micro front-end design supports the display of multiple instances of Asset Selector on a single screen.

![multiple-instance](assets/multiple-instance.png)
-->

<!--

### Controlled selection with multi-select

You can make default multi-selection of assets by specifying the assets to the component using `selectedAssets` property. You should specify an array of asset IDs. For example, `[{id: 'urn:234}, {id: 'urn:555'}].`
-->
<!--

### Action buttons

When you customize your application with Asset Selector based on ReactJS, you are provided with the following action buttons to perform various actions:
*   **Open in media library** Allows you to open the asset in media library.
*   **Upload** Allows you to upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector allows you to know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->