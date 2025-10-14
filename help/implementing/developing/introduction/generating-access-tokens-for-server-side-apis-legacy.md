---
title: サーバーサイド API のアクセストークンの生成（レガシー）
description: セキュアな JWT トークンを生成してサードパーティサーバーと AEM as a Cloud Service の間の通信を容易にする方法について説明します。
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 22216d2c045b79b7da13f09ecbe1d56a91f604df
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 95%

---

# サーバーサイド API のアクセストークンの生成（レガシー） {#generating-access-tokens-for-server-side-apis-legacy}

一部のアーキテクチャでは、AEM インフラストラクチャの外部にあるサーバーにホストされているアプリケーションから AEM as a Cloud Service への呼び出しの実行がベースになっています。例えば、モバイルアプリケーションがサーバーを呼び出し、その後、サーバーが AEM as a Cloud Service に対して API リクエストを行います。

サーバー間フローと簡略化した開発フローを以下に示します。認証プロセスに必要なトークンの生成には、AEM as a Cloud Service [開発者コンソール](development-guidelines.md#crxde-lite-and-developer-console)を使用します。

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=ja#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## サーバー間フロー {#the-server-to-server-flow}

IMS 組織管理者の役割を持ち、AEM オーサー上の「AEM ユーザー」または「AEM 管理者」製品プロファイルのメンバーでもあるユーザーは、AEM as a Cloud Service 資格情報を生成できます。その資格情報は後で、AEM as a Cloud Service 環境管理者の役割を持つユーザーに取得され、サーバーにインストールされることになるので、秘密鍵として慎重に取り扱う必要があります。この JSON 形式のファイルには、AEM as a Cloud Service API との統合に必要なすべてのデータが含まれています。このデータを使用して署名済み JWT トークンが作成され、IMS との間で IMS アクセストークンと交換されます。その後、このアクセストークンをベアラー認証トークンとして使用して、AEM as a Cloud Service にリクエストを行うことができます。資格情報はデフォルトで 1 年後に期限切れになりますが、必要に応じて更新できます。[資格情報の更新](#refresh-credentials)を参照してください。

サーバー間フローは次のステップで構成されます。

* Developer Console から AEM as a Cloud Service の資格情報を取得する
* AEM を呼び出す AEM 以外のサーバーに AEM as a Cloud Service の資格情報をインストールする
* JWT トークンを生成し、そのトークンをアドビの IMS API を使用してアクセストークンと交換する
* アクセストークンをベアラー認証トークンに使用して AEM API を呼び出す
* AEM 環境のテクニカルアカウントユーザーに適切な権限を設定する

### AEM as a Cloud Service 資格情報の取得 {#fetch-the-aem-as-a-cloud-service-credentials}

AEM as a Cloud Service の Developer Console にアクセスできるユーザーには、特定の環境の Developer Console の統合タブと 2 つのボタンが表示されます。AEM as a Cloud Service 環境管理者の役割を持つユーザーは、「**サービス資格情報を生成**」ボタンをクリックして、サービス資格情報の JSON を生成して表示できます。JSON には、選択したポッドにかかわらず、環境のオーサー層とパブリッシュ層用のクライアント ID、クライアント秘密鍵、秘密鍵、証明書、設定を含む、AEM 以外のサーバーに必要なすべての情報が含まれています。

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

生成後、同じ場所の「**サービス資格情報を取得**」ボタンをクリックすることで、後で、資格情報を取得することができます。

>[!IMPORTANT]
>
>IMS 組織管理者（通常は Cloud Manager 経由で環境をプロビジョニングしたユーザー）は、AEM オーサーの AEM ユーザーまたは AEM 管理者の製品プロファイルのメンバーでもある必要があり、Developer Console にアクセスします。次に、「**サービス資格情報を生成**」ボタンをクリックする必要があります。これにより、資格情報が生成され、後で AEM as a Cloud Service 環境への管理者権限を持つユーザーによって取得されます。IMS 組織管理者がこのタスクを実行していない場合は、IMS 組織管理者の役割が必要であることを通知するメッセージが表示されます。

### AEM サーバー以外での AEM サービス資格情報のインストール {#install-the-aem-service-credentials-on-a-non-aem-server}

AEM に対して呼び出しを行う AEM 以外のアプリケーションは、AEM as a Cloud Service 資格情報にアクセスしてそれをシークレットとして扱える必要があります。

### JWT トークンを生成してアクセストークンと交換する {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

資格情報を使用して、Adobe IMS サービスへの呼び出しで JWT トークンを作成し、24 時間有効なアクセストークンを取得します。

AEM CS サービス資格情報は、この目的で設計されたコードサンプルを使用して、アクセストークンと交換できます。 サンプルコードは [Adobeの公開 GitHub リポジトリ &#x200B;](https://github.com/adobe/aemcs-api-client-lib) から入手可能です。このリポジトリには、独自のプロジェクトに合わせてコピーおよび調整できるコード例が含まれています。 このリポジトリには、参照用のサンプルコードが含まれており、実稼動用のライブラリ依存関係として維持されているわけではありません。

```
/*jshint node:true */
"use strict";

const fs = require('fs');
// Sample code adapted from Adobe's GitHub repository
const exchange = require("./your-local-aemcs-client"); // Copy and adapt the code from the GitHub repository

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

アクセストークンは有効期限を定義します（通常は 24 時間）。Git リポジトリには、アクセストークンを管理して期限切れの前に更新するサンプルコードが含まれています。

### AEM API の呼び出し {#calling-the-aem-api}

ヘッダーにアクセストークンを含めて、AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。例えば、`curl` を使用して次のように呼び出します。

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### AEM のテクニカルアカウントユーザーに対する適切な権限の設定 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

テクニカルアカウントユーザーが AEM に作成されたら（これは、対応するアクセストークンを含んだ初回リクエストの後で行われます）、AEM **内の**&#x200B;適切な権限をテクニカルアカウントユーザーに付与する必要があります。

デフォルトでは、テクニカルアカウントユーザーは AEM オーサーサービスで投稿者ユーザーグループに追加されます。このグループは AEM への読み取りアクセスが可能です。

AEM のこのテクニカルアカウントユーザーには、通常の方法を使用して、さらに権限を付与することができます。

## 開発者フロー {#developer-flow}

開発者は、AEM as a Cloud Service 開発環境に対してリクエストを行う AEM 以外のアプリケーションの開発インスタンス（ラップトップ上で動作するか他でホストされている）を使用してテストを行う必要があります。ただし、開発者は必ずしも IMS 管理者役割の権限を持ってはいないので、アドビは通常のサーバー間フローで説明されている JWT ベアラーを開発者が生成できるとは想定できません。したがって、アドビは、開発者がアクセスできる AEM as a Cloud Service 環境へのリクエストで使用できるアクセストークンを直接生成するメカニズムを提供します。

AEM as a Cloud Service 開発者コンソールの使用に必要な権限については、[開発者ガイドラインドキュメント](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)を参照してください。

>[!NOTE]
>
>ローカル開発アクセストークンは最大 24 時間有効で、その後は同じ方法で再生成する必要があります。

開発者は、このトークンを使用して AEM 以外のテストアプリケーションから AEM as a Cloud Service 環境に呼び出しを行うことができます。一般的に、開発者は自分のノート PC で動作する AEM 以外のアプリケーションでこのトークンを使用します。また、AEM as a Cloud Service は通常、非実稼働環境です。

開発者フローは次のステップで構成されます。

* 開発者コンソールからアクセストークンを生成する
* そのアクセストークンを指定して AEM アプリケーションを呼び出す

また、開発者は、ローカルマシン上で動作している AEM プロジェクトに対して API 呼び出しを行うこともできます。この場合、アクセストークンは不要です。

### アクセストークンの生成 {#generating-the-access-token}

アクセストークンを生成するには、Developer Console で、「**ローカル開発トークンを取得**」をクリックします。

### アクセストークンを指定した AEM アプリケーションの呼び出し {#call-the-aem-application-with-an-access-token}

ヘッダーにアクセストークンを含めて、AEM 以外のアプリケーションから AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。

## 資格情報の更新 {#refresh-credentials}

デフォルトでは、AEM as a Cloud Service の資格情報は 1 年後に期限切れになります。サービスの継続性を確保するために、開発者は資格情報を更新して、利用期間をさらに 1 年間延長することができます。以下に示すように、Developer Console の「**統合**」タブから&#x200B;**サービス資格情報を更新**&#x200B;を使用します。

![資格情報の更新](assets/credential-refresh.png)

ボタンをクリックすると、新しい資格情報セットが生成されます。新しい資格情報でシークレットストレージを更新し、新しい資格情報が正常に機能していることを検証できます。

>[!NOTE]
>
> 「**サービス資格情報を更新**」ボタンをクリックしても、古い資格情報は期限が切れるまで登録されたままになりますが、開発者コンソールには常に最新のセットのみ表示されます。

## サービス資格情報の失効 {#service-credentials-revocation}

資格情報を取り消す必要がある場合は、次の手順に従って、カスタマーサポートにリクエストを送信する必要があります。

1. ユーザーインターフェイスで Adobe Admin Console のテクニカルアカウントユーザーを無効にします。
   * Cloud Manager で、環境の横にある **...** ボタンをクリックします。このアクションにより、製品プロファイルページが開きます
   * **AEM ユーザー**&#x200B;プロファイルをクリックして、ユーザーのリストを表示します。
   * 「**API 資格情報**」タブをクリックし、該当するテクニカルアカウントユーザーを探して削除します。
2. カスタマーサポートに連絡し、その特定の環境のサービス資格情報を削除するようにリクエストします。
3. 最後に、このドキュメントの説明に従って、資格情報を再生成します。また、作成した新しいテクニカルアカウントユーザーに適切な権限があることも確認してください。
