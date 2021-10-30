---
title: ヘッドレスアプリケーションの運用開始方法
description: AEM ヘッドレスデベロッパージャーニーのこのパートでは、Git 内のローカルコードを CI／CD パイプライン用に Cloud Manager Git に移行することでヘッドレスアプリケーションをライブ環境にデプロイする方法を説明します。
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 4a5967f682d122d20528b1d904590fb82f438fa7
workflow-type: ht
source-wordcount: '1907'
ht-degree: 100%

---

# ヘッドレスアプリケーションの運用開始方法 {#go-live}

[AEM ヘッドレスデベロッパージャーニー](overview.md)のこのパートでは、Git 内のローカルコードを CI／CD パイプライン用に Cloud Manager Git に移行することでヘッドレスアプリケーションをライブ環境にデプロイする方法を説明します。

## これまでの説明内容 {#story-so-far}

AEM ヘッドレスジャーニーの前のドキュメント [AEM Assets API を使用してコンテンツを更新する方法](update-your-content.md)では、API を使用して AEM の既存のヘッドレスコンテンツを更新する方法を説明し、以下を達成できました。

* AEM Assets HTTP API を理解する

この記事は、これらの基本事項に基づいているので、独自の AEM ヘッドレスプロジェクトの運用開始準備をする方法を理解できます。

## 目的 {#objective}

このドキュメントは、AEM ヘッドレス公開パイプラインと、アプリケーションの運用を開始する前に認識しておく必要があるパフォーマンスに関する考慮事項を理解するうえで役に立ちます。

* AEM SDK と必要な開発ツールの把握
* 運用開始前にコンテンツをシミュレートするためのローカル開発ランタイムのセットアップ
* AEM のコンテンツのレプリケーションとキャッシュに関する基本事項の理解
* ローンチ前のアプリケーションのセキュリティ確保とスケーリング
* パフォーマンスとデバッグの問題の監視

## AEM SDK {#the-aem-sdk}

AEM SDK は、カスタムコードのビルドとデプロイに使用されます。これは、ヘッドレスアプリケーションを開発し運用開始前にテストするために必要な主なツールです。次のアーティファクトで構成されます。

* クイックスタート JAR - オーサーインスタンスとパブリッシュインスタンスの両方をセットアップするために使用できる実行可能な JAR ファイル
* Dispatcher ツール - Windows および UNIX ベースシステム用の Dispatcher モジュールとその依存関係
* Java API JAR - AEM に対応した開発に使用できる、許可されたすべての Java API を公開する Java JAR／Maven 依存関係
* Javadoc JAR - Java API JAR の Javadoc

## その他の開発ツール {#additional-development-tools}

AEM SDK に加えて、コードとコンテンツのローカル開発およびテストを容易にする下記の追加ツールが必要になります。

* Java
* Git
* Apache Maven
* Node.js ライブラリ
* 任意の IDE

AEM は Java アプリケーションなので、AEM as a Cloud Service の開発をサポートするには、Java と Java SDK をインストールする必要があります。

ソース管理、および変更内容の Cloud Manager へのチェックインと実稼動インスタンスへのデプロイには、Git を使用します。

AEM Maven プロジェクトアーキタイプから生成されたプロジェクトをビルドするために、AEM では Apache Maven を使用します。主要な IDE はすべて Maven との統合をサポートしています。

Node.js は、AEM プロジェクトの `ui.frontend` サブプロジェクトのフロントエンドアセットを操作するために使用される JavaScript ランタイム環境です。Node.js は npm と一緒に配布され、JavaScript の依存関係の管理に使用される事実上の Node.js パッケージマネージャーとなっています。

## AEM システムのコンポーネントの概要 {#components-of-an-aem-system-at-a-glance}

次に、AEM 環境の構成要素を見てみましょう。

完全な AEM 環境は、オーサー、パブリッシュ、ディスパッチャーで構成されます。運用開始前にコードとコンテンツをプレビューしやすくするために、これらと同じコンポーネントがローカル開発ランタイムで使用可能になります。

* **オーサーサービス**&#x200B;では、内部ユーザーがコンテンツの作成、管理、プレビューを行います。

* **パブリッシュサービス**&#x200B;は「ライブ」環境と考えられ、通常はエンドユーザーがやり取りする相手になります。コンテンツは、オーサーサービスで編集および承認された後、パブリッシュサービスに配信されます。AEM ヘッドレスアプリケーションで最も一般的なデプロイメントパターンは、実稼動版のアプリケーションを AEM パブリッシュサービスに接続させることです。

* **ディスパッチャー**&#x200B;は、AEM Dispatcher モジュールで拡張された静的 Web サーバーです。パブリッシュインスタンスで生成された Web ページをキャッシュしてパフォーマンスを向上します。

## ローカル開発ワークフロー {#the-local-development-workflow}

