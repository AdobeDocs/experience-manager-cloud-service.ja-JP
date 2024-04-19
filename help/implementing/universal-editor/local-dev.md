---
title: ユニバーサルエディターを使用したローカル AEM 開発
description: ユニバーサルエディターが開発目的でローカルの AEM インスタンスでの編集に対応する方法を説明します。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: 11a244b7dd4810fbfec92b3effc362102e7322dc
workflow-type: ht
source-wordcount: '698'
ht-degree: 100%

---


# ユニバーサルエディターを使用したローカル AEM 開発 {#local-dev-ue}

ユニバーサルエディターが開発目的でローカルの AEM インスタンスでの編集に対応する方法を説明します。

## 概要 {#overview}

ユニバーサルエディターサービスは、ユニバーサルエディターとバックエンドシステムを結び付けるものです。ユニバーサルエディター用にローカルで開発できるようにするには、ユニバーサルエディターサービスのローカルコピーを実行する必要があります。理由は、次のとおりです。

* アドビ公式のユニバーサルエディターサービスはグローバルにホストされているので、ローカルの AEM インスタンスをインターネットに公開する必要があります。
* ローカルの AEM SDK を使用して開発している間は、アドビのユニバーサルエディターサービスにインターネットからアクセスできません。
* AEM インスタンスに IP 制限があり、アドビのユニバーサルエディターサービスが定義された IP 範囲にない場合は、自分でホストできます。

このドキュメントでは、ユニバーサルエディターを使用して AEM でローカルに開発を行えるよう、ユニバーサルエディターサービスのローカルコピーと共に HTTPS で AEM を実行する方法について説明します。

## HTTPS で実行する AEM の設定 {#aem-https}

HTTPS で保護された外側のフレーム内で、保護されていない HTTP フレームを読み込むことはできません。ユニバーサルエディターサービスは HTTPS 上で実行し、AEM または他のリモートページも HTTPS 上で実行する必要があります。

これを行うには、HTTPS で実行する AEM を設定する必要があります。開発目的で、自己署名証明書を使用できます。

使用できる自己署名付き証明書を含め、HTTPS で実行する AEM を設定する方法について詳しくは、[このドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=ja)を参照してください。

## ユニバーサルエディターサービスのインストール {#install-ue-service}

ユニバーサルエディターサービスは、ユニバーサルエディターの完全なコピーではなく、ローカル AEM 環境からの呼び出しがインターネット経由ではなく、制御する定義済みのエンドポイントからルーティングされることを保証する機能のサブセットにすぎません。

ユニバーサルエディターサービスのローカルコピーを実行するには、[NodeJS バージョン 16](https://nodejs.org/en/download/releases) が必要です。

ユニバーサルエディターサービスは、ソフトウェア配布から使用できます。アクセス方法について詳しくは、[ソフトウェア配布のドキュメント](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)を参照してください。

`universal-editor-service.cjs` ファイルをソフトウェア配布からローカル開発環境に保存します。

## HTTPS を使用してユニバーサルエディターサービスを実行するための証明書の作成 {#ue-https}

ユニバーサルエディターサービスでは、開発環境の HTTPS で実行する証明書も必要です。

次のコマンドを実行します。

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

このコマンドにより、`key.pem` および `certificate.pem` ファイルが生成されます。これらのファイルを `universal-editor-service.cjs` ファイルと同じパスに保存します。

## ユニバーサルエディターサービスの設定 {#setting-up-service}

ユニバーサルエディターサービスをローカルで実行するには、NodeJS で多数の環境変数を設定する必要があります。

`universal-editor-service.cjs`、`key.pem` および `certificate.pem` ファイルと同じパス上に、次のコンテンツが含まれる `.env` ファイルを作成します。

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

変数の意味は次のとおりです。

* `EXPRESS_PORT`：ユニバーサルエディターサービスがリッスンするポートを定義します
* `EXPRESS_PRIVATE`：[以前に作成した秘密鍵](#ue-https) `key.pem` を指し示します。
* `EXPRESS_CERT`：[以前に作成した証明書](#ue-https) `certificate.pem` を指し示します。
* `NODE_TLS_REJECT_UNAUTHORIZED=0`：自己署名付き証明書を受け取ります

## ユニバーサルエディターサービスの実行 {#running-ue}

ユニバーサルエディターサービスを開始するには、次のコマンドを実行します。

```text
$ node ./universal-editor-service.cjs
```

ターミナルに次の内容が出力されます。

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

サービスが HTTP サーバーではなく HTTPS サーバーを開始することを確認します。

## （グローバルサービスではなく）ローカルのユニバーサルエディターサービスの使用 {#using-local-ue}

ユニバーサルエディターは、ページが実装されている方法に基づいて、ページの編集に使用するユニバーサルエディターサービスを認識します。この処理は、ユニバーサルエディターで読み込まれたページのメタタグを使用して行われます。

ローカルのユニバーサルエディターサービスを使用してページを編集するには、次のメタタグを設定する必要があります。

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

設定が完了すると、コンテンツ更新呼び出しがデフォルトのデフォルトのではなく、`https://localhost:8000` に移動するのを確認できます。

>[!NOTE]
>
>`https://localhost:8000` に直接アクセスしようとすると、`404` エラーが発生します。これは予期された動作です。
>
>ローカルのユニバーサルエディターサービスへのアクセスをテストするには、`https://localhost:8000/corslib/LATEST` を使用します。詳しくは、[次の節](#editing)を参照してください。

>[!TIP]
>
>グローバルユニバーサルエディターサービスを使用するためのページの実装方法について詳しくは、[AEM でのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md#instrument-page)を参照してください。

## ローカルユニバーサルエディターサービスを使用したページの編集 {#editing}

[ローカルで実行されるユニバーサルエディターサービス](#running-ue)と[ローカルサービスを使用するために実装されたコンテンツページ](#using-loca-ue)を使用して、エディターを起動できるようになりました。

1. ブラウザーを `https://localhost:8000/corslib/LATEST` で開きます。
1. [自己署名証明書](#ue-https)に同意するようダイレクトされます。
1. 自己署名証明書が信頼されると、ローカルのユニバーサルエディターサービスを使用してページを編集できるようになります。

