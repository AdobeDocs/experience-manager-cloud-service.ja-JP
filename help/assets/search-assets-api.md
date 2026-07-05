---
title: アセット API の検索
description: 検索アセット API を使用する方法について説明します。
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: 0c52e793-4c33-4230-b4f2-27296dd9e4b3
source-git-commit: ef5161d89083284544283c8e059c5817faacbbb3
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 36%

---

# アセット API の検索 {#search-assets-api}

Experience Manager Assets リポジトリで使用可能なすべての[承認済みアセット](approve-assets.md)を検索し、配信 URL を使用して統合されたダウンストリームアプリケーションに配信できます。

Experience Manager リポジトリから適切な承認済みアセットを検索することは、配信 URL を使用してアセットを配信する最初のステップです。 検索リクエストへの応答は、検索条件を満たしたアセットに対応する JSON ドキュメントの配列で構成されます。 各 JSON ドキュメントは、アセット配信リクエストの作成に使用される「`id`」フィールドを使用して識別されます。

![直接バイナリアップロードプロトコルの概要](assets/search-assets-api-overview.png)

検索アセット API リクエスト内でプロパティを定義して、次の機能を有効にすることができます。

* **フルテキスト検索**：`match` クエリを使用して、検索するテキストを定義します。  また、`match` クエリ内で演算子を使用して結果をフィルタリングすることもできます。

* **フィルターを適用**：`term` クエリを使用して、`key` と 1 つまたは複数の値を定義することで、結果をさらにフィルタリングします。 `key` は、値が一致する必要があるフィールドを識別し、`value` は一致対象を表します。 同様に、`range` クエリを使用し、次より大きい（gt）、次より大きいまたは等しい（gte）、次より小さい（lt）、次より小さいまたは等しい（lte）の各プロパティを使用して、フィールドの範囲を定義できます。

* **結果を並べ替え**：`OrderBy` プロパティを使用して、1 つまたは複数のフィールドに基づいて検索結果を並べ替えます。 結果を昇順または降順で並べ替えることができます。

* **ページネーション**：`limit` プロパティと `cursor` プロパティを使用して、検索 API リクエスト内のページネーションプロパティを定義します。 `limit` プロパティは、API 応答で取得する最大項目数を定義します。 `cursor` プロパティを使用すると、`limit` プロパティで定義された次のアセットセットの開始点を取得することが簡単になります。 例えば、API リクエストで制限として `50` を定義した場合、`cursor` プロパティを使用して、次の API リクエストで次の 50 項目を開始および取得できます。

## 検索アセット API エンドポイント {#search-assets-api-endpoint}

Search assets API リクエストのエンドポイントは、次の形式である必要があります。


配信ドメインは、Experience Manager オーサー環境のドメインと構造が似ています。 唯一の違いは、`author` という用語を `delivery` に置き換えることです。

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

