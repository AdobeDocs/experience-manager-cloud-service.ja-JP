---
title: 実稼動パイプラインの設定
description: 実稼動パイプラインを設定し、コードをビルドして実稼働環境にデプロイする方法について説明します。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 100%

---

# 実稼動パイプラインの設定 {#configure-production-pipeline}

実稼動パイプラインを設定し、コードをビルドして実稼働環境にデプロイする方法について説明します。実稼動パイプラインは最初にコードをステージング環境にデプロイし、承認があると同じコードを実稼動環境にデプロイします。

実稼働パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

>[!NOTE]
>
>プログラムの作成が完了し、Git リポジトリーに少なくとも 1 つのブランチがあり、実稼働とステージングの環境セットが作成されるまで、実稼動パイプラインをセットアップできません。

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を指定する必要があります。

>[!NOTE]
>
>初期セットアップ後、[パイプライン設定を編集](managing-pipelines.md)できます。

## 新しい実稼動パイプラインの追加 {#adding-production-pipeline}

[!UICONTROL Cloud Manager] UI を使用してプログラムをセットアップし、1 つ以上の環境を用意したら、次の手順に従って実稼動パイプラインを追加する準備が整います。

>[!TIP]
>
>フロントエンドパイプラインを設定する前に、[AEM クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)を参照して、使いやすい AEM クイックサイト作成ツールによる包括的ガイドを確認してください。このジャーニーは AEM サイトのフロントエンド開発の効率化に役立ち、AEM のバックエンドに関する知識がなくても、このジャーニーを参考にサイトをすばやくカスタマイズできるようになります。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

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

1. 「**ソースコード**」タブで、パイプラインのコードの取得先とタイプを定義する必要があります。

   * **[フロントエンドコード](#front-end-code)**
   * **[フルスタックコード](#full-stack-code)**
   * **[Web 階層設定](#web-tier-config)**

実稼動パイプラインを作成する手順は、「**ソースコード**」で選択したオプションによって異なります。上記のリンクをたどると、このドキュメントの次の節にジャンプしてパイプラインの設定を完了できます。

### フロントエンドコード {#front-end-code}

フロントエンドコードパイプラインは、1 つ以上のクライアントサイド UI アプリケーションを含んだフロントエンドコードビルドをデプロイします。このタイプのパイプラインについて詳しくは、[CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)のドキュメントを参照してください。

フロントエンドコード実稼動パイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **リポジトリー** - このオプションは、パイプラインがコードを取得する Git リポジトリーを定義します。
   >[!TIP]
   > 
   >Cloud Manager でリポジトリーを追加および管理する方法については、[リポジトリーの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)のドキュメントを参照してください。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択の助けになります。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリーのブランチ内のパスを定義します。
   * **実稼動へのデプロイ前に一時停止** - このオプションを使用すると、実稼動環境にデプロイする前にパイプラインを一時停止できます。

   ![フロントエンドコード](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. 「**保存**」をクリックしてパイプラインを保存します。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

### フルスタックコード {#full-stack-code}

フルスタックコードパイプラインは、1 つ以上の AEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイします。このタイプのパイプラインについて詳しくは、[CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)のドキュメントを参照してください。

>[!NOTE]
>
>選択した環境にフルスタックコードパイプラインが既に存在する場合、この選択は無効になります。

フルスタックコード実稼動パイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **リポジトリー** - このオプションは、パイプラインがコードを取得する Git リポジトリーを定義します。
   >[!TIP]
   > 
   >Cloud Manager でリポジトリーを追加および管理する方法については、[リポジトリーの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)のドキュメントを参照してください。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択の助けになります。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリーのブランチ内のパスを定義します。
   * **実稼動へのデプロイ前に一時停止** - このオプションを使用すると、実稼動環境にデプロイする前にパイプラインを一時停止できます。
   * **スケジュール設定** - このオプションを使用すると、ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。

   ![フルスタックコード](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 「**続行**」をクリックして「**エクスペリエンス監査**」タブに進みます。ここでは、エクスペリエンス監査に常に含めるパスを定義できます。

   ![エクスペリエンス監査の追加](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. エクスペリエンス監査に含めるパスを指定します。

   * ページパスは `/` で始める必要があります。
   * 例えば、エクスペリエンス監査に `https://wknd.site/us/en/about-us.html` を含める場合は、`/us/en/about-us.html` というパスを入力します。

   ![エクスペリエンス監査に含めるパスの定義](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. 「**ページを追加**」をクリックすると、パスが使用中の環境のアドレスで自動的に補完され、パスのテーブルに追加されます。

   ![テーブルへのパスの保存](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. 上記の 2 つの手順を繰り返して、必要なパスを追加します。

   * 最大 25 個のパスを追加できます。
   * パスを定義しない場合は、デフォルトでサイトのホームページがエクスペリエンス監査に含められます。

1. 「**保存**」をクリックして、パイプラインを保存します。

エクスペリエンス監査の対象として設定されたパスはサービスに送信され、パイプラインの実行時にパフォーマンス、アクセシビリティ、SEO（検索エンジン最適化）、ベストプラクティス、PWA（プログレッシブ ｗeb アプリ）の各テストに従って評価されます。詳しくは、「[エクスペリエンス監査結果について](/help/implementing/cloud-manager/experience-audit-testing.md)」を参照してください。

パイプラインが保存され、**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードで[パイプラインを管理](managing-pipelines.md)できるようになりました。

### Web 階層設定 {#web-tier-config}

Web 階層設定パイプラインは HTTPD／Dispatcher 設定をデプロイします。このタイプのパイプラインについて詳しくは、[CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline)のドキュメントを参照してください。

フルスタックコード実稼動パイプラインの設定を完了するには、次の手順に従います。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **リポジトリー** - このオプションは、パイプラインがコードを取得する Git リポジトリーを定義します。
   >[!TIP]
   > 
   >Cloud Manager でリポジトリーを追加および管理する方法については、[リポジトリーの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)のドキュメントを参照してください。

   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択の助けになります。
   * **コードの場所** - このオプションは、パイプラインがコードを取得する必要がある、選択したリポジトリーのブランチ内のパスを定義します。
      * Web 階層設定パイプラインの場合、これは通常、`conf.d`、`conf.dispatcher.d` および `opt-in` ディレクトリを含んだパスになります。
      * 例えば、プロジェクト構造が [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)から生成された場合、パスは `/dispatcher/src` になります。
   * **実稼動へのデプロイ前に一時停止** - このオプションを使用すると、実稼動環境にデプロイする前にパイプラインを一時停止できます。
   * **スケジュール設定** - このオプションを使用すると、ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。

   ![Web 階層コード](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. 「**保存**」をクリックしてパイプラインを保存します。

>[!NOTE]
>
>環境に既にフルスタックパイプラインがデプロイされている場合、同じ環境に web 階層設定パイプラインを作成すると、フルスタックパイプライン内の既存の web 階層設定は無視されます。

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
