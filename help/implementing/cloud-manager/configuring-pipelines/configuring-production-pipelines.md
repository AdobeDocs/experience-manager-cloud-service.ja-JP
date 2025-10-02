---
title: 実稼動パイプラインの追加
description: 実稼動パイプラインを追加し、コードをビルドして実稼動環境にデプロイする方法について説明します。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ac918008c3f99d74e01be59c9841083abf3604aa
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 86%

---


# 実稼動パイプラインの追加 {#configure-production-pipeline}

本番パイプラインを設定し、コードをビルドして本番環境にデプロイする方法について説明します。本番パイプラインは、最初にコードをステージング環境にデプロイします。承認時に、同じコードが本番環境にデプロイされます。

本番パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

>[!NOTE]
>
>本番パイプラインは、以下の条件が満たされるまで設定できません。
>
>* プログラムが作成されます。
>* Git リポジトリには 1 つ以上の分岐があります。
>* 本番環境とステージング環境が作成されます。

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を行う必要があります。

>[!NOTE]
>
>初期設定後に、[パイプライン設定を編集](managing-pipelines.md)できます。

## 新しい実稼動パイプラインの追加 {#adding-production-pipeline}

[!UICONTROL Cloud Manager] UI を使用してプログラムをセットアップし、1 つ以上の環境を用意したら、次の手順に従って実稼動パイプラインを追加する準備が整います。

>[!TIP]
>
>フロントエンドパイプラインを設定する前に、[AEM クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)を参照して、使いやすい AEM クイックサイト作成ツールのエンドツーエンドのガイドを確認してください。このジャーニーを活用すると、AEM サイトのフロントエンド開発を効率化できるだけでなく、AEM のバックエンドに関する知識がなくても、サイトをすばやくカスタマイズすることができます。

