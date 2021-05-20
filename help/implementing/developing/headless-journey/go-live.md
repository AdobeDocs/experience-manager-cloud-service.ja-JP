---
title: ヘッドレスアプリケーションの運用開始方法
description: AEMヘッドレス開発者ジャーニーのこのパートでは、ローカルコードをGitに取り込み、CI/CDパイプライン用にCloud Manager Gitに移動することで、ヘッドレスアプリケーションをライブデプロイする方法を説明します。
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
source-git-commit: bc717c544bd4f0449d358b831a5132f85fa85e86
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 2%

---

# ヘッドレスアプリケーションでの運用開始方法{#go-live}

>[!CAUTION]
>
>古い — このドラフトコンテンツは、新しい[ヘッドレス開発者ジャーニードキュメントに置き換えられました。](/help/journey-headless/developer/overview.md)

[AEMヘッドレス開発者ジャーニー](overview.md)のこのパートでは、ヘッドレスアプリケーションをライブにデプロイする方法について説明します。そのためには、ローカルコードをGitで取得し、CI/CDパイプライン用にCloud Manager Gitに移動します。

## {#story-so-far}までの話

AEMヘッドレスジャーニーの前のドキュメント、[AEM Assets APIを使用したコンテンツの更新方法](update-your-content.md)では、APIを使用してAEMの既存のヘッドレスコンテンツを更新する方法を学習し、次の操作をおこなう必要があります。

* AEM Assets HTTP APIについて

この記事は、これらの基本事項に基づいて構築されるので、独自のAEMヘッドレスプロジェクトを運用に備える方法を理解できます。

## 目的 {#objective}

このドキュメントでは、AEMヘッドレス公開パイプラインと、アプリケーションの運用を開始する前に考慮する必要があるパフォーマンスに関する考慮事項について説明します。

* AEM SDKと必要な開発ツールについて説明します
* 本番運用開始前にローカル開発をシミュレートするコンテンツランタイムの設定
* AEMコンテンツのレプリケーションとキャッシュの基本について
* 起動前のアプリケーションのセキュリティ保護と拡張
* パフォーマンスとデバッグの問題の監視

## AEM SDK {#the-aem-sdk}

AEM SDKは、カスタムコードの作成とデプロイに使用されます。 運用を開始する前にヘッドレスアプリケーションを開発およびテストするために必要な主なツールです。 次のアーティファクトが含まれます。

* クイックスタートjar — オーサーインスタンスとパブリッシュインスタンスの両方を設定するために使用できる実行可能なjarファイル
* Dispatcherツール — WindowsおよびUNIXベースのシステム用のDispatcherモジュールとその依存関係
* Java API JAR - AEMに対する開発に使用できる、許可されたすべてのJava APIを公開するJava JAR/Maven依存関係
* Javadoc jar - Java API jarのJavadoc

## その他の開発ツール{#additional-development-tools}

AEM SDKに加えて、コードとコンテンツをローカルで開発およびテストするための追加ツールが必要になります。

* Java
* Git
* Apache Maven
* Node.jsライブラリ
* 選択したIDE

AEMはJavaCloud Serviceなので、AEM as a Applicationの開発をサポートするために、JavaとJava SDKをインストールする必要があります。

Gitは、ソース管理の管理や、Cloud Managerに対する変更のチェックイン、実稼動インスタンスへのデプロイに使用する機能です。

AEMは、AEM Mavenプロジェクトアーキタイプから生成されたプロジェクトを作成するためにApache Mavenを使用します。 主要なIDEはすべてMavenの統合サポートを提供します。

Node.jsは、AEMプロジェクトの`ui.frontend`サブプロジェクトのフロントエンドアセットを操作するために使用されるJavaScriptランタイム環境です。 Node.jsはnpmと共に配布され、JavaScriptの依存関係の管理に使用される事実上のNode.jsパッケージマネージャーです。

## AEMシステムのコンポーネントの概要{#components-of-an-aem-system-at-a-glance}

次に、AEM環境の構成要素を見てみましょう。

完全なAEM環境は、オーサー、パブリッシュ、ディスパッチャーで構成されます。 ライブにする前にコードとコンテンツを簡単にプレビューできるように、これらの同じコンポーネントがローカル開発ランタイムで使用可能になります。

* **Authorサービス** は、内部ユーザーがコンテンツを作成、管理、プレビューする場所です。

* **パブリッシュサ** ービスは「ライブ」環境と見なされ、通常はエンドユーザーがやり取りします。コンテンツは、編集されてAuthorサービスで適用された後、パブリッシュサービスに配布されます。 AEMヘッドレスアプリケーションで最も一般的なデプロイメントパターンは、実稼動版のアプリケーションをAEMパブリッシュサービスに接続させることです。

