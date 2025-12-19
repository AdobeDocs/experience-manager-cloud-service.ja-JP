---
title: Adobe Experience Manager as a Cloud Service 用マイクロフロントエンドコンテンツフラグメントセレクターのプロパティ
description: アプリケーションからコンテンツフラグメントを検索、発見、取得するマイクロフロントエンドコンテンツフラグメントセレクターを設定するプロパティ。
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: 58995ae9c29d5a76b3f94de43f2bafecdaf7cf68
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 63%

---

# コンテンツフラグメントセレクター - 関連プロパティ {#content-fragment-selector-related-properties}

マイクロフロントエンドコンテンツフラグメントセレクターを使用すると、リポジトリ内のコンテンツフラグメントを参照または検索し、アプリケーションで使用できます。

次のプロパティを使用して、コンテンツフラグメントセレクターのレンダリング方法と使用方法をカスタマイズできます。

## コンテンツフラグメントセレクターのプロパティ {#content-fragment-selector-properties}

| Property | タイプ | 必須 | デフォルト | 説明 |
|--- |--- |--- |--- |--- |
| `ref` | FragmentSelectorRef | | | `ContentFragmentSelector` インスタンスへの参照。`reload` などの提供された機能にアクセスできます。 |
| `imsToken` | 文字列 | 不要 | | 認証に使用される IMS トークン。 指定しない場合、IMS ログインフローが開始されます。 |
| `repoId` | 文字列 | 不要 | | フラグメントセレクターに使用されるリポジトリー ID。 指定した場合、セレクターは指定されたリポジトリに自動的に接続し、リポジトリドロップダウンは非表示になります。 指定しない場合、ユーザーは、アクセス可能なリポジトリのリストからリポジトリを選択できます。 |
| `defaultRepoId` | 文字列 | 不要 | | リポジトリセレクターが表示されたときにデフォルトで選択されるリポジトリ ID。 `repoId` が指定されていない場合にのみ使用されます。 `repoId` が設定されている場合、リポジトリセレクターは非表示になり、この値は無視されます。 |
| `orgId` | 文字列 | 不要 | | 認証に使用する組織 ID。 指定しない場合、ユーザーは、アクセス権を持つ別の組織からリポジトリを選択できます。 ユーザーがどのリポジトリや組織にもアクセスできない場合、コンテンツは読み込まれません。 |
| `locale` | 文字列 | 不要 | 「en-US」 | ロケール。 |
| `env` | 文字列 | 不要 | | デプロイメント環境。 許可されている環境名については、`Env` のタイプを参照してください。 |
| `filters` | FragmentFilter | いいえ | `{ folder: "/content/dam" }` | コンテンツフラグメントのリストに適用するフィルター。 デフォルトでは、`/content/dam` 下のフラグメントが表示されます。 |
| `isOpen` | ブーリアン | 不要 | `false` | セレクターが開いているか閉じているかを制御するフラグ。 |
| `noWrap` | ブーリアン | 不要 | `false` | フラグメントセレクターをラッピングダイアログなしでレンダリングするかどうかを決定します。 `true` に設定すると、フラグメントセレクターは親コンテナに直接埋め込まれます。 セレクターをカスタムレイアウトまたはワークフローに統合する場合に役立ちます。 |
| `onSelectionChange` | （{ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }） => void | いいえ | | コンテンツフラグメントの選択が変更されるたびにトリガーされるコールバック関数。 現在選択されているフラグメント、ドメイン名、テナント情報、リポジトリ ID および配信リポジトリを提供します。 |
| `onDismiss` | () => void | いいえ | | 解除アクションが実行される（セレクターを閉じるなど）ときにトリガーされるコールバック関数。 |
| `onSubmit` | （{ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }） => void | いいえ | | ユーザーが選択を確認するとトリガーされるコールバック関数。 選択したコンテンツフラグメント、ドメイン名、テナント情報、リポジトリ ID および配信リポジトリを受信します。 |
| `theme` | 「light」または「dark」 | いいえ | | フラグメントセレクターのテーマ。 デフォルトでは、unifiedShell 環境テーマに設定されています。 |
| `selectionType` | 「single」または「multiple」 | いいえ | `single` | 選択タイプを使用して、フラグメントセレクターの選択対象を制限できます。 |
| `dialogSize` | 「fullscreen」または「fullscreenTakeover」 | いいえ | `fullscreen` | ダイアログのサイズを制御するオプションの prop。 |
| `runningInUnifiedShell` | ブーリアン | 不要 | | DestinationSelector が UnifiedShell またはスタンドアロンのどちらで実行されているか。 |
| `readonlyFilters` | ResourceReadonlyFiltersField[] | いいえ | | コンテンツフラグメントのリストに適用される読み取り専用フィルター。 これらのフィルターは、ユーザーが削除することはできません。 |
| `selectedFragments` | ContentFragmentIdentifier[] | いいえ | `[]` | セレクターを開いたときに事前に選択されるコンテンツフラグメントの初期選択。 |
| `hipaaEnabled` | ブーリアン | 不要 | `false` | HIPAA 準拠が有効かどうかを示します。 |
| `inventoryView` | 在庫ビュータイプ | いいえ | `table` | セレクターで使用される在庫の既定の表示タイプ。 |
| `inventoryViewToggleEnabled` | ブーリアン | 不要 | `false` | ユーザーがテーブル表示とグリッド表示を切り替えることができる在庫表示切替スイッチが有効かどうかを示します。 |

