---
title: 実稼動パイプラインの追加
description: 実稼動パイプラインを追加し、コードをビルドして実稼動環境にデプロイする方法について説明します。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 57%

---


# 実稼動パイプラインの追加 {#configure-production-pipeline}

実稼動パイプラインを設定し、コードをビルドして実稼動環境にデプロイする方法について説明します。 実稼動パイプラインは、最初にコードをステージング環境にデプロイします。 承認時に、同じコードが実稼動環境にデプロイされます。

実稼働パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

>[!NOTE]
>
>実稼動パイプラインは、次の状況が発生するまで設定できません。
>
>* プログラムが作成されます。
>* Git リポジトリーには少なくとも 1 つのブランチがあります。
>* 実稼動環境とステージング環境が作成されます。

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプラインを設定します。

>[!NOTE]
>
>初期セットアップ後、[パイプライン設定を編集](managing-pipelines.md)できます。

## 新しい実稼動パイプラインの追加 {#adding-production-pipeline}

[!UICONTROL Cloud Manager] UI を使用してプログラムをセットアップし、1 つ以上の環境を用意したら、次の手順に従って実稼動パイプラインを追加する準備が整います。

>[!TIP]
>
>フロントエンドパイプラインを設定する前に、[AEM クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md) を参照して、使いやすいAEM クイックサイト作成ツールの包括的ガイドを確認してください。 このジャーニーはAEM サイトのフロントエンド開発の効率化に役立ち、AEMのバックエンドに関する知識がなくても、このジャーニーを参考にサイトをすばやくカスタマイズできます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、「**追加**」をクリックして「**実稼動パイプラインを追加**」を選択します。

   ![プログラムの概要ページのパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **実稼動パイプラインを追加**&#x200B;ダイアログボックスが表示されます。パイプラインを識別するための「**パイプライン名**」のほか、以下のオプションを指定します。「**続行**」をクリックします。

   **デプロイメントトリガー** - パイプラインを開始するデプロイメントトリガーを定義する際には、次のオプションがあります。

   * **手動** - パイプラインを手動で開始します。
   * **Git の変更時** – 設定された Git ブランチにコミットが追加されるたびに CI/CD パイプラインを開始します。 このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

   **重要な指標のエラー動作** - パイプラインの設定または編集中に、**デプロイメントマネージャー**&#x200B;には、品質ゲートのいずれかで重要なエラーが発生した場合のパイプラインの動作を定義するオプションがあります。使用できるオプションは以下のとおりです。

   * **毎回確認する** - デフォルト設定。 重要なエラーが発生した場合は、手動での介入が必要です。
   * **直ちに失敗** - 重要なエラーが検出されると、パイプラインはキャンセルされます。このプロセスでは、基本的に、各エラーを手動で却下するユーザーをエミュレートします。
   * **直ちに続行** – 重要なエラーが検出されても、パイプラインは自動的に続行されます。 このプロセスでは、基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。

   ![実稼働パイプライン設定](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 「**Source コード**」タブで、パイプラインが処理するコードのタイプを選択します。

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

1. 「**Source コード**」タブで、次のオプションを定義します。

   * **リポジトリ** - パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >Cloud Managerでリポジトリを追加および管理する方法については、[ リポジトリの追加と管理 ](/help/implementing/cloud-manager/managing-code/managing-repositories.md) を参照してください。

   * **Git ブランチ** – 選択したパイプラインがコードを取得するブランチを定義します。
ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが見つかり、選択の助けになります。
   * **Web 階層設定を無視** - オンにすると、パイプラインは web 階層設定をデプロイしなくなります。
   * **実稼動へのデプロイ前に一時停止** – 実稼動環境にデプロイする前にパイプラインを一時停止します。
   * **スケジュール設定** - ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。

   ![フルスタックコード](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 「**続行**」をクリックして「**エクスペリエンス監査**」タブに進みます。ここでは、エクスペリエンス監査に常に含めるパスを定義できます。

   ![エクスペリエンス監査の追加](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. エクスペリエンス監査に含めるパスを指定します。

   * 詳しくは、[ エクスペリエンス監査テスト ](/help/implementing/cloud-manager/experience-audit-dashboard.md#configuration) を参照してください。

1. 「**保存**」をクリックしてパイプラインを保存します。

パイプラインを実行すると、エクスペリエンス監査用に設定されたパスが送信され、パフォーマンス、アクセシビリティ、SEO、ベストプラクティス、PWAテストに基づいて評価されます。 詳しくは、[ エクスペリエンス監査結果について ](/help/implementing/cloud-manager/experience-audit-dashboard.md) を参照してください。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

### ターゲットデプロイメントパイプラインの設定 {#targeted-deployment}

ターゲットデプロイメントは、AEM アプリケーションの選択した部分のコードのみをデプロイします。このようなデプロイメントでは、次のいずれかのタイプのコードを **含める** を選択できます。

* **Config** - AEM環境の様々な機能に関する設定を行います。
   * サポートされている設定（ログ転送、パージ関連のメンテナンスタスク、様々な CDN 設定を含む）のリストと、これらが適切にデプロイされるようにリポジトリで管理する方法について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md)を参照してください。
   * ターゲットデプロイメントパイプラインを実行する場合、設定がパイプラインで定義された環境、リポジトリ、ブランチに保存されている限り、設定がデプロイされます。
   * 設定パイプラインは、常に 1 つの環境に 1 つしか存在できません。
* **フロントエンドコード** - AEM アプリケーションのフロントエンド用に JavaScript と CSS を設定します。
   * フロントエンドパイプラインを使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。
   * このプロセスの可能性を最大限に引き出すために知っておくべきいくつかの考慮事項と、このプロセスがどのように機能するかについては、[フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)のドキュメントを参照してください。
* **Web 階層設定** - Dispatcherのプロパティを設定して、クライアントに web ページを保存、処理、配信します。
   * 詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)のドキュメントを参照してください。
   * 選択した環境に web 階層コードパイプラインが存在する場合、この選択は無効になります。
   * 既存のフルスタックパイプラインを含む環境に web 階層設定パイプラインを作成した場合、フルスタックパイプラインの web 階層設定は無視されます。 この変更は、その環境の web 階層設定にのみ影響します。

>[!NOTE]
>
>Web 階層設定パイプラインは、プライベートリポジトリではサポートされていません。詳細と制限事項の一覧については、[Cloud Managerでのプライベートリポジトリの追加 ](/help/implementing/cloud-manager/managing-code/private-repositories.md) を参照してください。

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
   * **スケジュール設定** - ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。 Web 階層ターゲットのデプロイメントでのみ使用できます。

   ![設定パイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードの[パイプラインを管理](managing-pipelines.md)できるようになります。

## Dispatcher パッケージをスキップ {#skip-dispatcher-packages}

ビルドストレージに公開せずにパイプラインにDispatcher パッケージをビルドするには、「公開」オプションを無効にします。 これにより、パイプラインの実行時間を短縮できる場合があります。

Dispatcher パッケージの公開を無効にする次の設定を、プロジェクトの `pom.xml` ファイルを使用して追加する必要があります。環境変数は、Dispatcher ビルドコンテナで設定するフラグとして機能し、Cloud Manager パッケージを無視するタイミングを決定します。

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
