---
title: 配信 API
description: 配信 API の使用方法を説明します。
role: User
source-git-commit: 3e2fe458460fe8ec4c1dd12152c1134bfb9ca62b
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# 配信 API {#delivery-apis}

すべて [承認済みアセット](approve-assets.md) Experience Managerのアセットリポジトリで使用できるのは、次の場合です [検索対象](search-assets-api.md) その後、配信 URL を使用して、統合されたダウンストリームアプリケーションに配信されます。

バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに加えられた変更は、自動的に配信 URL に反映されます。 CDN を介したアセット配信に短期間有効（TTL）値の 10 分が設定されると、更新は、10 分以内にすべてのオーサリングインターフェイスおよび公開済みインターフェイスで表示されます。

次の画像は、使用可能な配信 URL を示しています。

![配信 API](assets/delivery-url.png)

次の表に、使用可能な様々な配信 API の使用方法を示します。

| 配信 API | 説明 |
|---|---|
| [リクエストされた出力形式でのアセットの web に最適化されたバイナリ表現](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetSeoFormat) | リクエストで送信されたアセット ID に基づいて、リクエストされた出力形式でのアセットの web に最適化されたバイナリ表現を返します。 さらに、幅、高さ、回転、反転、画質、切り抜き、形式、など、様々な画像修飾子を定義できます [スマート切り抜き](/help/assets/dynamic-media/image-profiles.md). を参照してください。 [API の詳細](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetSeoFormat) （サポートされる形式および画像修飾子）。<br>Adobeでは、すべての画像形式タイプに対してこの API を使用することをお勧めします。 |
| [アセットの web に最適化されたバイナリ表現](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAsset) | 応答で返されるアセットの web に最適化されたバイナリ表現にデフォルトで適用される便利な API。 デフォルトには、標準のJPEG/WEBP 形式、画質=> 65、幅=> 1024 が含まれます。 |
| [アセットのオリジナルのアップロード済みバイナリ](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetOriginal) | アセットに最初にアップロードされたバイナリを返します。 Adobeでは、ドキュメント形式タイプとSVG画像に、この API を使用することをお勧めします。 |
| [AEM Assets オーサリング環境で使用できる、アセットの事前生成レンディション](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetRendition) | リクエストで送信されたアセット ID とレンディション名に基づいて、AEM Assets オーサリング環境で使用可能なアセットレンディションのビットストリームを返します。 |
| [アセットメタデータ](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetMetadata) | タイトル、説明、CreateDate、ModifyDate など、アセットに関連付けられたプロパティを返します。 |
| [ビデオアセットのプレーヤーコンテナ](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/videoPlayerDelivery) | ビデオアセットのプレーヤーコンテナを返します。 Player を iframe HTML要素に埋め込んで、ビデオを再生できます。 |
| [再生マニフェストが選択した形式で表示されます](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/videoManifestDelivery) | 指定したビデオアセットの再生マニフェストファイルを、選択した出力形式で返します。 再生マニフェストファイルを取り込んでビデオを再生するには、HLS または DASH プロトコルによるアダプティブストリーミングが可能なカスタムプレーヤーを作成する必要があります。 |

## 配信 API エンドポイント {#delivery-apis-endpoint}

API エンドポイントは、配信 API ごとに異なります。 例えば、の API エンドポイントです `Web-optimized binary representation of the asset in the requested output format` API は次のとおりです。
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

配信ドメインは、Experience Managerオーサー環境のドメインと構造が似ています。 唯一の違いは用語を置き換えることです `author` （を使用） `delivery`.

`pXXXX` はプログラム ID を参照します

`eYYYY` は環境 ID を指します

参照： [API の詳細](https://adobe-aem-assets-delivery-experimental.redoc.ly/#tag/Assets) を参照してください。

## 配信 API リクエストメソッド {#delivery-api-request-method}

GET

## 配信 API ヘッダー {#deliver-assets-api-header}

Delivery API ヘッダーでヘッダーを定義する際には、次の詳細を指定する必要があります。

```java
headers: {
      'If-None-Match': 'string',
      Authorization: 'Bearer <YOUR_JWT_HERE>'
    }
```

配信 API を呼び出すには、に IMS トークンが必要です。 `Authorization` 制限されたアセットを配信するための詳細。 IMS トークンはテクニカルアカウントから取得されます。 参照： [AEM as a Cloud Service資格情報の取得](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) 新しいテクニカルアカウントを作成します。 参照： [アクセストークンの生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) ims トークンを生成して、配信 API リクエストヘッダーで適切に使用する。

要求サンプル、応答サンプルおよび応答コードを表示するには、次を参照してください [配信 API](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetSeoFormat).
