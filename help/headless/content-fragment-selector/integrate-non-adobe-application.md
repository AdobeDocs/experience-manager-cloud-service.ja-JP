---
title: コンテンツフラグメントセレクターとAdobe以外のアプリケーションまたはサードパーティアプリケーションとの統合
description: コンテンツフラグメントセレクターを様々なAdobe、Adobe以外およびサードパーティ製アプリケーションと統合します。
role: Admin, User, Developer
source-git-commit: 3af1a89489af96bf9c9908aea7fb20883956517b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 17%

---

# アドビ以外のアプリケーションとの統合 {#integration-with-non-adobe-application}

コンテンツフラグメントセレクターを使用すると、Adobe以外の様々なアプリケーションやサードパーティアプリケーションと統合し、シームレスに連携できるようになります。

## 前提条件 {#prerequisites}

コンテンツフラグメントセレクターをAdobe以外のアプリケーションと統合する場合は、次の前提条件を使用してください。

* [前提条件](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Adobe以外のアプリケーションと統合する場合、コンテンツフラグメントセレクターは、`imsScope` や `imsClientID` などのAdobe Experience Manager System （IMS）プロパティを使用して、Identity Management（AEM）as a Cloud Service リポジトリへの認証をサポートします。

## Adobe以外のアプリケーション用のコンテンツフラグメントセレクターの設定 {#configure-content-fragment-selector-for-a-non-adobe-application}

Adobe以外のアプリケーションに対してコンテンツフラグメントセレクターを設定するには、統合手順に進む前に、プロビジョニングのサポートチケットをログに記録する必要があります。

### サポートチケットのログ {#logging-a-support-ticket}

Admin Console を使用してサポートチケットを記録する手順は次のとおりです。

1. チケットのタイトルに **AEM フラグメントを使用したコンテンツフラグメントセレクター** を追加します。

1. 説明には、次の詳細を入力します。

   * Experience Manager as a Cloud Serviceの URL （プログラム ID および環境 ID）。
   * アドビ以外の web アプリケーションがホストされるドメイン名。

## 統合手順 {#integration-steps}

コンテンツフラグメントセレクターをAdobe以外のアプリケーションと統合する場合の認証用の `index.html` ファイルの例を次に示します。

* `Script` タグを使用して、コンテンツフラグメントセレクターパッケージにアクセスします。

* IMS フロープロパティ（`imsClientId`、`imsScope`、`redirectURL` など）を定義します。

   * この関数を使用するには、`imsClientId` プロパティと `imsScope` プロパティの少なくとも 1 つを定義する必要があります。
   * `redirectURL` の値を定義しない場合は、クライアント ID に登録されているリダイレクト URL が使用されます。

* この例では `imsToken` が生成されていないので、`registerFragmentsSelectorsAuthService` 関数と `renderFragmentSelectorWithAuthFlow` 関数を使用します。

   * `registerFragmentsSelectorsAuthService` の前に `renderFragmentSelectorWithAuthFlow` 関数を使用して、コンテンツフラグメントセレクターに `imsToken` を登録します。
   * Adobeでは、コンポーネントをインスタンス化する際に `registerFragmentsSelectorsAuthService` を呼び出すことをお勧めします。

* `const props` の節で、認証およびその他のフラグメント as a Cloud Service アクセス関連プロパティを定義します。
* `PureJSContentFragmentSelectors` グローバル変数を使用して、web ブラウザーでコンテンツフラグメントセレクターをレンダリングします。
* コンテンツフラグメントセレクターは、`<div>` コンテナ要素にレンダリングされます。 この例では、ダイアログを使用してコンテンツフラグメントセレクターを表示します。

**例`ìndex.html`**

```html {line-numbers="true"}
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <link rel="icon" type="image/svg+xml" href="/vite.svg" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>testing-cf-mfe-integration-with-3rd-party-app</title>
        <script
            id="content-fragments-selector"
            src="https://experience.adobe.com/solutions/CQ-sites-content-fragment-selector/static-assets/resources/content-fragment-selector.js"
        ></script>
        <script>
            const imsProps = {
                imsClientId: '<IMS_CLIENT_ID>',
                imsScope:
                    'additional_info.projectedProductContext, AdobeID, openid, read_organizations',
                redirectUrl: window.location.href,
                onImsServiceInitialized: (service) => {
                    // invoked when the ims service is initialized and is ready
                    console.log('onImsServiceInitialized', service);
                },
                onAccessTokenReceived: (token) => {
                    console.log('onAccessTokenReceived', token);
                },
                onAccessTokenExpired: () => {
                    console.log('onAccessTokenError');
                    // re-trigger sign-in flow
                },
                onErrorReceived: (type, msg) => {
                    console.log('onErrorReceived', type, msg);
                },
            };

            function load() {
                const registeredTokenService =
                    PureJSContentFragmentSelectors.registerContentFragmentSelectorAuthService(
                        imsProps
                    );
                imsInstance = registeredTokenService;
            }

            // initialize the IMS flow before attempting to render the content fragment selector
            load();

            // function that will render the content fragment selector
            function renderContentFragmentSelectorWithAuthFlow() {
                const contentFragmentSelectorDialog = document.getElementById(
                    'content-fragment-selector-dialog'
                );

                const contentFragmentSelectorProps = {
                    inventoryViewToggleEnabled: true,
                    isOpen: true,
                    noWrap: false,
                    orgId: 'YOUR_ORG_ID@AdobeOrg',
                    // repoId: "author-p12345-e67890.adobeaemcloud.com", // if wanted to restrict to a specific repo
                    runningInUnifiedShell: false,
                    onDismiss: () => contentFragmentSelectorDialog.close(),
                    onSubmit: ({ contentFragments }) => {
                        const selectedContentFragment = contentFragments[0];
                        alert(selectedContentFragment.path);
                    },
                };
                // container element on which you want to render the ContentFragmentSelector component
                const container = document.getElementById('content-fragment-selector');

                /// Use the PureJSContentFragmentSelectors in globals to render the ContentFragmentSelector component
                PureJSContentFragmentSelectors.renderContentFragmentSelectorWithAuthFlow(
                    container,
                    contentFragmentSelectorProps,
                    () => contentFragmentSelectorDialog.showModal()
                );
            }
        </script>
    </head>
    <body>
        <div>
            <button onclick="renderContentFragmentSelectorWithAuthFlow()">
                Content Fragment Selector - Select Content Fragments with Ims Flow
            </button>
        </div>
        <dialog id="content-fragment-selector-dialog">
            <div
                id="content-fragment-selector"
                style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px"
            ></div>
        </dialog>
    </body>
</html>
```

## 配信リポジトリにアクセスできない {#unable-to-access-delivery-repository}

「新規登録」サインインワークフローを使用してコンテンツフラグメントセレクターを統合しても、配信リポジトリにアクセスできない場合は、ブラウザーの Cookie が消去されていることを確認します。

そうしないと、コンソールに `invalid_credentials All session cookies are empty` エラーが表示される場合があります。