ローカル開発プロジェクトは Apache Maven をベースに構築され、ソース管理に Git を使用します。プロジェクトを更新するために、開発者は、Eclipse、Visual Studio Code、IntelliJ など、好みの統合開発環境を使用できます。

ヘッドレスアプリケーションによって取り込まれるコードまたはコンテンツのアップデートをテストするには、そのアップデートをローカルの AEM ランタイム（AEM オーサーサービスおよびパブリッシュサービスのローカルインスタンスを含む）にデプロイする必要があります。

アップデートが最も重要な場所でアップデートをテストすることが大切なので、ローカル AEM ランタイムの各コンポーネントの違いに注意してください。例えば、オーサーインスタンスでコンテンツのアップデートをテストしたり、パブリッシュインスタンスで新しいコードをテストしたりします。

実稼動システムでは、ディスパッチャーと HTTP Apache サーバーは常に AEM パブリッシュインスタンスの前に配置されます。これらは AEM システムのキャッシュサービスとセキュリティサービスを提供するので、ディスパッチャーに対してもコードとコンテンツのアップデートをテストすることが最も重要です。

## ローカル開発環境でのコードとコンテンツのローカルプレビュー {#previewing-your-code-and-content-locally-with-the-local-development-environment}

AEM ヘッドレスプロジェクトのローンチの準備をするには、プロジェクトの構成要素がすべて正常に機能していることを確認する必要があります。

それには、コード、コンテンツ、設定をすべて 1 つにまとめ、ローカル開発環境でテストして運用開始準備を行う必要があります。

ローカル開発環境は、次の 3 つの主な領域で構成されます。

1. AEM プロジェクト - AEM 開発者の作業対象となるすべてのカスタムコード、設定およびコンテンツが含まれます。
1. ローカル AEM ランタイム - AEM プロジェクトからコードをデプロイする際に使用される、AEM オーサーサービスおよびパブリッシュサービスのローカルバージョン。
1. ローカル Dispatcher ランタイム - Dispatcher モジュールを含んだ Apache httpd Web サーバーのローカルバージョン。

ローカル開発環境をセットアップしたら、静的な Node サーバーをローカルにデプロイすることで、React アプリに対するコンテンツ提供をシミュレートできます。

