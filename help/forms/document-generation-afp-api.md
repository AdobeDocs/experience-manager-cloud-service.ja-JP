---
title: AFP出力の同期APIを使用する方法？
description: AFP Output Sync APIを使用して、出力レンディションを取得および同期する方法を説明します。
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, User
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 5602fc63-ef74-44eb-b3be-61b8f8a2795a
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 14%

---

# AEM Forms API を使用した AFP 出力の生成

<span class="preview">これはプレリリース機能で、[プレリリースチャネル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features)を通してアクセスできます。</span>

Advanced Function Presentation （AFP）は、主に印刷目的で設計された高性能なドキュメント形式です。\
このガイドでは、AEM Formsを使用してAFP出力を生成するために必要なすべての手順と設定について説明します。

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
> * To enable AFP generation, the `FT_FORMS-17887` toggle configurations must be set in AEM configuration manager.
 -->

## AFP生成API

XDP テンプレートと入力データを使用して、AFP （Advanced Function Presentation）ファイルを生成します。

### 認証

ローカル環境には&#x200B;**BasicAuth** （管理者資格情報）を使用するか、AEM Cloud インスタンスには&#x200B;**OAuth サーバー間**&#x200B;認証を使用できます。

### リクエスト

**エンドポイント：**
[https://[publish-url].adobeaemcloud.com/adobe/forms/doc/v1/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post)

### ヘッダー

| キー | 値 |
| --------------- | ------------------------------------------------------ |
| `Content-Type` | `application/pdf` |
| `Authorization` | `(Bearer Access token)` |

### リクエスト本文

**Content-Type: multipart/form-data**

| キー | 型 | 必須 | 説明 |
| ---------- | ---- | -------- | ------------------------------------------------------------------------- |
| `template` | ファイル/テキスト | はい | AFP生成用のテンプレートとして使用されるXDP ファイル （例：`demo.xdp`） |
| `data` | ファイル/テキスト | いいえ | テンプレートと結合するデータファイル （XMLまたはJSON） （例：`data.xml`） |
| `options` | テキスト | いいえ | AFP出力（解像度、ロケールなど）を制御するためのオプションを含むJSON文字列 |

**例`options` JSON （テキストフィールド）:**

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
| `200` | 操作が成功しました。 AFP ドキュメントストリームを返します。 |
| `400` | 不正なリクエスト。 リクエストペイロードの形式が正しくないか、必須フィールドが見つかりません。 |
| `500` | 内部サーバーエラー。 しばらくしてからもう一度お試しください。 |

### Curl コマンド

```
curl --location 'http://<server>:<port>/adobe/forms/document/generate/afp' \
--header 'Authorization: Bearertoken <base64-encoded-credentials>' \
--form 'template=@"<path-to-template>.xdp"' \
--form 'data=@"<path-to-data-file>.xml"' \
--form 'options=<JSON-options-string>'
```

### APIのテスト

.yaml ファイルをダウンロードしてPostmanにアップロードし、APIの機能を確認できます。

![AFP Postman image](/help/forms/assets/afp-postman.png)

応答を保存し、保存したファイルをAFP リーダーで開いて表示できます。

![IC ドキュメントを検索](/help/forms/interactive-communication/assets/introimg.png)
