---
title: サーバー側 API のアクセストークンの生成
description: セキュアな JWT トークンを生成してサードパーティサーバーと AEM as a Cloud Service の間の通信を容易にする方法について説明します。
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: fc49b004a61d5f981ac61cca684dc0bacf843443
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 75%

---

# はじめに {#introduction}

一部のアーキテクチャでは、AEM インフラストラクチャの外部にあるサーバーにホストされているアプリケーションから AEM as a Cloud Service への呼び出しの実行がベースになっています。例えば、モバイルアプリケーションがサーバーを呼び出し、その後、サーバーが AEM as a Cloud Service に対して API リクエストを行います。

サーバー間フローと簡略化した開発フローを以下に示します。認証プロセスに必要なトークンの生成には、AEM as a Cloud Service [開発者コンソール](development-guidelines.md#crxde-lite-and-developer-console)を使用します。

>[!NOTE]
>
>このドキュメントに加えて、 [AEMas a Cloud Service用のトークンベース認証](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=ja#authentication) および [統合用のログイントークンの取得](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html).

## サーバー間フロー {#the-server-to-server-flow}

IMS 組織管理者の役割を持ち、AEM オーサー上の「AEM ユーザー」または「AEM 管理者」製品プロファイルのメンバーでもあるユーザーは、AEM as a Cloud Service 資格情報を生成できます。その資格情報は後で、AEM as a Cloud Service 環境管理者の役割を持つユーザーに取得され、サーバーにインストールされることになるので、秘密鍵として慎重に取り扱う必要があります。この JSON 形式のファイルには、AEM as a Cloud Service API との統合に必要なすべてのデータが含まれています。このデータを使用して署名済み JWT トークンが作成され、IMS との間で IMS アクセストークンと交換されます。その後、このアクセストークンをベアラー認証トークンとして使用して、AEM as a Cloud Service にリクエストを行うことができます。資格情報はデフォルトで 1 年後に期限切れになりますが、説明に従って、必要に応じて更新できます [ここ](#refresh-credentials).

サーバー間フローは次のステップで構成されます。

* 開発者コンソールから AEM as a Cloud Service 資格情報を取得する
* AEM に対して呼び出しを行う AEM 以外のサーバーに AEM as a Cloud Service 資格情報をインストールする
* JWT トークンを生成し、そのトークンをアドビの IMS API を使用してアクセストークンと交換する
* アクセストークンをベアラー認証トークンに使用して AEM API を呼び出す
* AEM 環境のテクニカルアカウントユーザーに適切な権限を設定する

### AEM as a Cloud Service 資格情報の取得 {#fetch-the-aem-as-a-cloud-service-credentials}

AEM as a Cloud Service 開発者コンソールにアクセスできるユーザーには、特定の環境用の「統合」タブのほか、2 つのボタンが開発者コンソールに表示されます。AEMas a Cloud Service環境管理者の役割を持つユーザーは、 **サービス資格情報の生成** ポッドの選択に関係なく、環境のオーサー層とパブリッシュ層のクライアント id、クライアントの秘密鍵、秘密鍵、証明書、設定など、AEM以外のサーバーに必要なすべての情報が含まれる、サービス資格情報 json を生成して表示するボタン。

![JWT の生成](assets/JWTtoken3.png)

出力は次のようになります。

```
{
  "ok": true,
  "integration": {
    "imsEndpoint": "ims-na1.adobelogin.com",
    "metascopes": "ent_aem_cloud_sdk,ent_cloudmgr_sdk",
    "technicalAccount": {
      "clientId": "cm-p123-e1234",
      "clientSecret": "4AREDACTED17"
    },
    "email": "abcd@techacct.adobe.com",
    "id": "ABCDAE10A495E8C@techacct.adobe.com",
    "org": "1234@AdobeOrg",
    "privateKey": "-----BEGIN RSA PRIVATE KEY-----\r\REDACTED\r\n==\r\n-----END RSA PRIVATE KEY-----\r\n",
    "publicKey": "-----BEGIN CERTIFICATE-----\r\nREDACTED\r\n-----END CERTIFICATE-----\r\n"
  },
  "statusCode": 200
}
```

生成後、 **サービス資格情報の取得** ボタンを同じ場所に配置します。

>[!IMPORTANT]
>
>AEM オーサーインスタンスのAEMユーザーまたはAEM管理者製品プロファイルのメンバーでもある IMS 組織管理者（通常は Cloud Manager を使用して環境をプロビジョニングした同じユーザー）は、最初に開発者コンソールにアクセスし、 **サービス資格情報の生成** ボタンを使用して、資格情報を生成し、AEMas a Cloud Service環境に対する管理者権限を持つユーザーが後で取得することができます。 IMS 組織管理者がこの操作をまだ行っていない場合は、IMS 組織管理者のロールが必要であることを通知するメッセージが表示されます。

### AEM 以外のサーバーへの AEM サービス資格情報のインストール {#install-the-aem-service-credentials-on-a-non-aem-server}

AEM に対して呼び出しを行う AEM 以外のアプリケーションは、AEM as a Cloud Service 資格情報にアクセスしてそれをシークレットとして扱える必要があります。

### JWT トークンの生成とアクセストークンとの交換  {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

アクセストークンを取得するには、アドビの IMS サービスへの呼び出しで資格情報を使用して JWT トークンを作成します。このトークンは 24 時間有効です。

AEM CS サービス資格情報は、専用のクライアントライブラリを使用して、アクセストークンと交換できます。このクライアントライブラリは、[アドビが公開している GitHub リポジトリー](https://github.com/adobe/aemcs-api-client-lib)から入手可能です。このリポジトリーには、より詳細なガイダンスと最新の情報が含まれています。

```
/*jshint node:true */
"use strict";

const fs = require('fs');
const exchange = require("@adobe/aemcs-api-client-lib");

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

同じ交換は、正しい形式の署名済み JWT トークンの生成と IMS トークン交換 API の呼び出しが可能な任意の言語で実行できます。

アクセストークンには有効期限が定義されます（通常は 24 時間です）。Git リポジトリーには、アクセストークンを管理して期限切れの前に更新するサンプルコードが含まれています。

### AEM API の呼び出し {#calling-the-aem-api}

ヘッダーにアクセストークンを含めて、AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。例えば、`curl` を使用して次のように呼び出します。

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### AEM のテクニカルアカウントユーザーに対する適切な権限の設定 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

テクニカルアカウントユーザーが AEM に作成されたら（これは、対応するアクセストークンを含んだ初回リクエストの後で行われます）、AEM **内の**&#x200B;適切な権限がテクニカルアカウントユーザーに付与される必要があります。

デフォルトでは、テクニカルアカウントユーザーは AEM オーサーサービスで寄稿者ユーザーグループに追加されます。このグループは AEM への読み取りアクセスが可能です。

AEMのこのテクニカルアカウントユーザーは、通常の方法を使用して、権限を使用してさらにプロビジョニングできます。

## 開発者フロー {#developer-flow}

開発者は、AEM as a Cloud Service 開発環境に対してリクエストを行う AEM 以外のアプリケーションの開発インスタンス（ラップトップ上で動作するか他でホストされている）を使用してテストを行うことになります。ただし、開発者は必ずしも IMS 管理者ロールの権限を持ってはいないので、通常のサーバー間フローで説明されている JWT ベアラーを開発者が生成できるとは想定できません。したがって、アクセスできる AEM as a Cloud Service 環境へのリクエストで使用できるアクセストークンを開発者が直接生成するメカニズムが用意されています。

AEM as a Cloud Service 開発者コンソールの使用に必要な権限については、[開発者ガイドラインドキュメント](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)を参照してください。

>[!NOTE]
>
>ローカル開発アクセストークンは最大 24 時間有効で、その後は同じ方法で再生成する必要があります。

開発者は、このトークンを使用して AEM 以外のテストアプリケーションから AEM as a Cloud Service 環境に呼び出しを行うことができます。通常、開発者は自分のノート PC で動作する AEM 以外のアプリケーションでこのトークンを使用します。また、AEM as a Cloud Service は通常、非実稼働環境です。

開発者フローは次のステップで構成されます。

* 開発者コンソールからアクセストークンを生成する
* そのアクセストークンを指定して AEM アプリケーションを呼び出す

また、開発者は、ローカルマシン上で動作している AEM プロジェクトに対して API 呼び出しを行うこともできます。この場合、アクセストークンは不要です。

### アクセストークンの生成 {#generating-the-access-token}

アクセストークンを生成するには、開発者コンソールで「**ローカル開発トークンを取得**」ボタンをクリックします。

### アクセストークンを指定した AEM アプリケーションの呼び出し {#call-the-aem-application-with-an-access-token}

ヘッダーにアクセストークンを含めて、AEM 以外のアプリケーションから AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。

## 資格情報を更新 {#refresh-credentials}

デフォルトでは、AEMのas a Cloud Service資格情報は 1 年後に期限切れになります。 サービスの継続性を確保するために、開発者は資格情報を更新し、1 年間使用可能な限りを延長するオプションが用意されています。

これを実現するには、 **サービス資格情報の更新** ボタン **統合** 」タブを使用します。

![資格情報の更新](assets/credential-refresh.png)

ボタンを押すと、新しい資格情報のセットが生成されます。 新しい資格情報でシークレットストレージを更新し、正しく機能していることを検証できます。

>[!NOTE]
>
> 次の **サービス資格情報の更新** 」ボタンをクリックすると、古い資格情報は期限が切れるまで登録されたままになりますが、開発者コンソールからは常に最新のセットのみが表示されます。

## サービス資格情報の失効 {#service-credentials-revocation}

資格情報を取り消す必要がある場合は、次の手順に従って、カスタマーサポートにリクエストを送信する必要があります。

1. ユーザーインターフェイスで Adobe Admin Console のテクニカルアカウントユーザーを無効にします。
   * Cloud Manager で、環境の横にある **...** ボタンをクリックします。製品プロファイルページが開きます。
   * **AEM ユーザー**&#x200B;プロファイルをクリックして、ユーザーのリストを表示します。
   * 「**API 資格情報**」タブをクリックし、該当するテクニカルアカウントユーザーを探して削除します。
2. カスタマーサポートに連絡し、その特定の環境のサービス資格情報を削除するようにリクエストします。
3. 最後に、このドキュメントの説明に従って、資格情報を再生成します。また、作成した新しいテクニカルアカウントユーザーに適切な権限があることも確認してください。
