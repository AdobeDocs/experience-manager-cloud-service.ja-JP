---
title: コンテンツフラグメントを使用したAEM GraphQLの設定と使用のベストプラクティス
description: コンテンツフラグメントでのAEM GraphQLの設定と使用に関して推奨されるベストプラクティスについて説明します。
source-git-commit: 9a544fb9d2494862efdb2263f3b9b61214c4b8b9
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 29%

---


# コンテンツフラグメントを使用したAEM GraphQLの設定と使用のベストプラクティス{#best-practices-setup-use-aem-graphql-content-fragments}

以下のガイドラインは、GraphQLおよびコンテンツフラグメントでAEMを設定、設定および使用する際に推奨されるベストプラクティスをまとめたものです。

## はじめに {#getting-started}

スピードを上げるには、以下を実行します。

* [ヘッドレスの概念と用語の概要については、ヘッドレスとは](/help/headless/what-is-headless.md)
* AEMの様々な環境の概要 [アーキテクチャ](/help/headless/deployment/architecture.md)

## セットアップ {#setup}

コンテンツフラグメントやアプリで使用するAEM GraphQLを安全にセットアップするには、様々なコンポーネントを設定する必要があります。

### GraphQLエンドポイントの作成（セキュリティを含む） {#graphql-endpoint-creation}

エンドポイントは、AEM 用 GraphQL へのアクセスに使用するパスです。安全にアクセスできるように、これらのエンドポイントを作成して公開する必要があります。

#### 詳細 {#details-graphql-endpoint-creation}

[AEM の GraphQL エンドポイントを管理](/help/headless/graphql-api/graphql-endpoint.md)

#### 環境 {#environments-graphql-endpoint-creation}

エンドポイントは、次の場所で設定する必要があります。

* オーサー
* プレビュー
* パブリッシュ

対象：

* 開発
* テスト
* 実稼動

### AEM Dispatcher のキャッシュ {#dispatcher-caching}

