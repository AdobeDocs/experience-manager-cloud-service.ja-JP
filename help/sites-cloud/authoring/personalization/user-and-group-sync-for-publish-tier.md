---
title: 登録、ログイン、ユーザープロファイル
description: AEM as a Cloud Service の登録、ログイン、ユーザーデータおよびグループ同期について説明します
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 98%

---

# 登録、ログイン、ユーザープロファイル {#registration-login-and-userprofile}

## はじめに {#introduction}

Web アプリケーションは、多くの場合、Web サイトへの登録用のアカウント管理機能を提供します。この機能は、ユーザーデータ情報を保持するので、ユーザーは登録後のログインで一貫した操作を楽しむことができます。この記事では、AEM as a Cloud Service の以下の概念について説明します。

* 登録
* ログイン
* ユーザープロファイルデータの保存
* グループメンバーシップ
* データ同期

## 登録 {#registration}

エンドユーザーが AEM アプリケーションのアカウントに登録すると、AEM Publish サービスにユーザーアカウントが作成されて、JCR リポジトリーの `/home/users` 下のユーザーリソースに反映されます。

以下に示すように、登録を実装するには 2 つの方法があります。

### AEM 管理 {#aem-managed-registration}

少なくともユーザーの名前とパスワードを受け取り、AEM でユーザーレコードを作成して、ログイン時の認証に使用できるように、カスタム登録コードを記述できます。通常、この登録メカニズムの構築には次の手順を使用します。

1. 登録情報を収集するカスタム AEM コンポーネントを表示します。
1. 送信時に、適切にプロビジョニングされたサービスユーザーが次のことに使用されます。
   1. UserManager API の `findAuthorizables()` メソッドの 1 つを使用して、既存のユーザーが存在しないことを確認します。
   1. UserManager API の `createUser()` メソッドの 1 つを使用して、ユーザーレコードを作成します。
   1. Authorizable インターフェイスの `setProperty()` メソッドを使用して、キャプチャされたプロファイルデータを永続化します。
1. ユーザーにメールの検証を求めるなどの、オプションのフロー。

**前提条件：**

