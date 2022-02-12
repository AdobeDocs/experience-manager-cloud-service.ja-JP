---
title: AEMヘッドレスを使用した Dispatcher 設定
description: Dispatcher は、Adobe Experience Managerパブリッシュ環境の前にあるキャッシュとセキュリティのレイヤーです。 ヘッドレスアプリケーションに対して GraphQL エンドポイントを開くには、いくつかの設定が使用されます。
feature: Dispatcher, GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# AEMヘッドレスを使用した Dispatcher 設定

この [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) は、Adobe Experience Managerパブリッシュ環境の前面にあるキャッシュとセキュリティレイヤーです。 ヘッドレスアプリケーションに対して GraphQL エンドポイントを開くためのいくつかの設定がデフォルトで含まれています。

>[!NOTE]
>
>Dispatcher に関する詳細なドキュメントについては、 [Dispatcher ガイド](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)

AEMプロジェクトの一部として、Dispatcher の設定を含む Dispatcher モジュールが含まれます。 から新しく生成されたプロジェクト [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) 自動的に含める [フィルター](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter) GraphQL エンドポイントを有効にする

## GraphQL エンドポイント

デフォルトのフィルターの一部として、 [GraphQL エンドポイント](/help/headless/graphql-api/graphql-endpoint.md) は次のルールで開かれます。

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

この `*` ワイルドカードを使用すると、AEMインスタンス上で複数のエンドポイントが開きます。 GraphQL エンドポイントを使用したクエリは、 `POST` そして応答は **not** をキャッシュします。

## GraphQL 永続クエリ

永続化クエリのリクエストは、別のエンドポイントに対しておこなわれます。 デフォルトのフィルター設定の一環として、 [永続クエリ](/help/headless/graphql-api/persisted-queries.md) は次のルールで開かれます。

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

永続的なクエリは、 `GET`したがって、Dispatcher および CDN レベルでの応答がキャッシュされます。 キャッシュとキャッシュの無効化について詳しくは、 [ここ](/help/implementing/dispatcher/caching.md).
