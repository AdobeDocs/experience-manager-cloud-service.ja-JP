---
title: サーバー側 API（レガシー）用のアクセストークンの生成
description: セキュアな JWT トークンを生成することで、サードパーティサーバーとAEMas a Cloud Serviceの間の通信を容易にする方法を説明します
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 55%

---

# サーバー側 API（レガシー）用のアクセストークンの生成 {#generating-access-tokens-for-server-side-apis-legacy}

一部のアーキテクチャでは、AEM インフラストラクチャの外部にあるサーバーにホストされているアプリケーションから AEM as a Cloud Service への呼び出しの実行がベースになっています。例えば、モバイルアプリケーションがサーバーを呼び出し、その後、サーバーが AEM as a Cloud Service に対して API リクエストを行います。

サーバー間フローと簡略化した開発フローを以下に示します。認証プロセスに必要なトークンの生成には、AEM as a Cloud Service [開発者コンソール](development-guidelines.md#crxde-lite-and-developer-console)を使用します。

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## サーバー間フロー {#the-server-to-server-flow}

IMS 組織管理者の役割を持ち、AEM オーサー上の「AEM ユーザー」または「AEM 管理者」製品プロファイルのメンバーでもあるユーザーは、AEM as a Cloud Service 資格情報を生成できます。この資格情報は、後でAEMas a Cloud Serviceの環境管理者の役割を持つユーザーが取得でき、サーバーにインストールする必要があり、秘密鍵として慎重に扱う必要があります。 この JSON 形式のファイルには、AEM as a Cloud Service API との統合に必要なすべてのデータが含まれています。このデータを使用して署名済み JWT トークンが作成され、IMS との間で IMS アクセストークンと交換されます。その後、このアクセストークンをベアラー認証トークンとして使用して、AEM as a Cloud Service にリクエストを行うことができます。資格情報はデフォルトで 1 年後に期限切れになりますが、[ここ](#refresh-credentials)の説明に従って、必要に応じて更新することができます。

サーバー間フローは次のステップで構成されます。

* 開発者コンソールからAEMas a Cloud Serviceの資格情報を取得します
* AEMを呼び出すAEM以外のサーバーに、AEMas a Cloud Serviceの資格情報をインストールします
* JWT トークンを生成し、そのトークンをアドビの IMS API を使用してアクセストークンと交換する
* アクセストークンをベアラー認証トークンに使用して AEM API を呼び出す
* AEM 環境のテクニカルアカウントユーザーに適切な権限を設定する

### AEM as a Cloud Service 資格情報の取得 {#fetch-the-aem-as-a-cloud-service-credentials}

AEM as a Cloud Service開発者コンソールへのアクセス権を持つユーザーは、特定の環境の開発者コンソールに「統合」タブと 2 つのボタンが表示されます。 AEMas a Cloud Service環境管理者の役割を持つユーザーは、 **サービス資格情報の生成** ボタンを使用して、サービス資格情報 json を生成して表示します。 JSON には、ポッドの選択に関係なく、環境のオーサー層とパブリッシュ層向けのクライアント ID、クライアントの秘密鍵、秘密鍵、証明書、設定など、AEM以外のサーバーに必要なすべての情報が含まれています。

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

認証情報は、生成後に **サービス資格情報の取得** ボタンを同じ場所に配置します。

>[!IMPORTANT]
>
>IMS 組織管理者（通常は Cloud Manager を通じて環境をプロビジョニングしたユーザー）。このユーザーは、AEM オーサー上のAEMユーザーまたはAEM管理者製品プロファイルのメンバーでもある必要があります。 次に、 **サービス資格情報の生成** ボタンを使用して、資格情報が生成され、AEM as a Cloud Service環境の管理者権限を持つユーザーが取得されるようにします。 IMS 組織管理者がこのタスクをまだ実行していない場合は、IMS 組織管理者の役割が必要であることを示すメッセージが表示されます。

### AEMサービス資格情報をAEM以外のサーバーにインストールする {#install-the-aem-service-credentials-on-a-non-aem-server}

AEMを呼び出すAEM以外のアプリケーションは、AEM as a Cloud Serviceの資格情報にアクセスして、秘密として扱うことができます。

### JWT トークンの生成とアクセストークンとの交換  {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

資格情報を使用して、Adobeの IMS サービスへの呼び出しで JWT トークンを作成し、24 時間有効なアクセストークンを取得します。

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

アクセストークンは、有効期限を定義します（通常は 24 時間）。 Git リポジトリーには、アクセストークンを管理して期限切れの前に更新するサンプルコードが含まれています。

### AEM API の呼び出し {#calling-the-aem-api}

ヘッダーにアクセストークンを含めて、AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。例えば、`curl` を使用して次のように呼び出します。

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### AEM のテクニカルアカウントユーザーに対する適切な権限の設定 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

テクニカルアカウントユーザーがAEMで作成された後（対応するアクセストークンを持つ最初のリクエストの後に発生）、テクニカルアカウントユーザーは適切に権限を付与される必要があります **in** AEM.

デフォルトでは、AEM オーサーサービスでは、テクニカルアカウントユーザーは、読み取りアクセスを提供するAEM Contributors ユーザーグループに追加されます。

AEM のこのテクニカルアカウントユーザーには、通常の方法を使用して、さらに権限を付与することができます。

## 開発者フロー {#developer-flow}

開発者は、開発AEM as a Cloud Service開発環境にリクエストを送信するAEM以外のアプリケーション（ノート PC で実行するか、ホストされている）の開発インスタンスを使用してテストする必要があります。 ただし、開発者には必ずしも IMS 管理者ロールの権限がないので、Adobeは、通常のサーバー間フローで説明される JWT ベアラーを生成できるとは想定できません。 したがって、Adobeは、開発者がアクセス権を持つAEMas a Cloud Service環境へのリクエストで使用できるアクセストークンを直接生成するメカニズムを提供します。

AEM as a Cloud Service 開発者コンソールの使用に必要な権限については、[開発者ガイドラインドキュメント](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)を参照してください。

>[!NOTE]
ローカル開発アクセストークンは最大 24 時間有効で、その後は同じ方法で再生成する必要があります。

開発者は、このトークンを使用して AEM 以外のテストアプリケーションから AEM as a Cloud Service 環境に呼び出しを行うことができます。通常、開発者は、このトークンを、自分のノート PC 上の非AEMアプリケーションで使用します。 また、AEM as a Cloud Service は通常、非実稼働環境です。

開発者フローは次のステップで構成されます。

* 開発者コンソールからアクセストークンを生成する
* そのアクセストークンを指定して AEM アプリケーションを呼び出す

また、開発者は、ローカルマシン上で動作している AEM プロジェクトに対して API 呼び出しを行うこともできます。この場合、アクセストークンは不要です。

### アクセストークンの生成 {#generating-the-access-token}

アクセストークンを生成するには、開発者コンソールで、 **ローカル開発トークンを取得**.

### アクセストークンを指定した AEM アプリケーションの呼び出し {#call-the-aem-application-with-an-access-token}

ヘッダーにアクセストークンを含めて、AEM 以外のアプリケーションから AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。

## 資格情報の更新 {#refresh-credentials}

デフォルトでは、AEMas a Cloud Serviceの資格情報は 1 年後に期限切れになります。 サービスの継続性を確保するために、開発者は資格情報を更新して、利用期間をさらに 1 年間延長することができます。用途 **サービス資格情報の更新** から **統合** 」タブを使用します。

![資格情報の更新](assets/credential-refresh.png)

ボタンをクリックすると、新しい資格情報セットが生成されます。新しい資格情報でシークレットストレージを更新し、新しい資格情報が正常に機能していることを検証できます。

>[!NOTE]
「**サービス資格情報を更新**」ボタンをクリックしても、古い資格情報は期限が切れるまで登録されたままになりますが、開発者コンソールには常に最新のセットのみ表示されます。

## サービス資格情報の失効 {#service-credentials-revocation}

資格情報を取り消す必要がある場合は、次の手順でカスタマーサポートにリクエストを送信する必要があります。

1. ユーザーインターフェイスで Adobe Admin Console のテクニカルアカウントユーザーを無効にします。
   * Cloud Manager で、環境の横にある **...** ボタンをクリックします。このアクションにより、製品プロファイルページが開きます
   * 次に、 **AEM Users** プロファイル（ユーザーのリストを表示）
   * 「**API 資格情報**」タブをクリックし、該当するテクニカルアカウントユーザーを探して削除します。
2. カスタマーサポートに連絡し、その特定の環境のサービス資格情報を削除するようにリクエストします。
3. 最後に、このドキュメントの説明に従って、資格情報を再生成します。また、作成した新しいテクニカルアカウントユーザーに適切な権限があることも確認してください。
