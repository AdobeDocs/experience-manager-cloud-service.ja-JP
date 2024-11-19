---
title: 配信 API
description: 配信 API の使用方法を説明します。
role: User
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 3%

---

# 配信 API {#delivery-apis}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Managerアセットリポジトリで使用可能なすべての [ 承認済みアセット ](approve-assets.md) は、配信 URL を使用して [ 検索 ](search-assets-api.md) 後、統合されたダウンストリームアプリケーションに配信できます。

バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに加えられた変更は、自動的に配信 URL に反映されます。 CDN を介したアセット配信に短期間有効（TTL）値の 10 分が設定されると、更新は、10 分以内にすべてのオーサリングインターフェイスおよび公開済みインターフェイスで表示されます。

次の画像は、使用可能な配信 URL を示しています。

![ 配信 API](assets/delivery-url.png)

次の表に、使用可能な様々な配信 API の使用方法を示します。

| 配信 API | 説明 |
|---|---|
| [ リクエストされた出力形式でのアセットの web に最適化されたバイナリ表現 ](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) | リクエストで送信されたアセット ID に基づいて、リクエストされた出力形式でのアセットの web に最適化されたバイナリ表現を返します。 さらに、幅、高さ、回転、反転、画質、切り抜き、形式、[ スマート切り抜き ](/help/assets/dynamic-media/image-profiles.md) など、様々な画像修飾子を定義できます。 サポートされる形式と画像修飾子について詳しくは、[API の詳細 ](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) を参照してください。<br>Adobeでは、すべての画像形式タイプに対してこの API を使用することをお勧めします。 |
| [Web に最適化されたアセットのバイナリ表現 ](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAsset) | 応答で返されるアセットの web に最適化されたバイナリ表現にデフォルトで適用される便利な API。 デフォルトには、標準のJPEG/WEBP 形式、画質=> 65、幅=> 1024 が含まれます。 |
| [ アセットのオリジナルのアップロード済みバイナリ ](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetOriginal) | アセットに最初にアップロードされたバイナリを返します。 Adobeでは、ドキュメント形式タイプとSVG画像に、この API を使用することをお勧めします。 |
| [AEM Assets オーサリング環境で使用できる、アセットの事前生成済みレンディション ](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetRendition) | リクエストで送信されたアセット ID とレンディション名に基づいて、AEM Assets オーサリング環境で使用可能なアセットレンディションのビットストリームを返します。 |
| [ アセットメタデータ ](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetMetadata) | タイトル、説明、CreateDate、ModifyDate など、アセットに関連付けられたプロパティを返します。 |
| [ ビデオアセットのプレーヤーコンテナ ](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoPlayerDelivery) | ビデオアセットのプレーヤーコンテナを返します。 Player を iframe HTML要素に埋め込んで、ビデオを再生できます。 |
| [ 選択した出力形式で再生マニフェストが表示されます ](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoManifestDelivery) | 指定したビデオアセットの再生マニフェストファイルを、選択した出力形式で返します。 再生マニフェストファイルを取り込んでビデオを再生するには、HLS または DASH プロトコルによるアダプティブストリーミングが可能なカスタムプレーヤーを作成する必要があります。 |

## 配信 API エンドポイント {#delivery-apis-endpoint}

API エンドポイントは、配信 API ごとに異なります。 例えば、`Web-optimized binary representation of the asset in the requested output format` の API の API エンドポイントは次のようになります。
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

配信ドメインは、Experience Managerオーサー環境のドメインと構造が似ています。 唯一の違いは、`author` という用語を `delivery` に置き換えることです。

`pXXXX` はプログラム ID を参照します

`eYYYY` は環境 ID を指します

詳しくは、[API の詳細 ](https://adobe-aem-assets-delivery.redoc.ly/#tag/Assets) を参照してください。

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

配信 API を呼び出すには、制限されたアセットを配信するために、`Authorization` 細に IMS トークンが必要です。 IMS トークンはテクニカルアカウントから取得されます。 新しいテクニカルアカウントを作成するには、[AEM as a Cloud Service資格情報の取得 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) を参照してください。 IMS トークンを生成して配信 API リクエストヘッダーで適切に使用するには、[ アクセストークンの生成 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) を参照してください。


リクエストサンプル、応答サンプルおよび応答コードについては、[ 配信 API](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) を参照してください。
