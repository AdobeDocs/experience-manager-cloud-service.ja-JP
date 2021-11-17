---
title: パッケージマネージャー
description: AE の基本を学ぶ。パッケージマネージャーを使用したパッケージ管理。
feature: Administering
role: Admin
source-git-commit: 108ebef7e2ea79323d873a126cc89aef26faae60
workflow-type: tm+mt
source-wordcount: '3584'
ht-degree: 14%

---


# パッケージマネージャー {#working-with-packages}

パッケージを使用すると、リポジトリコンテンツのインポートおよびエクスポートが可能になります。 パッケージを使用して、新しいコンテンツのインストール、インスタンス間でのコンテンツの転送、リポジトリコンテンツのバックアップをおこなうことができます。

パッケージマネージャーを使用すると、開発目的で、AEMインスタンスとローカルファイルシステムの間でパッケージを転送できます。

## パッケージとは {#what-are-packages}

パッケージとは、リポジトリコンテンツをファイルシステムのシリアル化形式で保持する zip ファイルで、vault のシリアル化と呼ばれ、使いやすく編集しやすい形式でファイルやフォルダを表現します。 パッケージに含まれるコンテンツは、フィルターを使用して定義します。

パッケージには、フィルタ定義や読み込み設定情報などの Vault メタ情報も含まれています。 説明、視覚的な画像、アイコンなど、パッケージの抽出には使用されない追加のコンテンツプロパティをパッケージに含めることができます。 これらの追加のコンテンツプロパティは、コンテンツパッケージコンシューマー向けのもので、情報提供だけを目的としています。

>[!NOTE]
>
>パッケージは、そのパッケージを作成した時点におけるコンテンツの現在のバージョンを表しています。AEM がリポジトリに保持している以前のバージョンのコンテンツは含まれません。

## Packages in AEM as a Cloud Service {#aemaacs-packages}

AEMas a Cloud Serviceのアプリケーション用に作成されたコンテンツパッケージでは、不変コンテンツと可変コンテンツを明確に分離する必要があります。 したがって、パッケージマネージャーは、コンテンツを含むパッケージの管理にのみ使用できます。 任意のコードは、Cloud Manager を使用してデプロイする必要があります。

>[!NOTE]
>
>パッケージには、コンテンツのみを含めることができます。 すべての機能 ( 例： `/apps`) は [Cloud Manager の CI/CD パイプラインを使用してデプロイされます。](/help/implementing/cloud-manager/deploy-code.md)

>[!IMPORTANT]
>
>パッケージマネージャー UI で **未定義** パッケージのインストールに 10 分以上かかる場合のエラーメッセージ。
>
>これは、インストールのエラーによるものではなく、すべての要求に対してCloud Serviceが持つタイムアウトのためです。
>
>このようなエラーが表示された場合は、インストールを再試行しないでください。 インストールはバックグラウンドで正しく進行しています。 インストールを再起動すると、複数の同時インポートプロセスによって競合が発生する可能性があります。

AEMaaCS 用のパッケージを管理する方法の詳細については、このドキュメントを参照してください [AEMへのデプロイ (as a Cloud Service)](/help/implementing/deploying/overview.md) （デプロイユーザーガイド）。

## パッケージマネージャー {#package-manager}

