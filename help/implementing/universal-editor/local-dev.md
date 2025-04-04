---
title: 独自のユニバーサルエディターサービスの実行
description: ローカル開発用または独自のインフラストラクチャの一部として、独自のユニバーサルエディターサービスを実行する方法について説明します。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 300dc71969e8e1da32d4f86f0a987b7e2777ccf5
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 98%

---


# 独自のユニバーサルエディターサービスの実行 {#local-ue-service}

ローカル開発用または独自のインフラストラクチャの一部として、独自のユニバーサルエディターサービスを実行する方法について説明します。

>[!NOTE]
>
>Edge Delivery ServicesでAEMをオーサリングするプロジェクトでは、ローカルユニバーサルエディターサービスは必要ないか、サポートされていません。

## 概要 {#overview}

ユニバーサルエディターサービスは、ユニバーサルエディターとバックエンドシステムを結び付けるものです。ユニバーサルエディター用にローカルで開発できるようにするには、ユニバーサルエディターサービスのローカルコピーを実行する必要があります。理由は、次のとおりです。

* アドビ公式のユニバーサルエディターサービスはグローバルにホストされているので、ローカルの AEM インスタンスをインターネットに公開する必要があります。
* ローカルの AEM SDK を使用して開発している間は、アドビのユニバーサルエディターサービスにインターネットからアクセスできません。
* AEM インスタンスに IP 制限があり、アドビのユニバーサルエディターサービスが定義された IP 範囲にない場合は、自分でホストできます。

## ユースケース {#use-cases}

ユニバーサルエディターサービスの独自のコピーは、次の操作を行う場合に役立ちます。

* ユニバーサルエディターで使用するために AEM 上でローカルに開発。
* アドビのユニバーサルエディターサービスから独立して、独自のインフラストラクチャの一部として独自のユニバーサルエディターサービスを実行。

どちらのユースケースもサポートされています。このドキュメントでは、ユニバーサルエディターサービスのローカルコピーと共に HTTPS で AEM を実行する方法について説明します。

独自のインフラストラクチャの一部として独自のユニバーサルエディターサービスを実行する場合は、ローカル開発の例と同じ手順に従います。

## HTTPS で実行する AEM の設定 {#aem-https}

HTTPS で保護された外側のフレーム内で、保護されていない HTTP フレームを読み込むことはできません。ユニバーサルエディターサービスは HTTPS 上で実行し、AEM または他のリモートページも HTTPS 上で実行する必要があります。

これを行うには、HTTPS で実行する AEM を設定する必要があります。開発目的で、自己署名証明書を使用できます。

使用できる自己署名付き証明書を含め、HTTPS で実行する AEM を設定する方法について詳しくは、[このドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=ja)を参照してください。

## ユニバーサルエディターサービスのインストール {#install-ue-service}

ユニバーサルエディターサービスは、ユニバーサルエディターの完全なコピーではなく、ローカル AEM 環境からの呼び出しがインターネット経由ではなく、制御する定義済みのエンドポイントからルーティングされることを保証する機能のサブセットにすぎません。

ユニバーサルエディターサービスのローカルコピーを実行するには、[NodeJS バージョン 20](https://nodejs.org/en/download/releases) が必要です。

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
UES_PORT=8000
UES_PRIVATE_KEY=./key.pem
UES_CERT=./certificate.pem
UES_TLS_REJECT_UNAUTHORIZED=false
UES_CORS_PRIVATE_NETWORK=true
```

これらは、この例でのローカル開発に必要な最小値です。

>[!NOTE]
>
>Chrome バージョン 130 以降を実行している場合は、`UES_CORS_PRIVATE_NETWORK` オプションを使用して、[プライベートネットワークアクセス](https://wicg.github.io/private-network-access/#private-network-request)用の CORS ヘッダーの送信を有効にする必要があります。


これらと使用可能なその他の値の詳細を次の表に示します。

| 値 | オプション | デフォルト | 説明 |
|---|---|---|---|
| `UES_PORT` | あり | `8080` | サーバーが動作しているポート |
| `UES_PRIVATE_KEY` | あり | なし | HTTPS サーバーの秘密鍵のパス |
| `UES_CERT` | あり | なし | HTTPS サーバーの証明書ファイルのパス |
| `UES_TLS_REJECT_UNAUTHORIZED` | あり | `true` | 許可されていない TLS 接続を拒否します |
| `UES_DISABLE_IMS_VALIDATION` | あり | `false` | IMS 検証を無効にします |
| `UES_ENDPOINT_MAPPING` | あり | 空白 | 内部書き換え用のエンドポイントのマッピング<br>例：`UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>結果：ユニバーサルエディターサービスは、指定された接続 `https://your-public-facing-author-domain.net` ではなく `http://10.0.0.1:4502` に接続します |
| `UES_LOG_LEVEL` | あり | `info` | サーバーのログレベル。指定可能な値は、`silly`、`trace`、`debug`、`verbose`、`info`、`log`、`warn`、`error` および `fatal` です |
| `UES_SPLUNK_HEC_URL` | あり | なし | Splunk エンドポイントへの HEC URL |
| `UES_SPLUNK_TOKEN` | あり | なし | Splunk トークン |
| `UES_SPLUNK_INDEX` | あり | なし | ログを書き込むインデックス |
| `UES_SPLUNK_SOURCE` | あり | `universal-editor-service` | Splunk ログでのソースの名前 |
| `UES_CORS_PRIVATE_NETWORK` | あり | `false` | [プライベートネットワーク](https://wicg.github.io/private-network-access/#private-network-request)を許可するには、CORS ヘッダーの送信を有効にします。Chrome バージョン 130 以降のユーザーに必須です |

>[!NOTE]
>
>[2024.08.13 リリース](/help/release-notes/universal-editor/current.md)より前のユニバーサルエディターでは、`.env` ファイルに次の変数が必要でした。後方互換性を保つために、これらの値は 2024年10月1日（PT）までサポートされます。
>
>`EXPRESS_PORT=8000`
>`EXPRESS_PRIVATE_KEY=./key.pem`
>`EXPRESS_CERT=./certificate.pem`
>`NODE_TLS_REJECT_UNAUTHORIZED=0`

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

[ローカルで実行されるユニバーサルエディターサービス](#running-ue)と[ローカルサービスを使用するのに実装されたコンテンツページ](#using-loca-ue)を使用して、エディターを起動できるようになりました。

1. ブラウザーを `https://localhost:8000/ping` で開きます。
1. [自己署名証明書](#ue-https)に同意するようダイレクトされます。
1. 自己署名証明書が信頼されると、ローカルのユニバーサルエディターサービスを使用してページを編集できるようになります。

