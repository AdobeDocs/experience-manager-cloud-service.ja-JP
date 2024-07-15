---
title: 実稼動パイプラインの設定
description: 実稼動パイプラインを設定し、コードをビルドして実稼働環境にデプロイする方法について説明します。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a5179851af8ec88e23d79a74265b10cbce2d50f1
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 100%

---


# 実稼動パイプラインの設定 {#configure-production-pipeline}

実稼動パイプラインを設定し、コードをビルドして実稼働環境にデプロイする方法について説明します。実稼動パイプラインは最初にコードをステージング環境にデプロイし、承認があると同じコードを実稼動環境にデプロイします。

実稼働パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

>[!NOTE]
>
>プログラムの作成が完了し、Git リポジトリに少なくとも 1 つのブランチがあり、実稼働とステージングの環境セットが作成されるまで、実稼動パイプラインをセットアップできません。

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を指定する必要があります。

>[!NOTE]
>
>初期セットアップ後、[パイプライン設定を編集](managing-pipelines.md)できます。

## 新しい実稼動パイプラインの追加 {#adding-production-pipeline}

[!UICONTROL Cloud Manager] UI を使用してプログラムをセットアップし、1 つ以上の環境を用意したら、次の手順に従って実稼動パイプラインを追加する準備が整います。

