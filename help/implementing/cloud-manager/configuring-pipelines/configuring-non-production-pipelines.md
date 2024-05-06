---
title: 実稼動以外のパイプラインの設定
description: 実稼動環境にデプロイする前にコードの品質をテストするための実稼動以外のパイプラインを設定する方法を説明します。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: d1b2226a1deec2e71056c43c84672cb4a358bc8c
workflow-type: ht
source-wordcount: '1371'
ht-degree: 100%

---


# 実稼動以外のパイプラインの設定 {#configuring-non-production-pipelines}

実稼動環境にデプロイする前にコードの品質をテストするための実稼動以外のパイプラインを設定する方法を説明します。

実稼働パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

## 実稼動以外のパイプライン {#non-production-pipelines}

ステージング環境と実稼動環境にデプロイする[実稼動パイプライン](#configuring-production-pipelines.md)に加えて、実稼動以外のパイプラインも設定して、コードを検証できます。

実稼動以外のパイプラインには次の 2 種類があります。

* **コード品質パイプライン** - これらの実行コード品質スキャンは、Git 分岐のコードに対して実行され、ビルドステップとコード品質ステップを実行します。
* **デプロイメントパイプライン** - コード品質パイプラインなどのビルドステップとコード品質ステップを実行する以外に、これらのパイプラインはコードを実稼動以外の環境にデプロイします。

>[!NOTE]
>
>初期設定後に[パイプライン設定を編集](managing-pipelines.md)できます。

## 実稼動以外の新しいパイプラインの追加 {#adding-non-production-pipeline}

Cloud Manager UI を使用してプログラムを設定し、1 つ以上の環境を用意したら、次の手順に従って実稼動以外のパイプラインを追加する準備が整います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. Cloud Manager のホーム画面から&#x200B;**パイプライン**&#x200B;カードにアクセスします。「**+追加**」をクリックし、「**実稼動以外のパイプラインを追加**」を選択します。

   ![実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **実稼動以外のパイプラインを追加**&#x200B;ダイアログの「**設定**」タブで、追加する実稼動以外のパイプラインのタイプを選択します。

   * **コード品質パイプライン** - コードを構築し、単体テストを実行し、コード品質を評価してもデプロイしないパイプラインを作成します。
   * **デプロイメントパイプライン** - コードを構築し、単体テストを実行し、コード品質を評価し、環境にデプロイするパイプラインを作成します。

   ![実稼動以外のパイプラインを追加ダイアログ](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. **実稼動以外のパイプライン名**&#x200B;を指定して、次の追加情報と共にパイプラインを特定します。

   * **デプロイメントトリガー** - 次のオプションで、パイプラインを開始するデプロイメントトリガーの時期を定義できます。

      * **手動** - このオプションを使用して、パイプラインを手動で開始します。
      * **Git の変更時** - このオプションは、設定された Git ブランチにコミットが追加されるたびに CI／CD パイプラインを開始します。このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

1. **デプロイメントパイプライン**&#x200B;を作成する場合、**重要な指標のエラー動作**&#x200B;も定義する必要があります。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出されたときに手動で介入する必要があります。
   * **直ちに失敗** - 重要なエラーが検出されると、パイプラインはキャンセルされます。このオプションでは、基本的に、各エラーをユーザーが手動で拒否する状況をエミュレートします。
   * **直ちに続行** - 重要なエラーが検出されても、パイプラインは自動的に続行されます。このオプションでは、基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。

1. 「**続行**」をクリックします。

1. **実稼動以外のパイプラインを追加**&#x200B;ダイアログの「**ソースコード**」タブで、パイプラインが処理するコードのタイプを選択する必要があります。

   * **[フルスタックコード](#full-stack-code)**
   * **[ターゲットのデプロイメント](#targeted-deployment)**

パイプラインのタイプについて詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を参照してください。

実稼動以外のパイプラインの作成を完了する手順は、選択したソースコードのタイプによって変わります。上記のリンクをたどって、このドキュメントの次の節に移動し、パイプラインの設定を完了します。

### フルスタックコード {#full-stack-code}

フルスタックコードパイプラインは、1 つ以上の AEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイします。

>[!NOTE]
>
>選択した環境にフルスタックコードパイプラインが存在する場合、この選択は無効になります。

フルスタックコードの実稼動以外のパイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境** - パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリ** - このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >Cloud Manager でリポジトリを追加および管理する方法については、[リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)を参照してください。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字と、このフィールドのオートコンプリート機能を入力します。これにより、選択できる一致するブランチを検索できます。
   * **web 階層設定を無視** - オンにすると、パイプラインは web 階層設定をデプロイしなくなります。
   * **パイプライン** - パイプラインがデプロイメントパイプラインの場合、テストフェーズを実行するように選択できます。このフェーズで有効にするオプションを選択します。どのオプションも選択していない場合、テストフェーズはパイプラインの実行中に表示されません。

      * **実稼動機能テスト** - 開発環境に対して[実稼動機能テスト](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)を実行します。
      * **カスタム機能テスト** - 開発環境に対して[カスタム機能テスト](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)を実行します。
      * **カスタム UI テスト** - カスタムアプリケーションに対して[カスタム UI テスト](/help/implementing/cloud-manager/ui-testing.md)を実行します。
      * **エクスペリエンス監査** - [エクスペリエンス監査](/help/implementing/cloud-manager/experience-audit-testing.md)の実行

   ![フルスタックパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

### ターゲットデプロイメント {#targeted-deployment}

ターゲットデプロイメントは、AEM アプリケーションの選択した部分のコードのみをデプロイします。このようなデプロイメントでは、次のいずれかのタイプのコードを&#x200B;**含む**&#x200B;よう選択できます。

* **設定** - AEM 環境のトラフィックフィルタールールの設定を行います。
   * リポジトリでフィックフィルタールールを管理し、適切にデプロイする方法については、[WAF ルールを含むトラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)を参照してください。
   * ターゲットのデプロイメントパイプラインを実行している場合、[WAF 設定などの](/help/security/traffic-filter-rules-including-waf.md)設定は、パイプラインで定義した環境、リポジトリ、ブランチに保存されていればデプロイされます。
   * 設定パイプラインは、常に 1 つの環境に 1 つしか存在できません。
* **フロントエンドコード** - AEM アプリケーションのフロントエンド用に JavaScript と CSS を設定します。
   * フロントエンドパイプラインを使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。
   * このプロセスの可能性を最大限に引き出すために知っておくべきいくつかの考慮事項と、このプロセスがどのように機能するかについては、[フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)のドキュメントを参照してください。
* **Web 階層の設定** - Web ページをクライアントに保存、処理、配信するための Dispatcher プロパティを設定します。
   * 詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)のドキュメントを参照してください。
   * 選択した環境に web 階層コードパイプラインが存在する場合、この選択は無効になります。
   * 環境に既にフルスタックパイプラインがデプロイされている場合、同じ環境に web 階層設定パイプラインを作成すると、フルスタックパイプライン内の既存の web 階層設定は無視されます。

実稼動以外のターゲットデプロイメントパイプラインの作成を完了する手順は、デプロイメントタイプを選択した場合と同じです。

1. 必要なデプロイメントのタイプを選択します。

![ターゲットデプロイメントオプション](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. **適格なデプロイメント環境**&#x200B;を定義します。

   * パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。

1. **ソースコード**&#x200B;の下で次のオプションを定義します。

   * **リポジトリ** - このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >Cloud Manager でリポジトリを追加および管理する方法については、[リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)を参照してください。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字と、このフィールドのオートコンプリート機能を入力します。これにより、選択可能な一致するブランチが検索されます。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリーのブランチ内のパスを定義します。
   * **パイプライン** - フロントエンドの実稼動以外のパイプラインの場合、**[エクスペリエンス監査を有効にするオプションがあります。](/help/implementing/cloud-manager/experience-audit-testing.md)**

   ![設定パイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)

1. エクスペリエンス監査を有効にした場合は、「**続行**」をタップまたはクリックして「**エクスペリエンス監査**」タブに進みます。ここでは、エクスペリエンス監査に常に含めるパスを定義できます。

   * 「**エクスペリエンス監査**」を有効にした場合、設定方法について詳しくは、[エクスペリエンス監査](/help/implementing/cloud-manager/experience-audit-testing.md#configuration)のドキュメントを参照してください。
   * 有効にしていない場合は、この手順をスキップします。

1. 「**保存**」をタップまたはクリックして、パイプラインを保存します。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

## Dispatcher パッケージのスキップ {#skip-dispatcher-packages}

Dispatcher パッケージをパイプラインの一部として作成しても、ストレージを作成するために公開しない場合は、そのパッケージの公開を無効にすることができます。その結果、パイプラインの実行時間が短くなる可能性があります。

Dispatcher パッケージの公開を無効にする次の設定を、プロジェクトの `pom.xml` ファイルを使用して追加する必要があります。この設定は環境変数に基づいています。この環境変数は、Cloud Manager ビルドコンテナに設定できるフラグの役目を果たすもので、Dispatcher パッケージをいつ無視すべきかを定義します。

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
