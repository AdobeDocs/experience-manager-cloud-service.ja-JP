---
title: AEM Developer Tools for Eclipse
description: Apache Sling 用の Eclipse プラグインに基づく Eclipse プラグインである、AEM Developer Tools for Eclipse の使用方法について説明します。
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 47%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![Experience Manager Developer Tools for Eclipse ロゴ](assets/eclipse-logo.png)

## 概要 {#overview}

_Experience Manager Developer Tools for Eclipse_ は、Apache License 2 に従ってリリースされた [Apache Sling 向け Eclipse プラグイン](https://sling.apache.org/documentation/development/ide-tooling.html)をベースとした Eclipse プラグインです。

このツールは、AEM 開発を容易にする次のような機能を提供します。

* Eclipse Server Connector による AEM インスタンスとのシームレスな統合
* コンテンツと OSGi バンドルの同期
* コードのホットスワップ機能を備えたデバッグサポート
* 固有のプロジェクト作成ウィザードからの AEM プロジェクトの簡単なブートストラップ
* JCR プロパティを容易に編集できる

## 要件 {#requirements}

AEM Developer Tools を使用する前に、次の作業が必要です。

* [Eclipse IDE for Enterprise Java and Web Developers.](https://www.eclipse.org/downloads/packages/) をダウンロードしてインストールします。
   * AEM Developer Tools for Eclipse のバージョン 1.4.0 は、Eclipse 2022-12 （4.26）以降と互換性があり、実行するには Java 17 以降が必要です。
* `eclipse.ini`Eclipse に関する FAQ[&#x200B; の説明に従って、](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F) 設定ファイルを編集し、ヒープメモリが 1 GB 以上になるように Eclipse を設定します。

>[!NOTE]
>
>macOSで、**Eclipse.app** を右クリックし、「**パッケージの内容を表示**」を選択して、パッ `eclipse.ini` ージを探します。

## Eclipse 用 AEM 開発者ツールのインストール方法 {#how-to-install-the-aem-developer-tools-for-eclipse}

前述の [requirements](#requirements) を満たしたら、次の手順で開発者ツールプラグインをインストールできます。

1. [AEM Developer Tools Web サイト](https://eclipse.adobe.com/)を開きます。

1. **インストール用リンク**&#x200B;をコピーします。

   * または、インストールリンクを使用する代わりに、アーカイブをダウンロードできます。
   * この方法ではオフラインインストールが可能ですが、自動更新の通知は受け取りません。

1. Eclipse で、**ヘルプ**&#x200B;メニューを開きます。
1. 「**Install New Software**」をクリックします。
1. 「**Add...**」をクリックします。
1. 「**Name**」フィールドに「`AEM Developer Tools`」と入力します。
1. 「**Location**」フィールドにインストール用 URL をコピーします。
1. 「**Add**」をクリックします。
1. 「**AEM**」プラグインと「**Sling**」プラグインの両方をオンにします。
1. 「**Next**」をクリックします。
1. **インストールの詳細** ウィンドウで、インストールする項目を確認し、もう一度 **次へ** をクリックします。
1. 使用許諾契約書に同意し、「**Finish**」をクリックします。
1. **信頼する機関** ダイアログが表示されるので、機関/サイト `https://eclipse.adobe.com` を選択して **信頼する選択** をクリックします。
1. **アーティファクトを信頼** ダイアログが表示されるので、コード署名者を選択して **選択項目を信頼** をクリックします。
1. 「**RestartNow**」をクリックして、Eclipse を再起動します。

## AEM パースペクティブ {#the-aem-perspective}

Eclipse では、**パースペクティブ** によって、ウィンドウ内で使用可能なアクションやビューが決定され、Eclipse のリソースとのタスク指向のやり取りが可能になります。 パースペクティブについて詳しくは、[Eclipse のドキュメント &#x200B;](https://help.eclipse.org/latest/index.jsp) を参照してください。

_Experience Manager Development Tools for Eclipse_ には、AEM プロジェクトおよびインスタンスを完全にコントロールできるAEM パースペクティブが用意されています。 AEM パースペクティブを開くには：

1. Eclipse メニューバーから、**ウィンドウ**／**パースペクティブ**／**パースペクティブを開く**／**その他**&#x200B;を選択します。
1. ダイアログで「**AEM**」を選択し、「**Open**」をクリックします。

![Eclipse の AEM パースペクティブ](assets/eclipse-aem-perspective.png)

## サンプルのマルチモジュールプロジェクト {#sample-multi-module-project}

_Experience Manager Developer Tools for Eclipse_ には、Eclipse でのプロジェクト設定を素早く習得できる、サンプルのマルチモジュールプロジェクトが付属しています。 また、[AEM プロジェクトアーキタイプを活用して、AEMのいくつかの機能のベストプラクティスガイドとしても役立ち &#x200B;](https://github.com/adobe/aem-project-archetype) す。

サンプルプロジェクトを作成する手順は次のとおりです。

1. **File**／**New**／**Project**&#x200B;メニューで、「**AEM**」セクションを参照して、「**AEM Sample Multi-Module Project**」を選択します。

   ![AEM サンプルマルチモジュールプロジェクト](assets/aem-sample-project.png)

1. 「**Next**」をクリックします。

   >[!NOTE]
   >
   >[m2eclipse](https://eclipse.dev/m2e/) がアーキタイプカタログをスキャンする必要があるので、この手順には数分かかることがあります。

1. `com.adobe.aem : aem-project-archetype : <highest-number>` アーキタイプ **ドロップダウンで** が自動的に選択されます。 必要に応じて、以前のバージョンを選択します。 「**次へ**」をクリックします。

   ![アーキタイプバージョンの選択](assets/select-archetype.png)

1. サンプルプロジェクトの次のフィールドを指定します。

   * **Name**
   * **Group Id**
   * **Artifact Id**
   * **appId** - この値を設定するには、「**Advanced**」オプションを展開する必要があります。
   * **appTitle** - この値を設定するには、「**Advanced**」オプションを展開する必要があります。
   * **Package** - この値を設定するには、「**Advanced**」オプションを展開する必要があります。

   ![アーキタイププロパティの定義](assets/archetype-properties.png)

1. 「**Next**」をクリックします。

1. **新規サーバーを設定** を選択し、サーバー名と必要な接続詳細を入力して、Eclipse が接続するAEM サーバーを設定します。

   ![AEM サーバーへの接続](assets/connect-server.png)

   * デバッガー機能を使用するには、`-agentlib` のパラメーターを指定してAEMをデバッグモードで起動する必要があります。以下に例を示します。

   ```text
   $ java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar aem-author-p4502.jar
   ```

   >[!TIP]
   >
   >ローカルのAEM SDKで動作するプロジェクトのデバッグについて詳しくは、[AEM SDKのリモートデバッグ &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-sdk/remote-debugging) を参照してください。

1. 「**終了**」をクリックします。

プロジェクト構造が作成されます。 必要なアーティファクトをプロジェクトにダウンロードするのに時間がかかる場合があります。

>[!NOTE]
>
>新規インストール時、または Maven の依存関係がまだダウンロードされていない場合、Eclipse は、プロジェクトが作成されたことをエラーで報告する場合があります。 その場合は、「無効なプロジェクト定義の解決 [&#x200B; の節で説明されている手順に従っ &#x200B;](#resolving-invalid-project-definition) ください。

## 既存プロジェクトの読み込み方法 {#how-to-import-existing-projects}

**新規プロジェクト** 機能を使用して、基本的なプロジェクト構造を作成します。

1. 手順に従って、基本的なプロジェクト構造を作成し [&#x200B; 関心事を合理的に分離した &#x200B;](#sample-multi-module-project) サンプル マルチモジュールプロジェクト」を作成します。

   * `PROJECT.ui.apps`：`/apps` および `/etc` のコンテンツ用
   * `PROJECT.ui.content`：`/content` の作成済みコンテンツ用
   * Java バンドルの `PROJECT.core`
   * `PROJECT.it.launcher` および `PROJECT.it.tests`：統合テスト用

1. `PROJECT.ui.apps` プロジェクトの内容をパッケージの `apps` フォルダーと `etc` フォルダーに置き換えます。

   1. **プロジェクトエクスプローラー** パネルで、`PROJECT.ui.apps`/`src`/`main`/`content`/`jcr_root`/`apps` を展開します。
   1. `apps` フォルダーを右クリックし、**表示**／**System Explorer** を選択します。
   1. そこで `apps` フォルダーと `etc` フォルダーを削除します。
   1. 同じ場所に、コンテンツパッケージの `apps` フォルダーと `etc` フォルダーを配置します。
   1. Eclipse で `PROJECT.ui.apps` プロジェクトを右クリックし、「**更新**」を選択します。

1. 続いて、`PROJECT.ui.content` に対して同じことを行い、そのコンテンツフォルダーを自分のパッケージの 1 つに置き換えます。

   1. **プロジェクトエクスプローラー** パネルで、`PROJECT.ui.content`/`src`/`main`/`content`/`jcr_root`/`content` を展開します。
   1. 深い階層のコンテンツフォルダーを右クリックし、**表示**／**System Explorer** を選択します。
   1. そこでコンテンツフォルダーを削除します。
   1. 同じ場所に、コンテンツパッケージのコンテンツフォルダーを配置します。
   1. Eclipse で `PROJECT.ui.content` プロジェクトを右クリックし、「**更新**」を選択します。

1. コンテンツパッケージの `filter.xml` ファイルを別のテキスト/コードエディターで開いて、コンテンツパッケージのコンテンツに対応するようにこれら 2 つのプロジェクトの `META-INF/vault/filter.xml` ファイルを更新します。

   * `filter.xml` ファイルの例を次に示します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. 2 つのプロジェクトに分割されたパッケージ内容については、これらのフィルタールールを 2 つに分割し、それに応じて 2 つのプロジェクトの `filter.xml` ファイルを更新する必要もあります。

   1. Eclipse で `PROJECT.ui.apps/src/main/content/META-INF/filter.xml` を開きます。
   1. `<workspaceFilter>` 要素の内容を、`/apps` または `/etc` で始まる、パッケージのルールに置き換えます
      * 次に例を示します。

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. 次に、`PROJECT.ui.content/src/main/content/META-INF/filter.xml` を開きます。
   1. ルールを、`/content` で始まる、パッケージのルールに置き換えます。
      * 次に例を示します。

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. すべての変更を保存してください。これで、新しいコンテンツが AEM インスタンスに同期するようになりました。

1. **サーバー** パネルで、接続が開始されていることを確認し、開始されていない場合は開始します。

1. 「**削除と公開**」アイコンをクリックします。

完了したら、パッケージがインスタンス上で実行されます。 保存時に、変更はすべてインスタンスに自動的に同期されます。

プロジェクトからパッケージを再ビルドする場合は、`PROJECT.ui.apps` または `PROJECT.ui.content` を右クリックし、**次として実行**／**Maven インストール**&#x200B;を選択します。

これで、パッケージ（例えば、`PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`）を含んだターゲットフォルダーが作成されました。

## トラブルシューティング {#troubleshooting}

### 無効なプロジェクト定義の解決 {#resolving-invalid-project-definition}

無効な依存関係およびプロジェクト定義を解決するには、次の手順を実行します。

1. 作成したプロジェクトをすべて選択します。
1. 右クリックします。
1. コンテキストメニューで、**Maven**／**プロジェクトを更新**&#x200B;を選択します。
1. 「**Force Updates of Snapshot/Releases**」をオンにします。
1. 「**OK**」をクリックします。

必要な依存関係が自動的にダウンロードされます。これには少し時間がかかる場合があります。

## 詳細情報 {#more-information}

Apache Sling IDE tooling for Eclipse の公式 web サイトでは、次の有益な追加情報を参照できます。

* [**Apache Sling IDE tooling for Eclipse** ユーザーガイド &#x200B;](https://sling.apache.org/documentation/development/ide-tooling.html) を参照しながら、全体のコンセプト、AEM Development Tools がサポートするサーバー統合およびデプロイメント機能を確認できます。
* [Apache Sling IDE ツールのトラブルシューティング &#x200B;](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [&#x200B; 既知の問題リスト &#x200B;](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

次の公式の [Eclipse](https://www.eclipse.org/) ドキュメントは、環境の設定に役立ちます。

* [Eclipse 使用の手引き](https://eclipseide.org/getting-started/)
* [Eclipse Luna ヘルプシステム](https://help.eclipse.org/latest/index.jsp)
* [Maven 統合（m2eclipse）](https://www.eclipse.org/m2e/)
