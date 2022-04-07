---
title: 実稼動パイプラインの設定
description: コードをビルドして実稼動環境にデプロイするための実稼動パイプラインを設定する方法について説明します。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 9804d9b71f082c3d4788667fdc3993af3b673588
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 29%

---

# 実稼動パイプラインの設定 {#configure-production-pipeline}

コードをビルドして実稼動環境にデプロイするための実稼動パイプラインを設定する方法について説明します。

ユーザーが **[デプロイメントマネージャー](/help/onboarding/learn-concepts/cloud-manager-introduction.md#role-based-permissions)** 実稼動パイプラインを設定するためのロール。

>[!NOTE]
>
>実稼動パイプラインは、プログラムの作成が完了し、Git リポジトリに少なくとも 1 つのブランチがあり、実稼動とステージング環境のセットが作成されるまで、設定できません。

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を指定する必要があります。

>[!NOTE]
>
>以下が可能です。 [パイプライン設定を編集](managing-pipelines.md) を設定します。

## 新しい実稼動パイプラインの追加 {#adding-production-pipeline}

プログラムを設定し、少なくとも 1 つの環境で [!UICONTROL Cloud Manager] UI で、次の手順に従って実稼動パイプラインを追加する準備が整いました。

>[!TIP]
>
>フロントエンドパイプラインを設定する前に、 [AEMクイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md) を参照してください。このガイドは、使いやすいAEM Quick Site Creation ツールです。 このジャーニーは、AEM Site のフロントエンド開発を合理化するのに役立ち、AEMのバックエンドに関する知識を持たずに、すばやくサイトをカスタマイズできます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 次に移動： **パイプライン** カード **プログラムの概要** ページを開き、をクリックします。 **追加** 選択 **実稼動パイプラインを追加**.

   ![プログラムマネージャーの概要のパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. この **実稼動パイプラインを追加** ダイアログボックスが表示されます。 次を提供： **パイプライン名** を使用して、以下のオプションと共にパイプラインを特定します。 「**続行**」をクリックします。

   **デプロイメントトリガー**  — パイプラインを開始するデプロイメントトリガーを定義する際に、次のオプションがあります。

   * **手動** - このオプションを使用して、パイプラインを手動で開始します。
   * **Git の変更時** - このオプションは、設定された Git ブランチにコミットが追加されるたびに CI／CD パイプラインを開始します。このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

   **重要な指標のエラー動作****- パイプラインの設定または編集中に、デプロイメントマネージャーには、品質ゲートのいずれかで重要なエラーが発生した場合のパイプラインの動作を定義するオプションがあります。**&#x200B;使用できるオプションは以下のとおりです。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出されたときに手動で介入する必要があります。
   * **直ちに失敗** - 重要なエラーが検出されると、パイプラインはキャンセルされます。このオプションでは、基本的に、各エラーをユーザーが手動で拒否する状況をエミュレートします。
   * **直ちに続行** - 重要なエラーが検出されても、パイプラインは自動的に続行されます。このオプションでは、基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。

   ![実稼動パイプラインの設定](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. の **ソースコード** 「 」タブを使用して、パイプラインがコードを取得する場所と取得するコードのタイプを定義する必要があります。

   * **[フロントエンドコード](#front-end-code)**
   * **[フルスタックコード](#full-stack-code)**
   * **[Web 階層設定](#web-tier-config)**

実稼動パイプラインの作成を完了する手順は、 **ソースコード** を選択しました。 上記のリンクをたどって、このドキュメントの次の節に移動し、パイプラインの設定を完了します。

### フロントエンドコード {#front-end-code}

フロントエンドコードパイプラインは、1 つ以上のクライアント側 UI アプリケーションを含むフロントエンドコードビルドをデプロイします。 ドキュメントを参照 [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) を参照してください。

フロントエンドコード実稼動パイプラインの設定を完了するには、次の手順に従います。

1. の **ソースコード** 「 」タブで、次のオプションを定義する必要があります。

   * **リポジトリ** - このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。
   >[!TIP]
   > 
   >ドキュメントを参照 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択に役立ちます。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリのブランチ内のパスを定義します。
   * **実稼動にデプロイする前に一時停止します**  — このオプションは、実稼動環境にデプロイする前にパイプラインを一時停止します。

   ![フロントエンドコード](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. 「**保存**」をクリックしてパイプラインを保存します。

パイプラインが保存され、次の操作が可能になります。 [パイプラインを管理](managing-pipelines.md) の **パイプライン** カード **プログラムの概要** ページ。

### フルスタックコード {#full-stack-code}

フルスタックコードパイプラインは、1 つ以上のAEMサーバーアプリケーションと HTTPD/Dispatcher 設定を含むバックエンドおよびフロントエンドコードビルドを同時にデプロイします。 ドキュメントを参照 [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) を参照してください。

>[!NOTE]
>
>選択した環境にフルスタックコードパイプラインが既に存在する場合、この選択は無効になります。

フルスタックコード実稼動パイプラインの設定を完了するには、次の手順に従います。

1. の **ソースコード** 「 」タブで、次のオプションを定義する必要があります。

   * **リポジトリ** - このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。
   >[!TIP]
   > 
   >ドキュメントを参照 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択に役立ちます。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリのブランチ内のパスを定義します。
   * **実稼動にデプロイする前に一時停止します**  — このオプションは、実稼動環境にデプロイする前にパイプラインを一時停止します。
   * **スケジュール設定** - このオプションを使用すると、ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。

   ![フルスタックコード](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. クリック **続行** 先に進む **エクスペリエンス監査** タブを使用して、エクスペリエンス監査に常に含めるパスを定義できます。

   ![エクスペリエンス監査の追加](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. エクスペリエンス監査に含める パスを指定.

   * ページのパスはで始める必要があります `/`.
   * 例えば、 `https://wknd.site/us/en/about-us.html` 「エクスペリエンス監査」に、パスを入力します。 `/us/en/about-us.html`.

   ![エクスペリエンス監査のパスの定義](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. クリック **ページを追加** パスは、環境のアドレスで自動入力され、パスのテーブルに追加されます。

   ![テーブルへのパスの保存](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. 必要に応じて、前の 2 つの手順を繰り返して、引き続きパスを追加します。

   * 最大 25 個のパスを追加できます。
   * パスを定義しない場合、サイトのホームページはデフォルトでエクスペリエンス監査に含まれます。

1. クリック **保存** をクリックしてパイプラインを保存します。

エクスペリエンス監査用に設定されたパスはサービスに送信され、パイプライン実行時のパフォーマンス、アクセシビリティ、SEO（検索エンジン最適化）、ベストプラクティス、PWA（プログレッシブ Web アプリ）のテストに従って評価されます。 詳しくは、「[エクスペリエンス監査結果について](/help/implementing/cloud-manager/experience-audit-testing.md)」ｓを参照してください。

パイプラインが保存され、次の操作が可能になります。 [パイプラインを管理](managing-pipelines.md) の **パイプライン** カード **プログラムの概要** ページ。

### Web 階層設定 {#web-tier-config}

Web 層設定パイプラインは、HTTPD/Dispatcher 設定をデプロイします。 ドキュメントを参照 [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) を参照してください。

フルスタックコード実稼動パイプラインの設定を完了するには、次の手順に従います。

1. の **ソースコード** 「 」タブで、次のオプションを定義する必要があります。

   * **リポジトリ** - このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。
   >[!TIP]
   > 
   >ドキュメントを参照 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択に役立ちます。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリのブランチ内のパスを定義します。
      * Web 層設定パイプラインの場合、通常は次を含むパスになります。 `conf.d`, `conf.dispatcher.d`、および `opt-in` ディレクトリ。
      * 例えば、プロジェクト構造が [AEMプロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) パスは次のようになります。 `/dispatcher/src`.
   * **実稼動にデプロイする前に一時停止します**  — このオプションは、実稼動環境にデプロイする前にパイプラインを一時停止します。
   * **スケジュール設定** - このオプションを使用すると、ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。

   ![Web 層コード](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. 「**保存**」をクリックしてパイプラインを保存します。

>[!NOTE]
>
>既存のフルスタックパイプラインが環境にデプロイされている場合、同じ環境に対して Web 層設定パイプラインを作成すると、フルスタックパイプライン内の既存の Web 層設定が無視されます。

パイプラインが保存され、次の操作が可能になります。 [パイプラインを管理](managing-pipelines.md) の **パイプライン** カード **プログラムの概要** ページ。

## Dispatcher パッケージをスキップ {#skip-dispatcher-packages}

Dispatcher パッケージをパイプラインの一部として構築し、それらを公開してストレージを構築したくない場合は、公開を無効にすると、パイプラインの実行時間が短縮される可能性があります。

次の設定で、Dispatcher パッケージの公開を無効にします。この設定は、プロジェクトを介して追加する必要があります `pom.xml` ファイル。 このフラグは、環境変数に基づいています。この変数は、Cloud Manager ビルドコンテナで設定できるフラグで、Dispatcher パッケージを無視するタイミングを定義できます。

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
