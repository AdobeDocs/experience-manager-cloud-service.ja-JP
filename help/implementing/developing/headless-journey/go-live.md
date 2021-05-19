---
title: ヘッドレスアプリケーションの使い方
description: AEMヘッドレス開発者ジャーニーのこの部分では、ローカルコードをGitに取り込み、CI/CDパイプライン用にCloud Manager Gitに移動して、ヘッドレスアプリケーションをライブにデプロイする方法を説明します。
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
source-git-commit: 7c30a7415cc424e7f417d92bad9eeb01877994d2
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 2%

---

# ヘッドレスアプリケーションの使い方{#go-live}

>[!CAUTION]
>
>作業中 — このドキュメントの作成は現在進行中で、完全なもの、最終的なもの、または実稼働目的で使用するものとして理解してはなりません。

[AEM Headless Developerジャーニー](overview.md)のこの部分では、ヘッドレスアプリケーションをライブにデプロイする方法を学びます。ここでは、ローカルコードをGitに取り込み、CI/CDパイプライン用にCloud Manager Gitに移動します。

## {#story-so-far}

以前のドキュメントのAEM headlessジャーニーでは、[AEM AssetsAPIを使用したコンテンツの更新方法](update-your-content.md)で、AEMの既存のheadlessコンテンツを更新する方法を学びました。今後は、次の操作を行う必要があります。

* AEM AssetsHTTP APIについて説明します。

この記事は、これらの基本事項に基づいて構築されているので、独自のAEMヘッドレスプロジェクトを実稼動に備える方法を理解しています。

## 目的 {#objective}

このドキュメントは、AEMヘッドレスパブリケーションのパイプラインと、アプリケーションの運用に当たる前に注意が必要なパフォーマンス上の考慮事項を理解するのに役立ちます。

* AEM SDKと必要な開発ツールについて説明します。
* ローカル開発ランタイムを設定して、本番運用開始前にコンテンツをシミュレートします。
* AEMコンテンツのレプリケーションとキャッシュの基本について
* 起動前のアプリケーションのセキュリティと拡張
* パフォーマンスとデバッグの問題の監視

## AEM SDK {#the-aem-sdk}

AEM SDKは、カスタムコードを構築しデプロイするために使用します。 これは、運用を開始する前にヘッドレスアプリケーションを開発し、テストするために必要な主なツールです。 次のアーティファクトが含まれます。

* Quickstart jar — 作成者インスタンスと発行インスタンスの両方を設定するのに使用できる実行可能なjarファイル
* ディスパッチャーツール — WindowsおよびUNIXベースのシステムのディスパッチャーモジュールとその依存関係
* Java API Jar - AEMに対する開発に使用できる、許可されているすべてのJava APIを公開するJava Jar/Maven依存関係
* Javadoc jar - Java API jarのjavadoc

## その他の開発ツール{#additional-development-tools}

AEM SDKに加えて、コードとコンテンツをローカルで開発およびテストするための追加ツールが必要になります。

* Java
* Git
* Apache Maven
* Node.jsライブラリ
* 選択したIDE

AEMはJavaアプリケーションなので、AEMをCloud Serviceとして開発するためには、JavaとJava SDKをインストールする必要があります。

Gitは、ソース管理の管理、Cloud Managerへの変更のチェックイン、実稼働インスタンスへの展開に使用するものです。

AEMでは、AEM Mavenプロジェクトアーキタイプから生成されたプロジェクトを作成する際にApache Mavenを使用します。 主要なIDEはすべてMavenの統合サポートを提供します。

Node.jsは、AEMプロジェクトの`ui.frontend`サブプロジェクトのフロントエンドアセットを操作するために使用されるJavaScriptランタイム環境です。 Node.jsはnpmと共に配布され、JavaScriptの依存関係を管理するために使用される、事実上のNode.jsパッケージマネージャーです。

## AEMシステムのコンポーネントの概要{#components-of-an-aem-system-at-a-glance}

次に、AEM環境の構成要素を見てみましょう。

完全なAEM環境は、作成者、発行、およびディスパッチャーで構成されます。 ライブにする前に、コードとコンテンツのプレビューを簡単にするために、これらの同じコンポーネントをローカル開発ランタイムで使用できるようになります。

* **Author** サービスでは、内部ユーザーがコンテンツを作成、管理、プレビューします。

* **発行** サービスは「ライブ」環境と見なされ、通常はエンドユーザーが操作します。コンテンツは、Authorサービスで編集および承認された後、Publishサービスに配信されます。 AEMヘッドレスアプリケーションで最も一般的なデプロイメントパターンは、実稼働版のアプリケーションをAEM Publishサービスに接続させることです。

