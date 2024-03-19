---
title: CDN エラーページの設定
description: デフォルトのエラーページを上書きする方法について説明します。静的ファイルをAmazon S3 や Azure Blob Storage などの自己ホストストレージにホストし、Cloud Manager 設定パイプラインを使用してデプロイされる設定ファイルで参照します。
feature: Dispatcher
source-git-commit: 11036c3e95f0444fc5d865232a7dccab5b7f26ae
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---


# CDN エラーページの設定 {#cdn-error-pages}

>[!NOTE]
>この機能は、まだ一般には利用できません。 早期採用プログラムに参加するには、E メールを送信します。 `aemcs-cdn-config-adopter@adobe.com` および使用例を説明します。

万が一 [Adobeが管理する CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) がAEMの接触チャネルに到達できない場合、デフォルトでは、CDN は、サーバーに到達できないことを示す、ブランド化されていない汎用エラーページを提供します。 デフォルトのエラーページを上書きするには、静的ファイルをAmazon S3 や Azure Blob Storage などの自己ホスト型ストレージにホストし、を使用してデプロイされる設定ファイルで参照します。 [Cloud Manager 設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline).

## 設定 {#setup}

デフォルトのエラーページを上書きする前に、次の作業を行う必要があります。

* まず、Git プロジェクトの最上位フォルダーに次のフォルダーとファイル構造を作成します。

```
config/
     cdn.yaml
```

* 次に、 `cdn.yaml` 設定ファイルには、以下に説明するように、メタデータとエラーページ参照を含める必要があります。

### 設定 {#configuration}

エラーページは単一ページアプリケーション (SPA) として実装され、次の例に示すように、いくつかのプロパティを参照します。  URL で参照される静的ファイルは、Amazon S3 や Azure Blob Storage などのインターネットアクセス可能なサービスでホストする必要があります。

設定例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```

| 名前 | 許可されたプロパティ | 意味 |
|-----------|--------------------------|-------------|
| **spa** | title | エラーページのタイトル。 |
|     | icoUrl | アイコンファイルの URL。 |
|     | cssUrl | CSS ファイルの URL。 |
|     | jsUrl | JavaScript ファイルの URL。 |

### サンプル生成HTML {#sample-generated-html}

CDN で生成され、ブラウザーなどのクライアントに提供されたHTMLコードは、次のスニペットに似ています（ただし、と同じではありません）。

```
<!DOCTYPE html>
<html lang="en">
    <head>
        ...
        <title>the error page</title>
        <link rel="icon" href="https://www.example.com/error.ico">
        <link rel="stylesheet" href="https://www.example.com/error.css">
    </head>
    <body>
        ...
        <div id="root" status="403"></div>
        <script src="https://www.example.com/error.js"> </script>
    </body>
</html>
```

### テスト {#testing}

テストの目的で、次の例のように、サポートされているエラーコードで専用のエンドポイントを呼び出します。

```
curl "https://publish-pXXXXX-eXXXXXX.adobeaemcloud.com/cdnstatus?code=403"
```

サポートされているコードは 403、404、406、500 および 503 です。

この方法で、CDN のエラーハンドラーを直接トリガーして、特定のエラーコードの合成応答をテストします。
