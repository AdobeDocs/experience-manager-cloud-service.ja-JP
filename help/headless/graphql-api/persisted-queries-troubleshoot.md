---
title: 永続化された GraphQL クエリをトラブルシューティングする
description: Adobe Experience Manager as a Cloud Service での永続的な GraphQL クエリの問題をトラブルシューティングする方法を説明します。
feature: Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
source-git-commit: 05548d56d791584781606b02839c5602b4469f7b
workflow-type: ht
source-wordcount: '353'
ht-degree: 100%

---

# 永続化された GraphQL クエリをトラブルシューティングする {#troubleshoot-persisted-graphql-queries}

[アクションセンター](/help/operations/actions-center.md)には、**GraphQL 永続クエリエラー**&#x200B;のアラートが含まれています。これは、GraphQL 永続化クエリのいずれかがエラーをスローするたびに通知されることを意味します。

このような問題のトラブルシューティングと解決に役立つよう、*最も一般的*&#x200B;な失敗の原因と、その修正方法に関する手順について説明します。

## コンテンツフラグメントモデルの変更 {#changes-to-content-fragment-model}

GraphQL で永続化されたクエリは、古い GraphQL タイプに基づいている場合に失敗する可能性があります。多くの場合、参照元のコンテンツフラグメントモデルの変更が原因です。

これは、様々な理由で発生する可能性があります。例えば、コンテンツモデルの作成者は：

* フィールドを削除したり、名前を変更します
* フラグメント参照用に定義された許可されたモデルを更新します
* 他のモデルが参照しているモデルを非公開にします
* その他のアクションと理由

これに対処するには：

* 失敗している永続化されたクエリは、コンテンツフラグメントモデルの変更に合わせて更新する必要があります
* または、問題が発生したモデルに対する変更を元に戻す必要があります

## GraphQL エンドポイントが設定されていません {#graphql-endpoint-not-configured}

永続化されたクエリが `400` または `500` のエラーコードを返し、情報 `No suitable endpoint found` が表示される場合、AEM 環境に GraphQL エンドポイントが設定されていません。

これを修正するには、[AEM の GraphQL エンドポイントを管理](/help/headless/graphql-api/graphql-endpoint.md)でエンドポイントを有効にして公開する手順に従います。

## GraphQL の永続クエリ URL にパスがありません {#missing-path-query-url}

永続化されたクエリが `400` または `500` のエラーコードと情報 `Suffix: '/' does not contain a path` を返す場合、GraphQL サーブレットは、パスのサフィックスなしで呼び出されています。

このパターンは `/graphql/execute.json/thePath` です。

## IP の許可リストによりブロックされました {#blocked-due-to-ip-allow-list}

この場合、クエリは `405` エラーコードを返します。

これは GraphQL に固有のものではありません。ナレッジベース記事 [405 エラー許可されていません](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-20824.html)を参照してください。

## Dispatcher によりブロックされました {#blocked-dispatcher}

`POST` リクエストの公開時に GraphQL エンドポイントが `404` エラーを返した場合、GraphQL クエリが Dispatcher レベルでブロックされており、エンドポイントを手動で有効にする必要があることを意味します。

デフォルトでは当てはまりませんが、カスタム Dispatcher 設定が原因で、この問題が発生する可能性があります。詳しくは、[Dispatcher - AEM ヘッドレスを使用したエンドポイントの設定](/help/headless/deployment/dispatcher.md)を参照してください。
