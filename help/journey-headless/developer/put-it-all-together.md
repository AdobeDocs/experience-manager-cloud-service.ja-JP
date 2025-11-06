---
title: すべてをまとめる方法 - AEM ヘッドレスのアプリとコンテンツ
description: AEM ヘッドレスデベロッパージャーニーのこの部分では、コンテンツフラグメント、GraphQL 呼び出し、REST API 呼び出し、アプリケーションを含む AEM プロジェクトを実行し、運用開始に備える方法を説明します。
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 100%

---

# すべてをまとめる方法 - AEM ヘッドレスのアプリとコンテンツ {#put-it-all-together}

[AEM ヘッドレス開発者ジャーニー](overview.md)のこのパートでは、AEM 開発ツールとヘッドレス SDK を使用してアプリケーションを統合する方法を説明します。

## これまでの説明内容 {#story-so-far}

AEM ヘッドレスジャーニーの前のドキュメント [AEM Assets API を使用してコンテンツを更新する方法](update-your-content.md)では、API を使用して AEM の既存のヘッドレスコンテンツを更新する方法を説明し、以下を達成できました。

* AEM Assets HTTP API を理解する

## 目的 {#objective}

この記事では、次の方法で AEM ヘッドレスアプリケーションをまとめる方法を説明します。

* AEM ヘッドレス SDK と必要な開発ツールの把握
* 運用開始前にコンテンツをシミュレートするためのローカル開発ランタイムのセットアップ
* AEM コンテンツレプリケーションの基本について

## AEM SDK {#the-aem-sdk}

AEM SDK は、カスタムコードのビルドとデプロイに使用されます。ヘッドレスアプリケーションを開発し運用開始前にテストするために必要な主なツールです。次のアーティファクトで構成されます。

* クイックスタート JAR - オーサーインスタンスとパブリッシュインスタンスの両方をセットアップするために使用できる実行可能な JAR ファイル
* Dispatcher ツール - Windows および UNIX® ベースシステム用の Dispatcher モジュールとその依存関係
* Java™ API JAR - AEM に対応した開発に使用できる、許可されたすべての Java™ API を公開する Java™ JAR／Maven 依存関係
* Javadoc JAR - Java™ API JAR の Javadoc

## AEM ヘッドレス SDK {#the-aem-headless-sdk}

AEM SDK とは異なり、AEM **ヘッドレス SDK** は、クライアントが HTTP 経由で AEM ヘッドレス API を素早く簡単に操作するために使用できるライブラリのセットです。

詳しくは、[AEM ヘッドレス SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=ja) を参照してください。

## その他の開発ツール {#additional-development-tools}

AEM SDK に加えて、コードとコンテンツのローカル開発およびテストを容易にする下記の追加ツールが必要です。

* Java™
* Git
* Apache Maven
* Node.js ライブラリ
* 任意の IDE

AEM は Java™ アプリケーションなので、AEM as a Cloud Service の開発をサポートするには、Java™ と Java™ SDK をインストールする必要があります。

Git は、ソースコントロールの管理、Cloud Manager への変更内容のチェックイン、さらにそれらを実稼動インスタンスにデプロイするために使用します。

AEM Maven プロジェクトアーキタイプから生成されたプロジェクトをビルドするために、AEM では Apache Maven を使用します。主要な IDE はすべて Maven との統合をサポートしています。

Node.js は、AEM プロジェクトの `ui.frontend` サブプロジェクトのフロントエンドアセットを操作するために使用される JavaScript ランタイム環境です。Node.js は npm と併せて配布され、JavaScript の依存関係の管理に使用される、事実上の Node.js パッケージマネージャーです。

## AEM システムのコンポーネントの概要 {#components-of-an-aem-system-at-a-glance}

 次に、AEM 環境の構成要素を見てみましょう。

完全な AEM 環境は、オーサー、パブリッシュ、Dispatcher で構成されます。運用開始前にコードおよびコンテンツをプレビューしやすくするために、これらと同じコンポーネントがローカル開発ランタイムで使用可能です。

* **オーサーサービス**&#x200B;では、内部ユーザーがコンテンツの作成、管理、プレビューを行います。

