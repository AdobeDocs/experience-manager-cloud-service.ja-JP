---
title: '登録、ログイン、ユーザープロファイル '
description: 公開層での登録、ログイン、ユーザープロファイルについて説明します。
translation-type: tm+mt
source-git-commit: 2c00c3723c3c84365044b5cd2fe6779de0360736
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 1%

---


# 登録、ログイン、ユーザープロファイル{#registration-login-and-userprofile}

## 概要 {#introduction}

Web アプリケーションは、多くの場合、Webサイトへの登録用のアカウント管理機能を提供します。この機能は、ユーザープロファイル情報を保持し、将来ログインして一貫した操作を楽しむことができます。 この記事では、以下について説明します。

* 登録
* ログイン
* ユーザープロファイルデータの保存
* グループのメンバーシップ
* Data Synchronization

>[!IMPORTANT]
>
>この記事で説明する機能を動作させるには、ユーザーデータ同期機能を有効にする必要があります。この機能を有効にするには、該当するプログラムと環境を示すカスタマーサポートの要請が必要です。 有効にしない場合、ユーザー情報は短い期間（1 ～ 24時間）のみ保持され、表示されなくなります。

## 登録 {#registration}

エンドユーザーがAEMアプリケーションのアカウントに登録すると、JCRリポジトリの`/home/users`下のユーザーリソースに反映され、AEM Publishサービスにユーザーアカウントが作成されます。

以下に示すように、登録を実装するには2つの方法があります。

### AEM管理{#aem-managed-registration}

カスタム登録コードは、エンドユーザーのユーザー名とパスワードを最小限にして受け取り、AEMでユーザーレコードを作成し、ログイン時の認証に使用できるように記述できます。 通常、この登録メカニズムの構築には次の手順を使用します。

1. 登録情報を収集するカスタムAEMコンポーネントの表示
1. 送信時に、適切にプロビジョニングされたサービスユーザーが
   1. UserManager APIの`findAuthorizables()`メソッドの1つを使用して、既存のユーザーが存在しないことを確認します
   1. UserManager APIの`createUser()`メソッドの1つを使用してユーザーレコードを作成する
   1. Authorizableインターフェイスの`setProperty()`メソッドを使用してキャプチャされたプロファイルデータを永続化します
1. ユーザーに電子メールの検証を求めるなど、オプションのフローです。

### 外部 Web アプリケーション {#external-managed-registration}

場合によっては、AEM以外のインフラストラクチャで登録やユーザー作成が行われていました。 このシナリオでは、ログイン時にAEMにユーザーレコードが作成されます。

## ログイン {#login}

エンドユーザーがAEM発行サービスに登録されると、これらのユーザーはログインして認証済みアクセス(AEM認証メカニズムを使用)および持続的なユーザー固有のデータ(プロファイルデータなど)を取得できます。

## 実装 {#implementation}

ログインは、次の2つの方法で実装できます。

### AEM管理{#aem-managed-implementation}

お客様は独自のカスタムコンポーネントを作成できます。 詳しくは、次の事項に関する知識を身に付けてください。