Package Manager manages the packages on your AEM installation. [](#permissions-needed-for-using-the-package-manager)

### 必要な権限 {#required-permissions}

パッケージを作成、変更、アップロード、インストールするには、次のノードに対する適切な権限が必要です。

* 削除を除く完全な権限 `/etc/packages`
* The node that contains the package contents

>[!CAUTION]
>
>パッケージに対する権限を付与すると、機密情報の開示やデータの損失が発生する場合があります。
>
>これらのリスクを制限するには、専用のサブツリーに対してのみ特定のグループ権限を付与することを強くお勧めします。

### パッケージマネージャーへのアクセス {#accessing}

パッケージマネージャーには次の 3 つの方法でアクセスできます。

1. AEMのメインメニューから —> **ツール** -> **導入** -> **パッケージ**
1. 送信者 [CRXDE Lite](crxde.md) 上部のスイッチャーバーの使用
1. に直接アクセス `http://<host>:<port>/crx/packmgr/`

### パッケージマネージャー UI {#ui}

パッケージマネージャーは、次の 4 つの主な機能領域に分かれています。

* **左ナビゲーションパネル**  — このパネルでは、パッケージのリストをフィルタリングおよび並べ替えることができます。
* **パッケージリスト**  — これは、左側のナビゲーションパネルでの選択に従ってフィルタリングおよび並べ替えられた、インスタンス上のパッケージのリストです。
* **アクティビティログ**  — このパネルは最初は最小化され、パッケージのビルド時やインストール時など、パッケージマネージャーのアクティビティの詳細を表示するように拡張されます。 「アクティビティログ」タブには、次の操作を行うための追加のボタンがあります。
   * ****
   * **表示／非表示**
* **ツールバー**  — ツールバーには、左側のナビゲーションパネルとパッケージリスト用の更新ボタン、およびパッケージを検索、作成、アップロードするためのボタンが含まれています。

![パッケージマネージャー UI](assets/package-manager-ui.png)

左側のナビゲーションパネルでオプションをクリックすると、パッケージリストが直ちにフィルタリングされます。

パッケージ名をクリックすると、「パッケージリスト」のエントリが展開され、パッケージの詳細が表示されます。

![拡張されたパッケージの詳細](assets/package-expand.png)

パッケージの詳細を展開する際に使用できるツールバーボタンを使用して、パッケージで実行できるアクションは多数あります。

* [編集](#edit-package)
* [ビルド](#building-a-package)
* [再インストール](#reinstalling-packages)
* [ダウンロード](#downloading-packages-to-your-file-system)

その他のアクションは、 **詳細** 」ボタンをクリックします。

* [削除](#deleting-packages)
* [カバレッジ](#package-coverage)
* [目次](#viewing-package-contents-and-testing-installation)
* [再折り返し](#rewrapping-a-package)
* [その他のバージョン](#other-versions)
* [アンインストール](#uninstalling-packages)
* [Test Install](#viewing-package-contents-and-testing-installation)
* [Validate（検証）](#validating-packages)
* [レプリケーション](#replicating-packages)

### パッケージステータス {#package-status}

パッケージリスト内の各エントリには、パッケージのステータスを一目で把握できるステータスインジケーターが表示されます。 ステータスの上にマウスポインターを置くと、ステータスの詳細を示すツールチップが表示されます。

![パッケージのステータス](assets/package-status.png)

パッケージが変更された、またはビルドされなかった場合、ステータスは、パッケージを再構築またはインストールするためのクイックアクションを実行するためのリンクとして表示されます。

## パッケージ設定 {#package-settings}

パッケージとは基本的に、一連のフィルターと、これらのフィルターに基づくリポジトリデータです。 パッケージマネージャーの UI を使用して、パッケージをクリックし、 **編集** ボタンをクリックすると、次の設定を含むパッケージの詳細が表示されます。

* [一般設定](#general-settings)
* [パッケージフィルター](#package-filters)
* [パッケージの依存関係](#package-dependencies)
* [詳細設定](#advanced-settings)
* [パッケージスクリーンショット](#package-screenshots)

### 一般設定 {#general-settings}

You can edit a variety of package settings to define information such as the package description, dependencies, and provider details.

この **パッケージ設定** ダイアログは、 **編集** ボタンを [作成中](#creating-a-new-package) または [編集中](#viewing-and-editing-package-information) パッケージ。 変更が完了したら、「 **保存**.

![パッケージを編集ダイアログ、一般設定](assets/general-settings.png)

| フィールド | 説明 |
|---|---|
| 名前 | The name of the package |
| グループ | パッケージを整理するために、新しいグループの名前を入力するか、既存のグループを選択できます |
| バージョン | Text to use for the version |
| 説明 | 書式設定用のHTMLマークアップを許可するパッケージの簡単な説明 |
| サムネール | パッケージリストと共に表示されるアイコン |

### パッケージフィルター {#package-filters}

****

* ****
* ****

を使用してルールを追加する **+** 」ボタンをクリックします。 次を使用してルールを削除： **-** 」ボタンをクリックします。

ルールは順序に従って適用され、必要に応じて **上** および **下** 矢印ボタン

Filters can include zero or more rules. When no rules are defined, the package contains all content below the root path.

You can define one or more filter definitions for a package. Use more than one filter to include content from multiple root paths.

![「フィルター」タブ](assets/edit-filter.png)

フィルターを作成する際に、パスを定義するか、正規表現を使用して、含めるまたは除外するすべてのノードを指定できます。

| Rule Type | 説明 |
|---|---|
| include | **** |
| exclude | Excluding a directory will exclude that directory and all files and folders in that directory (i.e. the entire subtree). |

パッケージフィルターは、最初に [パッケージを作成します。](#creating-a-new-package) ただし、後で編集することもでき、その後、パッケージを再構築して、新しいフィルター定義に基づいてその内容を更新する必要があります。

>[!TIP]
>
>One package can contain multiple filter definitions so that nodes from different locations can easily be combined into one package.

### 依存関係 {#dependencies}

![「依存関係」タブ](assets/dependencies.png)

| フィールド | 説明 | 例/詳細 |
|---|---|---|
| Tested with | このパッケージのターゲットまたは互換性のある製品名およびバージョン。 | `AEMaaCS` |
| 修正された問題 | このパッケージで修正されたバグの詳細をリストするテキストフィールド。1 行に 1 つのバグが表示されます。 | - |
| 依存 | 現在のパッケージがインストール時に期待どおりに実行されるように、必要なその他のパッケージをリストします | `groupId:name:version` |
| 置き換え | このパッケージで置き換えられる、廃止されたパッケージのリスト | `groupId:name:version` |

### 詳細設定 {#advanced-settings}

![「詳細設定」タブ](assets/advanced-settings.png)

| フィールド | 説明 | 例/詳細 |
|---|---|---|
| 名前 | パッケージのプロバイダーの名前 | `WKND Media Group` |
| URL | URL of the provider | `https://wknd.site` |
| リンク | Package-specific link to a provider page | `https://wknd.site/package/` |
| 次を必要とする | パッケージのインストール時に制限があるかどうかを定義します | **管理者**  — パッケージは管理者権限でのみインストールする必要があります&#x200B;<br>**再起動** - AEMはパッケージのインストール後に再起動する必要があります |
| AC の処理 | Specifies how the access control information defined in the package is handled when the package is imported | **無視**  — リポジトリ内の ACL を保持&#x200B;<br>**上書き**  — リポジトリ内の ACL を上書き&#x200B;<br>**結合**  — 両方の ACL セットをマージする&#x200B;<br>**MergePreserve**  — コンテンツ内に存在しないプリンシパルのアクセス制御エントリを追加して、コンテンツ内のアクセス制御をパッケージに付属するエントリと結合します&#x200B;<br>**クリア** - ACL をクリア |

### パッケージスクリーンショット {#package-screenshots}

パッケージに複数のスクリーンショットを添付して、コンテンツがどのように表示されるかを視覚的に示すことができます。

![「スクリーンショット」タブ](assets/screenshots.png)

## パッケージアクション {#package-actions}

1 つのパッケージで実行できるアクションは多数あります。

### Creating a Package {#creating-a-new-package}

1. [パッケージマネージャーにアクセスします。](#accessing)

1. 「**パッケージを作成**」をクリックします。

   >[!TIP]
   >
   >インスタンスに多数のパッケージがある場合は、フォルダー構造が存在する可能性があります。 そのような場合は、新しいパッケージを作成する前に必要なターゲットフォルダーに移動する方が簡単です。

1. 内 **新規パッケージ** ダイアログで、次のフィールドを入力します。

   ![新規パッケージダイアログ](assets/new-package-dialog.png)

   * **パッケージ名**  — パッケージのコンテンツを（その他のユーザーが）簡単に識別できるように、説明的な名前を選択します。

   * **バージョン**  — これは、バージョンを示すためのテキストフィールドです。 これがパッケージ名に追加され、zip ファイルの名前が形成されます。

   * **グループ**  — ターゲットグループ（またはフォルダー）の名前です。 グループは、パッケージの整理に役立ちます。 グループのフォルダーがまだ存在しない場合は作成されます。 グループ名を空白のままにすると、メインのパッケージリストにパッケージが作成されます。

1. 「**OK**」をクリックしてパッケージを作成します。

1. AEMでは、新しいパッケージがパッケージのリストの最上部に表示されます。

   ![](assets/new-package.png)

1. クリック **編集** を定義するには、 [パッケージの内容。](#package-contents)****

1. これで、パッケージを[ビルド](#building-a-package)できます。

パッケージを作成した後すぐにビルドする必要はありません。 未ビルドパッケージにはコンテンツが含まれず、フィルターデータとパッケージの他のメタデータのみで構成されます。

### パッケージのビルド {#building-a-package}

多くの場合、パッケージはユーザーと同時に構築されます [パッケージを作成](#creating-a-new-package)に変更された場合は、後で戻って、パッケージをビルドまたは再構築できます。 これは、リポジトリ内のコンテンツが変更された場合や、パッケージフィルターが変更された場合に役立ちます。

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、パッケージリストからパッケージの詳細を開きます。

1. ****&#x200B;既存のパッケージの内容が上書きされるので、パッケージをビルドするかどうかを確認するダイアログが表示されます。

1. 「**OK**」をクリックします。AEMがパッケージをビルドし、パッケージに追加されたすべてのコンテンツがアクティビティリストに表示されます。 パッケージの構築が完了すると、パッケージが構築されたことを示すダイアログが表示されます。また、（このダイアログを閉じると）パッケージリストの内容が更新されます。

### パッケージの編集 {#edit-package}

パッケージをAEMにアップロードした後は、その設定を変更できます。

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、パッケージリストからパッケージの詳細を開きます。

1. クリック **編集** を更新し、 **[パッケージ設定](#package-settings)** 必要に応じて。

1. ****

必要に応じて、 [パッケージを再構築します。](#building-a-package) をクリックして、変更に基づいてコンテンツを更新します。

### パッケージを再度含める {#rewrapping-a-package}

Once a package has been built, it can be rewrapped. 再ラップは、パッケージのコンテンツを変更せずに、サムネール、説明などを含まずにパッケージ情報を変更します。

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、パッケージリストからパッケージの詳細を開きます。

1. クリック **編集** を更新し、 **[パッケージ設定](#package-settings)** 必要に応じて。

1. クリック **保存** 保存します。

1. ********

### 他のパッケージバージョンの表示 {#other-versions}

パッケージのすべてのバージョンは他のパッケージとしてリストに表示されるので、パッケージマネージャーは選択したパッケージの他のバージョンを検索できます。

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、パッケージリストからパッケージの詳細を開きます。

1. クリック **詳細** -> **その他のバージョン** ダイアログが開き、同じパッケージの他のバージョンとステータス情報が表示されます。

### パッケージコンテンツの表示とインストールのテスト {#viewing-package-contents-and-testing-installation}

After a package has been built, you can view the contents.

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、パッケージリストからパッケージの詳細を開きます。

1. コンテンツを表示するには、 **詳細** -> **内容**、およびパッケージマネージャーには、パッケージのコンテンツ全体がアクティビティログにリストされます。

   ![パッケージコンテンツ](assets/package-contents.png)

1. インストールのドライランを実行するには、をクリックします。 **詳細** -> **インストールをテスト** 「パッケージマネージャー」レポートと「 」アクティビティで、インストールが実行された場合と同じように結果がログに記録されます。

   ![インストールのテスト](assets/test-install.png)

### ファイルシステムへのパッケージのダウンロード {#downloading-packages-to-your-file-system}

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、パッケージリストからパッケージの詳細を開きます。

1. 次をクリック： **ダウンロード** ボタンまたはパッケージのリンクされたファイル名（パッケージの詳細領域内）

1. AEMがお使いのコンピューターにパッケージをダウンロードします。

### ファイルシステムからのパッケージのアップロード {#uploading-packages-from-your-file-system}

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージのアップロード先となるグループフォルダーを選択します。

1. 次をクリック： **パッケージをアップロード** 」ボタンをクリックします。

1. アップロードしたパッケージに関する必要な情報を入力します。

   ![パッケージのアップロードダイアログ](assets/package-upload-dialog.png)

   * **パッケージ** - **参照…** ボタンをクリックして、必要なパッケージをローカルファイルシステムから選択します。
   * **アップロードを強制**  — この名前のパッケージが既に存在する場合は、このオプションを選択すると、アップロードが強制され、既存のパッケージが上書きされます。

1. クリック **OK** 選択したパッケージがアップロードされ、それに応じてパッケージリストが更新されます。

パッケージコンテンツがAEMに存在しますが、コンテンツを使用できるようにするには、必ず [パッケージをインストール](#installing-packages).

### パッケージの検証 {#validating-packages}

パッケージは既存のコンテンツを変更する可能性があるので、多くの場合、インストール前にこれらの変更を検証すると便利です。

#### 検証オプション {#validation-options}

パッケージマネージャーは次の検証を実行できます。

* [OSGi パッケージの読み込み](#osgi-package-imports)
* [オーバーレイ](#overlays)
* [ACL](#acls)

##### OSGi パッケージの読み込みを検証 {#osgi-package-imports}

>[!NOTE]
>
>AEMaaCS でのコードのデプロイにパッケージを使用できないので、 **OSGi パッケージのインポート** 検証は不要です。

**チェック内容**

`manifest.xml`

**レポート方法**

Any versioned dependencies that cannot be satisfied by the AEM instance are listed in the Activity Log of Package Manager.

**エラーの状態**

未解決の依存関係がある場合、それらの依存関係を持つパッケージ内の OSGi バンドルは開始しません。This results in a broken application deployment as anything relying on the unstarted OSGi bundle will in turn not function properly.

**エラーの解決**

To resolve errors due to unsatisfied OSGi bundles, the dependency version in the bundle with unsatisfied imports must be adjusted.

##### オーバーレイを検証 {#overlays}

>[!NOTE]
>
>AEMaaCS でのコードのデプロイにパッケージを使用できないので、 **オーバーレイ** 検証は不要です。

**確認内容**

この検証では、インストールするパッケージに、宛先の AEM インスタンスにすでにオーバーレイされているファイルが含まれているかどうかを確認します。

`/apps/sling/servlet/errorhandler/404.jsp``/libs/sling/servlet/errorhandler/404.jsp``/libs/sling/servlet/errorhandler/404.jsp`

**レポートの内容**

Any such overlays are described in the Activity Log of Package Manager.

**エラー状態**

パッケージがすでにオーバーレイされているファイルをデプロイしようとしています。したがって、パッケージ内の変更はオーバーレイによって上書きされ（つまり「非表示」となり）、有効になりません。

**エラーの解決**

`/apps``/libs``/apps`

>[!NOTE]
>
>The validation mechanism has no way to reconcile if the overlaid content has been properly incorporated into the overlay file. したがって、この検証では、必要な変更が加えられた後も競合についてレポートし続けます。

##### ACL を検証 {#acls}

**確認内容**

この検証では、どの権限が追加されるか、それらがどのように処理されるか（マージ／置換）、および現在の権限が影響を受けるかどうかを確認します。

**レポートの内容**

The permissions are described in the Activity Log of Package Manager.

**エラー状態**

明示的なエラーはありません。この検証は、パッケージをインストールすることで新しい ACL 権限が追加されるか、または影響があるかどうかを示すだけです。

**エラーの解決**

検証によって提供された情報を使用して、影響を受けたノードを CRXDE で確認したり、必要に応じて ACL をパッケージ内で調整したりできます。

>[!CAUTION]
>
>As best practice it is recommended that packages should not affect AEM-provided ACLs as this may result in unexpected behavior.

#### 検証の実行 {#performing-validation}

パッケージの検証は 2 とおりの方法で行うことができます。

* [パッケージマネージャーの UI から](#via-package-manager)
* [cURL などの HTTP POST リクエストを介して](#via-post-request)

検証は、パッケージをアップロードした後で、インストールする前に必ず行う必要があります。

##### Package Validation Via Package Manager {#via-package-manager}

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、パッケージリストからパッケージの詳細を開きます。

1. パッケージを検証するには、 **詳細** -> **検証**,

1. 表示されるモーダルダイアログボックスで、チェックボックスを使用して検証の種類を選択し、「**検証**」をクリックして検証を開始します。

1. 選択した検証が実行され、結果がパッケージマネージャーのアクティビティログに表示されます。

##### HTTP POST リクエストを介したパッケージ検証 {#via-post-request}

POST リクエストの形式は以下のとおりです。

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

`type`

* `osgiPackageImports`
* `overlays`
* `acls`

`type``osgiPackageImports`

When using cURL, execute a statement similar to the following:

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

POSTリクエストを介して検証する場合、応答は JSON オブジェクトとして返されます。

### パッケージカバレッジの表示 {#package-coverage}

パッケージは、フィルターによって定義されます。 パッケージマネージャーで既存のリポジトリコンテンツにパッケージのフィルターを適用して、パッケージのフィルター定義でカバーされるリポジトリのコンテンツを表示できます。

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、パッケージリストからパッケージの詳細を開きます。

1. クリック **詳細** -> **対象範囲**.

1. 有効範囲の詳細は、アクティビティログにリストされます。

### パッケージのインストール {#installing-packages}

パッケージをアップロードすると、パッケージのコンテンツがリポジトリに追加されるだけですが、アクセスできません。 パッケージのコンテンツを使用するには、アップロードしたパッケージをインストールする必要があります。

>[!CAUTION]
>
>パッケージをインストールすると、既存のコンテンツが上書きまたは削除される可能性があります。必要なコンテンツが削除または上書きされないと確認できる場合にのみ、パッケージをアップロードしてください。

パッケージをインストールする前に、上書きされるコンテンツを含むスナップショットパッケージがパッケージマネージャーによって自動的に作成されます。 This snapshot will be reinstalled if you uninstall your package.

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、インストールするパッケージのパッケージ詳細をパッケージリストから開きます。

1. 次のいずれかをクリックします。 **インストール** 項目の詳細または **インストール** リンクをクリックします。

1. 確認を求めるダイアログが表示され、追加のオプションを指定できます。

   * **抽出のみ**  — スナップショットが作成されず、アンインストールができないように、パッケージのみを抽出します
   * ****
   * **サブパッケージを抽出**  — サブパッケージの自動抽出を有効にする
   * **アクセス制御の処理**  — パッケージのインストール時に、パッケージで定義されたアクセス制御情報を処理する方法を指定します ( オプションは [詳細パッケージ設定](#advanced-settings))
   * **依存関係の処理**  — インストール中の依存関係の処理方法を指定します

1. 「**インストール**」をクリックします。

1. インストールの進行状況の詳細は、アクティビティログに記録されます。

インストールが完了し、成功すると、パッケージリストが更新され、「 **インストール済み** パッケージのステータスに表示されます。

### パッケージの再インストール {#reinstalling-packages}

パッケージの再インストールは、既にインストール済みのパッケージに対して実行されます。この手順は、 [パッケージを初めてインストールします。](#installing-packages)

### ファイルシステムベースのアップロードおよびインストール {#file-system-based-upload-and-installation}

パッケージをインストールする際に、パッケージマネージャーを完全に終了できます。 AEMは、ホストマシンのローカルファイルシステム上の特定の場所に配置されたパッケージを検出し、それらを自動的にアップロードしてインストールできます。

1. AEMのインストールフォルダーに、 `crx-quicksart` jar と `license.properties` ファイル。 という名前のフォルダーを作成します。 `install` under `crx-quickstart` 結果としてパスが生成されます `<aem-home>/crx-quickstart/install`.

1. このフォルダーにパッケージを追加します。 追加したパッケージは、インスタンスに自動的にアップロードおよびインストールされます。

1. アップロードとインストールが完了すると、パッケージマネージャーで、パッケージマネージャー UI を使用してインストールした場合と同じようにパッケージを確認できます。

インスタンスが実行中の場合、パッケージに追加すると、アップロードとインストールが直ちに開始されます。 `install` フォルダー

インスタンスが実行されていない場合、 `install` フォルダは、起動時にアルファベット順にインストールされます。

### パッケージのアンインストール {#uninstalling-packages}

パッケージをアンインストールすると、リポジトリの内容が、インストール前に Package Manager が自動的に作成したスナップショットに戻ります。

1. [パッケージマネージャーにアクセスします。](#accessing)

1. アンインストールするパッケージのパッケージ詳細をパッケージリストから開き、パッケージ名をクリックします。

1. クリック **詳細** -> **アンインストール**&#x200B;をクリックして、リポジトリからこのパッケージのコンテンツを削除します。

1. 確認を要求するダイアログが表示され、行われたすべての変更が一覧表示されます。

1. パッケージが削除され、スナップショットが適用されます。 処理の進行状況がアクティビティログに表示されます。

### Deleting Packages {#deleting-packages}

パッケージを削除すると、その詳細のみがパッケージマネージャーから削除されます。 If this package was already installed, then the installed content will not be deleted.

1. [パッケージマネージャーにアクセスします。](#accessing)

1. パッケージ名をクリックして、削除するパッケージのパッケージ詳細をパッケージリストから開きます。

1. AEM asks for confirmation that you want to delete the package. 「**OK**」をクリックして削除を確認します。

1. パッケージ情報が削除され、詳細がアクティビティログに報告されます。

### パッケージのレプリケーション {#replicating-packages}

Replicate the contents of a package to install it on the publish instance.

1. [パッケージマネージャーにアクセスします。](#accessing)

1. レプリケートするパッケージのパッケージ詳細をパッケージリストから開き、パッケージ名をクリックします。

1. クリック **詳細** -> **複製**.

1. パッケージがレプリケートされ、詳細がアクティビティログにレポートされます。

## Software Distribution {#software-distribution}

AEMパッケージを使用して、AEMaaCS 環境全体でコンテンツを作成および共有できます。

[ソフトウェア配布](https://downloads.experiencecloud.adobe.com) には、AEM ローカル開発 SDK で使用するAEMパッケージが用意されています。 ソフトウェア配布で提供されるAEMパッケージは、Adobeサポートによって明示的に承認されない限り、AEMaaCS クラウド環境にインストールしてはなりません。

詳しくは、 [ソフトウェア配布ドキュメント](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html).
