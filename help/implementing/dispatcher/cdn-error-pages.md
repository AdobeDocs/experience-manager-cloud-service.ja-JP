---
title: CDN エラーページの設定
description: Amazon S3 や Azure Blob Storage などの自己ホスト型ストレージで静的ファイルをホストし、Cloud Manager 設定パイプラインを使用してデプロイされた設定ファイルで静的ファイルを参照することで、デフォルトのエラーページを上書きする方法について説明します。
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
source-git-commit: 395e2faa6cd2a3430ce00208a4d904fe8e0c2333
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 100%

---

# CDN エラーページの設定 {#cdn-error-pages}

万が一、[アドビが管理する CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) が AEM の接触チャネルに到達できない場合、CDN はデフォルトで、サーバーに到達できないことを示す、ブランド化されていない汎用のエラーページを表示します。Amazon S3 や Azure Blob Storage などの自己ホスト型ストレージで静的ファイルをホストし、[Cloud Manager 設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)を使用してデプロイされた設定ファイルで静的ファイルを参照することで、デフォルトのエラーページを上書きできます。

## 設定 {#setup}

デフォルトのエラーページを上書きする前に、次の作業を行う必要があります。

* Git プロジェクトの最上位フォルダーに次のフォルダーとファイル構造を作成します。

```
config/
     cdn.yaml
```

* `cdn.yaml` 設定ファイルには、メタデータと以下の例で説明するルールの両方を含める必要があります。`kind` パラメーターは `CDN` に設定し、バージョンはスキーマバージョン（現在 `1`）に設定する必要があります。

* Cloud Manager でターゲットデプロイメント設定パイプラインを作成します。[実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)および[実稼動以外のパイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)を参照してください。

**備考**

* RDE は現在、設定パイプラインをサポートしていません。
* `yq` を使用すると、設定ファイル（例：`yq cdn.yaml`）の YAML 形式をローカルで検証できます。

### 設定 {#configuration}

エラー ページはシングルページ アプリケーション（SPA）として実装され、以下の例に示すように、いくつかのプロパティを参照します。URL によって参照される静的ファイルは、Amazon S3 や Azure Blob Storage などのインターネットにアクセスできるサービス上でホストする必要があります。

設定例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  errorPages:
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

### サンプル生成 HTML {#sample-generated-html}

CDN によって生成され、ブラウザーなどのクライアントに提供される HTML コードは、次のスニペットに似ています（ただし、同一ではありません）。

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

テストの目的で、サポートされているエラーコードを使用して専用のエンドポイントを呼び出します。次に例を示します。

```
curl "https://publish-pXXXXX-eXXXXXX.adobeaemcloud.com/cdnstatus?code=403"
```

サポートされているコードは、403、404、406、500 および 503 です。

この方法で、CDN のエラーハンドラーを直接トリガーして、特定のエラーコードに対する合成応答をテストします。