検索 API を呼び出すには、`Authorization` の詳細で IMS トークンを定義する必要があります。 IMS トークンは、テクニカルアカウントから取得されます。 新しいテクニカルアカウントを作成する方法について詳しくは、[AEM as a Cloud Service の資格情報の取得](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=ja#fetch-the-aem-as-a-cloud-service-credentials)を参照してください。 IMS トークンを生成し、検索アセット API リクエストヘッダーで適切に使用する方法について詳しくは、[アクセストークンの生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=ja#generating-the-access-token)を参照してください。

リクエストサンプル、応答サンプルおよび応答コードを表示する方法について詳しくは、[検索アセット API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/search) を参照してください。

## よくある質問 {#faqs-search-assets-apis}

### OpenAPIを使用したDynamic MediaのSearch Assets APIとは何ですか？また、どのように機能しますか？ {#search-assets-api-overview}

Dynamic Media with OpenAPI Search Assets APIを使用すると、Adobe Experience Manager Assets リポジトリで承認済みアセットを検索し、配信URLを使用して統合されたダウンストリームアプリケーションに配信できます。 承認済みアセットの検索は、配信ワークフローの最初のステップです。API応答は、検索条件を満たす各アセットに対してJSON ドキュメントの配列を返します。各ドキュメントは、アセット配信リクエストの作成に使用されるID フィールドで識別されます。 Search Assets APIでは、フルテキスト検索、フィルターベースの検索、結果の並べ替え、ページネーションを1回のリクエストでサポートしています。

### Search Assets APIはどのような検索機能をサポートしていますか？ {#search-assets-api-capabilities}

OpenAPI検索機能を備えたDynamic Media Assets APIは、4つのコア検索機能をサポートしています。 フルテキスト検索では、一致クエリを使用してテキストを検索し、演算子を使用して結果をフィルタリングできます。 フィルターベースの検索では、「クエリー」という用語を使用して、キーと1つまたは複数の値で結果をフィルタリングするか、「範囲」クエリーを使用して、より大きい、より大きい、より小さい、および等小さい演算子を使用して値の範囲でフィルタリングします。 結果の並べ替えは、OrderBy プロパティを使用して、昇順または降順の1つまたは複数のフィールドに基づいて結果を並べ替えます。 ページネーションでは、limit プロパティとcursor プロパティを使用して、リクエストごとに返される結果の数を制御し、後続の結果ページを取得します。

### Search Assets APIを使用してフルテキスト検索を実行するにはどうすればよいですか？ {#search-assets-api-full-text-search}

OpenAPI検索Assets APIを使用したDynamic Mediaでのフルテキスト検索は、リクエスト本文のmatch query プロパティを使用して実行されます。 一致クエリ内で検索するテキストを定義します。 演算子は、一致クエリ内で使用して、返される結果をさらにフィルタリングすることもできます。 一致クエリは、AEM Assets リポジトリ内の承認済みアセットを検索し、一致するアセットのJSON配列を返します。各アセットは、配信URLの作成に使用されるID フィールドで識別されます。

### Search Assets APIを使用して検索結果をフィルタリングするにはどうすればよいですか？ {#search-assets-api-filters}

OpenAPI検索Assets APIを備えたDynamic Mediaでは、2つのフィルタークエリタイプをサポートしています。 「クエリ」という用語は、一致するフィールドを識別するキーと、一致する1つまたは複数の値を指定することで、結果をフィルタリングします。 範囲クエリは、次の演算子を使用して定義された範囲を使用して、特定のフィールドの結果をフィルタリングします。gtより大きい、gteより大きい、または等しい、ltより小さい、およびlteより小さい、または等しい。 両方のクエリタイプを同じAPI リクエスト内で使用して、複数のフィルターを同時に適用できます。

### Search Assets APIでのページネーションの仕組み？ {#search-assets-api-pagination}

OpenAPI検索Assets APIを使用したDynamic Mediaのページネーションは、リクエストの2つのプロパティ（limitとcursor）を使用して制御されます。 limit プロパティは、1つのAPI応答で取得するアセットの最大数を定義します。 cursor プロパティは、定義された制限に基づいて、次のアセット セット セット セット セットの開始点を定義します。 例えば、最初のリクエストで50の制限を設定すると、最初の50個の一致するアセットが返されます。次のリクエストのカーソルプロパティは、次の50個のアセットを取得し、大規模な結果セットのシーケンシャルトラバーサルを可能にします。

### Search Assets APIから返された検索結果を並べ替えるにはどうすればよいですか？ {#search-assets-api-sort}

OpenAPIを使用したDynamic Media Search Assets APIの検索結果は、リクエスト本文のOrderBy プロパティを使用して並べ替えられます。 OrderBy プロパティで1つまたは複数のフィールドを指定して、結果を並べ替えます。 並べ替えは、昇順または降順で適用できます。 複数のソートフィールドを組み合わせて、APIによって返される検索結果に階層化されたソートを適用できます。

### Search Assets APIのエンドポイント形式は何ですか？ {#search-assets-api-endpoint=faqs}

OpenAPI Search Assets API エンドポイントを使用するDynamic Mediaは、次のフォーマットに従う必要があります。https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search. 配信ドメインは、AEM オーサー環境ドメインと同様の構造を持ちます。唯一の違いは、オーサーという用語を配信に置き換えることです。 URLでは、pXXXXはプログラム IDを表し、eYYYYYは環境IDを表します。 Search Assets APIでは、HTTP POST リクエストメソッドを使用します。

### Search Assets APIを呼び出すために必要なヘッダーは何ですか？ {#search-assets-api-headers}

OpenAPIを使用したDynamic Media Search Assets APIには、Content-Typeをapplication/jsonに設定し、X-Adobe-Accept-Experimentalを1に設定し、IMS トークンを含むベアラートークンとしての認証と、API キーを含むX-Api-Keyの4つのヘッダーフィールドが必要です。 IMS トークンは、AEM as a Cloud Service資格情報ワークフローを使用して作成されたテクニカルアカウントから取得されます。 Search Assets APIを呼び出す前に、テクニカルアカウントを作成し、生成されたアクセストークンを使用する必要があります。

### Search Assets API レスポンスでID フィールドはどのような役割を果たしますか？ {#search-assets-api-response-id}

Search Assets API応答の各JSON ドキュメントは、検索条件を満たし、ID フィールドで識別されるアセットに対応します。 このID フィールドは、アセット配信リクエストの作成に使用されるアセット識別子です。これは、Dynamic Media with OpenAPI Delivery API エンドポイント URLのassetId パラメーターとして渡されます。 検索応答からIDをキャプチャすることは、エンドツーエンドのワークフローで必要な手順であり、配信URLを介して承認済みアセットを検索して配信します。