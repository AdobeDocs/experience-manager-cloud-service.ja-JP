---
title: AFP 出力同期 API の使い方
description: AFP Output Sync API を使用して出力レンディションを取得し、同期する方法を説明します。
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, User
exl-id: 5602fc63-ef74-44eb-b3be-61b8f8a2795a
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 14%

---

# AEM Forms API を使用した AFP 出力の生成

<span class="preview">これはプレリリース機能で、[プレリリースチャネル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features)を通してアクセスできます。</span>

AFP （Advanced Function Presentation）は、主に印刷用に設計された高性能なドキュメント形式です。\
このガイドでは、AEM Formsを使用して AFP 出力を生成するために必要なすべての手順と設定の概要を説明します。

<!--
## Prerequisites

To support AFP output generation, the following OSGi bundles must be present and in an **active** state:

* **AFP Core Bundle** – Available in the AFP repository
* **Forms Output Core** – Found in the Forms Output comments package
* **Bedrock Connector** – Provided by the Forms Output API
* **Cloud Ready Implementation** – Available through the Forms installer

>[!NOTE]
>
> * If any bundle is inactive, resolve dependency issues or reinstall manually.
> * To enable AFP generation, the `FT_FORMS-17887` toggle configurations must be set in AEM configuration manager.-->

## AFP 生成 API

XDP テンプレートと入力データを使用して、AFP （Advanced Function Presentation）ファイルを生成します

### 認証

ローカル環境の場合は **BasicAuth** （管理者資格情報）を、AEM Cloud インスタンスの場合は **BearerAuth** 認証を使用できます。

### リクエスト

**エンドポイント：**
`POST http://<server>:<port>/adobe/forms/document/generate/afp`

### ヘッダー

| キー | 値 |
| --------------- | ------------------------------------------------------ |
| `Content-Type` | `application/pdf` |
| `Authorization` | `(Bearer Access token)` |

### リクエスト本文

**Content-Type: multipart/form-data**

| キー | 型 | 必須 | 説明 |
| ---------- | ---- | -------- | ------------------------------------------------------------------------- |
| `template` | ファイル/テキスト | はい | AFP 生成のテンプレートとして使用される XDP ファイル（例：`demo.xdp`） |
| `data` | ファイル/テキスト | いいえ | テンプレートと結合するデータファイル （XML または JSON） （例：`data.xml`） |
| `options` | テキスト | いいえ | AFP 出力を制御するオプションを含む JSON 文字列（解像度、ロケールなど） |

**例 `options` JSON （テキストフィールド）:**

```json
{
  "pdfVersion": "1.7",
  "resolution": 300,
  "locale": "en-US",
  "embedFonts": true,
  "contentRoot": "/usr/tmp"
}
```

### 応答

| コード | 説明 |
| ----- | ------------------------------------------------------------------------- |
| `200` | 操作に成功しました。 AFP ドキュメント ストリームを返します。 |
| `400` | リクエストが正しくありません。 リクエストペイロードの形式が正しくないか、必須フィールドがありません。 |
| `500` | 内部サーバーエラー。 しばらくしてからもう一度やり直してください。 |

### Curl コマンド

```
curl --location 'http://<server>:<port>/adobe/forms/document/generate/afp' \
--header 'Authorization: Bearertoken <base64-encoded-credentials>' \
--form 'template=@"<path-to-template>.xdp"' \
--form 'data=@"<path-to-data-file>.xml"' \
--form 'options=<JSON-options-string>'
```

### API のテスト

.yaml ファイルをダウンロードし、Postmanにアップロードして API の機能を確認できます。

![AFPPostman画像 ](/help/forms/assets/afp-postman.png)

AFP リーダーで応答を保存し、保存したファイルを開いて確認できます。

![PDF リーダー ](/help/forms/assets/afp-pdf.png)
