---
title: 実稼動以外のパイプラインの設定
description: 実稼動環境にデプロイする前にコードの品質をテストするための非実稼動パイプラインの設定方法について説明します。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 57%

---


# 実稼動以外のパイプラインの設定 {#configuring-non-production-pipelines}

実稼動環境にデプロイする前にコードの品質をテストするための非実稼動パイプラインの設定方法について説明します。

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

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. Cloud Manager のホーム画面から&#x200B;**パイプライン**&#x200B;カードにアクセスします。クリック **+追加** を選択し、 **実稼動以外のパイプラインを追加**.

   ![実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **実稼動以外のパイプラインを追加**&#x200B;ダイアログの「**設定**」タブで、追加する実稼動以外のパイプラインのタイプを選択します。

   * **コード品質パイプライン** - コードを構築し、単体テストを実行し、コード品質を評価してもデプロイしないパイプラインを作成します。
   * **デプロイメントパイプライン** - コードを構築し、単体テストを実行し、コード品質を評価し、環境にデプロイするパイプラインを作成します。

   ![実稼動以外のパイプラインを追加ダイアログ](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. **実稼動以外のパイプライン名**&#x200B;を指定して、次の追加情報と共にパイプラインを特定します。

   * **デプロイメントトリガー** - 次のオプションで、パイプラインを開始するデプロイメントトリガーの時期を定義できます。

      * **手動** - このオプションを使用して、パイプラインを手動で開始します。
      * **Git の変更時**  — このオプションは、設定された Git ブランチにコミットが追加されるたびに CI/CD パイプラインを開始します。 このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

1. を作成する場合、 **デプロイメントパイプライン**&#x200B;を使用する場合は、 **重要な指標の失敗の動作**.

   * **毎回確認する**  — この動作はデフォルトの設定で、重要なエラーが発生した場合に手動で介入する必要があります。
   * **すぐに失敗**  — 重要なエラーが発生すると、常にパイプラインはキャンセルされます。 基本的に、各エラーをユーザーが手動で拒否する状況をエミュレートします。
   * **すぐに続行**  — 重要なエラーが発生した場合は常に、パイプラインが自動的に処理されます。 基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。

1. 「**続行**」をクリックします。

1. **実稼動以外のパイプラインを追加**&#x200B;ダイアログの「**ソースコード**」タブで、パイプラインが処理するコードのタイプを選択する必要があります。

   * **[フロントエンドコード](#front-end-code)**
   * **[フルスタックコード](#full-stack-code)**
   * **[Web 階層設定](#web-tier-config)**

実稼動以外のパイプラインの作成を完了する手順は、選択した&#x200B;**ソースコード**&#x200B;のオプションによって変わります。上記のリンクに従って、このドキュメントの次の節に移動し、パイプラインの設定を完了します。

### フロントエンドコード {#front-end-code}

フロントエンドコードパイプラインは、1 つ以上のクライアントサイド UI アプリケーションを含んだフロントエンドコードビルドをデプロイします。このタイプのパイプラインについて詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)ドキュメントを参照してください。

フロントエンドコードの実稼動以外のパイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境** - パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリ**  — このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >詳しくは、 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) そのため、Cloud Manager でリポジトリを追加および管理する方法を学ぶことができます。

   * **Git ブランチ**  — このオプションは、選択したパイプライン内のどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字と、このフィールドのオートコンプリート機能を入力します。 選択可能な一致する分岐が見つかります。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリーのブランチ内のパスを定義します。

   ![フロントエンドパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードの[パイプラインを管理](managing-pipelines.md)できるようになります。

### フルスタックコード {#full-stack-code}

フルスタックコードパイプラインは、1 つ以上の AEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイします。このタイプのパイプラインについて詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)のドキュメントを参照してください。

>[!NOTE]
>
>選択した環境にフルスタックコードパイプラインが存在する場合、この選択は無効になります。

フルスタックコードの実稼動以外のパイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境** - パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリ**  — このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >詳しくは、 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) そのため、Cloud Manager でリポジトリを追加および管理する方法を学ぶことができます。

   * **Git ブランチ**  — このオプションは、選択したパイプライン内のどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字と、このフィールドのオートコンプリート機能を入力します。 選択できる一致するブランチを見つけるのに役立ちます。
   * **Web 層の構成を無視**  — オンにすると、パイプラインは Web 層設定をデプロイしません。

   * **パイプライン** - パイプラインがデプロイメントパイプラインの場合、テストフェーズを実行するように選択できます。このフェーズで有効にするオプションを選択します。 どのオプションも選択していない場合、パイプラインの実行中にテストフェーズは表示されません。

      * **実稼動機能テスト** - 開発環境に対して[実稼動機能テスト](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)を実行します。
      * **カスタム機能テスト** - 開発環境に対して[カスタム機能テスト](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)を実行します。
      * **カスタム UI テスト** - カスタムアプリケーションに対して[カスタム UI テスト](/help/implementing/cloud-manager/ui-testing.md)を実行します。

   ![フルスタックパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードの[パイプラインを管理](managing-pipelines.md)できるようになります。

### Web 階層設定 {#web-tier-config}

Web 層設定パイプラインは、HTTPD/Dispatcher 設定をデプロイします。 詳しくは、 [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) を参照してください。

>[!NOTE]
>
>選択した環境に Web 層コードパイプラインが存在する場合、この選択は無効になります。

Web 階層コードの実稼動以外のパイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境** - パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリ**  — このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。

   >[!TIP]
   > 
   >詳しくは、 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) そのため、Cloud Manager でリポジトリを追加および管理する方法を学ぶことができます。

   * **Git ブランチ**  — このオプションは、選択したパイプライン内のどのブランチからコードを取得するかを定義します。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリーのブランチ内のパスを定義します。
      * Web 層設定パイプラインの場合、このパスには通常、 `conf.d`, `conf.dispatcher.d`、および `opt-in` ディレクトリ。
      * 例えば、プロジェクト構造が [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)から生成された場合、パスは `/dispatcher/src` のようになります。

   ![Web 階層パイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. 「**保存**」をクリックします。

>[!NOTE]
>
>既存のフルスタックパイプラインが環境にデプロイされている場合、同じ環境に対して web 層設定パイプラインを作成すると、フルスタックパイプライン内の既存の web 層設定が無視されます。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

## フロントエンドパイプラインを使用したサイトの開発 {#developing-with-front-end-pipeline}

フロントエンドパイプラインを使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。

ドキュメントを参照 [フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) このプロセスの仕組みと、このプロセスを最大限に活用するために考慮すべきいくつかの検討事項について説明します。

## Dispatcher パッケージのスキップ {#skip-dispatcher-packages}

Dispatcher パッケージをパイプラインの一部として構築し、それらを公開してストレージを構築したくない場合は、公開を無効にすると、パイプラインの実行時間を短縮できます。

次の設定で、Dispatcher パッケージの公開を無効にします。この設定は、プロジェクトを介して追加する必要があります `pom.xml` ファイル。 このフラグは、環境変数に基づいています。環境変数は、Cloud Manager ビルドコンテナで設定できるフラグで、Dispatcher パッケージを無視するタイミングを定義します。

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
