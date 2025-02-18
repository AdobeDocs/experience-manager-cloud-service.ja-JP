---
title: CDN エラーページの設定
description: Amazon S3 や Azure Blob Storage などの自己ホスト型ストレージで静的ファイルをホストし、Cloud Manager 設定パイプラインを使用してデプロイされた設定ファイルで静的ファイルを参照することで、デフォルトのエラーページを上書きする方法について説明します。
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '388'
ht-degree: 100%

---


# CDN エラーページの設定 {#cdn-error-pages}

万が一、[アドビが管理する CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) が AEM の接触チャネルに到達できない場合、CDN はデフォルトで、サーバーに到達できないことを示す、ブランド化されていない汎用のエラーページを表示します。Amazon S3 や Azure Blob Storage などの自己ホスト型ストレージで静的ファイルをホストし、Cloud Manager [設定パイプライン](/help/operations/config-pipeline.md#managing-in-cloud-manager)を使用してデプロイされた設定ファイルで静的ファイルを参照することで、デフォルトのエラーページを上書きできます。

## 設定 {#setup}

デフォルトのエラーページを上書きする前に、次の作業を行う必要があります。

1. 以下の構文の節を参照して、`cdn.yaml` または類似の名前のファイルを作成します。

1. [設定パイプラインの使用](/help/operations/config-pipeline.md#folder-structure)で説明されているように、*config* または類似の名前の最上位フォルダーの下のどこかにファイルを配置します。

1. [設定パイプラインの使用](/help/operations/config-pipeline.md#managing-in-cloud-manager)の説明に従って、Cloud Manager で設定パイプラインを作成します。

1. 設定をデプロイします。

### 構文 {#syntax}

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
データノード上のプロパティの説明について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md#common-syntax)を参照してください。kind プロパティの値は *CDN* に設定し、`version` プロパティは *1* に設定する必要があります。


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

### チュートリアル

CDN で提供されるエラーページの作成、デプロイ、テストの手順について詳しくは、[CDN エラーページ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/content-delivery/custom-error-pages#cdn-error-pages)チュートリアルを参照してください。


