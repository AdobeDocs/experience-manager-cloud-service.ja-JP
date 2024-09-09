---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] のアセットセレクター'
description: アセットセレクターを様々なAdobe、Adobe以外のアプリケーションおよびサードパーティアプリケーションと統合します。
role: Admin, User
exl-id: 55848de0-aff2-42a0-b959-c771235d9425
source-git-commit: 575980320c1dbd32f799bf9c2fddf3d6773c838a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 73%

---

# Adobe以外のアプリケーションとの統合 {#integrate-asset-selector-non-adobe-app}

アセットセレクターを使用すると、Adobe以外の様々なアプリケーションやサードパーティのアプリケーションを統合し、それらをシームレスに連携できるようになります。

## 前提条件 {#prereqs-non-adobe-app}

アセットセレクターをアドビ以外のアプリケーションと統合する場合は、次の前提条件を使用します。

* [通信方法](/help/assets/overview-asset-selector.md#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

アセットセレクターは、アドビ以外のアプリケーションと統合する場合に、`imsScope` や `imsClientID` などの Identity Management System（IMS）プロパティを使用した [!DNL Experience Manager Assets] リポジトリへの認証をサポートします。

## Adobe以外のアプリケーション用のアセットセレクターを設定する {#configure-non-adobe-app}

Adobe以外のアプリケーションにアセットセレクターを設定するには、プロビジョニングのサポートチケットをログに記録してから、統合手順を実行する必要があります。

### サポートチケットのログ {#log-a-support-ticket}

Admin Console を使用してサポートチケットを記録する手順は次のとおりです。

1. チケットのタイトルに **AEM Assets を含むアセットセレクター**&#x200B;を追加します。

1. 説明には、次の詳細を入力します。

   * [!DNL Experience Manager Assets] as a [!DNL Cloud Service] URL（プログラム ID および環境 ID）。
   * アドビ以外の web アプリケーションがホストされるドメイン名。

## 統合手順 {#non-adobe-app-integration-steps}

アセットセレクターをAdobe以外のアプリケーションと統合する場合の認証用の `index.html` ファイルの例を次に示します。

`index.html` ファイルの例の *9 行目*&#x200B;から *11 行目*&#x200B;に示すように、`Script` タグを使用してアセットセレクターパッケージにアクセスします。

この例の *14 行目*&#x200B;から *38 行目*&#x200B;では、`imsClientId`、`imsScope`、`redirectURL` などの IMS フロープロパティが記載されています。この関数では、`imsClientId` プロパティと `imsScope` プロパティの少なくとも 1 つを定義する必要があります。`redirectURL` の値を定義しない場合は、クライアント ID に登録されているリダイレクト URL が使用されます。

`imsToken` が生成されていないので、`index.html` ファイルの例の 40 行目から 50 行目に示すように、`registerAssetsSelectorsAuthService` 関数と `renderAssetSelectorWithAuthFlow` 関数を使用します。`renderAssetSelectorWithAuthFlow` の前に `registerAssetsSelectorsAuthService` 関数を使用して、`imsToken` をアセットセレクターに登録します。[!DNL Adobe] では、コンポーネントをインスタンス化する際に `registerAssetsSelectorsAuthService` を呼び出すことをお勧めします。

`index.html` ファイルの例の *54 行目*&#x200B;から *60 行目*&#x200B;に示すように、`const props` セクションで認証およびその他の Assets as a Cloud Service アクセス関連のプロパティを定義します。

*65 行目*&#x200B;に示している `PureJSSelectors` グローバル変数は、web ブラウザーでアセットセレクターをレンダリングするために使用されます。

*74 行目*&#x200B;から *81 行目*&#x200B;に示すように、アセットセレクターは `<div>` コンテナ要素にレンダリングされます。例では、ダイアログを使用してアセットセレクターを表示します。

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

## 配信リポジトリにアクセスできません {#unable-to-access-delivery-repository}

>[!TIP]
>
>新規登録ログインワークフローを使用してアセットセレクターを統合したにもかかわらず配信リポジトリにアクセスできない場合は、ブラウザーの Cookie をクリーンアップする必要があります。そうしないと、コンソールに `invalid_credentials All session cookies are empty` エラーが表示されます。

>[!MORELIKETHIS]
>
>* [ アセットセレクターと様々なアプリケーションの統合 ](/help/assets/integrate-asset-selector.md)
>* [ アセットセレクターのプロパティ ](/help/assets/asset-selector-properties.md)
>* [ アセットセレクターとDynamic Mediaの OpenAPI 機能との統合 ](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [ アセットセレクターのカスタマイズ ](/help/assets/asset-selector-customization.md)
