---
title: 'AEM Developer Tools for Eclipse '
description: 'AEM Developer Tools for Eclipse '
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '1182'
ht-degree: 100%

---

# AEM Developer Tools for Eclipse {#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## 概要 {#overview}

AEM Developer Tools for Eclipse は、Apache License 2 に従ってリリースされた [Apache Sling 向け Eclipse プラグイン](https://sling.apache.org/documentation/development/ide-tooling.html) をベースとする Eclipse プラグインです。

このツールは、AEM 開発を容易にする次のような機能を提供します。

* Eclipse Server Connector による AEM インスタンスとのシームレスな統合
* コンテンツと OSGi バンドルの同期
* コードのホットスワップ機能を備えたデバッグサポート
* 固有のプロジェクト作成ウィザードからの AEM プロジェクトの簡単なブートストラップ
* JCR プロパティの容易な編集

## 要件 {#requirements}

AEM Developer Tools を使用する前に、次の作業が必要です。

* [Eclipse IDE for Enterprise Java Developers](https://www.eclipse.org/downloads/packages/) をダウンロードしてインストールします。
* [Eclipse に関する FAQ](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse) の説明に従って、`eclipse.ini` 設定ファイルを編集し、ヒープメモリが 1 GB 以上になるように Eclipse を設定します。

>[!NOTE]
>
>macOS では、**Eclipse.app** を右クリックし、「**パッケージの内容を表示**」を選択して、`eclipse.ini`**を探します。**

## AEM Developer Tools for Eclipse のインストール方法 {#how-to-install-the-aem-developer-tools-for-eclipse}

上記の[要件](#requirements)を満たしたら、次の手順でプラグインをインストールできます。

1. [AEM Developer Tools Web サイト](https://eclipse.adobe.com/aem/dev-tools/)を開きます。

1. **インストール用リンク**&#x200B;をコピーします。

   または、インストール用リンクを使用する代わりに、アーカイブをダウンロードすることもできます。この方法ではオフラインインストールが可能ですが、自動アップデート通知は受けられません。

1. Eclipse で、**Help** メニューを開きます。
1. 「**Install New Software**」をクリックします。
1. 「**Add...**」をクリックします。
1. 「**Name**」に `AEM Developer Tools` と入力します。
1. 「**Location**」にインストール用 URL をコピーします。
1. 「**Add**」をクリックします。
1. 「**AEM**」プラグインと「**Sling**」プラグインの両方をオンにします。
1. 「**Next**」をクリックします。
1. **Install Details** ウィンドウで、「**Next**」を再度クリックします。
1. 使用許諾契約書に同意し、「**Finish**」をクリックします。
1. 「**Restart Now**」をクリックして、Eclipse を再起動します。

## AEM パースペクティブ {#the-aem-perspective}

Eclipse では、パースペクティブによって、ウィンドウ内で使用可能なアクションやビューが決まり、Eclipse のリソースとのタスク指向のやり取りが可能になります。パースペクティブについて詳しくは、[Eclipse のドキュメント](https://help.eclipse.org)を参照してください。

AEM Development Tools for Eclipse には、AEM プロジェクトおよびインスタンスを完全にコントロールできる AEM パースペクティブが用意されています。AEM パースペクティブを開くには、次の操作を行います。

1. Eclipse メニューバーから、**Window**／**Perspective**／**Open Perspective**／**Other** を選択します。
1. ダイアログで「**AEM**」を選択し、「**Open**」をクリックします。

![Eclipse の AEM パースペクティブ](assets/eclipse-aem-perspective.png)

## サンプルのマルチモジュールプロジェクト {#sample-multi-module-project}

AEM Developer Tools for Eclipse には、サンプルのマルチモジュールプロジェクトが同梱されています。このプロジェクトは、Eclipse でのプロジェクト設定を手早く行うために役立つだけでなく、いくつかの AEM 機能に対するベストプラクティスガイドの役割も果たします。プロジェクトのアーキタイプについて詳しくは、[こちら](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)を参照してください。

次の手順を実行して、サンプルプロジェクトを作成します。

1. **File**／**New**／**Project**&#x200B;メニューで、「**AEM**」セクションを参照して、「**AEM Sample Multi-Module Project**」を選択します。

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

1. 次に、Eclipse の接続先となる AEM サーバーを設定します。

   デバッガー機能を使用するには、AEM をデバッグモードで起動する必要があります。コマンドラインに以下を追加するなどして、デバッグモードで起動できます。

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![AEM サーバーへの接続](assets/connect-server.png)

1. 「**Finish**」をクリックします。プロジェクト構造が作成されます。

   >[!NOTE]
   >
   >新規インストールの場合（より具体的には、Maven の依存関係をダウンロードしたことがない場合）は、プロジェクトを作成するとエラーが表示されることがあります。その場合は、[無効なプロジェクト定義の解決](#resolving-invalid-project-definition)で説明されている手順に従ってください。

## 既存プロジェクトの読み込み方法 {#how-to-import-existing-projects}

**New Project** 機能を使用して、適切な構造を次の手順で作成できます。

1. [サンプルのマルチモジュールプロジェクト](#sample-multi-module-project)を作成する手順に従うと、次のプロジェクトが自動的に作成されます。これらを使用して、関心事を合理的に分離できます。

   * `PROJECT.ui.apps`：`/apps` および `/etc` のコンテンツ用
   * `PROJECT.ui.content`：`/content` の作成済みコンテンツ用
   * `PROJECT.core`：Java バンドル用（Java コードの追加が必要になれば関心も高くなります）
   * `PROJECT.it.launcher` および `PROJECT.it.tests`：統合テスト用

1. `PROJECT.ui.apps` プロジェクトの内容をパッケージの `apps` フォルダーと `etc` フォルダーに置き換えます。

   1. Project Explorer パネルで、`PROJECT.ui.apps`／`src`／`main`／`content`／`jcr_root`／`apps` を展開します。
   1. `apps` フォルダーを右クリックし、**Show In**／**System Explorer** を選択します。
   1. 表示される `apps` フォルダーと `etc` フォルダーを削除し、その場所にコンテンツパッケージの `apps` フォルダーと `etc` フォルダーを配置します。
   1. Eclipse で `PROJECT.ui.apps` プロジェクトを右クリックし、「**Refresh**」を選択します。

1. 続いて、`PROJECT.ui.content` に対して同じことを行い、そのコンテンツフォルダーをパッケージの 1 つに置き換えます。

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

1. 2 つのプロジェクトに分割されたパッケージ内容については、これらのフィルタールールを 2 つに分割し、それに応じて 2 つのプロジェクトの `filter.xml` ファイルを更新する必要もあります。

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

これで、ターゲットフォルダーが作成されて、その中にパッケージ（例：`PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`）が含まれています。

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

Apache Sling IDE tooling for Eclipse の公式 Web サイトでは、次の役立つ情報を参照できます。

* 『[**Apache Sling IDE tooling for Eclipse** ユーザーガイド](https://sling.apache.org/documentation/development/ide-tooling.html)』：このドキュメントでは、全体のコンセプト、AEM Development Tools でサポートされているサーバー統合およびデプロイメント機能について説明しています。
* [トラブルシューティング情報](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [既知の問題リスト](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

次の公式の [Eclipse](https://eclipse.org/) ドキュメントは、環境の設定に役立ちます。

* [Eclipse 使用の手引き](https://eclipse.org/users/)
* [Eclipse Luna ヘルプシステム](https://help.eclipse.org/luna/index.jsp)
* [Maven 統合（m2eclipse）](https://www.eclipse.org/m2e/)
