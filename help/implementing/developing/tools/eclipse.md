---
title: AEM Developer Tools for Eclipse
description: AEM Eclipse開発者ツール
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 27%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## 概要 {#overview}

AEM Developer Tools for Eclipse は、Apache License 2 に従ってリリースされた [Apache Sling 向け Eclipse プラグイン](https://sling.apache.org/documentation/development/ide-tooling.html) をベースとする Eclipse プラグインです。

このツールは、AEM 開発を容易にする次のような機能を提供します。

* Eclipse Server Connectorを通じたAEMインスタンスとのシームレスな統合
* コンテンツとOSGiバンドルの両方の同期
* コードのホットスワップ機能によるデバッグのサポート
* 特定のプロジェクト作成ウィザードを使用したAEMプロジェクトの単純なブートストラップ
* JCRプロパティの簡単な編集

## 要件 {#requirements}

AEM Developer Toolsを使用する前に、次の操作を行う必要があります。

* [Eclipse IDE for Enterprise Java Developers](https://www.eclipse.org/downloads/packages/)をダウンロードしてインストールします。
* [Eclipse FAQ](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse)の説明に従って`eclipse.ini`設定ファイルを編集し、少なくとも1 GBのヒープメモリがあることを確認するようにEclipseを設定します。

>[!NOTE]
>
>macOSでは、**Eclipse.app**&#x200B;を右クリックし、「**パッケージの内容を表示**」を選択して&#x200B;`eclipse.ini`**を探す必要があります。**

## Eclipse用AEM Developer Toolsのインストール方法{#how-to-install-the-aem-developer-tools-for-eclipse}

上記の[要件](#requirements)を満たしたら、次のようにプラグインをインストールできます。

1. [AEM Developer Tools Webサイトを開きます。](https://eclipse.adobe.com/aem/dev-tools/)

1. **インストール用リンク**&#x200B;をコピーします。

   または、インストール用リンクを使用する代わりに、アーカイブをダウンロードすることもできます。この方法ではオフラインインストールが可能ですが、自動アップデート通知は受けられません。

1. Eclipse で、**Help** メニューを開きます。
1. 「**Install New Software**」をクリックします。
1. 「**Add...**」をクリックします。
1. **名前**&#x200B;に`AEM Developer Tools`と入力します。
1. 「**Location**」にインストール用 URL をコピーします。
1. 「**追加**」をクリックします。
1. 「**AEM**」プラグインと「**Sling**」プラグインの両方をオンにします。
1. 「**次へ**」をクリックします。
1. **詳細をインストール**&#x200B;ウィンドウで、**次へ**&#x200B;を再度クリックします。
1. 使用許諾契約に同意し、[**終了**]をクリックします。
1. Eclipseを再起動するには、**RestartNow**&#x200B;をクリックします。

## AEM パースペクティブ {#the-aem-perspective}

Eclipseでは、パースペクティブによってウィンドウ内で使用できるアクションと表示が決定され、Eclipse内のタスク指向のリソースとのやり取りが可能になります。 パースペクティブの詳細については、[Eclipseのドキュメントを参照してください。](https://help.eclipse.org)

AEM Development Tools for Eclipseは、AEMプロジェクトとインスタンスをオファーがフルコントロールできるAEMの視点を提供します。 AEMパースペクティブを開くには：

1. Eclipseメニューバーから、「**Window** -> **Perspective** -> **Open Perspective** -> **Other**」を選択します。
1. ダイアログで「**AEM**」を選択し、「**開く**」をクリックします。

![EclipseのAEMパースペクティブ](assets/eclipse-aem-perspective.png)

## サンプルのマルチモジュールプロジェクト {#sample-multi-module-project}

AEM Developer Tools for Eclipse には、サンプルのマルチモジュールプロジェクトが同梱されています。このプロジェクトは、Eclipse でのプロジェクト設定を手早くおこなうために役立つだけでなく、いくつかの AEM 機能に対するベストプラクティスガイドの役割も果たします。[プロジェクトのアーキタイプについて詳しくは、こちらを参照してください。](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype) 

次の手順を実行して、サンプルプロジェクトを作成します。

1. **File**／**New**／**Project**&#x200B;メニューで、「**AEM**」セクションを参照して、「**AEM Sample Multi-Module Project**」を選択します。

   ![AEMマルチモジュールプロジェクトのサンプル](assets/aem-sample-project.png)

1. 「**次へ**」をクリックします。

   >[!NOTE]
   >
   >m2eclipseがアーキタイプカタログをスキャンする必要があるので、この手順には少し時間がかかる場合があります。

1. メニューから「`com.adobe.granite.archetypes : sample-project-archetype : <highest-number>`」を選択し、「**次へ**」をクリックします。

   ![アーキタイプバージョンの選択](assets/select-archetype.png)

1. サンプルプロジェクトに次のフィールドを指定します。

   * **名前**
   * **グループID**
   * **アーティファクトID**
   * **appId**  — この値を設定するには、「 **** 詳細」オプションを展開する必要がある場合があります。
   * **appTitle**  — この値を設定するには、「 **** 詳細」オプションを展開する必要がある場合があります。
   * **パッケージ**  — この値を設定するには、 **** 詳細オプションを展開する必要がある場合があります。

   ![アーキタイププロパティの定義](assets/archetype-properties.png)

1. 「**次へ**」をクリックします。

1. 次に、Eclipseが接続するAEMサーバーを設定します。

   デバッガ機能を使用するには、デバッグモードでAEMを起動しておく必要があります。これは、次のようにコマンドラインに追加することで実現できます。

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![AEMサーバーに接続](assets/connect-server.png)

1. 「**Finish**」をクリックします。プロジェクト構造が作成されます。

   >[!NOTE]
   >
   >新規インストール（具体的には、maven依存関係がダウンロードされていない場合）では、エラーが発生してプロジェクトが作成されることがあります。 この場合は、[無効なプロジェクト定義の解決](#resolving-invalid-project-definition)で説明されている手順に従ってください。

## 既存プロジェクトの読み込み方法 {#how-to-import-existing-projects}

**新しいプロジェクト**&#x200B;機能を使用して、次のような適切な構造を作成できます。

1. [サンプルのマルチモジュールプロジェクト](#sample-multi-module-project)を作成する手順に従うと、次のプロジェクトが自分用に作成されます。これにより、懸念事項を健全に分離できます。

   * `PROJECT.ui.apps` for  `/apps` and  `/etc` content
   * `PROJECT.ui.content` それ `/content` は書かれている
   * `PROJECT.core` Javaバンドルの場合（Javaコードを追加するとすぐに興味深い内容になります）
   * `PROJECT.it.launcher` 統合テスト `PROJECT.it.tests` の場合は、

1. `PROJECT.ui.apps`プロジェクトの内容をパッケージの`apps`フォルダーと`etc`フォルダーに置き換えます。

   1. プロジェクトエクスプローラーパネルで、`PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`を展開します。
   1. `apps`フォルダーを右クリックし、****&#x200B;に表示/**システムエクスプローラー**&#x200B;を選択します。
   1. 表示する`apps`フォルダーと`etc`フォルダーを削除し、コンテンツパッケージの`apps`フォルダーと`etc`フォルダーをここに配置します。
   1. Eclipseで、`PROJECT.ui.apps`プロジェクトを右クリックし、「**更新**」を選択します。

1. 次に、`PROJECT.ui.content`に対して同じことを行い、そのコンテンツフォルダーをパッケージの1つに置き換えます。

   1. プロジェクトエクスプローラーパネルで、`PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`を展開します。
   1. より深いコンテンツフォルダーを右クリックし、「**** -> **システムエクスプローラー**&#x200B;に表示」を選択します。
   1. 表示されるコンテンツフォルダーを削除し、コンテンツパッケージのコンテンツフォルダーをここに配置します。
   1. Eclipseで、`PROJECT.ui.content`プロジェクトを右クリックし、「**更新**」を選択します。

1. 次に、これら2つのプロジェクトの`filter.xml`ファイルを更新して、コンテンツパッケージの内容に合わせる必要があります。 その場合は、コンテンツパッケージの`META-INF/vault/filter.xml`ファイルを別のテキスト/コードエディターで開きます。

   * `filter.xml`ファイルの例を次に示します。

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

1. パッケージを2つのプロジェクトに分割したコンテンツについては、これらのフィルタールールを2つに分割し、2つのプロジェクトの`filter.xml`ファイルに合わせて更新する必要もあります。

   1. Eclipseで、`PROJECT.ui.apps/src/main/content/META-INF/filter.xml`を開きます。
   1. `<workspaceFilter>`要素の内容を、`/apps`と`/etc`を含む開始ーを含むパッケージのルールに置き換えます
      * 次に例を示します。

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/apps/foo"/>
            <filter root="/apps/foundation/components/bar"/>
            <filter root="/etc/designs/foo"/>
         </workspaceFilter>
         ```
   1. 次に`PROJECT.ui.content/src/main/content/META-INF/filter.xml`を開きます。
   1. ルールを、`/content`を開始したパッケージのルールに置き換えます。
      * 次に例を示します。

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. すべての変更を保存してください。 これで、新しいコンテンツをAEMインスタンスに同期できます。

1. Serversパネルで、接続が開始されていることを確認します。開始していない場合は確認します。
1. 「**クリーンアップして公開**」アイコンをクリックします。

完了したら、インスタンスでパッケージを実行させ、保存すると、変更が自動的にインスタンスに同期されます。

プロジェクトからパッケージを再構築する場合は、`PROJECT.ui.apps`または`PROJECT.ui.content`を右クリックし、「**Run As** -> **Maven Install**」を選択します。

これで、パッケージを含むターゲットフォルダーが作成されました(`PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`)。

## トラブルシューティング {#troubleshooting}

### 無効なプロジェクト定義の解決 {#resolving-invalid-project-definition}

無効な依存関係およびプロジェクト定義を解決するには、次の手順を実行します。

1. 作成したプロジェクトをすべて選択します。
1. 右クリックします。
1. コンテキストメニューで、「**Maven** -> **プロジェクトを更新**」を選択します。
1. 「**Force Updates of Snapshot/Releases**」をオンにします。
1. 「**OK**」をクリックします。

Eclipseは必要な依存関係をダウンロードします。 これには少し時間がかかるかもしれません。

## 詳細情報 {#more-information}

Apache Sling IDE tooling for Eclipse の公式 Web サイトでは、次の役立つ情報を参照できます。

* [**Apache Sling IDEツール（『Eclipse**&#x200B;ユーザガイド](https://sling.apache.org/documentation/development/ide-tooling.html)』）では、このドキュメントを使用して、AEM開発ツールでサポートされる全体的な概念、サーバー統合およびデプロイメント機能を説明します。
* [トラブルシューティング情報](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [既知の問題リスト](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

次の公式の [Eclipse](https://eclipse.org/) ドキュメントは、環境の設定に役立ちます。

* [Eclipse 使用の手引き](https://eclipse.org/users/)
* [Eclipse Luna ヘルプシステム](https://help.eclipse.org/luna/index.jsp)
* [Maven 統合（m2eclipse）](https://www.eclipse.org/m2e/)
