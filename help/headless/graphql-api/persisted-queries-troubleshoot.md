---
title: 永続化されたGraphQLクエリのトラブルシューティング
description: Adobe Experience Manager as a Cloud Serviceでの永続的なGraphQLクエリの問題をトラブルシューティングする方法を説明します。
feature: Content Fragments,GraphQL API
source-git-commit: c8ea9846600d1773e6f269973635f5338f31906f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# 永続化されたGraphQLクエリのトラブルシューティング {#troubleshoot-persisted-graphql-queries}

The [アクションセンター](/help/operations/actions-center.md) 次を含む **GraphQLの永続クエリエラー** アラート。 つまり、GraphQLで永続的なクエリの 1 つでエラーがスローされるたびに通知されます。

このような問題のトラブルシューティングと解決に役立つよう、 *最も一般的* 失敗の原因と、その修正方法に関する手順について説明します。

## コンテンツフラグメントモデルの変更 {#changes-to-content-fragment-model}

GraphQLで永続化されたクエリは、古いGraphQLタイプに基づいている場合に失敗する可能性があります。多くの場合、基になるコンテンツフラグメントモデルの変更が原因です。

これは様々な理由で発生する可能性があります。 例えば、コンテンツモデルの作成者は、次のように設定します。

* フィールドを削除するか、名前を変更します
* フラグメント参照用に定義された許可されたモデルを更新します。
* 他のモデルによって参照されているモデルを非公開にします。
* その他の行為及び理由

これに対処するには、次のいずれかを実行します。

* 失敗している永続化されたクエリは、コンテンツフラグメントモデルの変更に合わせて更新する必要があります
* または、問題が発生したモデルに対する変更を元に戻す必要があります

## GraphQLエンドポイントが設定されていません {#graphql-endpoint-not-configured}

永続化されたクエリが `400` または `500` エラーコードと情報 `No suitable endpoint found`と呼ばれる場合、AEM環境にGraphQLエンドポイントが設定されていません。

これを修正するには、次の手順に従って、エンドポイントを有効にし、 [AEMでのGraphQLエンドポイントの管理](/help/headless/graphql-api/graphql-endpoint.md).

## GraphQLの永続クエリ URL にパスがありません {#missing-path-query-url}

永続化されたクエリが `400` または `500` エラーコードと情報 `Suffix: '/' does not contain a path`に設定されている場合、GraphQLサーブレットは、パスサフィックスなしで呼び出されます。

パターンは次のようになります。 `/graphql/execute.json/thePath`.

## IP の許可リストによりブロック済み {#blocked-due-to-ip-allow-list}

この場合、クエリは `405` エラーコード。

これはGraphQLに固有のものではありません。 ナレッジベース記事を参照 [405 エラーは許可されていません](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-20824.html).

## Dispatcher によるブロック {#blocked-dispatcher}

GraphQLエンドポイントが `404` 次の公開用にエラーが発生しました： `POST` リクエストの場合、GraphQLクエリは Dispatcher レベルでブロックされ、エンドポイントを手動で有効にする必要があります。

デフォルトではそうではありませんが、カスタム Dispatcher 設定が原因で、この問題が発生する可能性があります。 詳しくは、以下を参照してください。 [Dispatcher - AEMヘッドレスを使用したエンドポイントの設定](/help/headless/deployment/dispatcher.md).
