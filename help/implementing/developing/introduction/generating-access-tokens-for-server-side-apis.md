---
title: サーバー側APIのアクセストークンの生成
description: セキュアなJWTトークンを生成し、サードパーティのサーバーとAEM間のCloud Serviceを容易にする方法を学びます。
translation-type: tm+mt
source-git-commit: 9a4cb6d981fdf5eea4d1b9c7ae9e3c99947d9745
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---


# 概要 {#introduction}

>[!IMPORTANT]
>
>この機能はまだ使用できません。 最新の機能のリストについては、[リリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

一部のアーキテクチャは、AEMインフラストラクチャの外部のサーバにホストされるアプリケーションから、AEMへのCloud Serviceとしてのコールを行うことに依存しています。 例えば、サーバーを呼び出し、AEMにCloud ServiceとしてAPIリクエストを送信するモバイルアプリケーションです。

サーバー間のフローを以下に示し、開発のためのシンプルなフローを示します。 Cloud Service[Developer Console](development-guidelines.md#crxde-lite-and-developer-console)としてのAEMは、認証プロセスに必要なトークンの生成に使用されます。

## サーバ間のフロー{#the-server-to-server-flow}

管理者ロールを持つユーザーは、JWTベアラトークンを生成できます。JWTベアラトークンは、サーバーにインストールし、秘密キーとして慎重に扱う必要があります。 JWTベアラトークンは、IMSと交換して、AEMへの要求に含まれるアクセストークンをCloud Serviceとして取り替える必要があります。

サーバー間のフローは次の手順で行います。

* 開発者コンソールからJWTベアラートークンを生成します
* AEMに対して呼び出しを行うAEM以外のサーバーにトークンをインストールする
* AdobeのIMS APIを使用して、JWTベアラトークンをアクセストークンに交換する
* AEM APIの呼び出し

### JWTベアラトークンの生成{#generating-the-jwt-bearer-token}

組織の管理者ロールを持つユーザーには、特定の環境の開発者コンソールに、2つのボタンと共に「統合」タブが表示されます。 「**Get Service Credentials**」ボタンをクリックすると、秘密鍵、証明書、設定が生成されます。

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

### AEM以外のサーバーにトークンをインストールする{#install-the-token-on-a-non-aem-server}

AEMに対して呼び出しを行う非AEMアプリケーションでは、JWTベアラトークンをインストールし、それを秘密として扱う必要があります。

### JWTトークンをアクセストークン{#exchange-the-jwt-token-for-an-access-token}に交換する

AdobeのIMSサービスへの呼び出しにJWTトークンを含めて、アクセストークンを取得します。これは24時間有効です。

### AEM API {#calling-the-aem-api}を呼び出しています

アクセストークンを含め、AEMに対する適切なサーバー間API呼び出しをCloud Service環境として作成します。 したがって、&quot;Authorization&quot;ヘッダーには`"Bearer <access_token>"`の値を使用します。

<!-- ### Code Samples {#code-samples}

https://git.corp.adobe.com/boston/skyline-api-client-lib (internal note: URL will change to public git repo before we publish) contains client libraries written in node.js that will exchange the JSON outputted by the developer console for an access token. -->

## 開発者フロー{#developer-flow}

開発者は、Cloud Service開発環境として開発AEMに要求を行うAEM以外のアプリケーション（ラップトップ上で実行しているか、ホストされている）の開発インスタンスを使用してテストを行うと考えられます。 ただし、開発者は必ずしもAEMへの管理者ロールアクセス権をCloud Service開発環境として持っていないので、通常のサーバ間フローで記述されたJWTベアラを生成できるとは想定できません。 したがって、AEMへのリクエストで、開発者がアクセス権を持つCloud Service環境として使用できるアクセストークンを直接生成するメカニズムを提供する。 AEMをCloud Service開発者コンソールとして使用するために必要な権限については、[開発者ガイドラインドキュメント](/help/implementing/developing/introduction/development-guidelines.md)を参照してください。

>[!NOTE]
>
>トークンは24時間有効で、その後同じ方法で再生成する必要があります。

開発者は、このトークンを使用して、AEM以外のテストアプリケーションからAEMにCloud Service環境として呼び出しを行うことができます。 通常、開発者は、AEM以外のアプリケーションで、自分のノートブックPCにこのトークンを使用します。 また、クラウドとしてのAEMは、通常実稼働以外の環境です。

開発者のフローは次の手順で構成されます。

* Developer Consoleからのアクセストークンの生成
* アクセストークンでAEMアプリケーションを呼び出します。

また、開発者は、ローカルマシン上で実行しているAEMプロジェクトに対してAPI呼び出しを行うこともできます。この場合、アクセストークンは必要ありません。

### アクセストークンの生成{#generating-the-access-token}

アクセストークンを生成するには、Developer Consoleで「**Get Local Development Token**」ボタンをクリックします。

### アクセストークン{#call-the-aem-application-with-an-access-token}を使用して、次にAEMアプリケーションを呼び出す

Cloud Service環境として、AEM以外のアプリケーションからAEMに対する適切なサーバー間API呼び出しを行います。ヘッダーにアクセストークンを含めます。 したがって、&quot;Authorization&quot;ヘッダーには`"Bearer <access_token>"`の値を使用します。

## JWTベアラトークンの失効{#jwt-bearer-token-revocation}

JWTベアラトークンを取り消す必要がある場合は、カスタマーサポートにリクエストを送信してください。