* **ディス** パッチャーは、AEMディスパッチャーモジュールで拡張された静的なWebサーバーです。パブリッシュインスタンスで生成された Web ページをキャッシュしてパフォーマンスを向上します。

## ローカル開発ワークフロー{#the-local-development-workflow}

ローカル開発プロジェクトはApache Mavenを基に構築されており、ソース管理にGitを使用しています。 プロジェクトを更新するために、開発者はEclipse、Visual Studio Code、IntelliJなどの望ましい統合開発環境を使用できます。

ヘッドレスアプリケーションで取り込まれるコードまたはコンテンツの更新をテストするには、AEM作成者のローカルインスタンスと発行サービスを含むローカルAEMランタイムに更新を展開する必要があります。

アップデートが最も重要な場所でテストすることが重要なので、ローカルAEMランタイムの各コンポーネント間の違いを必ず書き留めてください。 例えば、作成者でコンテンツの更新をテストしたり、発行インスタンスで新しいコードをテストしたりします。

実稼働システムでは、ディスパッチャーとhttp Apacheサーバーは、常にAEM発行インスタンスの前に配置されます。 また、AEMシステムのキャッシュおよびセキュリティサービスを提供するので、ディスパッチャーに対してコードおよびコンテンツの更新をテストすることもお勧めします。

## ローカル開発環境{#previewing-your-code-and-content-locally-with-the-local-development-environment}を使用したコードとコンテンツのローカルプレビュー

AEMヘッドレスプロジェクトを起動用に準備するには、プロジェクトの構成要素がすべて正常に機能していることを確認する必要があります。

そのためには、すべてをまとめる必要があります。コード、コンテンツ、設定を行い、ローカル開発環境でテストして、運用準備を実現します。

ローカル開発環境は、

1. AEMプロジェクト —AEM開発者が作業するすべてのカスタムコード、設定、コンテンツが含まれます。
1. Local AEM Runtime - AEMプロジェクトからコードをデプロイするために使用されるAEM作成者サービスおよび発行サービスのローカルバージョン
1. Local Dispatcher Runtime - Dispatcherモジュールを含むApache httpd Webサーバーのローカルバージョンです。

ローカル開発環境を設定したら、静的なノードサーバーをローカルにデプロイすることで、Reactアプリに対するコンテンツサービングをシミュレートできます。

ローカル開発環境の設定と、コンテンツプレビューに必要なすべての依存関係について詳しく調べるには、[実稼働環境の導入ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites)を参照してください。

## AEM Go-Live用ヘッドレスアプリケーションの準備{#prepare-your-aem-headless-application-for-golive}

次に示すベストプラクティスに従って、AEMのヘッドレスアプリケーションを起動できる状態にします。

### {#secure-and-scale-before-launch}を起動する前にヘッドレスアプリケーションを保護し、拡張する

1. GraphQLリクエストで[トークンベースの認証](/help/assets/content-fragments/graphql-authentication-content-fragments.md)を設定
1. [キャッシュ](/help/implementing/dispatcher/caching.md)を構成します。

### モデル構造とGraphQL出力{#structure-vs-output}

* 15 KBを超えるJSON（gzip圧縮）を出力するクエリは作成しないでください。 長いJSONファイルは、クライアントアプリケーションが解析する際にリソースを大量に消費します。
* 5つ以上の階層化されたフラグメント階層を避けます。 レベルが上がると、コンテンツ作成者は変更の影響を考慮するのが困難になります。
* モデル内の依存関係クエリを持つクエリをモデリングする代わりに、マルチオブジェクト階層を使用します。 これにより、多くのコンテンツの変更を行うことなく、JSON出力を再構築できる柔軟性が長期にわたって高まります。

### CDNキャッシュヒット率の最大化{#maximize-cdn}

* サーフェスからライブコンテンツをリクエストする場合を除き、直接GraphQLクエリを使用しないでください。
   * 持続的なクエリは可能な限り使用してください。
   * CDNがキャッシュするCDNのTTLを600秒以上にします。
   * AEMでは、既存のクエリに対するモデル変更の影響を計算できます。
* JSONファイル/GraphQLクエリを低コンテンツ変更率と高コンテンツ変更率の間で分割し、CDNへのクライアントトラフィックを減らし、より高いTTLを割り当てます。 これにより、接触チャネルサーバーでJSONを再検証するCDNが最小化されます。
* CDNからコンテンツをアクティブに無効にするには、「ソフトパージ」を使用します。 これにより、CDNは、キャッシュミスを招くことなく、コンテンツを再ダウンロードできます。