1. [experience.adobe.com](https://experience.adobe.com) でCloud Managerにログインします。
1. 「**クイックアクセス**」セクションで、「**Experience Manager**」をクリックします。
1. 左側のパネルで、「**Cloud Manager**」をクリックします。
1. 必要な組織を選択します。
1. **マイプログラム** コンソールで、プログラムをクリックします。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、「**追加**」をクリックして「**実稼動パイプラインを追加**」を選択します。

   ![プログラムの概要ページのパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **実稼動パイプラインを追加**&#x200B;ダイアログボックスが表示されます。パイプラインを識別するための「**パイプライン名**」のほか、以下のオプションを指定します。「**続行**」をクリックします。

   **デプロイメントトリガー** - パイプラインを開始するデプロイメントトリガーを定義する際には、次のオプションがあります。

   * **手動** - パイプラインを手動で開始します。
   * **Git の変更時** - 設定された Git 分岐にコミットが追加されるたびに CI/CD パイプラインを開始します。このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

   **重要な指標のエラー動作** - パイプラインの設定または編集中に、**デプロイメントマネージャー**&#x200B;には、品質ゲートのいずれかで重要なエラーが発生した場合のパイプラインの動作を定義するオプションがあります。使用できるオプションは以下のとおりです。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出された場合は手動で介入する必要があります。
   * **直ちに失敗** - 重要なエラーが検出されると、パイプラインがキャンセルされます。このプロセスでは、基本的に、ユーザーが各エラーを手動で拒否する状況をエミュレートします。
   * **直ちに続行** - 重要なエラーが検出されても、パイプラインが自動的に続行されます。このプロセスでは、基本的に、ユーザーが各エラーを手動で承認する状況をエミュレートします。

   ![本番パイプライン設定](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 「**ソースコード**」タブでは、パイプラインで処理するコードのタイプを選択します。

   * **[フルスタックコードパイプラインの設定](#full-stack-code)**
   * **[ターゲットデプロイメントパイプラインの設定](#targeted-deployment)**

このタイプのパイプラインについて詳しくは、[CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を参照してください。

実稼動パイプラインを作成する手順は、選択したソースコードのタイプによって異なります。上記のリンクをたどって、このドキュメントの次の節に移動し、パイプラインの設定を完了します。

### フルスタックコードパイプラインの設定 {#full-stack-code}

フルスタックコードパイプラインは、1 つ以上の AEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイします。

>[!NOTE]
>
>選択した環境にフルスタックコードパイプラインが既に存在する場合、この選択は無効になります。

**フルスタックコードパイプラインを設定するには：**

1. 「**ソースコード**」タブで、次のオプションを定義します。

   * **リポジトリ** - パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >Cloud Manager でリポジトリを追加および管理する方法については、[リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/managing-repositories.md)を参照してください。

   * **Git 分岐** - 選択したパイプラインがどの分岐からコードを取得するかを定義します。
分岐名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致する分岐が検索され、選択しやすくなります。
   * **Web 階層設定を無視** - オンにすると、パイプラインは web 階層設定をデプロイしなくなります。
   * **実稼動へのデプロイ前に一時停止** - 実稼動環境にデプロイする前にパイプラインを一時停止します。
   * **スケジュール設定** - ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。

   ![フルスタックコード](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 「**続行**」をクリックして「**エクスペリエンス監査**」タブに進みます。ここでは、エクスペリエンス監査に常に含めるパスを定義できます。

   ![エクスペリエンス監査の追加](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. エクスペリエンス監査に含めるパスを指定します。

   * 詳しくは、[エクスペリエンス監査テスト](/help/implementing/cloud-manager/reports/report-experience-audit.md#configuration)を参照してください。

1. 「**保存**」をクリックしてパイプラインを保存します。

パイプラインの実行時に、エクスペリエンス監査の対象として設定したパスが送信され、パフォーマンス、アクセシビリティ、SEO、ベストプラクティス、PWA テストに基づいて評価されます。詳しくは、[エクスペリエンス監査結果について](/help/implementing/cloud-manager/reports/report-experience-audit.md)を参照してください。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

### ターゲットデプロイメントパイプラインの設定 {#targeted-deployment}

ターゲットデプロイメントは、AEM アプリケーションの選択した部分のコードのみをデプロイします。このようなデプロイメントでは、次のいずれかのタイプのコードを&#x200B;**含める**&#x200B;よう選択できます。

* **設定** - AEM 環境の様々な機能の設定を行います。
   * ログ転送、パージ関連のメンテナンスタスク、様々な CDN 設定など、サポートされる設定のリストと、それらが適切にデプロイされるようにリポジトリで管理するには、[&#x200B; 設定パイプラインの使用 &#x200B;](/help/operations/config-pipeline.md) を参照してください。
   * ターゲットデプロイメントパイプラインを実行すると、パイプラインで定義されている環境、リポジトリ、ブランチに設定が保存された場合、その設定がデプロイされます。
   * 設定パイプラインは、常に 1 つの環境に 1 つしか存在できません。
* **Edge Delivery Services設定パイプラインを設定** - Edge Delivery設定パイプラインには、開発環境、ステージング環境および実稼動環境は個別には存在しません。 AEM as a Cloud Serviceでは、変更は開発層、ステージ層、実稼動層を通じて進みます。 これに対し、Edge Delivery設定パイプラインは、Cloud Managerに登録されたすべてのEdge Delivery Sites ドメインに設定を直接適用します。 詳しくは、[Edge Delivery パイプラインの追加 &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md) を参照してください。
* **フロントエンドコード** - AEM アプリケーションのフロントエンド用に JavaScript と CSS を設定します。
   * フロントエンドパイプラインを使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。
   * このプロセスの可能性を最大限に引き出すために知っておくべきいくつかの考慮事項と、このプロセスがどのように機能するかについては、[フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)のドキュメントを参照してください。
* **Web 階層の設定** - Web ページをクライアントに保存、処理、配信するための Dispatcher プロパティを設定します。
   * 詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)のドキュメントを参照してください。
   * 選択した環境に web 階層コードパイプラインが存在する場合、この選択は無効になります。
   * 既存のフルスタックパイプラインがある環境に対して web 階層設定パイプラインを作成すると、フルスタックパイプライン内の web 階層設定は無視されます。この変更は、その環境の web 階層設定にのみ影響します。

>[!NOTE]
>
>Web 階層設定パイプラインは、プライベートリポジトリではサポートされていません。制限の詳細と完全なリストについては、[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/private-repositories.md)を参照してください。

**ターゲットデプロイメントパイプラインを設定するには：**

1. 必要なデプロイメントのタイプを選択します。

![ターゲットデプロイメントオプション](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. **適格なデプロイメント環境**&#x200B;を定義します。

   * パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。

1. **ソースコード**&#x200B;の下で次のオプションを定義します。

   * **リポジトリ** - このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >Cloud Manager でリポジトリを追加および管理する方法については、[リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/managing-repositories.md)を参照してください。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字と、このフィールドのオートコンプリート機能を入力します。これにより、選択可能な一致するブランチが検索されます。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリーのブランチ内のパスを定義します。
   * **実稼動へのデプロイ前に一時停止** - このオプションを使用すると、実稼動環境にデプロイする前にパイプラインを一時停止できます。
   * **スケジュール設定** - ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。Web 階層ターゲットのデプロイメントでのみ使用できます。

   ![設定パイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

## Dispatcher パッケージのスキップ {#skip-dispatcher-packages}

ビルドストレージに公開せずにパイプラインで Dispatcher パッケージを作成するには、公開オプションを無効にします。これにより、パイプラインの実行時間を短縮できる場合があります。

Dispatcher パッケージの公開を無効にする次の設定を、プロジェクトの `pom.xml` ファイルを使用して追加する必要があります。環境変数は、Cloud Manager ビルドコンテナで設定して、Dispatcher パッケージを無視するタイミングを決定するフラグとして機能します。

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
