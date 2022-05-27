---
title: すべてをまとめる方法 - AEM ヘッドレスのアプリとコンテンツ
description: AEM ヘッドレスデベロッパージャーニーのこの部分では、コンテンツフラグメント、GraphQL 呼び出し、REST API 呼び出し、アプリケーションを含む AEM プロジェクトを実行し、運用開始に備える方法を説明します。
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 53%

---

# すべてをまとめる方法 - AEM ヘッドレスのアプリとコンテンツ {#put-it-all-together}

この部分では、 [AEMヘッドレス開発者ジャーニー](overview.md)を使用すると、AEM開発ツールとヘッドレス SDK を使用してアプリケーションを統合する方法を理解できます。

## これまでの説明内容 {#story-so-far}

AEM ヘッドレスジャーニーの前のドキュメント [AEM Assets API を使用してコンテンツを更新する方法](update-your-content.md)では、API を使用して AEM の既存のヘッドレスコンテンツを更新する方法を説明し、以下を達成できました。

* AEM Assets HTTP API を理解する

## 目的 {#objective}

この記事では、次の方法でAEMヘッドレスアプリケーションを組み立てる方法を説明します。

* AEMヘッドレス SDK と必要な開発ツールについて
* 運用開始前にローカル開発をシミュレートするためのコンテンツランタイムの設定
* AEMコンテンツレプリケーションの基本について

## AEM SDK {#the-aem-sdk}

AEM SDK は、カスタムコードのビルドとデプロイに使用されます。本番運用を開始する前にヘッドレスアプリケーションを開発およびテストするために必要な主なツールです。 次のアーティファクトで構成されます。

* クイックスタート JAR - オーサーインスタンスとパブリッシュインスタンスの両方をセットアップするために使用できる実行可能な JAR ファイル
* Dispatcher ツール — Windows および UNIX®ベースのシステム用の Dispatcher モジュールとその依存関係
* Java™ API Jar - AEMに対応した開発に使用できる、許可されたすべての Java™ API を公開する Java™ Jar/Maven 依存関係
* Javadoc jar - Java™ API jar の Javadoc

## AEMヘッドレス SDK {#the-aem-headless-sdk}

AEM SDK とは異なり、AEM **ヘッドレス SDK** は、クライアントが HTTP 経由でAEMヘッドレス API をすばやく簡単に操作するために使用できるライブラリのセットです。

AEMヘッドレス SDK について詳しくは、 [ドキュメントはこちら](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/how-to/aem-headless-sdk.html?lang=en).

## その他の開発ツール {#additional-development-tools}

AEM SDK の他に、コードやコンテンツをローカルで開発およびテストするための追加のツールが必要になります。

* Java™
* Git
* Apache Maven
* Node.js ライブラリ
* 任意の IDE

AEMは Java™アプリケーションなので、AEM as a Cloud Serviceの開発をサポートするために、Java™と Java™ SDK をインストールする必要があります。

Git は、ソース管理の管理や Cloud Manager への変更のチェックイン、実稼動インスタンスへのデプロイに使用するものです。

AEMは、Apache Maven を使用して、AEM Maven プロジェクトアーキタイプから生成されたプロジェクトを構築します。 主要な IDE はすべて Maven との統合をサポートしています。

Node.js は、AEM プロジェクトの `ui.frontend` サブプロジェクトのフロントエンドアセットを操作するために使用される JavaScript ランタイム環境です。Node.js は npm と一緒に配布され、JavaScript の依存関係の管理に使用される事実上の Node.js パッケージマネージャーとなっています。

## AEM システムのコンポーネントの概要 {#components-of-an-aem-system-at-a-glance}

次に、AEM 環境の構成要素を見てみましょう。

完全な AEM 環境は、オーサー、パブリッシュ、ディスパッチャーで構成されます。運用を開始する前にコードとコンテンツを簡単にプレビューできるように、ローカル開発ランタイムでも同じコンポーネントを使用できるようになりました。

