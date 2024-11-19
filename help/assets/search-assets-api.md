---
title: Assets検索 API
description: Search Assets API の使用方法について説明します。
role: User
exl-id: 0c52e793-4c33-4230-b4f2-27296dd9e4b3
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 4%

---

# Assets検索 API {#search-assets-api}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Managerアセットリポジトリで利用可能なすべての [ 承認済みアセット ](approve-assets.md) は、検索された後、配信 URL を使用して統合ダウンストリームアプリケーションに配信できます。

Experience Managerリポジトリから適切な承認済みアセットを検索することは、配信 URL を使用してアセットを配信するための最初のステップです。 検索リクエストへの応答は、検索条件を満たすアセットに対応する JSON ドキュメントの配列で構成されます。 各 JSON ドキュメントは、アセット配信リクエストの作成に使用される `id` フィールドを使用して識別されます。

![直接バイナリアップロードプロトコルの概要](assets/search-assets-api-overview.png)

検索Assets API リクエスト内でプロパティを定義すると、次の機能を有効にできます。

* **フルテキスト検索**:`match` クエリを使用して、検索するテキストを定義します。  また、`match` クエリ内で演算子を使用して、結果をフィルタリングすることもできます。

* **フィルターの適用**:`term` クエリを使用すると、1 つの値と 1 つまたは複数の `key` を定義して結果をさらにフィルタリングできます。 `key` は、値を照合する必要があるフィールドを識別し、`value` は照合する対象を表します。 同様に、`range` クエリを使用して、「次よりも大きい」（gt）、「次よりも大きいまたは等しい」（gte）、「次よりも小さい」（lt）、「次よりも小さいまたは等しい」（lte）の各プロパティを使用してフィールドの範囲を定義できます。

* **結果を並べ替え**:1 つ以上のフィールドに基づいて検索結果を並べ替えるには、`OrderBy` プロパティを使用します。 結果は、昇順または降順で並べ替えることができます。

* **ページネーション**:`limit` プロパティと `cursor` プロパティを使用して、Search API リクエスト内のページネーションプロパティを定義します。 プロパティ `limit`、API 応答で取得する最大項目数を定義します。 プロパティ `cursor`、`limit` プロパティで定義された次のアセットセットの開始点を簡単に取得できます。 例えば、API リクエストで制限として `50` を定義した場合、`cursor` プロパティを使用して、次の API リクエストを使用して次の 50 個の項目を開始および取得できます。

## Assets API エンドポイントを検索 {#search-assets-api-endpoint}

Search assets API リクエストのエンドポイントは、次の形式にする必要があります。
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

配信ドメインは、Experience Managerオーサー環境のドメインと構造が似ています。 唯一の違いは、`author` という用語を `delivery` に置き換えることです。

`pXXXX` はプログラム ID を参照します

`eYYYY` は環境 ID を指します

## Assets API リクエストメソッドを検索 {#search-assets-api-request-method}

POST

## Assets API ヘッダーを検索 {#search-assets-api-header}

Search Assets API でヘッダーを定義する際には、次の詳細を指定する必要があります。

```java
headers: {
      'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    },
```

検索 API を呼び出すには、`Authorization` の詳細でを定義するために IMS トークンが必要です。 IMS トークンはテクニカルアカウントから取得されます。 新しいテクニカルアカウントを作成するには、[AEM as a Cloud Service資格情報の取得 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) を参照してください。 IMS トークンを生成して Search Assets API リクエストヘッダーで適切に使用するには、[ アクセストークンの生成 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) を参照してください。

リクエストサンプル、レスポンスサンプルおよびレスポンスコードについては、[Assets API の検索 ](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search) を参照してください。
