---
title: AEM ヘッドレスを使用した Dispatcher エンドポイントの設定
description: Dispatcherは、Adobe Experience Manager パブリッシュ環境の前にあるキャッシュとアクセス フィルタリングのレイヤーです。 ヘッドレスアプリケーションに対して GraphQL エンドポイントを開くには、いくつかの設定が使用されます。
feature: Headless, Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
role: Admin, Developer
source-git-commit: ecf3f0ac54acf4ac772d2906fa0b26d283549929
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 72%

---


# Dispatcher - AEM ヘッドレスを使用したエンドポイントの設定

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)は、Adobe Experience Manager パブリッシュ環境の前にあるキャッシュおよびアクセス フィルタリング レイヤーです。 ヘッドレスアプリケーションに対して GraphQL エンドポイントを開くためのいくつかの設定がデフォルトで含まれています。

>[!IMPORTANT]
>
>Dispatcher フィルタールールはアクセスフィルタリング制御であり、パブリッシュインスタンスのJCR ACL ベースのアクセス制御の代わりにはなりません。 パブリッシュインスタンスは、Dispatcher設定とは別に保護する必要があります。 Dispatcher フィルター設定に関係なく、リポジトリーレベルで`everyone`および`anonymous` プリンシパルの`jcr:read`を拒否することで、機密性の高いリソースが保護されるようにします。

>[!NOTE]
>
>Dispatcher に関する詳細なドキュメントについては、[Dispatcher ガイド](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。

AEM プロジェクトの一部として、Dispatcher の設定を含む Dispatcher モジュールが含まれます。 [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)から新しく生成されたプロジェクトは、GraphQL エンドポイントを有効にする[フィルター](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#defining-a-filter)を自動的に含めます。

## GraphQL エンドポイント

デフォルトのフィルターの一部として、[GraphQL エンドポイント](/help/headless/graphql-api/graphql-endpoint.md)は次のルールで開かれます。

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

`*` ワイルドカードを使用すると、AEM インスタンス上で複数のエンドポイントが開きます。 GraphQL エンドポイントを使用したクエリは、`POST` を使用して作成され、応答は&#x200B;**キャッシュされません**。

## GraphQL 永続クエリ

永続クエリのリクエストは、別のエンドポイントに対して行われます。 デフォルトのフィルター設定の一環として、[永続クエリ](/help/headless/graphql-api/persisted-queries.md)の URL は次のルールで開かれます。

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

永続クエリは `GET` を使用してリクエストされるため、Dispatcher および CDN レベルで応答がキャッシュされます。 キャッシュとキャッシュの無効化について詳しくは、[AEM as a Cloud Service でのキャッシュの概要](/help/implementing/dispatcher/caching.md)を参照してください。
