---
title: 実稼動以外のパイプラインの追加
description: 本番環境にデプロイする前にコードの品質をテストするため、本番以外のパイプラインを追加する方法について説明します。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 0171e2e6a27a8b60bcd94792e616961598f580fb
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 29%

---


# 実稼動以外のパイプラインの追加 {#configuring-non-production-pipelines}

プログラムを設定し、Cloud Manager UIで少なくとも1つの環境を作成したら、実稼動以外のパイプラインを追加できます。 これらのパイプラインを使用すると、実稼動環境にデプロイする前にコード品質をテストできます。

実稼働パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

>[!NOTE]
>
>初期設定後に、[パイプライン設定を編集](managing-pipelines.md)できます。

## 新しい実稼動以外のパイプラインの追加

プログラムを設定し、Cloud Manager UIで少なくとも1つの環境を作成したら、実稼動以外のパイプラインを追加できます。 実稼動環境にデプロイする前に、これらのパイプラインを使用してコード品質をテストします。

**実稼動以外の新しいパイプラインを追加するには：**

{{sign-in-to-cloud-manager}}

1. **マイプログラム** コンソールで、プログラムをクリックします。
1. 左側のパネルで、**パイプライン**&#x200B;をクリックします。
1. **パイプライン** ページの右上隅付近で、**パイプラインを追加** > **実稼動以外のパイプラインを追加**&#x200B;をクリックします。

   ![実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **実稼動以外のパイプラインを追加** ダイアログボックスの「**設定**」タブで、作成する次のいずれかの実稼動以外のパイプラインを選択します。

   * **コード品質パイプライン** - GIT ブランチでコードをビルドし、単体テストを実行し、環境にデプロイせずにコード品質を評価するパイプラインを作成します。
   * **デプロイメントパイプライン** - コードのビルド、単体テストの実行、コード品質の評価、実稼動以外の環境へのデプロイを行うパイプラインを作成します。

   ![実稼動以外のパイプラインを追加ダイアログ](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 「**パイプライン設定**」セクションの「**実稼動以外のパイプライン名**」フィールドに、実稼動以外のパイプラインの説明を入力します。
1. 「**デプロイメントオプション**」セクションで、使用するデプロイメントトリガーの1つを選択します。

   * **手動** - パイプラインを手動で開始します。
   * **Git の変更時** - 設定された Git 分岐にコミットが追加される際にパイプラインを開始します。 このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

1. 使用する&#x200B;**重要な指標の失敗の動作**&#x200B;を選択します。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出されたときに手動で介入する必要があります。
   * **直ちに失敗** - 重要なエラーが検出されると、パイプラインはキャンセルされます。 各エラーを手動で拒否する場合にユーザーをエミュレートします。
   * **直ちに続行** - 重要なエラーが検出されても、パイプラインが自動的に続行されます。 各エラーを手動で承認する場合にユーザーがエミュレーションされます。

1. 「**続行**」をクリックします。

1. 実稼動以外のパイプラインの設定を完了するために使用する残りの手順は、使用するソースコードのタイプによって異なります。
**実稼動以外のパイプラインを追加** ダイアログボックスの「**Source コード**」タブで、実稼動以外のパイプラインプロセスのコードの種類を選択します。

   * **[フルスタックコードを使用しています](#full-stack-code)**
   * **[ターゲットデプロイメントを使用しています](#targeted-deployment)**

   パイプラインのタイプについて詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を参照してください。


### フルスタックコードを使用している

フルスタックコードパイプラインは、1 つ以上の AEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイします。

>[!NOTE]
>
>選択した環境にフルスタックコードパイプラインが存在する場合、この選択は無効になります。

フルスタックコードの実稼動以外のパイプラインの設定を完了するには、次の操作を行います。

1. 「**Source コード**」セクションで、次のオプションを定義します。

   * **適格なデプロイメント環境** – 実稼動以外のパイプラインを編集する場合にのみ使用できます。 パイプラインがデプロイメントパイプラインの場合は、デプロイ先の環境を選択します。
   * **リポジトリ** - ドロップダウンリストから、パイプラインがソースとして使用するGit リポジトリを選択します。 Cloud Managerは、ここで選択したリポジトリからコードをビルドします。

     >[!TIP]
     > 
     >Cloud Manager でリポジトリを追加および管理する方法については、[リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/managing-repositories.md)を参照してください。

   * **Git Branch** - ドロップダウンリストから、パイプラインの構築に使用する選択したリポジトリ内のブランチを選択します。 デフォルトは、`main` です。 パイプラインは、選択したブランチをビルドとデプロイメントのソースとして使用します。 必要に応じて、**更新**&#x200B;をクリックして、選択したリポジトリで使用可能なブランチのリストを更新します。 最近作成したブランチがリストに表示されない場合は、このオプションを使用します。
   * **戦略の構築**
      * **完全ビルド** - リポジトリ内のすべてのモジュールを毎回作成します
      * BETA **スマートビルド** – 前回のコミット以降に変更されたモジュールのみをビルドします。<br>実稼動以外のパイプラインで[ スマートビルドを使用する方法について詳しく見る](#about-smart-build-non-production-pipeline)。

        >[!IMPORTANT]
        >
        >スマートビルドは、コード品質パイプラインとDev フルスタックコードのデプロイメントパイプラインでのみ使用できます。

   * **Web階層設定を無視** チェックボックス – オンにすると、パイプラインがWeb階層設定をデプロイしません。

1. 「**パイプライン**」セクションでは、パイプラインがデプロイメントパイプラインの場合、テストフェーズを実行することを選択できます。 このフェーズで有効にするオプションを選択します。 どのオプションも選択していない場合、テストフェーズはパイプラインの実行中に表示されません。

   * **製品機能テスト** - [製品機能テスト ](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)を開発環境に対して実行します。
   * **カスタム機能テスト** - [ カスタム機能テスト ](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)を開発環境に対して実行します。
   * **カスタム UI テスト** - カスタムアプリケーションの[ カスタム UI テスト ](/help/implementing/cloud-manager/ui-testing.md)を実行します。
   * **エクスペリエンス監査** - [ エクスペリエンス監査](/help/implementing/cloud-manager/reports/report-experience-audit.md)を実行

   ![フルスタックパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

### ターゲットデプロイメントを使用しています {#targeted-deployment}

ターゲットデプロイメントは、AEM アプリケーションの選択した部分のコードのみをデプロイします。 このようなデプロイメントでは、次のいずれかのタイプのコードを&#x200B;**含む**&#x200B;よう選択できます。

![ターゲットデプロイメントオプション](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment1.png)

<!--
* **Config** - Configure settings for various features in your AEM environment.
  * See [Using Config Pipelines](/help/operations/config-pipeline.md) for a list of supported configurations, which include log forwarding, purge-related maintenance tasks, and various CDN configurations, and to manage them in your repository so they are deployed properly.
  * When running a targeted deployment pipeline, configurations are deployed, provided they are saved to the environment, repository, and branch you defined in the pipeline.
  * At any time, there can only be one config pipeline per environment.
* **Configure Edge Delivery Services config pipeline** - Edge Delivery Configuration Pipelines do not have separate development, staging, and production environments. In AEM as a Cloud Service, changes move through development, stage, and production tiers. In contrast, an Edge Delivery Configuration Pipeline applies its configuration directly to all Edge Delivery Sites domains registered in Cloud Manager. To learn more, see [Add an Edge Delivery Pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
-->


* **フロントエンドコード** - AEM アプリケーションのフロントエンド用に JavaScript と CSS を設定します。
   * フロントエンドパイプラインを使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。
   * このプロセスの可能性を最大限に引き出すために知っておくべきいくつかの考慮事項と、このプロセスがどのように機能するかについては、[フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)のドキュメントを参照してください。
* **Web階層設定** - Web ページをクライアントに保存、処理、配信するためのDispatcher プロパティを設定します。
   * 詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)のドキュメントを参照してください。
   * 選択した環境に web 階層コードパイプラインが存在する場合、この選択は無効になります。
   * フルスタックパイプラインが既に環境にデプロイされている場合でも、同じ環境に対してweb層設定パイプラインを作成できます。 これを行うと、Cloud Managerはフルスタックパイプラインのweb層設定を無視します。

     >[!NOTE]
     >
     >Web 階層設定パイプラインは、プライベートリポジトリではサポートされていません。 制限の詳細と完全なリストについては、[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/private-repositories.md)を参照してください。

<!--
The steps to complete the creation of your non-production, targeted deployment pipeline are the same once you choose a deployment type.

1. Choose which deployment type you require.

![Targeted deployment options](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. Define the **Eligible Deployment Environments**.

   * If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
-->

1. 「**Source コード**」セクションで、次のオプションを定義します。

   * **リポジトリ** – このオプションは、実稼動以外のパイプラインがコードを取得するGIT リポジトリを定義します。

     >[!TIP]
     > 
     >Cloud Manager でリポジトリを追加および管理する方法については、[リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/managing-repositories.md)を参照してください。

   * **Git ブランチ** – このオプションは、選択したパイプラインがコードを取得するブランチを定義します。 ブランチ名の最初の数文字を入力し、このフィールドのオートコンプリート機能を使用します。 これにより、選択可能な一致するブランチが検索されます。
   * **コードの場所** – このオプションは、選択したリポジトリのブランチ内のパスを定義し、パイプラインがコードを取得します。

<!--
   * **Pipeline** - For front-end non-production pipelines, you have the option to enable **[Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)**.
   
   ![Config pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)
-->

1. エクスペリエンス監査を有効にした場合は、**続行**&#x200B;をクリックして、**エクスペリエンス監査** タブに進みます。 エクスペリエンス監査に常に含まれるパスを定義します。

   * 「**エクスペリエンス監査**」を有効にした場合、設定方法について詳しくは、[エクスペリエンス監査](/help/implementing/cloud-manager/reports/report-experience-audit.md)のドキュメントを参照してください。
   * 有効にしていない場合は、この手順をスキップします。

1. 「**保存**」をクリックしてパイプラインを保存します。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。


## 実稼動以外のパイプラインでのスマートビルドの使用について{#about-smart-build-non-production-pipeline}

Cloud Managerの&#x200B;**スマートビルド**&#x200B;は、実稼動以外のパイプライン向けに最適化されたビルド戦略です。 スマートビルド モジュールをキャッシュし、前回の正常な実行以降に変更されたモジュールのみを再構築することで、ビルド時間を短縮します。 変更されていないモジュールはキャッシュから再利用されますが、変更されたモジュールとその依存関係のみが再構築され、反復的な開発ワークフローの効率が向上します。

スマートビルドは現在、次の場合にのみ使用できます。

* コード品質パイプライン。
* フルスタックのデプロイメントパイプラインを開発する。

>[!NOTE]
>
>スマートビルドを有効にした後の最初の実行は、キャッシュが空であるため、フルビルドのように動作します。

次のような場合は、スマートビルドをお勧めします。

* 段階的な変更を頻繁に行っています。
* プロジェクトに複数のMaven モジュールが含まれています。
* 完全なビルドには膨大な時間がかかります。

スマートビルドは、次のような場合には必ずしも理想的ではありません。

* ビルドは、Mavenの依存グラフ外で操作を実行するプラグインに大きく依存しています。
* すべての実行に対して完全な再構築の検証が必要です。

### ビルドパフォーマンスについて{#smart-build-performance}

スマートビルドの使用によるパフォーマンスの向上は、次のような要因によって異なります。

* プロジェクト内のモジュール数。
* コード変更の頻度と範囲。
* モジュール間の依存関係の分布：

多くの独立したモジュールを使用したプロジェクトは、大きな改善が見られます。

### モジュールごとのキャッシュオプトアウト{#smart-build-cache-optout}

スマートビルドでは、特定のモジュールのキャッシュを無効にできるきめ細かい制御が提供されます。 この機能は、特定のモジュールで次のような場合に便利です。

* `exec-maven-plugin`や`maven-antrun-plugin`などのプラグインを使用します。
* Mavenの依存関係によって追跡されないファイル操作を実行します。
* キャッシュされたコンテンツは、一貫性のない結果を生成します。

### モジュールのキャッシュを無効にする{#smart-build-disable-caching}

影響を受けるモジュールの`pom.xml`に次のプロパティを追加できます。

```xml
<properties>
  <maven.build.cache.enabled>false</maven.build.cache.enabled>
</properties>
```

この設定では、他のモジュールがキャッシュのメリットを引き続き享受する一方で、パイプラインの実行ごとにモジュールを再構築する必要があります。

### スマートビルドを使用する際の制限事項と考慮事項{#smart-build-limitations}

スマートビルドを使用する場合は、次の点に注意してください。

* スマートビルドはMaven依存関係分析に依存しています。
* 依存関係グラフ以外の変更は、トリガーの再構築を行いません。
* 一部のプラグインは、キャッシュと完全に互換性がありません。
* 実稼動以外のパイプラインを編集することで、いつでも&#x200B;**フルビルド**&#x200B;に切り替えることができます。

予期しないビルド動作が発生した場合は、特定のモジュールのキャッシュを無効にするか、ビルド戦略を&#x200B;**フルビルド**&#x200B;に一時的に切り替えることを検討してください。

### スマートビルドの問題のトラブルシューティング{#smart-build-troubleshoot}

| 問題 | 推奨される解決策 |
| --- | --- |
| ビルド結果に一貫性がありません | ・ 影響を受けるモジュールのキャッシュを無効にします。<br>・ プラグインの動作を確認します（特に`exec`/`antrun` プラグイン）。 |
| パフォーマンスが向上しない | ・ 複数の実行が発生していることを確認します（キャッシュ ウォームアップ）。<br> ・ほとんどのモジュールが頻繁に変更されているかどうかを確認します。 |
| 予期しないアーティファクトまたは欠落している変更 | ・ Maven依存関係のトラッキング外の変更があるかどうかを確認します。<br>・ **完全ビルド**&#x200B;を使用して検証します。 |

スマートビルドを有効にするには、[実稼動以外のパイプラインを追加](#add-non-production-pipeline)を参照してください。











<!--
## Add a non-production pipeline

Once you have set up your program and have at least one environment using the Cloud Manager UI, you are ready to add a non-production pipeline by following these steps.

{{sign-in-to-cloud-manager}}

1. On the **My Programs** console, click a program. 

1. Access the **Pipelines** card from the Cloud Manager home screen. Click **+Add** and select **Add Non-Production Pipeline**. 

   ![Add non-production pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. On the **Configuration** tab of the **Add Non-Production Pipeline** dialog, select the type of non-production pipeline you with to add.

   * **Code Quality Pipeline** - Create a pipeline that builds your code, runs unit tests, and evaluates code quality but does NOT deploy.
   * **Deployment Pipeline** - Create a pipeline that builds your code, runs unit tests, evaluates code quality, and deploys to an environment.

   ![Add Non-Production pipeline dialog](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Provide a **Non-Production Pipeline Name** to identify your pipeline along with the following additional information.

   * **Deployment Trigger** - You have the following options when defining the deployment triggers to start the pipeline.
   
     * **Manual** - Use this option to start the pipeline manually.
     * **On Git Changes** - This option starts the CI/CD pipeline whenever commits are added to the configured Git branch. With this option, you can still start the pipeline manually as required.

1. If you choose to create a **Deployment Pipeline**, you must also define the **Important Metric Failures Behavior**.

   * **Ask every time** - This behavior is the default setting and requires manual intervention on any important failure.
   * **Fail Immediately** - If selected, the pipeline is canceled whenever an important failure occurs. It is essentially emulating a user manually rejecting each failure.
   * **Continue Immediately** - If selected, the pipeline procedes automatically whenever an important failure occurs. It is essentially emulating a user manually approving each failure.

1. Click **Continue**.

1. On the **Source Code** tab of the **Add Non-Production Pipeline** dialog, you must select which type of code the pipeline should process.

   * **[Full Stack Code](#full-stack-code)**
   * **[Targeted deployment](#targeted-deployment)**

See [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) for more information about the types of pipelines.

The steps to complete the creation of your non-production pipeline vary depending on the type of source code you selected. Follow the links above to jump to the next section of this document so you can complete the configuration of your pipeline.

### Full Stack Code

A full-stack code pipeline simultaneously deploys back-end and front-end code builds containing one or more AEM server applications along with HTTPD/Dispatcher configuration.

>[!NOTE]
>
>If a full-stack code pipeline exists for the selected environment, this selection is disabled.

To finish the configuration of the full-stack code non-production pipeline, follow these steps.

1. On the **Source Code** tab, you must define the following options.

   * **Eligible Deployment Environments** - If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
   * **Repository** - This option defines from which git repo that the pipeline should retrieve the code.

   >[!TIP]
   > 
   >See [Adding and Managing Repositories](/help/implementing/cloud-manager/managing-code/managing-repositories.md) so you can learn how to add and manage repositories in Cloud Manager.

   * **Git Branch** - This option defines from which branch in the selected pipeline should retrieve the code.
     * Enter the first few characters of the branch name and the auto-complete feature of this field. It helps you find the matching branches that you can select.
   * **Ignore Web Tier Configuration** - When checked, the pipeline does not deploy your web tier configuration.
   * **Pipeline** - If your pipeline is a deployment pipeline, you can choose to run a testing phase. Check the options that you want to enable in this phase. If none of the options are selected, the testing phase is not displayed during the pipeline's run.

     * **Product Functional Testing** - Execute [product functional tests](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) against the development environment.
     * **Custom Functional Testing** - Execute [custom functional tests](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) against the development environment.
     * **Custom UI Testing** - Execute [custom UI tests](/help/implementing/cloud-manager/ui-testing.md) for custom applications.
     * **Experience Audit** - Execute [Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Full-stack pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Click **Save**.

The pipeline is saved and you can now [manage your pipelines](managing-pipelines.md) on the **Pipelines** card on the **Program Overview** page.

-->



## Dispatcher パッケージの除外 {#exclude-dispatcher-packages}

パイプラインにDispatcher パッケージを組み込むが、ストレージを構築するためにアップロードしない場合は、公開を無効にします。 この設定により、パイプラインの実行時間を短縮できます。

Dispatcher パッケージの公開を無効にするには、プロジェクト `pom.xml` ファイルに次の設定を追加します。 Cloud Manager ビルドコンテナで環境変数を設定して、Dispatcher パッケージを無視するタイミングをフラグします。 パイプラインはこのフラグを読み取り、それに応じて無視します。

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>[!NOTE]rue</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
