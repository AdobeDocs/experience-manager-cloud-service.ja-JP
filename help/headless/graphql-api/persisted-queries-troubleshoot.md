---
title: 永続化された GraphQL クエリをトラブルシューティングする
description: Adobe Experience Manager as a Cloud Service での永続的な GraphQL クエリの問題をトラブルシューティングする方法を説明します。
feature: Headless, Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: ht
source-wordcount: '363'
ht-degree: 100%

---

# 永続化された GraphQL クエリをトラブルシューティングする {#troubleshoot-persisted-graphql-queries}

[アクションセンター](/help/operations/actions-center.md)には、**GraphQL 永続クエリエラー**&#x200B;のアラートが含まれています。これは、GraphQL 永続化クエリのいずれかがエラーをスローするたびに通知されることを意味します。

このような問題のトラブルシューティングと解決に役立つよう、このページでは、*最も一般的*&#x200B;な失敗の原因と、その修正方法に関する手順について説明します。

## コンテンツフラグメントモデルの変更 {#changes-to-content-fragment-model}

GraphQL で永続化されたクエリは、古い GraphQL タイプに基づいている場合に失敗する可能性があります。多くの場合、参照元のコンテンツフラグメントモデルの変更が原因です。

このようなエラーは、様々な理由で発生する可能性があります。例えば、コンテンツフラグメントモデルの作成者が次のような場合があります（リストがすべてではありません）。

* フィールドを削除したり、名前を変更します
* フラグメント参照に使用できるモデルを定義する&#x200B;**モデルタイプ**&#x200B;を更新します
* 他のモデルが参照しているモデルを非公開にします

このようなエラーに対処するには、次のいずれかを実行する必要があります。

* コンテンツフラグメントモデルの変更に対応できない永続クエリを更新する
* 問題が発生したモデルに対する変更を元に戻す

## GraphQL エンドポイントが設定されていません {#graphql-endpoint-not-configured}

永続クエリが情報 `No suitable endpoint found` と共に `404` のエラーコードを返す場合は、AEM 環境に GraphQL エンドポイントが設定されていません。

これを修正するには、[AEM の GraphQL エンドポイントを管理](/help/headless/graphql-api/graphql-endpoint.md)でエンドポイントを有効にして公開する手順に従います。

## GraphQL の永続クエリ URL にパスがありません {#missing-path-query-url}

永続クエリが情報 `Suffix: '/' does not contain a path` と共に `400` のエラーコードを返す場合は、GraphQL サーブレットがパスのサフィックスなしで呼び出されています。

このパターンは `/graphql/execute.json/thePath` です。

## IP の許可リストによりブロックされました {#blocked-due-to-ip-allow-list}

この場合、クエリは `405` エラーコードを返します。

このようなエラーは GraphQL に固有のものではありません。ナレッジベース記事 [405 エラー許可されていません](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-20824)を参照してください。

## Dispatcher によりブロックされました {#blocked-dispatcher}

`POST` リクエストの公開時に GraphQL エンドポイントが `404` エラーを返した場合、GraphQL クエリが Dispatcher レベルでブロックされており、エンドポイントを手動で有効にする必要があることを意味します。

デフォルトでは当てはまりませんが、カスタム Dispatcher 設定が原因で、この問題が発生する可能性があります。詳しくは、[Dispatcher - AEM ヘッドレスを使用したエンドポイントの設定](/help/headless/deployment/dispatcher.md)を参照してください。