* **パブリッシュサービス**&#x200B;は「ライブ」環境と考えられ、通常はエンドユーザーがやり取りする相手になります。コンテンツは、オーサーサービスで編集および承認された後、パブリッシュサービスに配信されます。AEM ヘッドレスアプリケーションで最も一般的なデプロイメントパターンは、実稼動版のアプリケーションを AEM パブリッシュサービスに接続させることです。

* **Dispatcher** は、AEM Dispatcher モジュールで拡張された静的 web サーバーです。パブリッシュインスタンスで生成された Web ページをキャッシュしてパフォーマンスを向上します。

## ローカル開発ワークフロー {#the-local-development-workflow}

ローカル開発プロジェクトは Apache Maven をベースに構築され、ソース管理に Git を使用します。プロジェクトを更新するために、開発者は、Eclipse、Visual Studio Code、IntelliJ など、好みの統合開発環境を使用できます。

ヘッドレスアプリケーションによって取り込まれるコードまたはコンテンツのアップデートをテストするには、そのアップデートをローカルの AEM ランタイム（AEM オーサーサービスおよびパブリッシュサービスのローカルインスタンスを含む）にデプロイする必要があります。

アップデートが最も重要な場所でアップデートをテストすることが大切なので、ローカル AEM ランタイムの各コンポーネントの違いに注意してください。例えば、オーサーインスタンスでコンテンツのアップデートをテストしたり、パブリッシュインスタンスで新しいコードをテストしたりします。

実稼動システムでは、Dispatcher と HTTP Apache サーバーは常に AEM パブリッシュインスタンスの前に配置されます。これらは AEM システムのキャッシュサービスとセキュリティサービスを提供するので、Dispatcher に対してもコードとコンテンツのアップデートをテストすることが最も重要です。

## ローカル開発環境でのコードとコンテンツのローカルプレビュー {#previewing-your-code-and-content-locally-with-the-local-development-environment}

AEM ヘッドレスプロジェクトのローンチの準備をするには、プロジェクトの構成要素がすべて正常に機能していることを確認する必要があります。

それには、コード、コンテンツ、設定をすべて 1 つにまとめ、ローカル開発環境でテストして運用開始準備を行う必要があります。

ローカル開発環境は、次の 3 つの主な領域で構成されます。

1. AEM プロジェクト - このプロジェクトには、AEM 開発者の作業対象となるすべてのカスタムコード、設定およびコンテンツが含まれています
1. ローカル AEM ランタイム - AEM プロジェクトからコードをデプロイする際に使用される、AEM オーサーサービスおよびパブリッシュサービスのローカルバージョン
1. ローカル Dispatcher ランタイム - Dispatcher モジュールを含んだ Apache httpd Web サーバーのローカルバージョン。

ローカル開発環境をセットアップしたら、静的な Node サーバーをローカルにデプロイすることで、React アプリに対するコンテンツ提供をシミュレートできます。

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## 次のステップ {#whats-next}

これで、ここでの AEM ヘッドレスデベロッパージャーニーは完了です。次ができるようになったはずです。

* AEM 開発ツールの詳細
* ローカル開発ワークフローについて

次に、[ヘッドレスアプリケーションを運用する方法](/help/journey-headless/developer/go-live.md)のドキュメントを確認し、AEM ヘッドレスプロジェクトを実際に運用して、AEM ヘッドレスジャーニーを続けてください。

## その他のリソース {#additional-resources}

* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [ローカル AEM 環境のセットアップ](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=ja)
* [クライアントサイドブラウザー用 AEM ヘッドレス SDK（JavaScript）](https://github.com/adobe/aem-headless-client-js)
* [サーバーサイド／Node.js（JavaScript）用 AEM ヘッドレス SDK](https://github.com/adobe/aem-headless-client-nodejs)
* [Java™ 用 AEM ヘッドレス SDK](https://github.com/adobe/aem-headless-client-java)
* [ヘッドレス CMS としての AEM の概要](/help/headless/introduction.md)
* [AEM 開発者ポータル](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)
* [AEM のヘッドレスに関するチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ja)
