---
title: 実稼動以外のパイプラインの設定
description: 実稼動環境にデプロイする前にコードの品質をテストするための非実稼動パイプラインを設定する方法を説明します。
index: true
source-git-commit: 536740f8bb5e54a3a831a22f4e6d237863aea324
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 8%

---


# 実稼動以外のパイプラインの設定 {#configuring-non-production-pipelines}

実稼動環境にデプロイする前にコードの品質をテストするための非実稼動パイプラインを設定する方法を説明します。

## 実稼動以外のパイプライン {#non-production-pipelines}

に加えて [実稼動パイプライン](#configuring-production-pipelines.md) をステージング環境と実稼動環境にデプロイする場合、非実稼動パイプラインを設定して、コードを検証することもできます。

実稼動以外のパイプラインには次の 2 種類があります。

* **コード品質パイプライン**  — これらの実行コード品質スキャンは、Git ブランチのコードに対して実行され、ビルドステップとコード品質ステップを実行します。
* **デプロイメントパイプライン**  — コード品質パイプラインなどのビルドステップとコード品質ステップを実行する以外に、これらのパイプラインはコードを実稼動以外の環境にデプロイします。

>[!NOTE]
>
>以下が可能です。 [パイプライン設定を編集](managing-pipelines.md) を設定します。

## 実稼動以外の新しいパイプラインの追加 {#adding-non-production-pipeline}

Cloud Manager UI を使用してプログラムを設定し、1 つ以上の環境を持つと、次の手順に従って非実稼動パイプラインを追加する準備が整います。

1. Cloud Manager( ) にログインします。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 適切な組織およびプログラムを選択します。

1. Cloud Manager のホーム画面から&#x200B;**パイプライン**&#x200B;カードにアクセスします。「**+追加**」をクリックし、「**実稼動以外のパイプラインを追加**」を選択します。

   ![実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. の **設定** タブ **実稼動以外のパイプラインを追加** ダイアログで、追加する非実稼動パイプラインのタイプを選択します。 **コード品質パイプライン** または **デプロイメントパイプライン**.

   ![実稼動以外のパイプラインを追加ダイアログ](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 次を提供： **実稼動以外のパイプライン名** を使用して、次の追加情報と共にパイプラインを特定します。

   * **デプロイメントトリガー**  — パイプラインを開始するデプロイメントトリガーを定義する際に、次のオプションがあります。

      * **手動**  — このオプションを使用して、パイプラインを手動で開始します。
      * **Git の変更時**  — このオプションは、設定された Git ブランチにコミットが追加されるたびに CI/CD パイプラインを開始します。 このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。
   * **重要な指標の失敗の動作**  — パイプラインの設定または編集中に、 **デプロイメントマネージャー** には、品質ゲートのいずれかで重要なエラーが発生した場合のパイプラインの動作を定義するオプションがあります。 次のオプションがあります。

      * **毎回確認する**  — これはデフォルトの設定で、重要なエラーが発生した場合に手動で介入する必要があります。
      * **すぐに失敗**  — 重要なエラーが発生すると、常にパイプラインはキャンセルされます。 このオプションでは、基本的に、各エラーをユーザーが手動で拒否する状況をエミュレートします。
      * **すぐに続行**  — 重要なエラーが発生した場合は常に、パイプラインは自動的に続行されます。 このオプションでは、基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。


1. 「**続行**」をクリックします。

1. の **ソースコード** タブ **実稼動以外のパイプラインを追加** ダイアログで、パイプラインが処理するコードのタイプを選択する必要があります。

   * **[フロントエンドコード](#front-end-code)**
   * **[フルスタックコード](#full-stack-code)**
   * **[Web 階層設定](#web-tier-config)**

実稼動以外のパイプラインの作成を完了する手順は、 **ソースコード** を選択しました。 上記のリンクをたどって、このドキュメントの次の節に移動し、パイプラインの設定を完了します。

### フロントエンドコード {#front-end-code}

フロントエンドコードパイプラインは、1 つ以上のクライアント側 UI アプリケーションを含むフロントエンドコードビルドをデプロイします。 ドキュメントを参照 [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) を参照してください。

フロントエンドコードの非実稼動パイプラインの設定を完了するには、次の手順に従います。

1. の **ソースコード** 「 」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境**  — パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリ**  — このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >ドキュメントを参照 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

   * **Git ブランチ**  — このオプションは、選択した内のどのブランチからコードを取得するかを定義します。
   * **コードの場所**  — このオプションは、パイプラインがコードを取得する元となる、選択したリポジトリのブランチ内のパスを定義します。

   ![フロントエンドパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、次の操作が可能になります。 [パイプラインを管理](managing-pipelines.md) の **パイプライン** カード **プログラムの概要** ページ。

### フルスタックコード {#full-stack-code}

フルスタックコードパイプラインは、1 つ以上のAEMサーバーアプリケーションと HTTPD/Dispatcher 設定を含むバックエンドおよびフロントエンドコードビルドを同時にデプロイします。 ドキュメントを参照 [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) を参照してください。

>[!NOTE]
>
>選択した環境にフルスタックコードパイプラインが既に存在する場合、この選択は無効になります。

フルスタックコードの非実稼動パイプラインの設定を完了するには、次の手順に従います。

1. の **ソースコード** 「 」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境**  — パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリ**  — このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >ドキュメントを参照 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

   * **Git ブランチ**  — このオプションは、選択した内のどのブランチからコードを取得するかを定義します。
   * **Web 階層設定を無視** -

   ![フルスタックパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、次の操作が可能になります。 [パイプラインを管理](managing-pipelines.md) の **パイプライン** カード **プログラムの概要** ページ。

### Web 階層設定 {#web-tier-config}

Web 層設定パイプラインは、HTTPD/Dispatcher 設定をデプロイします。 ドキュメントを参照 [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) を参照してください。

>[!NOTE]
>
>選択した環境に Web 層コードパイプラインが既に存在する場合、この選択は無効になります。

フルスタックコードの非実稼動パイプラインの設定を完了するには、次の手順に従います。

1. の **ソースコード** 「 」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境**  — パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリ**  — このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >ドキュメントを参照 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

   * **Git ブランチ**  — このオプションは、選択した内のどのブランチからコードを取得するかを定義します。
   * **コードの場所**  — このオプションは、パイプラインがコードを取得する元となる、選択したリポジトリのブランチ内のパスを定義します。
      * Web 層設定パイプラインの場合、通常は次を含むパスになります。 `conf.d`, `conf.dispatcher.d`、および `opt-in` ディレクトリ。
      * 例えば、プロジェクト構造が [AEMプロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) パスは次のようになります。 `/dispatcher/src`.

   ![Web 層パイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. 「**保存**」をクリックします。

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