* **Dispatcherは** AEM Dispatcherモジュールで拡張された静的Webサーバーです。パブリッシュインスタンスで生成された Web ページをキャッシュしてパフォーマンスを向上します。

## ローカル開発ワークフロー{#the-local-development-workflow}

ローカル開発プロジェクトはApache Mavenを基に構築され、ソース管理にGitを使用しています。 プロジェクトを更新するために、開発者は、Eclipse、Visual Studio Code、IntelliJなど、好みの統合開発環境を使用できます。

ヘッドレスアプリケーションによって取り込まれるコードまたはコンテンツの更新をテストするには、AEMオーサーサービスとパブリッシュサービスのローカルインスタンスを含む、ローカルのAEMランタイムに更新をデプロイする必要があります。

最も重要な場所で更新をテストすることが重要なので、ローカルAEMランタイムの各コンポーネントの違いに注意してください。 例えば、オーサーインスタンスでコンテンツの更新をテストしたり、パブリッシュインスタンスで新しいコードをテストしたりします。

実稼動システムでは、DispatcherとHTTP Apacheサーバーは常にAEMパブリッシュインスタンスの前に配置されます。 AEMシステムのキャッシュとセキュリティサービスを提供するので、Dispatcherに対するコードとコンテンツの更新もテストすることが最も重要です。

## ローカル開発環境{#previewing-your-code-and-content-locally-with-the-local-development-environment}でのコードとコンテンツのローカルでのプレビュー

AEMヘッドレスプロジェクトを起動用に準備するには、プロジェクトの構成要素がすべて正常に機能していることを確認する必要があります。

それには、すべてをまとめる必要があります。コード、コンテンツ、設定を実稼動環境でテストし、ローカル開発環境で運用開始準備を行う。

ローカル開発環境は、次の3つの主な領域で構成されます。

1. AEMプロジェクト — AEM開発者が作業するすべてのカスタムコード、設定およびコンテンツが含まれます。
1. Local AEM Runtime - AEMプロジェクトからコードをデプロイする際に使用される、AEMオーサーサービスとパブリッシュサービスのローカルバージョン
1. Local Dispatcher Runtime - Dispatcherモジュールを含むApache httpd Webサーバーのローカルバージョン

ローカル開発環境を設定したら、静的なNodeサーバーをローカルにデプロイすることで、Reactアプリケーションに対するコンテンツサービングをシミュレートできます。

ローカル開発環境と、コンテンツのプレビューに必要なすべての依存関係の設定について詳しくは、[実稼動環境のデプロイメントに関するドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites)を参照してください。

## AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}の準備

次に、以下に示すベストプラクティスに従って、AEMヘッドレスアプリケーションを起動に備えます。

### 起動前のヘッドレスアプリケーションの保護と拡張{#secure-and-scale-before-launch}

1. GraphQLリクエストで[トークンベースの認証](/help/assets/content-fragments/graphql-authentication-content-fragments.md)を設定します
1. [キャッシュ](/help/implementing/dispatcher/caching.md)を設定します。

### モデル構造とGraphQL出力{#structure-vs-output}

* 15 kbを超えるJSON（gzip圧縮）を出力するクエリを作成しないでください。 長いJSONファイルは、クライアントアプリケーションが解析する際にリソースを集中的に消費します。
* フラグメント階層のネストされたレベルを5つ以上回避します。 レベルを増やすと、コンテンツ作成者は変更の影響を考慮するのが困難になります。
* モデル内の依存関係階層を持つクエリをモデリングする代わりに、複数オブジェクトクエリを使用します。 これにより、多くのコンテンツ変更を行うことなく、JSON出力を再構築する際に、より長期的な柔軟性を実現します。

### CDNキャッシュヒット率を最大化{#maximize-cdn}

* サーフェスからライブコンテンツをリクエストする場合を除き、直接GraphQLクエリを使用しないでください。
   * 可能な限り、永続化されたクエリを使用します。
   * CDNがキャッシュするために、CDNのTTL値を600秒を超える値に設定します。
   * AEMは、既存のクエリに対するモデルの変更の影響を計算できます。
* JSONファイル/GraphQLクエリを低コンテンツ変更率と高コンテンツ変更率の間で分割し、CDNへのクライアントトラフィックを減らし、より高いTTLを割り当てます。 これにより、CDNでのオリジンサーバーとのJSONの再検証が最小限に抑えられます。
* CDNからのコンテンツをアクティブに無効にするには、ソフトパージを使用します。 これにより、CDNは、キャッシュミスを引き起こすことなく、コンテンツを再ダウンロードできます。

