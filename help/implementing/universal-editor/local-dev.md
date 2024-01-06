---
title: ユニバーサルエディターを使用したローカル AEM 開発
description: ユニバーサルエディターが開発目的でローカルの AEM インスタンスでの編集に対応する方法を説明します。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 94%

---


# ユニバーサルエディターを使用したローカル AEM 開発 {#local-dev-ue}

ユニバーサルエディターが開発目的でローカルの AEM インスタンスでの編集に対応する方法を説明します。

{{universal-editor-status}}

## 概要 {#overview}

このドキュメントでは、ユニバーサルエディターを使用してAEM上でローカルに開発できるように、ユニバーサルエディターサービスのローカルコピーと共に HTTPS でAEMを実行する方法を説明します。

## HTTPS で実行する AEM の設定 {#aem-https}

HTTPS で保護された外側のフレーム内で、保護されていない HTTP フレームを読み込むことはできません。ユニバーサルエディターサービスは HTTPS 上で実行し、AEM または他のリモートページも HTTPS 上で実行する必要があります。

これを行うには、HTTPS で実行する AEM を設定する必要があります。開発目的で、自己署名証明書を使用できます。

使用できる自己署名付き証明書を含め、HTTPS で実行する AEM を設定する方法については、このドキュメントを参照してください。

## ユニバーサルエディターサービスのインストール {#install-ue-service}

ユニバーサルエディターサービスは、ユニバーサルエディターとバックエンドシステムを結び付けるものです。公式のユニバーサルエディターサービスはグローバルにホストされているので、ローカルの AEM インスタンスはインターネットに公開する必要があります。これを回避するには、ユニバーサルエディターサービスのローカルコピーを実行します。

そのためには、[NodeJS バージョン 16](https://nodejs.org/en/download/releases) が必要です。

ユニバーサルエディターサービスは、AEM Engineering によって直接配布されます。ローカルコピーを入手するには、VIP プログラムのエンジニアにお問い合わせください。

Engineering から `universal-editor-service.cjs` ファイルが提供されますので、ローカルの開発環境に保存してください。

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

>[!TIP]
>
>グローバルユニバーサルエディターサービスを使用するためのページの実装方法について詳しくは、[AEM でのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md#instrument-page)を参照してください。

## ローカルユニバーサルエディターサービスを使用したページの編集 {#editing}

[ローカルで実行されるユニバーサルエディターサービス](#running-ue)と[ローカルサービスを使用するために実装されたコンテンツページ](#using-loca-ue)を使用して、エディターを起動できるようになりました。

1. ブラウザーを `https://localhost:8000/` で開きます。
1. [自己署名証明書](#ue-https)に同意するようダイレクトされます。
1. 自己署名証明書が信頼されると、ローカルのユニバーサルエディターサービスを使用してページを編集できるようになります。