>[!TIP]
>
>フロントエンドパイプラインを設定する前に、[AEM クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)を参照して、使いやすい AEM クイックサイト作成ツールによる包括的ガイドを確認してください。このジャーニーは AEM サイトのフロントエンド開発の効率化に役立ち、AEM のバックエンドに関する知識がなくても、このジャーニーを参考にサイトをすばやくカスタマイズできるようになります。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、「**追加**」をクリックして「**実稼動パイプラインを追加**」を選択します。

   ![プログラムの概要ページのパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **実稼動パイプラインを追加**&#x200B;ダイアログボックスが表示されます。パイプラインを識別するための「**パイプライン名**」のほか、以下のオプションを指定します。「**続行**」をクリックします。

   **デプロイメントトリガー** - パイプラインを開始するデプロイメントトリガーを定義する際には、次のオプションがあります。

   * **手動** - このオプションを使用して、パイプラインを手動で開始します。
   * **Git の変更時** - このオプションは、設定された Git ブランチにコミットが追加されるたびに CI／CD パイプラインを開始します。このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

   **重要な指標のエラー動作** - パイプラインの設定または編集中に、**デプロイメントマネージャー**&#x200B;には、品質ゲートのいずれかで重要なエラーが発生した場合のパイプラインの動作を定義するオプションがあります。使用できるオプションは以下のとおりです。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出されたときに手動で介入する必要があります。
   * **直ちに失敗** - 重要なエラーが検出されると、パイプラインはキャンセルされます。このオプションでは、基本的に、各エラーをユーザーが手動で拒否する状況をエミュレートします。
   * **直ちに続行** - 重要なエラーが検出されても、パイプラインは自動的に続行されます。このオプションでは、基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。

   ![実稼働パイプライン設定](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 「**ソースコード**」タブでは、パイプラインが処理するコードのタイプを選択する必要があります。

   * **[フルスタックコード](#full-stack-code)**
   * **[ターゲットのデプロイメント](#targeted-deployment)**

このタイプのパイプラインについて詳しくは、[CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を参照してください。

実稼動パイプラインを作成する手順は、選択したソースコードのタイプによって異なります。上記のリンクをたどって、このドキュメントの次の節に移動し、パイプラインの設定を完了します。

### フルスタックコード {#full-stack-code}

フルスタックコードパイプラインは、1 つ以上の AEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイします。

>[!NOTE]
>
>選択した環境にフルスタックコードパイプラインが既に存在する場合、この選択は無効になります。

フルスタックコード実稼動パイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **リポジトリー** - このオプションは、パイプラインがコードを取得する Git リポジトリーを定義します。

   >[!TIP]
   > 
   >Cloud Manager でリポジトリーを追加および管理する方法については、[リポジトリーの追加と管理](/help/implementing/cloud-manager/managing-code/managing-repositories.md)のドキュメントを参照してください。

   * **Git ブランチ** - このオプションでは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択の助けになります。
   * **Web 階層設定を無視** - オンにすると、パイプラインは web 階層設定をデプロイしなくなります。
   * **実稼動へのデプロイ前に一時停止** - このオプションを使用すると、実稼動環境にデプロイする前にパイプラインを一時停止できます。
   * **スケジュール設定** - このオプションを使用すると、ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。

   ![フルスタックコード](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 「**続行**」をタップまたはクリックして「**エクスペリエンス監査**」タブに進みます。ここでは、エクスペリエンス監査に常に含めるパスを定義できます。

   ![エクスペリエンス監査の追加](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. エクスペリエンス監査に含めるパスを指定します。

   * 詳しくは、[エクスペリエンス監査のテスト](/help/implementing/cloud-manager/experience-audit-testing.md#configuration)のドキュメントを参照してください。

1. 「**保存**」をクリックしてパイプラインを保存します。

エクスペリエンス監査の対象として設定されたパスはサービスに送信され、パイプラインの実行時にパフォーマンス、アクセシビリティ、SEO（検索エンジン最適化）、ベストプラクティスおよび PWA（プログレッシブ ｗeb アプリ）の各テストに従って評価されます。詳しくは、[エクスペリエンス監査結果について](/help/implementing/cloud-manager/experience-audit-testing.md)を参照してください。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

### ターゲットデプロイメント {#targeted-deployment}

ターゲットデプロイメントは、AEM アプリケーションの選択した部分のコードのみをデプロイします。このようなデプロイメントでは、次のいずれかのタイプのコードを&#x200B;**含む**&#x200B;よう選択できます。

* **設定** - AEM 環境のトラフィックフィルタールールの設定を行います。
   * [WAF ルールを含むトラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)ドキュメントを参照して、リポジトリの設定を管理し、適切にデプロイする方法を確認してください。
   * ターゲットのデプロイメントパイプラインを実行している場合、[WAF 設定](/help/security/traffic-filter-rules-including-waf.md)などの設定は、パイプラインで定義した環境、リポジトリ、分岐に保存されていれば、デプロイされます。
   * 設定パイプラインは、常に 1 つの環境に 1 つしか存在できません。
* **フロントエンドコード** - AEM アプリケーションのフロントエンド用に JavaScript と CSS を設定します。
   * フロントエンドパイプラインを使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。
   * このプロセスの可能性を最大限に引き出すために知っておくべきいくつかの考慮事項と、このプロセスがどのように機能するかについては、[フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)のドキュメントを参照してください。
* **Web 階層の設定** - Web ページをクライアントに保存、処理、配信するための Dispatcher プロパティを設定します。
   * 詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)のドキュメントを参照してください。
   * 選択した環境に web 階層コードパイプラインが存在する場合、この選択は無効になります。
   * 環境に既にフルスタックパイプラインがデプロイされている場合、同じ環境に web 階層設定パイプラインを作成すると、フルスタックパイプライン内の既存の web 階層設定は無視されます。

>[!NOTE]
>
>Web 階層設定パイプラインは、プライベートリポジトリではサポートされていません。制限の詳細と完全なリストについては、[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/private-repositories.md)ドキュメントを参照してください。

実稼動環境の作成を完了する手順では、デプロイメントタイプを選択したら、ターゲットとするデプロイメントパイプラインは同じです。

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
   * **スケジュール設定** - このオプションを使用すると、ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。Web 階層ターゲットのデプロイメントでのみ使用できます。

   ![設定パイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

## Dispatcher パッケージのスキップ {#skip-dispatcher-packages}

Dispatcher パッケージをパイプラインの一部として作成しても、ビルドストレージに公開しない場合は、そのパッケージの公開を無効にすることができます。その結果、パイプラインの実行時間が短くなる可能性があります。

Dispatcher パッケージの公開を無効にする次の設定を、プロジェクトの `pom.xml` ファイルを使用して追加する必要があります。この設定は環境変数に基づいています。この環境変数は、Cloud Manager ビルドコンテナに設定できるフラグの役目を果たすもので、Dispatcher パッケージをいつ無視すべきかを指定します。

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