ローカル開発環境のセットアップと、コンテンツのプレビューに必要なすべての依存関係について詳しくは、[実稼働デプロイメントのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=ja#prerequisites)を参照してください。

## AEM ヘッドレスアプリケーションの運用開始準備 {#prepare-your-aem-headless-application-for-golive}

それではいよいよ、以下に示すベストプラクティスに従って、AEM ヘッドレスアプリケーションのローンチの準備を行います。

### ローンチ前のヘッドレスアプリケーションのセキュリティ確保とスケーリング {#secure-and-scale-before-launch}

1. GraphQL リクエストに[トークンベースの認証](/help/assets/content-fragments/graphql-authentication-content-fragments.md)を設定します。
1. [キャッシュ](/help/implementing/dispatcher/caching.md)を設定します。

### モデル構造と GraphQL 出力 {#structure-vs-output}

* 15 KB を超える JSON コード（gzip で圧縮）を出力するクエリを作成しないようにします。長い JSON ファイルの場合、クライアントアプリケーションで解析する際に大量のリソースを消費します。
* フラグメント階層のネストレベルは 5 以内にします。レベルを増やすと、コンテンツ作成者は変更の影響を考慮しにくくなります。
* モデル内の依存関係階層を使用したクエリをモデル化するのではなく、複数オブジェクトクエリを使用します。これにより、多数のコンテンツ変更を行わなくても、より長期にわたって柔軟に JSON 出力を再構成できます。

### CDN キャッシュヒット率の最大化 {#maximize-cdn}

* サーフェスからライブコンテンツをリクエストする場合を除き、直接の GraphQL クエリは使用しません。
   * 可能な限り、永続的クエリを使用します。
   * これらのクエリを CDN でキャッシュするために、CDN の TTL 値を 600 秒以上に設定します。
   * AEM は既存のクエリに対するモデル変更の影響を計算できます。
* CDN へのクライアントトラフィックを減らし、より高い TTL を割り当てるため、JSON ファイル／GraphQL クエリをコンテンツ変更率の低いものと高いものに分けます。これにより、CDN でのオリジンサーバーに対する JSON の再検証が最小限に抑えられます。
* CDN からコンテンツを能動的に無効にするには、ソフトパージを使用します。これにより、CDN は、キャッシュミスを引き起こすことなくコンテンツを再ダウンロードできます。

### ヘッドレスコンテンツのダウンロード時間の短縮 {#improve-download-time}

* HTTP クライアントで必ず HTTP/2 を使用します。
* HTTP クライアントで gzip に対するリクエストには必ず Accept ヘッダーを付けます。
* JSON および参照先アーティファクトをホストするために使用するドメインの数を最小限に抑えます。
* `Last-modified-since` を利用してリソースを更新します。
* JSON ファイルで `_reference` 出力を使用すると、完全な JSON ファイルを解析しなくても、アセットのダウンロードを開始できます。

## 実稼動へのデプロイ {#deploy-to-production}

すべてがテストされ、正しく動作していることを確認したら、[Cloud Manager に一元化されている Git リポジトリー](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=ja)にコードのアップデートをプッシュする準備が整います。

アップデートが Cloud Manager にアップロードされたら、[Cloud Managerの CI／CD パイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=ja#how-to-use)を使用して、アップデートを AEM as a Cloud Service にデプロイできます。

コードのデプロイを開始するには、Cloud Manager CI／CD パイプラインを利用します。このパイプラインについて詳しくは、[こちら](/help/implementing/deploying/overview.md)を参照してください。

## パフォーマンスの監視 {#performance-monitoring}

AEM ヘッドレスアプリケーションの使用時に最高のユーザーエクスペリエンスを得るためには、以下に説明するように、主要パフォーマンス指標を監視することが重要です。

* アプリのプレビューバージョンと実稼動バージョンの動作を検証する
* AEM ステータスページで現在のサービス稼働状況を確認する
* パフォーマンスレポートにアクセスする
   * 配信のパフォーマンス
      * CDN（Fastly）パフォーマンス - 呼び出し数、キャッシュ率、エラー率、ペイロードトラフィックを確認する
      * オリジンサーバー - 呼び出し数、エラー率、CPU 負荷、ペイロードトラフィックを確認する
   * オーサーのパフォーマンス
      * ユーザー数、リクエスト数、読み込み数を確認する
* アプリおよびスペース固有のパフォーマンスレポートにアクセスする
   * サーバーが起動したら、一般的な指標が緑／オレンジ／赤のどれになっているかを確認し、アプリの具体的な問題を特定する
   * 特定のアプリやスペース（例：Photoshop デスクトップ、ペイウォール）に限定した上記レポートを開く
   * Splunk ログ API を使用してサービスやアプリケーションのパフォーマンスにアクセスする
   * その他の問題が発生した場合は、カスタマーサポートに連絡する

## トラブルシューティング {#troubleshooting}

### デバッグ {#debugging}

デバッグに対する一般的なアプローチとして、次のベストプラクティスに従います。

* アプリケーションのプレビューバージョンで機能とパフォーマンスを検証する
* アプリケーションの実稼動バージョンで機能とパフォーマンスを検証する
* コンテンツフラグメントエディターの JSON プレビューを使用して検証する
* クライアントアプリケーションで JSON を調べて、クライアントアプリケーションや配信の問題の有無を確認する
* GraphQL を使用して JSON を調べ、キャッシュされたコンテンツまたは AEM に関係する問題の有無を確認する

### サポートへのバグの登録 {#logging-a-bug-with-support}

さらにサポートが必要な場合に備えてサポートにバグを効率的に登録するには、次の手順に従います。

* 必要に応じて、問題のスクリーンショットを撮る
* 問題の再現方法を説明する
* 問題が再現するコンテンツを説明する
* AEM サポートポータルを通じて問題を適切な優先度で登録する

## ジャーニーの完了  {#journey-ends}

おめでとうございます。AEM ヘッドレスデベロッパージャーニーが完了し、以下を理解できました。

* ヘッドレスコンテンツ配信とヘッドフルコンテンツ配信の違い
* AEM のヘッドレス機能
* AEM ヘッドレスプロジェクトを編成する方法
* AEM でヘッドレスコンテンツを作成する方法
* AEM でヘッドレスコンテンツを取得および更新する方法
* AEM ヘッドレスプロジェクトの運用を開始する方法
* 運用開始後の作業

皆さんは初めての AEM ヘッドレスプロジェクトの運用を既に開始したかもしれませんし、そうでなくても、そのために必要な知識はすべて習得したことになります。お疲れ様でした。

### 単一ページアプリケーションの調査 {#explore-spa}

ただし、AEM のヘッドレスストアは、ここで終わる必要はありません。[ジャーニーの「はじめに」のパート](getting-started.md#integration-levels)では、AEM でヘッドレス配信と従来のフルスタックモデルをサポートできるだけでなく、両方の利点を組み合わせたハイブリッドモデルもサポートできることを簡単に説明しました。

このような柔軟性がプロジェクトに必要な場合は、さらにジャーニーのオプションパート [AEM で単一ページアプリケーション（SPA）を作成する方法](create-spa.md)に進んでください。

## その他のリソース {#additional-resources}

* [AEM as a Cloud Service へのデプロイの概要](/help/implementing/deploying/overview.md)
* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [ローカル AEM 環境のセットアップ](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=ja)
* [Cloud Manager を使用したコードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=ja#how-to-use)
* [Cloud Manager Git リポジトリーと外部 Git リポジトリーの統合および AEM as a Cloud Service へのプロジェクトのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=ja)