## ImsAuthProps プロパティ {#imsauthprops-properties}

`ImsAuthProps` プロパティは、コンテンツフラグメントセレクターが `imsToken` を取得するのに使用する認証情報とフローを定義します。これらのプロパティを設定すると、認証フローの動作を制御し、様々な認証イベントのリスナーを登録できます。

| プロパティ名 | 説明 |
|--- |--- |
| `imsClientId` | 認証目的で使用される IMS クライアント ID を表す文字列値。この値はアドビが指定し、アドビの AEM CS 組織に固有です。 |
| `imsScope` | 認証で使用されるスコープについて説明します。スコープは、組織のリソースに対するアプリケーションのアクセスレベルを決定します。複数のスコープは、コンマで区切ることができます。 |
| `redirectUrl` | 認証後にユーザーがリダイレクトされる URL を表します。この値は通常、アプリケーションの現在の URL に設定されます。`redirectUrl` を指定していない場合、`ImsAuthService` は `imsClientId` の登録に使用した redirectUrl を使用します。 |
| `modalMode` | 認証フローをモーダル（ポップアップ）に表示するかどうかを示すブール値。`true` に設定すると、認証フローがポップアップで表示されます。`false` に設定すると、認証フローはページ全体をリロードして表示されます。<br>**メモ：** UX を向上させるために、ユーザーがブラウザーのポップアップを無効にしている場合は、この値を動的に制御できます。 |
| `onImsServiceInitialized` | Adobe IMS 認証サービスを初期化する際に呼び出されるコールバック関数。この関数は、Adobe IMS サービスを表すオブジェクトである `service` という 1 つのパラメーターを受け取ります。詳しくは、[`ImsAuthService`](#imsauthservice-ims-auth-service) を参照してください。 |
| `onAccessTokenReceived` | Adobe IMS 認証サービスから `imsToken` を受信する際に呼び出されるコールバック関数。この関数は、アクセストークンを表す文字列である `imsToken` という 1 つのパラメーターを受け取ります。 |
| `onAccessTokenExpired` | アクセストークンの有効期限が切れる際に呼び出されるコールバック関数。この関数は通常、新しい認証フローをトリガーして新しいアクセストークンを取得するために使用されます。 |
| `onErrorReceived` | 認証中にエラーが発生する際に呼び出されるコールバック関数。この関数は、エラータイプとエラーメッセージという 2 つのパラメーターを受け取ります。エラータイプはエラータイプを表す文字列で、エラーメッセージはエラーメッセージを表す文字列です。 |

## ImsAuthService プロパティ {#imsauthservice-properties}

`ImsAuthService` クラスは、コンテンツフラグメントセレクターの認証フローを処理します。これは、Adobe IMS 認証サービスから `imsToken` を取得する役割を果たします。`imsToken` は、ユーザーを認証し、Adobe Experience Manager（AEM）CS リポジトリへのアクセスを認証するのに使用されます。ImsAuthService は、`ImsAuthProps` プロパティを使用して認証フローを制御し、様々な認証イベントのリスナーを登録します。便利な `registerContentFragmentSelectorAuthService` 関数を使用して、`ImsAuthService` インスタンスをコンテンツフラグメントセレクターに登録できます。`ImsAuthService` クラスでは、次の関数を使用できます。ただし、`registerContentFragmentSelectorAuthService` 関数を使用している場合は、これらの関数を直接呼び出す必要はありません。

| 関数名 | 説明 |
|--- |--- |
| `isSignedInUser` | ユーザーが現在サービスにログインしているかどうかを判断し、それに応じてブール値を返します。 |
| `getImsToken` | 現在ログインしているユーザーの認証 `imsToken` を取得します。これは、アセット&#x200B;_レンディション_&#x200B;の生成など、他のサービスへのリクエストを認証するのに使用できます。 |
| `signIn` | ユーザーのログインプロセスを開始します。この関数は、`ImsAuthProps` を使用して、ポップアップまたはページ全体のリロードで認証を表示します。 |
| `signOut` | ユーザーをサービスからログアウトし、認証トークンを無効にし、保護されたリソースにアクセスするには再度ログインするようにリクエストします。この関数を呼び出すと、現在のページがリロードされます。 |
| `refreshToken` | 現在ログインしているユーザーの認証トークンを更新して、トークンの有効期限切れを防ぎ、保護されたリソースに中断なくアクセスできるようになります。後続のリクエストに使用できる新しい認証トークンを返します。 |