### ヘッドレスコンテンツのダウンロード時間を短縮{#improve-download-time}

* HTTPクライアントがHTTP/2を使用していることを確認します。
* gzipに対するHTTPクライアントのAccept Headersリクエストを確認します。
* JSONおよび参照されるアーティファクトをホストするために使用するドメインの数を最小限に抑えます。
* `Last-modified-since`を利用してリソースを更新します。
* JSONファイルの`_reference`出力を使用すると、完全なJSONファイルを解析することなく、アセットのダウンロードを開始できます。

## 実稼動へのデプロイ {#deploy-to-production}

すべてのテストが完了し、正しく動作していることを確認したら、Cloud Managerの[一元化されたGitリポジトリにコードの更新をプッシュする準備が整います。](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)

更新内容がCloud Managerにアップロードされたら、[Cloud ManagerのCI/CDパイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=ja#how-to-use)を使用して、AEMにCloud Serviceとしてデプロイできます。

Cloud Manager CI/CDパイプラインを活用して、コードのデプロイを開始できます。このパイプラインについては、[ここ](/help/implementing/deploying/overview.md)で詳しく説明します。

## パフォーマンスの監視 {#performance-monitoring}

AEMヘッドレスアプリケーションを使用する際に、ユーザーが最高のエクスペリエンスを得るためには、次に説明するように、主要なパフォーマンス指標を監視することが重要です。

* アプリケーションのプレビューバージョンと実稼動バージョンの検証
* AEMステータスページで現在のサービス可用性ステータスを確認する
* パフォーマンスレポートへのアクセス
   * 配信パフォーマンス
      * CDN(Fastly)パフォーマンス — 呼び出し数、キャッシュレート、エラー率、ペイロードトラフィックを確認します。
      * オリジンサーバー — 呼び出し数、エラー率、CPU負荷、ペイロードトラフィック
   * 作成者のパフォーマンス
      * ユーザー数、リクエスト数、読み込み数の確認
* アプリケーションおよびSpace固有のパフォーマンスレポートへのアクセス
   * サーバーが稼働したら、一般的な指標が緑/オレンジ/赤かどうかを確認し、特定のアプリケーションの問題を特定します
   * 上記のレポートを開きますが、アプリケーションまたはスペース(Photoshopデスクトップ、ペイウォールなど)にフィルターします。
   * [SplunkログAPIを使用し](/help/implementing/developing/introduction/logging.md#splunk-logs) て、サービスとアプリケーションのパフォーマンスにアクセスする
   * その他の問題が発生した場合は、カスタマーサポートにお問い合わせください。

## トラブルシューティング {#troubleshooting}

### デバッグ {#debugging}

デバッグの一般的なアプローチとして、次のベストプラクティスに従います。

* アプリケーションのプレビューバージョンを使用した機能とパフォーマンスの検証
* 実稼動版のアプリケーションで機能とパフォーマンスを検証する
* コンテンツフラグメントエディターの[JSONプレビュー](/help/assets/content-fragments/content-fragments-json-preview.md)を使用して検証します。
* クライアントアプリケーションでJSONをInspectして、クライアントアプリケーションまたは配信の問題の有無を確認します。
* GraphQLを使用したJSONの確認(キャッシュされたコンテンツまたはAEMに関する問題の有無の確認)

### サポートを使用したバグのログ{#logging-a-bug-with-support}

サポートが必要な場合にサポートに関するバグを効率的に記録するには、次の手順に従います。

* 必要に応じて、問題のスクリーンショットを取る
* 問題の再現方法を文書化する
* 問題が再現するコンテンツを文書化する
* AEMサポートポータルで問題を特定のアプリケーションの優先度で記録する

## ジャーニーが終了するか、終了するか。{#journey-ends}

バリデーターがAEMヘッドレス開発者ジャーニーが完了しました。 これで、次の内容について理解できるはずです。

* ヘッドレスコンテンツ配信とヘッドフルコンテンツ配信の違い。
* AEMヘッドレス機能
* ヘッドレスプロジェクトの整理とAEMの方法。
* AEMでヘッドレスコンテンツを作成する方法。
* AEMでヘッドレスコンテンツを取得して更新する方法。
* AEMヘッドレスプロジェクトの運用方法。
* 運用開始後の作業

## その他のリソース {#additional-resources}

* [AEM as aCloud Serviceへのデプロイの概要](/help/implementing/deploying/overview.md)
* [AEM as a Cloud Service の SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [ローカルAEM環境の設定](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [Cloud Managerを使用したコードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Cloud Manager Gitリポジトリを外部Gitリポジトリと統合し、プロジェクトをAEMにCloud Serviceとしてデプロイします](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)