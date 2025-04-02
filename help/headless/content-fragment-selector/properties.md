---
title: Adobe Experience Manager as a Cloud Service用マイクロフロントエンドコンテンツフラグメントセレクタープロパティ
description: アプリケーションからコンテンツフラグメントを検索、検索、取得するようにマイクロフロントエンドコンテンツフラグメントセレクターを設定するためのプロパティ。
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: a3d8961b6006903c42d983c82debb63ce8abe9ad
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 48%

---

# コンテンツフラグメントセレクター – 関連プロパティ {#content-fragment-selector-related-properties}

マイクロフロントエンドコンテンツフラグメントセレクターを使用すると、リポジトリ内のコンテンツフラグメントを参照または検索し、アプリケーションで使用できます。

次のプロパティを使用して、コンテンツフラグメントセレクターのレンダリング方法と使用方法をカスタマイズできます。

## コンテンツフラグメントセレクターのプロパティ {#content-fragment-selector-properties}

| Property | タイプ | 必須 | デフォルト | 説明 |
|--- |--- |--- |--- |--- |
| `imsToken` | 文字列 | いいえ | | 認証に使用される IMS トークン。 |
| `repoId` | 文字列 | いいえ | | 認証に使用されるリポジトリ ID。 |
| `orgId` | 文字列 | はい | | 認証に使用する組織 ID。 |
| `locale` | 文字列 | いいえ | | ロケールデータ |
| `env` | 環境 | なし | | コンテンツフラグメントセレクターのデプロイメント環境 |
| `filters` | FragmentFilter | なし | | コンテンツフラグメントのリストに適用するフィルター。 デフォルトでは、`/content/dam` 下のフラグメントが表示されます。 デフォルト値：`{ folder: "/content/dam" }` |
| `isOpen` | ブール値 | あり | `false` | セレクターを開いたり閉じたりするトリガーを示すフラグ。 |
| `onDismiss` | （） => 無効 | あり | | **解除** が選択されたときに呼び出される関数。 |
| `onSubmit` | （{ contentFragments: `{id: string, path: string}[]`, domainNames: `string[]` }） => void | あり | | 1 つ以上のコンテンツフラグメントを選択した後に **Select** を使用した場合に呼び出される関数。 <br><br> 関数は次を受け取ります。<br><ul><li> 選択したコンテンツフラグメントの「`id`」フィールドと「`path`」フィールド</li><li>リポジトリのプログラム id と環境 id に関連するドメイン名（ステータス `ready` と `tier` パブリッシュを持つ）</li></ul><br> ドメイン名がない場合は、パブリッシュインスタンスがフォールバックドメインとして使用されます。 |
| `theme` | 「明るい」または「暗い」 | なし | | コンテンツフラグメントセレクターのテーマ。 デフォルトのテーマは、UnifiedShell 環境のテーマに設定されています。 |
| `selectionType` | 「single」または「multiple」 | なし | `single` | FragmentSelector の選択制限に使用できる選択タイプ。 |
| `dialogSize` | 「fullscreen」または「fullscreenTakeover」 | なし | `fullscreen` | ダイアログのサイズを制御するオプションのプロパティ。 |
| `waitForImsToken` | ブール値 | いいえ | `false` | コンテンツフラグメントセレクターが SUSI フローのコンテキストでレンダリングされるかどうかを示し、コンテン `imsToken` が準備されるのを待つ必要があります。 |
| `imsAuthInfo` | ImsAuthInfo | なし | | ログインしたユーザーの IMS 認証情報を含むオブジェクト。 |
| `runningInUnifiedShell` | ブール値 | いいえ | | コンテンツフラグメントセレクターが UnifiedShell またはスタンドアロンのどちらで実行されているかを示します。 |
| `readonlyFilters` | ResourceReadonlyFiltersField | なし | | コンテンツのリストに適用できる読み取り専用フィルター – は削除できません。 |

## ImsAuthProps プロパティ {#imsauthprops-properties}

`ImsAuthProps` のプロパティでは、コンテンツフラグメントセレクターがア `imsToken` ットを取得するために使用する認証情報およびフローを定義します。 これらのプロパティを設定すると、認証フローの動作を制御し、様々な認証イベントのリスナーを登録できます。