>[!NOTE]
>Dispatcher でのキャッシュが有効な場合、 [CORS の設定](#cors-setup) は不要なので、無視できます。

永続化されたクエリのキャッシュは、Dispatcher ではデフォルトで有効になっていません。 複数のオリジンで CORS（クロスオリジンリソース共有）を使用している場合、Dispatcher 設定を確認し、場合によっては更新する必要があるので、デフォルトを有効にすることはできません。

#### 詳細 {#details-dispatcher-caching}

[GraphQLの永続クエリ — Dispatcher でのキャッシュの有効化](/help/headless/deployment/dispatcher-caching.md)

#### 環境 {#environments-dispatcher-caching}

Dispatcher は通常、以下の目的で設定されます。

* 公開：実稼動

### CORS の設定 {#cors-setup}

>[!NOTE]
>キャッシュが [AEM Dispatcher](#dispatcher-caching) が有効になっている場合、CORS の設定は不要なので、このセクションは無視できます。

GraphQL エンドポイントにアクセスするには、CORS ポリシーを設定し、Cloud Manager を使用して AEM にデプロイされた AEM プロジェクトに追加する必要があります。それには、目的のエンドポイントに適した OSGi CORS 設定ファイルを追加します。

#### 詳細 {#details-cors-setup}

[クロスオリジンリソース共有（CORS）設定](/help/headless/deployment/cross-origin-resource-sharing.md)

#### 環境 {#environments-cors-setup}

CORS は通常、次の目的で設定されます。

* 公開：実稼動

### 認証 {#authentication}

コンテンツフラグメント配信用のAdobe Experience Manager as a Cloud Service(AEM)GraphQL API の主な使用例は、サードパーティのアプリケーションまたはサービスからのリモートクエリを受け入れることです。 これらのリモートクエリでヘッドレスコンテンツ配信を保護するには、認証済み API アクセスが必要になる場合があります。

#### 詳細 {#details-authentication}

[コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証](/help/headless/security/authentication.md)

#### 環境 {#environments-authentication}

認証は通常、次の目的で設定されます。

* プレビュー
* パブリッシュ

対象：

* 開発
* テスト
* 実稼動

### 権限 {#permissions}

ヘッドレス実装では、対処が必要なセキュリティおよび権限の領域がいくつかあります。権限とペルソナは、概ね、**オーサー**&#x200B;または&#x200B;**パブリッシュ**&#x200B;の AEM 環境に基づいていると考えることができます。各環境には、様々なペルソナが含まれており、ニーズも異なります。

#### 詳細 {#details-permissions}

[ヘッドレスコンテンツの権限に関する考慮事項](/help/headless/security/permissions.md)

#### 環境 {#environments-permissions}

権限は通常、次の目的で設定されます。

* オーサー
* プレビュー
* パブリッシュ

対象：

* 開発
* テスト
* 実稼動

### コンテンツ配信ネットワーク (CDN) の使用 {#cdn}

GraphQLクエリとその JSON 応答は、をターゲット設定した場合はキャッシュできます `GET` リクエストを送信する必要があります。 これに対し、キャッシュされていないリクエストは、（リソース）非常に高コストで処理に時間がかかる場合があり、元のリソースにさらに悪影響を及ぼす可能性があります。

#### 詳細 {#details-cdn}

[AEM as a Cloud Service での CDN](/help/implementing/dispatcher/cdn.md)

#### 環境 {#environments-cdn}

CDN は通常、次の目的で設定されます。

* 公開：実稼動

### コンテンツフラグメントの設定と作成 {#cconfigure-create-content-fragments}

AEM GraphQLは、コンテンツフラグメントから情報を取得するために使用されます。 これらを設定し、次にコンテンツを作成する前に、構造と場所を定義する必要があります。

#### 詳細 {#details-content-fragments}

* [設定の作成](/help/headless/setup/create-configuration.md)
* [コンテンツフラグメントモデルの作成](/help/headless/setup/create-content-model.md)
* [アセットフォルダーの作成](/help/headless/setup/create-assets-folder.md)
* [コンテンツフラグメントを作成および編集します。](/help/headless/setup/create-content-fragment.md)

#### 環境 {#eenvironments-content-fragments}

コンテンツフラグメントは、次の場所で定義、作成、テスト、公開、アクセスされます。

* オーサー
* プレビュー
* パブリッシュ

対象：

* 開発
* テスト
* 実稼動

## AEM GraphQLの使用 {#use-aem-graphql}

### GraphQLクエリの最適化 {#optimize-graphql-queries}

これらのガイドラインは、GraphQLクエリでのパフォーマンスの問題を防ぐために提供されています。

#### 詳細 {#details-optimize-graphql-queries}

[GraphQLクエリの最適化](/help/headless/graphql-api/graphql-optimization.md)

>[!NOTE]
>
>最適化ガイドラインでは、既に [設定](#setup).

### アプリからGraphQLにアクセス {#access-graphql-from-your-apps}

AEMヘッドレス CMS を使用すると、開発者は、既になじみのある言語、フレームワークおよびツールを使用して、優れたエクスペリエンスを自由に構築し、提供できます。

#### 詳細 {#details-your-apps}

* [開発用AEM SDK をインストールして使用する](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=ja)
* [AEMヘッドレス開発者リソース](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)
* 例： [React](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/react-app.html?lang=ja), [Next.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/next-js.html), [Node.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/server-to-server-app.html)その他

#### 環境 {#environments-your-apps}

通常、アプリは次の場所で開発、テスト、使用されます。

* プレビュー
* パブリッシュ

対象：

* 開発
* テスト
* 実稼動

### その他のリソース

AEM GraphQLとコンテンツフラグメントについて詳しくは、次を参照してください。

* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [GraphiQL IDE の使用](/help/headless/graphql-api/graphiql-ide.md)
* [AEMヘッドレス開発者リソース](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)
