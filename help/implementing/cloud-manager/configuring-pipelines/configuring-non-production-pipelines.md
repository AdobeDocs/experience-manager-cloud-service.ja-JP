---
title: 実稼動以外のパイプラインの設定
description: 実稼動環境にデプロイする前にコードの品質をテストするための実稼動以外のパイプラインを設定する方法を説明します。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: 9804d9b71f082c3d4788667fdc3993af3b673588
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 100%

---

# 実稼動以外のパイプラインの設定 {#configuring-non-production-pipelines}

実稼動環境にデプロイする前にコードの品質をテストするための実稼動以外のパイプラインを設定する方法を説明します。

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

1. Cloud Manager のホーム画面から&#x200B;**パイプライン**&#x200B;カードにアクセスします。「**+追加**」をクリックし、「**実稼動以外のパイプラインを追加**」を選択します。

   ![実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **実稼動以外のパイプラインを追加**&#x200B;ダイアログの「**設定**」タブで、追加する実稼働以外のパイプラインのタイプ（**コード品質パイプライン**&#x200B;または&#x200B;**デプロイメントパイプライン**）を選択します。

   ![実稼動以外のパイプラインを追加ダイアログ](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. **実稼動以外のパイプライン名**&#x200B;を指定して、次の追加情報と共にパイプラインを特定します。

   * **デプロイメントトリガー** - 次のオプションで、パイプラインを開始するデプロイメントトリガーの時期を定義できます。

      * **手動** - このオプションを使用して、パイプラインを手動で開始します。
      * **Git の変更時** - このオプションは、設定された Git ブランチにコミットが追加されるたびに CI／CD パイプラインを開始します。このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

1. 「**続行**」をクリックします。

1. **実稼動以外のパイプラインを追加**&#x200B;ダイアログの「**ソースコード**」タブで、パイプラインが処理するコードのタイプを選択する必要があります。

   * **[フロントエンドコード](#front-end-code)**
   * **[フルスタックコード](#full-stack-code)**
   * **[Web 階層設定](#web-tier-config)**

実稼動以外のパイプラインの作成を完了する手順は、選択した&#x200B;**ソースコード**&#x200B;のオプションによって変わります。上記のリンクをたどって、このドキュメントの次の節に移動し、パイプラインの設定を完了します。

### フロントエンドコード {#front-end-code}

フロントエンドコードパイプラインは、1 つ以上のクライアントサイド UI アプリケーションを含んだフロントエンドコードビルドをデプロイします。このタイプのパイプラインについて詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)ドキュメントを参照してください。

フロントエンドコードの実稼動以外のパイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境** - パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリー** - このオプションは、パイプラインがコードを取得する Git リポジトリーを定義します。

   >[!TIP]
   > 
   >Cloud Manager でリポジトリーを追加および管理する方法については、[リポジトリーの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)のドキュメントを参照してください。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択の助けになります。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリーのブランチ内のパスを定義します。

   ![フロントエンドパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードの[パイプラインを管理](managing-pipelines.md)できるようになります。

### フルスタックコード {#full-stack-code}

フルスタックコードパイプラインは、1 つ以上の AEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイします。このタイプのパイプラインについて詳しくは、[CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)のドキュメントを参照してください。

>[!NOTE]
>
>選択した環境にフルスタックコードパイプラインが既に存在する場合、この選択は無効になります。

フルスタックコードの実稼動以外のパイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境** - パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリー** - このオプションは、パイプラインがコードを取得する Git リポジトリーを定義します。

   >[!TIP]
   > 
   >Cloud Manager でリポジトリーを追加および管理する方法については、[リポジトリーの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)のドキュメントを参照してください。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択の助けになります。
   * **web 階層設定を無視** - オンにすると、パイプラインは web 階層設定をデプロイしなくなります。

   ![フルスタックパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 「**保存**」をクリックします。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードの[パイプラインを管理](managing-pipelines.md)できるようになります。

### Web 階層設定 {#web-tier-config}

Web 階層設定パイプラインは HTTPD／Dispatcher 設定をデプロイします。このタイプのパイプラインについて詳しくは、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline)ドキュメントを参照してください。

>[!NOTE]
>
>選択した環境に web 階層コードパイプラインが既に存在する場合、この選択は無効になります。

Web 階層コードの実稼動以外のパイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境** - パイプラインがデプロイメントパイプラインの場合、デプロイ先の環境を選択する必要があります。
   * **リポジトリー** - このオプションは、パイプラインがコードを取得する Git リポジトリーを定義します。

   >[!TIP]
   > 
   >Cloud Manager でリポジトリーを追加および管理する方法については、[リポジトリーの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)のドキュメントを参照してください。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリーのブランチ内のパスを定義します。
      * Web 階層設定パイプラインの場合、これは通常、`conf.d`、`conf.dispatcher.d` および `opt-in` ディレクトリを含んだパスになります。
      * 例えば、プロジェクト構造が [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)から生成された場合、パスは `/dispatcher/src` のようになります。

   ![Web 階層パイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. 「**保存**」をクリックします。

>[!NOTE]
>
>既存のフルスタックパイプラインが環境にデプロイされている場合、同じ環境に対して web 層設定パイプラインを作成すると、フルスタックパイプライン内の既存の web 層設定が無視されます。

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
