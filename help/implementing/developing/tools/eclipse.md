---
title: AEM Developer Tools for Eclipse
description: AEM Developer Tools for Eclipse
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 64%

---

# AEM Developer Tools for Eclipse {#aem-developer-tools-for-eclipse}

![Experience ManagerDeveloper Tools for Eclipse ロゴ](assets/eclipse-logo.png)

## 概要 {#overview}

_Eclipse のExperience Manager開発者ツール_ は、 [Eclipse plugin for Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) Apache License 2 に基づいてリリースされました。

このツールは、AEM 開発を容易にする次のような機能を提供します。

* Eclipse Server Connector による AEM インスタンスとのシームレスな統合
* コンテンツと OSGi バンドルの同期
* コードのホットスワップ機能を備えたデバッグサポート
* 特定のプロジェクト作成ウィザードを使用したAEM Projects のシンプルなBootstrap
* JCR プロパティの容易な編集

## 要件 {#requirements}

AEM Developer Tools を使用する前に、次の作業が必要です。

* ダウンロードとインストール [Eclipse IDE for Enterprise Java™ Developers](https://www.eclipse.org/downloads/packages/).
* Eclipse のインストールを設定し、1 GB 以上のヒープメモリがあることを確認するには、 `eclipse.ini` 設定ファイル ( [Eclipse の FAQ](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>macOS では、**Eclipse.app** を右クリックし、「**パッケージの内容を表示**」を選択して、`eclipse.ini`**を探します。**

## Eclipse 用 AEM 開発者ツールのインストール方法 {#how-to-install-the-aem-developer-tools-for-eclipse}

前述の[要件](#requirements)を満たしたら、次の手順でプラグインをインストールできます。

1. [AEM 開発者ツールの web サイト](https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip)を開きます。 <!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. を **インストールリンク**.

   または、インストールリンクを使用する代わりにアーカイブをダウンロードできます。 この方法ではオフラインインストールが可能ですが、自動アップデート通知は受けられません。

1. Eclipse で、 **ヘルプ** メニュー
1. クリック **新しいソフトウェアのインストール**.
1. クリック **追加…**.
1. 内 **名前** フィールドに入力 `AEM Developer Tools`.
1. 内 **場所** 「 」フィールドで、インストール URL をコピーします。
1. 「**Add**」をクリックします。
1. 両方を選択 **AEM** および **Sling** プラグイン
1. 「**Next**」をクリックします。
1. **Install Details** ウィンドウで、「**Next**」を再度クリックします。
1. 使用許諾契約書に同意し、「**Finish**」をクリックします。
1. 「**Restart Now**」をクリックして、Eclipse を再起動します。

## AEM パースペクティブ {#the-aem-perspective}

Eclipse では、パースペクティブは、ウィンドウ内で使用可能なアクションとビューを決定し、Eclipse 内のリソースとタスク指向のやり取りを可能にします。 パースペクティブについて詳しくは、[Eclipse のドキュメント](https://help.eclipse.org/latest/index.jsp)を参照してください。

_Eclipse 用Experience Manager開発ツール_ AEMプロジェクトとインスタンスを完全に制御できるAEMパースペクティブを提供します。 AEM パースペクティブを開くには、次の操作を行います。

1. Eclipse メニューバーから、「 」を選択します。 **ウィンドウ** -> **遠近法** -> **Open Perspective** -> **その他**.
1. ダイアログで「**AEM**」を選択し、「**Open**」をクリックします。

![Eclipse の AEM パースペクティブ](assets/eclipse-aem-perspective.png)

## サンプルのマルチモジュールプロジェクト {#sample-multi-module-project}

この _Eclipse のExperience Manager開発者ツール_ には、Eclipse でのプロジェクト設定をすばやく習得できる、サンプルのマルチモジュールプロジェクトが付属しています。 また、AEMのいくつかの機能のベストプラクティスガイドとしても機能します。 プロジェクトのアーキタイプについて詳しくは、[こちら](https://github.com/adobe/aem-project-archetype)を参照してください。

サンプルプロジェクトを作成するには、次の手順に従います。

1. 内 **ファイル** > **新規** > **プロジェクト** メニュー、参照 **AEM** 「 」セクションで「 」を選択します。 **AEM Sample Multi-Module Project**.

   ![AEM サンプルマルチモジュールプロジェクト](assets/aem-sample-project.png)

1. 「**Next**」をクリックします。

   >[!NOTE]
   >
   >m2eclipse がアーキタイプカタログをスキャンする必要があるので、この手順には少し時間がかかることがあります。

1. メニューから「`com.adobe.granite.archetypes : sample-project-archetype : <highest-number>`」を選択し、「**Next**」をクリックします。

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

1. 次に、Eclipse が接続するAEMサーバーを設定します。

   デバッガー機能を使用するには、デバッグモードでAEMを起動する必要があります。これを実現するには、次のコマンドをコマンドラインに追加します。

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![AEM サーバーへの接続](assets/connect-server.png)

1. 「**終了**」をクリックします。プロジェクト構造が作成されます。

   >[!NOTE]
   >
   >新規インストールの場合（より具体的には、Maven の依存関係をダウンロードしたことがない場合）は、プロジェクトを作成するとエラーが表示されることがあります。この場合は、 [無効なプロジェクト定義の解決](#resolving-invalid-project-definition).

## 既存プロジェクトの読み込み方法 {#how-to-import-existing-projects}

**New Project** 機能を使用して、適切な構造を次の手順で作成できます。

1. 手順に従って、 [マルチモジュールプロジェクトのサンプル](#sample-multi-module-project) 次のプロジェクトが作成され、問題の健全な分離を可能にします。

   * `PROJECT.ui.apps`：`/apps` および `/etc` のコンテンツ用
   * `PROJECT.ui.content`：`/content` の作成済みコンテンツ用
   * `PROJECT.core` Java™バンドルの場合 (Java™コードを追加すると興味深くなります )
   * `PROJECT.it.launcher` および `PROJECT.it.tests`：統合テスト用

1. `PROJECT.ui.apps` プロジェクトの内容をパッケージの `apps` フォルダーと `etc` フォルダーに置き換えます。

   1. Project Explorer パネルで、`PROJECT.ui.apps`／`src`／`main`／`content`／`jcr_root`／`apps` を展開します。
   1. `apps` フォルダーを右クリックし、**Show In**／**System Explorer** を選択します。
   1. 表示される `apps` フォルダーと `etc` フォルダーを削除し、その場所にコンテンツパッケージの `apps` フォルダーと `etc` フォルダーを配置します。
   1. Eclipse で `PROJECT.ui.apps` プロジェクトを右クリックし、「**Refresh**」を選択します。

1. 次に、 `PROJECT.ui.content` そのコンテンツフォルダーを、次のいずれかのパッケージに置き換えます。

   1. Project Explorer パネルで、`PROJECT.ui.content`／`src`／`main`／`content`／`jcr_root`／`content` を展開します。
   1. 深い階層のコンテンツフォルダーを右クリックし、**Show In**／**System Explorer** を選択します。
   1. 表示されるコンテンツフォルダーを削除し、その場所にコンテンツパッケージのコンテンツフォルダーを配置します。
   1. Eclipse で `PROJECT.ui.content` プロジェクトを右クリックし、「**Refresh**」を選択します。

1. 次に、コンテンツパッケージの内容に対応するように、これら 2 つのプロジェクトの `filter.xml` ファイルを更新する必要があります。それには、コンテンツパッケージの `META-INF/vault/filter.xml` ファイルを別のテキスト／コードエディターで開きます。

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

1. 2 つのプロジェクトに分割されたパッケージのコンテンツについては、これらのフィルタールールも 2 つに分割し、それに応じて `filter.xml` 2 つのプロジェクトのファイル。

   1. Eclipse で `PROJECT.ui.apps/src/main/content/META-INF/filter.xml` を開きます。
   1. `<workspaceFilter>` 要素の内容を、`/apps` または `/etc` で始まる、パッケージのルールに置き換えます
      * 例えば、次のようにします。

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
      * 例えば、次のようにします。

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. すべての変更を保存してください。これで、新しいコンテンツが AEM インスタンスに同期するようになりました。

1. Servers パネルで、接続が開始されていることを確認します。開始していない場合は開始します。
1. 「**Clean and Publish**」アイコンをクリックします。

完了したら、インスタンスでパッケージが動作しており、保存時には、変更が自動的にインスタンスに同期します。

プロジェクトからパッケージを再ビルドする場合は、`PROJECT.ui.apps` または `PROJECT.ui.content` を右クリックし、**Run As**／**Maven install** を選択します。

これで、パッケージ（例えば、`PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`）を含んだターゲットフォルダーが作成されました。

## トラブルシューティング {#troubleshooting}

### 無効なプロジェクト定義の解決 {#resolving-invalid-project-definition}

無効な依存関係およびプロジェクト定義を解決するには、次の手順を実行します。

1. 作成したプロジェクトをすべて選択します。
1. 右クリックします。
1. コンテキストメニューで、**Maven**／**Update Projects** を選択します。
1. 「**Force Updates of Snapshot/Releases**」をオンにします。
1. 「**OK**」をクリックします。

必要な依存関係が自動的にダウンロードされます。これには少し時間がかかる場合があります。

## 詳細情報 {#more-information}

Apache Sling IDE tooling for Eclipse の公式 web サイトでは、次の有益な情報を参照できます。

* この [**Eclipse 用 Apache Sling IDE ツール** ユーザーガイド](https://sling.apache.org/documentation/development/ide-tooling.html)このドキュメントでは、AEM開発ツールでサポートされる概念、サーバー統合、デプロイメント機能の概要を説明します。
* [トラブルシューティング情報](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [既知の問題リスト](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

次の公式の [Eclipse](https://www.eclipse.org/) ドキュメントは、環境の設定に役立ちます。

* [Eclipse 使用の手引き](https://www.eclipse.org/getting-started/)
* [Eclipse Luna ヘルプシステム](https://help.eclipse.org/latest/index.jsp)
* [Maven 統合（m2eclipse）](https://www.eclipse.org/m2e/)