* **オーサーサービス**&#x200B;では、内部ユーザーがコンテンツの作成、管理、プレビューを行います。

* **パブリッシュサービス**&#x200B;は「ライブ」環境と考えられ、通常はエンドユーザーがやり取りする相手になります。コンテンツは、オーサーサービスで編集および承認された後、パブリッシュサービスに配信されます。AEM ヘッドレスアプリケーションで最も一般的なデプロイメントパターンは、実稼動版のアプリケーションを AEM パブリッシュサービスに接続させることです。

* **Dispatcher** は、AEM Dispatcher モジュールで拡張された静的 Web サーバーです。 パブリッシュインスタンスで生成された Web ページをキャッシュしてパフォーマンスを向上します。

## ローカル開発ワークフロー {#the-local-development-workflow}

ローカル開発プロジェクトは Apache Maven をベースに構築され、ソース管理に Git を使用します。プロジェクトを更新するために、開発者は、Eclipse、Visual Studio Code、IntelliJ など、望ましい統合開発環境を使用できます。

ヘッドレスアプリケーションによって取り込まれるコードやコンテンツの更新をテストするには、AEMオーサーサービスとパブリッシュサービスのローカルインスタンスを含む、ローカルAEMランタイムに更新をデプロイする必要があります。

アップデートが最も重要な場所でアップデートをテストすることが大切なので、ローカル AEM ランタイムの各コンポーネントの違いに注意してください。例えば、オーサーインスタンスでコンテンツのアップデートをテストしたり、パブリッシュインスタンスで新しいコードをテストしたりします。

実稼働システムでは、Dispatcher と HTTP Apache サーバーは常にAEMパブリッシュインスタンスの前に配置されます。 AEMシステムのキャッシュとセキュリティサービスを提供するので、Dispatcher に対するコードおよびコンテンツの更新も最も適切にテストします。

## ローカル開発環境でのコードとコンテンツのローカルプレビュー {#previewing-your-code-and-content-locally-with-the-local-development-environment}

AEM ヘッドレスプロジェクトのローンチの準備をするには、プロジェクトの構成要素がすべて正常に機能していることを確認する必要があります。

それには、すべてをまとめる必要があります。コード、コンテンツ、設定をテストし、運用開始準備をローカル開発するための環境でテストします。

ローカル開発環境は、次の 3 つの主な領域で構成されます。

1. AEM プロジェクト - AEM 開発者の作業対象となるすべてのカスタムコード、設定およびコンテンツが含まれます。
1. ローカル AEM ランタイム - AEM プロジェクトからコードをデプロイする際に使用される、AEM オーサーサービスおよびパブリッシュサービスのローカルバージョン。
1. ローカル Dispatcher ランタイム - Dispatcher モジュールを含んだ Apache httpd Web サーバーのローカルバージョン。

ローカル開発環境をセットアップしたら、静的な Node サーバーをローカルにデプロイすることで、React アプリに対するコンテンツ提供をシミュレートできます。

コンテンツのプレビューに必要なローカル開発環境とすべての依存関係の設定について詳しくは、 [実稼動デプロイメントドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=ja#prerequisites).

## 次のステップ {#whats-next}

これで、ここでの AEM ヘッドレスデベロッパージャーニーは完了です。次ができるようになったはずです。

* AEM Development Tools の詳細
* ローカル開発ワークフロー

次に、「[実際に AEM ヘッドレスプロジェクトをライブにする方法](/help/journey-headless/developer/go-live.md)」のドキュメントを確認して、AEM ヘッドレスジャーニーを続けてください。

## その他のリソース {#additional-resources}

* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [ローカル AEM 環境のセットアップ](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=ja)
* [クライアント側ブラウザー用のAEMヘッドレス SDK(JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [AEMヘッドレス SDK for server-side/Node.js (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [AEM Headless SDK for Java™](https://github.com/adobe/aem-headless-client-java)

