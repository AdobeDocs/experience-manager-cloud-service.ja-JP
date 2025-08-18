---
title: アセット API の検索
description: 検索アセット API を使用する方法について説明します。
role: User
exl-id: 0c52e793-4c33-4230-b4f2-27296dd9e4b3
source-git-commit: 8b596c6e82d9beaeb922cc6635717f151bb390e7
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 99%

---

# アセット API の検索 {#search-assets-api}

Experience Manager Assets リポジトリで使用可能なすべての[承認済みアセット](approve-assets.md)を検索し、配信 URL を使用して統合されたダウンストリームアプリケーションに配信できます。

Experience Manager リポジトリから適切な承認済みアセットを検索することは、配信 URL を使用してアセットを配信する最初のステップです。検索リクエストへの応答は、検索条件を満たしたアセットに対応する JSON ドキュメントの配列で構成されます。各 JSON ドキュメントは、アセット配信リクエストの作成に使用される「`id`」フィールドを使用して識別されます。

![直接バイナリアップロードプロトコルの概要](assets/search-assets-api-overview.png)

検索アセット API リクエスト内でプロパティを定義して、次の機能を有効にすることができます。

* **フルテキスト検索**：`match` クエリを使用して、検索するテキストを定義します。また、`match` クエリ内で演算子を使用して結果をフィルタリングすることもできます。

* **フィルターを適用**：`term` クエリを使用して、`key` と 1 つまたは複数の値を定義することで、結果をさらにフィルタリングします。`key` は、値が一致する必要があるフィールドを識別し、`value` は一致対象を表します。同様に、`range` クエリを使用し、次より大きい（gt）、次より大きいまたは等しい（gte）、次より小さい（lt）、次より小さいまたは等しい（lte）の各プロパティを使用して、フィールドの範囲を定義できます。

* **結果を並べ替え**：`OrderBy` プロパティを使用して、1 つまたは複数のフィールドに基づいて検索結果を並べ替えます。結果を昇順または降順で並べ替えることができます。

* **ページネーション**：`limit` プロパティと `cursor` プロパティを使用して、検索 API リクエスト内のページネーションプロパティを定義します。`limit` プロパティは、API 応答で取得する最大項目数を定義します。`cursor` プロパティを使用すると、`limit` プロパティで定義された次のアセットセットの開始点を取得することが簡単になります。例えば、API リクエストで制限として `50` を定義した場合、`cursor` プロパティを使用して、次の API リクエストで次の 50 項目を開始および取得できます。

## 検索アセット API エンドポイント {#search-assets-api-endpoint}

検索アセット API リクエストのエンドポイントは、次の形式にする必要があります。
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

配信ドメインは、Experience Manager オーサー環境のドメインと構造が似ています。唯一の違いは、`author` という用語を `delivery` に置き換えることです。

`pXXXX` はプログラム ID を参照します。

`eYYYY` は環境 ID を参照します。

## 検索アセット API リクエストメソッド {#search-assets-api-request-method}

POST

## 検索アセット API ヘッダー {#search-assets-api-header}

検索アセット API でヘッダーを定義する際には、次の詳細を指定する必要があります。

```java
headers: {
      'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    },
```

検索 API を呼び出すには、`Authorization` の詳細で IMS トークンを定義する必要があります。IMS トークンは、テクニカルアカウントから取得されます。新しいテクニカルアカウントを作成する方法について詳しくは、[AEM as a Cloud Service の資格情報の取得](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=ja#fetch-the-aem-as-a-cloud-service-credentials)を参照してください。IMS トークンを生成し、検索アセット API リクエストヘッダーで適切に使用する方法について詳しくは、[アクセストークンの生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=ja#generating-the-access-token)を参照してください。

リクエストサンプル、応答サンプルおよび応答コードを表示する方法について詳しくは、[検索アセット API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/search) を参照してください。
