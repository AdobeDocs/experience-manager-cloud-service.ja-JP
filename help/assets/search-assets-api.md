---
title: Assets検索 API
description: Search Assets API の使用方法について説明します。
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Assets検索 API {#search-assets-api}

すべて [承認済みアセット](approve-assets.md) Experience Managerのアセットリポジトリーで使用可能で、検索した後、配信 URL を使用して統合ダウンストリームアプリケーションに配信できます。

Experience Managerリポジトリから適切な承認済みアセットを検索することは、配信 URL を使用してアセットを配信するための最初のステップです。 検索リクエストへの応答は、検索条件を満たすアセットに対応する JSON ドキュメントの配列で構成されます。 各 JSON ドキュメントは、 `id` アセット配信リクエストを作成するために使用されるフィールド。

![直接バイナリアップロードプロトコルの概要](assets/search-assets-api-overview.png)

検索Assets API リクエスト内でプロパティを定義すると、次の機能を有効にできます。

* **フルテキスト検索**：を使用します `match` 検索するテキストを定義するクエリ。  内で演算子を使用することもできます `match` 結果をフィルターするクエリ。

* **フィルターの適用**：を使用します `term` を定義して結果をさらにフィルタリングするためのクエリ `key` および 1 つ以上の値。 `key` は、値をと一致させる必要があるフィールドを識別します。 `value` 照合する対象を表します。 同様に、 `range` 「次よりも大きい」（gt）、「次よりも大きいまたは等しい」（gte）、「次よりも小さい」（lt）、「次よりも小さい」または「次よりも小さい」（lte）の各プロパティを使用してフィールドの範囲を定義するクエリ。

* **結果を並べ替え**：を使用します `OrderBy` 1 つ以上のフィールドに基づいて検索結果を並べ替えるためのプロパティ。 結果は、昇順または降順で並べ替えることができます。

* **ページネーション**：を使用します `limit` および `cursor` properties :Search API リクエスト内のページネーションプロパティを定義します。 `limit` プロパティは、API 応答で取得する最大項目数を定義します。 `cursor` プロパティを使用すると、 `limit` プロパティ。 例えば、次のように定義するとします `50` api リクエストの制限として、を使用できます。 `cursor` 次の API リクエストを使用して、次の 50 項目を開始および取得するプロパティ。

## Assets API エンドポイントを検索 {#search-assets-api-endpoint}

Search assets API リクエストのエンドポイントは、次の形式にする必要があります。
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

配信ドメインは、Experience Managerオーサー環境のドメインと構造が似ています。 唯一の違いは用語を置き換えることです `author` （を使用） `delivery`.

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

検索 API を呼び出すには、で定義するために IMS トークンが必要です `Authorization` の詳細。 IMS トークンはテクニカルアカウントから取得されます。 参照： [AEM as a Cloud Service資格情報の取得](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) 新しいテクニカルアカウントを作成します。 参照： [アクセストークンの生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) ims トークンを生成して、Search Assets API リクエストヘッダーで適切に使用する。

要求サンプル、応答サンプルおよび応答コードを表示するには、次を参照してください [Assets検索 API](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search).

