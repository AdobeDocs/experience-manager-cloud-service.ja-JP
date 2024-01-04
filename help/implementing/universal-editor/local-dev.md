---
title: ユニバーサルエディターを使用したローカルAEM開発
description: 開発目的で、ユニバーサルエディターがローカルのAEMインスタンスでの編集をサポートする方法を説明します。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# ユニバーサルエディターを使用したローカルAEM開発 {#local-dev-ue}

開発目的で、ユニバーサルエディターがローカルのAEMインスタンスでの編集をサポートする方法を説明します。

{{universal-editor-status}}

## 概要 {#overview}

このドキュメントでは、ユニバーサルエディターを使用してAEM上でローカルに開発できるように、ユニバーサルエディターサービスのローカルコピーと共に HTTPS でAEMを実行する方法を説明します。

## HTTPS で実行するAEMを設定 {#aem-https}

HTTPS で保護された外側のフレーム内で、セキュリティで保護されていない HTTP フレームを読み込むことはできません。 ユニバーサルエディターサービスは HTTPS 上で実行されるので、AEMまたは他のリモートページも HTTPS 上で実行する必要があります。

これをおこなうには、HTTPS で実行するAEMを設定する必要があります。 開発目的で、自己署名証明書を使用できます。

HTTPS で実行するAEMを設定する方法（使用できる自己署名付き証明書を含む）については、このドキュメントを参照してください。

## Universal Editor Service のインストール {#install-ue-service}

ユニバーサルエディターサービスは、ユニバーサルエディターとバックエンドシステムを結び付けるものです。 公式の Universal Editor Service はグローバルにホストされているので、ローカルのAEMインスタンスはインターネットに公開する必要があります。 この問題を回避するには、Universal Editor Service のローカルコピーを実行します。

[NodeJS バージョン 16](https://nodejs.org/en/download/releases) Universal Editor Service のローカルコピーを実行するにはが必要です。

Universal Editor Service は、AEM Engineering によって直接配布されます。 ローカルコピーを入手するには、VIPプログラムのエンジニアにお問い合わせください。

エンジニアリングによって `universal-editor-service.cjs` ファイル。 これをローカル開発環境に保存します。

## HTTPS を使用して Universal Editor Service を実行するための証明書を作成する {#ue-https}

また、Universal Editor Service では、開発環境で HTTPS 上で実行する証明書も必要です。

次のコマンドを実行します。

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

このコマンドにより、 `key.pem` および `certificate.pem` ファイル。 これらのファイルを `universal-editor-service.cjs` ファイル。

## ユニバーサルエディターサービスの設定 {#setting-up-service}

Universal Editor Service をローカルで実行するには、NodeJS で多数の環境変数を設定する必要があります。

同じパス上に `universal-editor-service.cjs`, `key.pem` および `certificate.pem` ファイル、作成する `.env` ファイルの内容を次に示します。

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

変数の意味は次のとおりです。

* `EXPRESS_PORT`:Universal Editor Service がリッスンするポートを定義します。
* `EXPRESS_PRIVATE`：を指します。 [以前に作成した秘密鍵](#ue-https) `key.pem`
* `EXPRESS_CERT`：を指します。 [以前に作成した証明書](#ue-https) `certificate.pem`
* `NODE_TLS_REJECT_UNAUTHORIZED=0`：自己署名付き証明書を受け入れる

## Universal Editor サービスの実行 {#running-ue}

Universal Editor Service を開始するには、次のコマンドを実行します。

```text
$ node ./universal-editor-service.cjs
```

端末に次の内容を出力します。

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

サービスが HTTP サーバーではなく HTTPS サーバーを開始することを確認します。

## Global Service の代わりに Local Universal Editor Service を使用する {#using-local-ue}

ユニバーサルエディターは、ページが実装されている方法に基づいて、ページの編集に使用するユニバーサルエディターサービスを把握します。 これは、ユニバーサルエディターで読み込まれたページのメタタグを使用しておこなわれます。

ローカルのユニバーサルエディターサービスを使用してページを編集するには、次のメタタグを設定する必要があります。

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

設定が完了すると、コンテンツ更新呼び出しが次の場所に移動するのを確認できます。 `https://localhost:8000` デフォルトの Universal Editor Service の代わりにを使用します。

>[!TIP]
>
>グローバルユニバーサルエディターサービスを使用するためにページが実装される方法について詳しくは、このドキュメントを参照してください [AEMでのユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md#instrument-page)

## ローカルユニバーサルエディターサービスを使用したページの編集 {#editing}

を使用 [ローカルで実行されるユニバーサルエディターサービス](#running-ue) および [ローカルサービスを使用するために実装されたコンテンツページ](#using-loca-ue) これで、エディターを起動できます。

1. 次の場所にブラウザーを開きます。 `https://localhost:8000/`.
1. ブラウザーに同意を促す [自己署名証明書。](#ue-https)
1. 自己署名証明書が信頼されると、ローカルのユニバーサルエディターサービスを使用してページを編集できます。
