---
title: 配信 API
description: 配信 API の使用方法について説明します。
role: User
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: 870f3f1826ea88cae0fc1fa31177bb9ffc8646f3
workflow-type: ht
source-wordcount: '627'
ht-degree: 100%

---

# 配信 API {#delivery-apis}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能搭載 Dynamic Media のガイドを、PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE OpenAPI 機能搭載 Dynamic Media ガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Manager Assets リポジトリで使用可能なすべての[承認済みアセット](approve-assets.md)を[検索](search-assets-api.md)し、配信 URL を使用して統合されたダウンストリームアプリケーションに配信できます。

バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに行われた変更は、配信 URL に自動的に反映されます。CDN 経由のアセット配信に 10 分という短い有効期限（TTL）値を設定すると、更新は 10 分以内にすべてのオーサリングインターフェイスと公開済みインターフェイスに表示されます。

次の画像は、使用可能な配信 URL を示しています。

![配信 API](assets/delivery-url.png)

次の表に、使用可能な様々な配信 API の使用方法を示します。

| 配信 API | 説明 |
|---|---|
| [リクエストされた出力形式でのアセットの web に最適化されたバイナリ表現](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) | リクエストで送信されたアセット ID に基づいて、リクエストされた出力形式でアセットの web に最適化されたバイナリ表現を返します。さらに、幅、高さ、回転、反転、画質、切り抜き、形式、[スマート切り抜き](/help/assets/dynamic-media/image-profiles.md)など、様々な画像修飾子を定義できます。サポートされる形式と画像修飾子について詳しくは、[API の詳細](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat)を参照してください。<br>アドビでは、すべての画像形式タイプにこの API を使用することをお勧めします。 |
| [アセットの web に最適化されたバイナリ表現](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAsset) | 応答で返されるアセットの web に最適化されたバイナリ表現にデフォルトを適用する便利な API。デフォルトでは、標準の JPEG／WEBP 形式、画質 => 65、幅 => 1024 が含まれます。 |
| [アセットの元のアップロードされたバイナリ](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetOriginal) | アセットの元のアップロードされたバイナリを返します。アドビでは、ドキュメント形式タイプと SVG 画像にこの API を使用することをお勧めします。 |
| [AEM Assets オーサリング環境で使用可能なアセットの事前生成済みレンディション](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetRendition) | リクエストで送信されたアセット ID とレンディション名に基づいて、AEM Assets オーサリング環境で使用可能なアセットレンディションのビットストリームを返します。 |
| [アセットのメタデータ](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetMetadata) | タイトル、説明、CreateDate、ModifyDate など、アセットに関連付けられたプロパティを返します。 |
| [ビデオアセットのプレーヤーコンテナ](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoPlayerDelivery) | ビデオアセットのプレーヤーコンテナを返します。プレーヤーを iframe HTML 要素に埋め込んでビデオを再生できます。 |
| [選択した出力形式の再生マニフェスト](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoManifestDelivery) | 指定されたビデオアセットの再生マニフェストファイルを、選択した出力形式で返します。再生マニフェストファイルを取り込んでビデオを再生するには、HLS または DASH プロトコルを通じてアダプティブストリーミングが可能なカスタムプレーヤーを作成する必要があります。 |


>[!NOTE]
>
* [画像プリセット、スマートイメージング、追加の画像の修飾子](https://adobe-aem-assets-delivery-advancemodifiers.redoc.ly/)は、限定提供機能として使用できます。アクセス権を取得するには、[アドビカスタマーサポートケースを作成および送信してください](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)。
* スマート切り抜きは、[Assets Prime](/help/assets/assets-ultimate-overview.md) では使用できません。

## 配信 API エンドポイント {#delivery-apis-endpoint}

API エンドポイントは、配信 API ごとに異なります。例えば、`Web-optimized binary representation of the asset in the requested output format` API の API エンドポイントは、次のようになります。
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

配信ドメインは、Experience Manager オーサー環境のドメインと構造が似ています。唯一の違いは、`author` という用語を `delivery` に置き換えることです。

`pXXXX` はプログラム ID を参照します。

`eYYYY` は環境 ID を参照します。

詳しくは、[API の詳細](https://adobe-aem-assets-delivery.redoc.ly/#tag/Assets)を参照してください。

## 配信 API リクエストメソッド {#delivery-api-request-method}

GET

## 配信 API ヘッダー {#deliver-assets-api-header}

配信 API ヘッダーでヘッダーを定義する際には、次の詳細を指定する必要があります。

```java
headers: {
      'If-None-Match': 'string',
      Authorization: 'Bearer <YOUR_JWT_HERE>'
    }
```

配信 API を呼び出すには、制限されたアセットを配信する `Authorization` の詳細に IMS トークンが必要です。IMS トークンは、テクニカルアカウントから取得されます。新しいテクニカルアカウントを作成する方法について詳しくは、[AEM as a Cloud Service の資格情報の取得](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=ja#fetch-the-aem-as-a-cloud-service-credentials)を参照してください。IMS トークンを生成し、配信 API リクエストヘッダーで適切に使用する方法について詳しくは、[アクセストークンの生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=ja#generating-the-access-token)を参照してください。


リクエストサンプル、応答サンプルおよび応答コードを表示する方法について詳しくは、[配信 API](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) を参照してください。
