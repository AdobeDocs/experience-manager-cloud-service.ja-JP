---
title: サーバー側APIのアクセストークンの生成
description: セキュアなJWTトークンを生成し、サードパーティのサーバーとAEM間のCloud Serviceを容易にする方法を学びます。
translation-type: tm+mt
source-git-commit: 41b4bb3a63089c05750a40e910ee7578727d8b15
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 0%

---


# 概要 {#introduction}

一部のアーキテクチャは、AEMインフラストラクチャの外部のサーバにホストされるアプリケーションから、AEMへのCloud Serviceとしてのコールを行うことに依存しています。 例えば、サーバーを呼び出し、AEMにCloud ServiceとしてAPIリクエストを送信するモバイルアプリケーションです。

サーバー間のフローを以下に示し、開発のためのシンプルなフローを示します。 Cloud Service[Developer Console](development-guidelines.md#crxde-lite-and-developer-console)としてのAEMは、認証プロセスに必要なトークンの生成に使用されます。

>[!NOTE]
>
>このドキュメントに加えて、[AEM用のトークンベースの認証(Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)として)に関するチュートリアルも参照できます。

## サーバ間のフロー{#the-server-to-server-flow}

IMS組織管理者の役割を持つユーザーは、AEM資格情報をCloud Service資格情報として生成できます。この資格情報は、AEMをCloud Service環境管理者の役割として持つユーザーが取得でき、サーバーにインストールする必要があり、秘密キーとして慎重に扱う必要があります。 このJSON形式のファイルには、AEMとの統合に必要なCloud ServiceAPIとしてのすべてのデータが含まれています。 データは、署名付きJWTトークンの作成に使用され、IMSアクセストークンと交換されます。 その後、このアクセストークンをベアラ認証トークンとして使用し、AEMにCloud Serviceとしてリクエストを行うことができます。

サーバー間のフローは次の手順で行います。

* 開発者コンソールからAEMをCloud Service資格情報として取得する
* AEMに対して呼び出しを行う非AEMサーバー上に、Cloud Service資格情報としてAEMをインストールします
* JWTトークンを生成し、AdobeのIMS APIを使用してアクセストークンとそのトークンを交換する
* アクセストークンをベアラ認証トークンとして使用してAEM APIを呼び出す
* AEM環境で、テクニカルアカウントユーザーに適切な権限を設定します

### AEMをCloud Service資格情報として取得{#fetch-the-aem-as-a-cloud-service-credentials}

Cloud Service開発者コンソールとしてAEMにアクセスできるユーザーには、特定の環境用の「統合」タブと2つのボタンがDeveloper Consoleに表示されます。 AEMをCloud Service環境管理者ロールとして持つユーザーは、「**サービス資格情報を取得**」ボタンをクリックして、サービス資格情報を表示できます。jsonには、ポッドの選択に関係なく、AEM以外の環境の作成者層と公開層の設定が含まれます。

![JWT生成](assets/JWTtoken3.png)

出力結果は次のようになります。

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

>[!IMPORTANT]
>
>IMS組織管理者(通常、Cloud Managerを介して環境をプロビジョニングした同じユーザー)は、まずデベロッパーコンソールにアクセスし、「**サービス資格情報を取得**」ボタンをクリックして、Cloud Service環境としてAEMに資格情報を生成し、後で取得します。 IMS組織管理者がこの操作を行っていない場合は、IMS組織管理者の役割が必要であることを通知するメッセージが表示されます。

### AEMサービス資格情報をAEM以外のサーバーにインストールする{#install-the-aem-service-credentials-on-a-non-aem-server}

AEMに対して呼び出しを行うAEM以外のアプリケーションは、AEMにCloud Service資格情報としてアクセスでき、暗号鍵として扱う必要があります。

### JWTトークンを生成し、アクセストークンと交換する{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

AdobeのIMSサービスへの呼び出しで秘密鍵証明書を使用してJWTトークンを作成し、アクセストークンを取得します。この認証は24時間有効です。

AEM CSサービスの資格情報は、この目的で設計されたクライアントライブラリを使用して、アクセストークンと交換できます。 クライアントライブラリは、[AdobeのパブリックGitHubリポジトリ](https://github.com/adobe/aemcs-api-client-lib)から入手できます。このリポジトリには、より詳細なガイダンスと最新の情報が含まれています。

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

同じ交換は、正しい形式で署名済みJWTトークンを生成し、IMS Token Exchange APIを呼び出すことのできる任意の言語で実行できます。

アクセストークンは、有効期限を定義します（通常は24時間）。 gitリポジトリには、アクセストークンを管理し、期限が切れる前に更新するためのサンプルコードがあります。

### AEM API {#calling-the-aem-api}を呼び出しています

アクセストークンを含め、AEMに対する適切なサーバー間API呼び出しをCloud Service環境として作成します。 したがって、&quot;Authorization&quot;ヘッダーには`"Bearer <access_token>"`の値を使用します。 例えば、`curl`を使用します。

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}のテクニカルアカウントユーザーに適切な権限を設定します

テクニカルアカウントユーザがAEMで作成されたら(これは、対応するアクセストークンを持つ最初のリクエストの後に発生します)、テクニカルアカウントユーザは&#x200B;**AEMで適切に権限**&#x200B;を付与される必要があります。

デフォルトでは、AEM Authorサービスでは、技術アカウントユーザーが読み取りアクセスを提供するContributorsユーザーグループに追加されます。

AEMのこのテクニカルアカウントユーザーは、通常の方法を使用して、権限を付与することができます。

## 開発者フロー{#developer-flow}

開発者は、Cloud Service開発環境として開発AEMに要求を行うAEM以外のアプリケーション（ラップトップ上で実行しているか、ホストされている）の開発インスタンスを使用してテストを行うと考えられます。 ただし、開発者は必ずしもIMS管理ロールの権限を持っていないので、通常のサーバー間フローで説明されているJWTベアラーを生成できるとは想定できません。 したがって、AEMへのリクエストで、開発者がアクセス権を持つCloud Service環境として使用できるアクセストークンを直接生成するメカニズムを提供する。

AEMをCloud Service開発者コンソールとして使用するために必要な権限については、[開発者ガイドラインドキュメント](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)を参照してください。

>[!NOTE]
>
>ローカル開発アクセストークンは、最大24時間有効です。その後、同じ方法で再生成する必要があります。

開発者は、このトークンを使用して、AEM以外のテストアプリケーションからAEMにCloud Service環境として呼び出しを行うことができます。 通常、開発者は、AEM以外のアプリケーションで、自分のノートブックPCにこのトークンを使用します。 また、クラウドとしてのAEMは、通常実稼働以外の環境です。

開発者のフローは次の手順で構成されます。

* Developer Consoleからのアクセストークンの生成
* アクセストークンでAEMアプリケーションを呼び出します。

また、開発者は、ローカルマシン上で実行しているAEMプロジェクトに対してAPI呼び出しを行うこともできます。この場合、アクセストークンは必要ありません。

### アクセストークンの生成{#generating-the-access-token}

アクセストークンを生成するには、Developer Consoleで「**Get Local Development Token**」ボタンをクリックします。

### アクセストークン{#call-the-aem-application-with-an-access-token}を使用して、次にAEMアプリケーションを呼び出す

Cloud Service環境として、AEM以外のアプリケーションからAEMに対する適切なサーバー間API呼び出しを行います。ヘッダーにアクセストークンを含めます。 したがって、&quot;Authorization&quot;ヘッダーには`"Bearer <access_token>"`の値を使用します。

## サービス資格情報の失効{#service-credentials-revocation}

資格情報を取り消す必要がある場合は、次の手順に従って、カスタマーサポートにリクエストを送信する必要があります。

1. ユーザーインターフェイスでAdobe Admin Consoleのテクニカルアカウントユーザーを無効にします。
   * Cloud Managerで、**...**&#x200B;ボタンをクリックします。 これにより、製品のプロファイルページが開きます
   * 次に、**AEM Users**&#x200B;プロファイルをクリックして、ユーザーのリストを表示します
   * 「**API Credentials**」タブをクリックし、適切なテクニカルアカウントユーザーを探して削除します
2. カスタマーサポートに連絡し、特定の環境のサービス資格情報の削除をリクエストします
3. 最後に、このドキュメントで説明されているとおり、秘密鍵証明書を再び生成できます。 また、作成した新しいテクニカルアカウントユーザーに適切な権限があることも確認してください。