| プロパティ名 | 説明 |
|--- |--- |
| `imsClientId` | 認証目的で使用される IMS クライアント ID を表す文字列値。この値はアドビが指定し、アドビの AEM CS 組織に固有です。 |
| `imsScope` | 認証で使用されるスコープについて説明します。スコープは、組織のリソースに対するアプリケーションのアクセスレベルを決定します。複数のスコープは、コンマで区切ることができます。 |
| `redirectUrl` | 認証後にユーザーがリダイレクトされる URL を表します。この値は通常、アプリケーションの現在の URL に設定されます。`redirectUrl` が指定されていない場 `ImsAuthService`、`imsClientId` の登録に使用される redirectUrl が使用されます |
| `modalMode` | 認証フローをモーダル（ポップアップ）に表示するかどうかを示すブール値。`true` に設定すると、認証フローがポップアップで表示されます。`false` に設定すると、認証フローはページ全体の再読み込みで表示されます。<br>**メモ：** UX を向上させるために、ユーザーがブラウザーのポップアップを無効にしている場合は、この値を動的に制御できます。 |
| `onImsServiceInitialized` | Adobe IMS 認証サービスを初期化する際に呼び出されるコールバック関数。この関数は、Adobe IMS サービスを表すオブジェクトである `service` という 1 つのパラメーターを受け取ります。詳しくは、[`ImsAuthService`](#imsauthservice-ims-auth-service) を参照してください。 |
| `onAccessTokenReceived` | Adobe IMS 認証サービスから `imsToken` を受信する際に呼び出されるコールバック関数。この関数は、アクセストークンを表す文字列である `imsToken` という 1 つのパラメーターを受け取ります。 |
| `onAccessTokenExpired` | アクセストークンの有効期限が切れる際に呼び出されるコールバック関数。この関数は通常、新しい認証フローをトリガーして新しいアクセストークンを取得するために使用されます。 |
| `onErrorReceived` | 認証中にエラーが発生する際に呼び出されるコールバック関数。この関数は、エラータイプとエラーメッセージという 2 つのパラメーターを受け取ります。エラータイプはエラータイプを表す文字列で、エラーメッセージはエラーメッセージを表す文字列です。 |

## ImsAuthService プロパティ {#imsauthservice-properties}

`ImsAuthService` クラスは、コンテンツフラグメントセレクターの認証フローを処理します。 これは、Adobe IMS 認証サービスから `imsToken` を取得する役割を果たします。`imsToken` を使用してユーザーを認証し、Adobe Experience Manager（AEM） CS リポジトリへのアクセスを認証します。 ImsAuthService は、`ImsAuthProps` プロパティを使用して認証フローを制御し、様々な認証イベントのリスナーを登録します。便利な `registerContentFragmentSelectorAuthService` 関数を使用して、コンテンツフラグメントセレクターで `ImsAuthService` インスタンスを登録できます。 `ImsAuthService` クラスでは、次の関数を使用できます。ただし、`registerContentFragmentSelectorAuthService` 関数を使用している場合は、これらの関数を直接呼び出す必要はありません。

| 関数名 | 説明 |
|--- |--- |
| `isSignedInUser` | ユーザーが現在サービスにログインしているかどうかを判断し、それに応じてブール値を返します。 |
| `getImsToken` | 現在ログインしているユーザーの認証 `imsToken` を取得します。これは、アセット _レンディション_ の生成など、他のサービスへのリクエストを認証するために使用できます。 |
| `signIn` | ユーザーのログインプロセスを開始します。この関数は、`ImsAuthProps` を使用して、ポップアップまたはページ全体のリロードで認証を表示します。 |
| `signOut` | ユーザーをサービスからログアウトし、認証トークンを無効にし、保護されたリソースにアクセスするには再度ログインするようにリクエストします。この関数を呼び出すと、現在のページがリロードされます。 |
| `refreshToken` | 現在ログインしているユーザーの認証トークンを更新して、トークンの有効期限切れを防ぎ、保護されたリソースに中断なくアクセスできるようになります。後続のリクエストに使用できる新しい認証トークンを返します。 |