### ヘッドレスコンテンツのダウンロード時間の短縮{#improve-download-time}

* HTTPクライアントがHTTP/2を使用していることを確認します。
* HTTPクライアントがgzipに対するヘッダ要求を受け入れることを確認します。
* JSONおよび参照されるアーティファクトをホストするために使用されるドメインの数を最小限に抑えます。
* `Last-modified-since`を利用してリソースを更新します。
* 完全なJSONファイルを解析することなく、JSONファイル内の`_reference`出力を使用して、開始によるアセットのダウンロードを行う。

## 実稼動へのデプロイ {#deploy-to-production}

すべての動作がテスト済みで正常に動作していることを確認したら、Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)の[中央管理されたGitリポジトリにコードの更新をプッシュする準備が整います。

アップデートがCloud Managerにアップロードされた後、[Cloud ManagerのCI/CDパイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=ja#how-to-use)を使用して、AEMにCloud Serviceーとして展開できます。

Cloud ManagerのCI/CDパイプラインを活用して、コードの展開を開始できます。このパイプラインについては、[ここ](/help/implementing/deploying/overview.md)で詳しく説明しています。

## パフォーマンスの監視 {#performance-monitoring}

AEMヘッドレスアプリケーションを使用する場合、ユーザーが最高のエクスペリエンスを得られるようにするには、主要なパフォーマンス指標を以下に示すように監視することが重要です。

* アプリのプレビュー版と実稼働版を検証する
* 現在のサービスの可用性の状態に関するAEMステータスページの確認
* パフォーマンスレポートへのアクセス
   * 配信パフォーマンス
      * CDN(Fastly)パフォーマンス — 呼び出し数、キャッシュ率、エラー率、ペイロードトラフィックの確認
      * 接触チャネルサーバ — 呼び出し数、エラー率、CPU負荷、ペイロードトラフィック
   * 発言者の実績
      * ユーザー数、要求数、読み込み数の確認
* AppおよびSpace固有のパフォーマンスレポートへのアクセス
   * サーバーが起動したら、一般的な指標が緑/オレンジ/赤かどうかを確認し、特定のアプリの問題を特定します。
   * 上記と同じレポートを開き、アプリまたはスペースにフィルタリング(Photoshopのデスクトップ、ペイウォールなど)
   * SplunkログAPIを使用してサービスとアプリケーションのパフォーマンスにアクセスする
   * その他の問題が発生した場合は、カスタマーサポートにお問い合わせください。

## トラブルシューティング {#troubleshooting}

### デバッグ {#debugging}

デバッグの一般的なアプローチとして、次のベストプラクティスに従います。

* アプリケーションのプレビュー版で機能とパフォーマンスを検証する
* アプリケーションの実稼働バージョンでの機能とパフォーマンスの検証
* コンテンツフラグメントエディターのJSONプレビューで検証
* クライアントアプリケーションでJSONをInspectし、クライアントアプリケーションまたは配信の問題の存在を確認
* GraphQLを使用したJSONのInspectによる、キャッシュされたコンテンツまたはAEMに関する問題の存在の確認

### サポートを使用したバグのログ{#logging-a-bug-with-support}

さらなる支援が必要な場合に備えて、サポートにバグを効率的に記録するには、次の手順に従います。

* 必要に応じて、問題のスクリーンショットを取得します。
* 問題を再現する方法をドキュメントする
* 雑誌号が再現するコンテンツのドキュメント
* 適切な優先順位を持つAEMサポートポータルから問題をログに記録します。

## ジャーニーは終了しますか。それとも終了しますか。{#journey-ends}

バリデーターがAEMヘッドレス開発者ジャーニーが完了しました。 これで、次の内容を理解できるようになります。

* ヘッドレスコンテンツとヘッドフルコンテンツの配信の違い。
* AEMヘッドレス機能
* ヘッドレスプロジェクトの編成とAEM化の方法。
* AEMでヘッドレスコンテンツを作成する方法。
* AEMでヘッドレスコンテンツを取得して更新する方法。
* AEM Headlessプロジェクトとの連携方法。
* ゴーライブの後はどうしますか。

## その他のリソース {#additional-resources}

* [Cloud ServiceとしてのAEMへのデプロイの概要](/help/implementing/deploying/overview.md)
* [AEM as a Cloud Service の SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [ローカルAEM環境の設定](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [Cloud Managerを使用したコードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Cloud Manager Git Repositoryを外部Gitリポジトリと統合し、プロジェクトをAEMにCloud Serviceとしてデプロイする](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)