上記のロジックを正しく機能させるには、適切なプログラムと環境を示すリクエストをカスタマーサポートに送信して、
[データ同期](#data-synchronization-data-synchronization)を有効にしてください。

### 外部 web アプリケーション {#external-managed-registration}

場合によっては、AEM 以外のインフラストラクチャで登録やユーザーの作成が既に行われています。このシナリオでは、ログイン時に AEM にユーザーレコードが作成されます。

## ログイン {#login}

エンドユーザーが AEM Publish サービスに登録されると、これらのユーザーは、ログインして認証済みアクセス（AEM 認証メカニズムを使用）および持続的なユーザー固有のデータ（プロファイルデータなど）を取得できます。

## 実装 {#implementation}

ログインは、次の 2 つの方法で実装できます。

### AEM 管理 {#aem-managed-implementation}

顧客は独自のカスタムコンポーネントを作成できます。詳しくは、以下を参照してください。

* [Sling 認証フレームワーク](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* あるいは、[AEM コミュニティエキスパートセッション](https://bit.ly/ATACEFeb15)にログインについて質問してみてください。

**前提条件：**

上記のロジックを正しく機能させるには、適切なプログラムと環境を示すリクエストをカスタマーサポートに送信して、
[データ同期](#data-synchronization-data-synchronization)を有効にしてください。

### ID プロバイダーとの統合 {#integration-with-an-idp}

顧客は、ユーザーを認証する IdP（ID プロバイダー）と統合できます。以下に示すように、統合テクノロジーには SAML および OAuth/SSO あどがあります。

**SAML ベース**

顧客は、好みの SAML IdP を使用して SAML ベースの認証を使用できます。AEM で IdP を使用する場合、SAML アサーションで説明されているように、IdP はエンドユーザーの資格情報の認証、ユーザー認証の AEM での転送、AEM でのユーザーレコードの作成（必要な場合）、および AEM でのユーザーグループのメンバーシップの管理を行います。

>[!NOTE]
>
>IdP では、ユーザーの資格情報の初期認証のみ行います。cookie が使用可能であれば、その後の AEM へのリクエストは AEM ログイントークン cookie を使用して実行されます。

[SAML 2.0 認証ハンドラー](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=ja)について詳しくは、ドキュメントを参照してください。

**OAuth/SSO**

AEM SSO 認証ハンドラーサービスの使用について詳しくは、[シングルサインオン（SSO）のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html?lang=ja)を参照してください。

`com.adobe.granite.auth.oauth.provider` インターフェイスは、任意の Oauth プロバイダーを使用して実装できます。

**前提条件：**

ベストプラクティスとして、ユーザー固有のデータを保存する際は、常に idP（ID プロバイダー）を唯一の信頼できる情報源として利用します。追加のユーザー情報が idP の一部ではないローカルリポジトリに保存されている場合は、適切なプログラムと環境を示すリクエストをカスタマーサポートに送信して、[データ同期](#data-synchronization-data-synchronization)を有効にしてください。[データ同期](#data-synchronization-data-synchronization)に加えて、SAML 認証プロバイダーの場合は、[動的グループメンバーシップ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)が有効になっていることを確認します。

### スティッキーセッションとカプセル化されたトークン {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service では cookie ベースのスティッキーセッションが有効になり、エンドユーザーがリクエストのたびに同じ公開ノードにルーティングされようにします。ユーザートラフィックのスパイクなどの特定のケースでは、カプセル化されたトークン機能によってパフォーマンスが向上する可能性があるので、リポジトリ内のユーザーレコードを各リクエストで参照する必要はありません。エンドユーザーに親和性のある公開ノードが置き換えられた場合、以下の[データ同期](#data-synchronization-data-synchronization)の節で説明するように、ユーザー ID レコードは新しい公開ノードで使用できます。

カプセル化されたトークン機能を活用するには、適切なプログラムと環境を示すリクエストをカスタマーサポートに送信してください。さらに重要なのは、カプセル化されたトークンは[データ同期](#data-synchronization-data-synchronization)しなければ有効にできず、一緒に有効にする必要があることです。したがって、有効にする前にユースケースを慎重に確認し、機能が不可欠であることを確認してください。

## ユーザープロファイル {#user-profile}

データを保存する方法は、データの性質に応じて様々です。

### AEM リポジトリー {#aem-repository}

ユーザープロファイル情報の書き込みと読み取りは、次の 2 つの方法で行うことができます。

* サーバーサイドで `com.adobe.granite.security.user` インターフェイスを使用。UserPropertiesManager インターフェイスにより、`/home/users` のユーザーのノードの下にデータが配置されます。ユーザーごとに一意のページが、キャッシュされていないことを確認します。
* [ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=ja#personalization)に説明されているように、クライアントサイドで ContextHub を使用。

**前提条件：**

サーバーサイドのユーザープロファイルの永続性ロジックを正しく機能させるには、適切なプログラムと環境を示すリクエストをカスタマーサポートに送信して、
[データ同期](#data-synchronization-data-synchronization)を有効にしてください。

### サードパーティのデータストア {#third-party-data-stores}

エンドユーザーデータは、CRM などのサードパーティベンダーに送信し、ユーザーが AEM にログインする時に API を介して取得できます。また、AEM ユーザーのプロファイルノードで保持（または更新）され、必要に応じて AEM で使用できます。

サードパーティのサービスにリアルタイムでアクセスしてプロファイル属性を取得することはできますが、これが実質的に AEM のリクエスト処理に影響を与えないようにすることが重要です。

**前提条件：**

上記のロジックを正しく機能させるには、適切なプログラムと環境を示すリクエストをカスタマーサポートに送信して、
[データ同期](#data-synchronization-data-synchronization)を有効にしてください。

## 権限（クローズドユーザーグループ） {#permissions-closed-user-groups}

Publish層のアクセスポリシー（クローズドユーザーグループ（CUG）とも呼ばれます）は、AEM オーサーで定義されます。[ クローズドユーザーグループの作成 ](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=ja#applying-your-closed-user-group-to-content-pages) を参照してください。 一部のユーザーから web サイトの特定のセクションまたはページを制限するには、ここで説明されているように AEM オーサーを使用して、必要に応じて CUG を適用し、パブリッシュ層に複製します。

* ユーザーが SAML を使用して ID プロバイダー（IdP）の認証でログインすると、認証ハンドラーはユーザーのグループメンバーシップ（パブリッシュ層の CUG と一致する必要がある）を識別し、リポジトリーレコードを介してユーザーとグループの関連付けを保持します。
* IdP 統合を使用せずにログインを完了した場合、カスタムコードは同じリポジトリー構造の関係を適用できます。

ログインとは別に、カスタムコードは、組織の固有の要件に応じて、ユーザーのグループメンバーシップを保持および管理することもできます。

## データ同期 {#data-synchronization}

Web サイトのエンドユーザーは、別のブラウザーを使用してログインした場合、知らないうちに、パブリッシュ層インフラストラクチャの異なるサーバーノードに接続されたとしても,すべての web ページリクエストで一貫したエクスペリエンスを期待しています。AEM as a Cloud Service は、`/home` フォルダー階層（ユーザープロファイル情報、グループメンバーシップなど）をパブリッシュ層のすべてのノード間で迅速に同期することでこれを実現します。

他の AEM ソリューションとは異なり、AEM as a Cloud Service でのユーザーとグループメンバーシップの同期では、ポイントツーポイントメッセージングアプローチを使用せず、ユーザーの設定を必要としない公開サブスクライブアプローチを実装します。

>[!NOTE]
>
>デフォルトでは、ユーザープロファイルとグループメンバーシップの同期は有効になっていないので、データはパブリッシュ層に同期されず、永続的に保持されることもありません。この機能を有効にするには、適切なプログラムと環境を示してカスタマーサポートにリクエストする必要があります。

>[!IMPORTANT]
>
>実稼動環境でデータ同期を有効にする前に、実装を大規模にテストします。ユースケースと永続化されるデータによっては、一貫性と待ち時間に関する問題が発生する可能性があります。

## キャッシュに関する考慮事項 {#cache-considerations}

認証済みの HTTP リクエストは、CDN とディスパッチャーの両方でキャッシュするのが困難な場合があります。これは、リクエストの応答の一部としてユーザー固有のステートが転送される可能性があるからです。認証済みのリクエストを誤ってキャッシュして他のリクエスト元のブラウザーに提供すると、誤ったエクスペリエンスが発生したり、保護されたリクエストやユーザーデータが漏洩したりする場合があります。

ユーザー固有の応答をサポートしながら、リクエストの高いキャッシュ機能を維持する方法には次のようなものがあります。

* AEM ディスパッチャー権限の機密性の高いキャッシュ
* Sling の動的インクルード
* AEM ContextHub