* [Sling認証フレームワーク](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* [AEMコミュニティエキスパートセッション](http://bit.ly/ATACEFeb15)にログインについて尋ねることを検討します。

### IDプロバイダーとの統合{#integration-with-an-idp}

ユーザーは、ユーザーを認証するIdP（IDプロバイダー）と統合できます。 以下に示すように、統合テクノロジーにはSAMLおよびOAuth/SSOが含まれます。

**SAMLベース**

お客様は、希望するSAML IdPを使用してSAMLベースの認証を使用できます。 AEMでIdPを使用する場合、IdPは、エンドユーザーの資格情報を認証し、ユーザーの認証をAEMで転送し、必要に応じてAEMでユーザーレコードを作成し、SAMLアサーションの説明に従って、AEMでユーザーのグループメンバーシップを管理します。

>[!NOTE]
>
>IdPでは、ユーザーの資格情報の初期認証のみが認証され、cookieが使用できる限り、AEMへの以降のリクエストはAEMログイントークンcookieを使用して実行されます。

[SAML 2.0認証ハンドラー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=en#saml-authentication-handler)について詳しくは、ドキュメントを参照してください。

**OAuth/SSO**

AEM SSO認証ハンドラーサービスの使用について詳しくは、[シングルサインオン(SSO)のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html)を参照してください。

`com.adobe.granite.auth.oauth.provider`インターフェイスは、任意のOAuthプロバイダーを使用して実装できます。

### スティッキーセッションとカプセル化されたトークン{#sticky-sessions-and-encapsulated-tokens}

AEMをCloud Serviceとして使用する場合、cookieベースのスティッキーセッションが有効になっており、エンドユーザーはリクエストのたびに同じ発行ノードにルーティングされます。 パフォーマンスを向上させるために、カプセル化トークン機能はデフォルトで有効になっているので、リポジトリ内のユーザーレコードを各リクエストで参照する必要はありません。 エンドユーザが置き換えるアフィニティがある発行ノードは、以下のデータ同期の節で説明するように、新しい発行ノードでユーザIDレコードを使用できます。

## ユーザープロファイル {#user-profile}

データの性質に応じて、データを保存する方法は様々です。

### AEMリポジトリ{#aem-repository}

ユーザープロファイル情報の書き込みと読み取りは、次の2つの方法で行うことができます。

* `com.adobe.granite.security.user`インターフェイスUserPropertiesManagerインターフェイスでのサーバー側の使用。これにより、`/home/users`のユーザーのノードの下にデータが配置されます。 ユーザーごとに一意のページがキャッシュされていないことを確認します。
* [ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization)の説明に従い、ContextHubを使用するクライアント側。

### サードパーティのデータストア{#third-party-data-stores}

エンドユーザーデータは、CRMなどのサードパーティベンダーに送信し、ユーザーのAEMへのログイン時にAPIを介して取得し、AEMユーザーのプロファイルノードで保持（または更新）し、必要に応じてAEMで使用できます。

サードパーティのサービスにリアルタイムでアクセスしてプロファイル属性を取得できますが、AEMでは、これが実質的にリクエスト処理に影響を与えないようにすることが重要です。

## 権限（閉じたユーザーグループ） {#permissions-closed-user-groups}

公開層アクセスポリシー(Closed User Groups(CUG)とも呼ばれます)は、AEM作成者では[ここ](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages)で説明されているとおりに定義されています。 一部のユーザーからWebサイトの特定のセクションまたはページを制限するには、ここで説明するAEMの作成者を使用して、必要に応じてCUGを適用し、公開層に複製します。

* ユーザーがSAMLを使用してIDプロバイダー(IdP)との認証でログインすると、認証ハンドラーはユーザーのグループメンバーシップ（発行層のCUGと一致する必要がある）を識別し、リポジトリレコードを介してユーザーとグループの関連付けを保持します
* IdP統合を使用せずにログインを完了した場合、カスタムコードは同じリポジトリ構造の関係を適用できます。

ログインとは別に、カスタムコードは、組織の固有の要件に応じて、ユーザーのグループメンバーシップを保持および管理することもできます。

## Data Synchronization {#data-synchronization}

Webサイトのエンドユーザーは、各Webページリクエストに対して、または別のブラウザーを使用してログインした場合でも、公開層インフラストラクチャの異なるサーバーノードに一貫した操作を行うことを期待します。 AEM asCloud Serviceは、これを実現するために、`/home`フォルダーの階層(ユーザープロファイル情報、グループのメンバーシップなど)を、発行層のすべてのノード間で迅速に同期します。

他のAEMソリューションとは異なり、Cloud ServiceとしてのAEMでのユーザーとグループのメンバーシップの同期では、ポイントツーポイントメッセージングアプローチを使用せず、ユーザーの設定を必要としない公開サブスクライブアプローチを実装します。

>[!NOTE]
>
>デフォルトでは、ユーザープロファイルとグループメンバーシップの同期は有効になっていないので、データは発行層に同期されず、または永続的に保持されません。 この機能を有効にするには、適切なプログラムと環境を示すリクエストをカスタマーサポートに送信します。

## キャッシュの考慮事項{#cache-considerations}

認証済みのHTTPリクエストは、CDNとディスパッチャーの両方でキャッシュするのが困難な場合があります。これは、リクエストの応答の一部としてユーザー固有の状態が転送される可能性があるからです。 認証済みの要求を誤ってキャッシュし、要求を他の要求元のブラウザーに提供すると、誤ったエクスペリエンスが発生したり、保護された要求やユーザーデータが漏洩したりする場合があります。

ユーザー固有の応答をサポートしながら、リクエストの高いキャッシュ機能を維持する方法を次に示します。

* AEMディスパッチャー権限の機密性の高いキャッシュ
* Sling動的インクルード
* AEM ContextHub