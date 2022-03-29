---
title: Experience Manager Sites ページでフォームポータルを作成する方法
description: フォームポータルを作成し、標準搭載のコアコンポーネントを AEM Sites ページで使用する方法を説明します。
exl-id: 13cfe3ba-2e85-46bf-a029-2673de69c626
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1784'
ht-degree: 100%

---

# ポータル上のアダプティブフォームを一覧表示 {#publish-forms-on-portal}

一般的なフォーム中心のポータル展開シナリオでは、フォームの開発とポータルの開発が別々に行われます。フォーム開発者はフォームを設計してリポジトリに保存する一方、Web 開発者は Web アプリケーションを作成してフォームを一覧表示し、フォームの送信を処理します。フォームリポジトリと Web アプリケーション間では通信が行われないため、フォームは Web 層にコピーされます。

このようなシナリオでは、管理問題が発生したり生産が遅延したりすることがよくあります。例えば、リポジトリで新しいバージョンのフォームを利用できる場合、Web 層でフォームを置換し、Web アプリケーションを変更し、公共サイトでフォームを再展開する必要があります。Web アプリケーションの再展開によって、サーバーのダウンタイムが発生する可能性があります。通常、サーバーのダウンタイムは計画的に行われるため、変更を瞬時に公共サイトにプッシュすることはできません。

AEM Forms は管理のオーバーヘッドと実稼働の遅延を低減するポータルコンポーネントを提供します。コンポーネントにより、web 開発者は Adobe Experience Manager（AEM）を使用して作成された web サイト上にフォームポータルを作成してカスタマイズできます。

フォームポータルコンポーネントにより、次の機能が追加されます。

* カスタマイズしたレイアウトでフォームを一覧表示します。標準搭載で、リスト表示およびカード表示が提供されます。独自のカスタムレイアウトを作成できます。
* カスタムメタデータとカスタムアクションをリストにしながら表示できます。
* フォームポータルコンポーネントを使用しているパブリッシュインスタンス上の AEM Forms UI が発行したフォームを一覧表示します。
* エンドユーザーが HTML 形式および PDF 形式でフォームをレンダリングできるようにします。
* タイトルと説明に基づいてフォームを検索できるようにします。
* カスタム CSS を使用してポータルのルックアンドフィールをカスタマイズします。
* フォームへのリンクを作成します。
* エンドユーザーが作成したアダプティブフォームに関連するドラフトおよび送信をリスト表示します。

## フォームポータルページのコンポーネント {#forms-portal-components}

AEM Forms は、次のポータルコンポーネントを標準搭載しています。

* 検索とリスター：このコンポーネントを使用すると、フォームリポジトリからポータルページにフォームを一覧表示でき、指定した基準に基づいてフォームを一覧表示するための設定オプションが提供されます。

* ドラフトと送信：「検索とリスター」コンポーネントはフォーム作成者が発行しれたフォームを表示するのに対し、「ドラフトと送信」コンポーネントはドラフトとして保存され、後で完了して送信されるフォームを表示します。このコンポーネントはログインユーザーに対してパーソナライズされたエクスペリエンスを提供します。

* Link：このコンポーネントを使用すると、ページの任意の場所にフォームへのリンクを作成できます。

AEM プロジェクトアーキタイプから [標準搭載のフォームポータルコンポーネントを読み込む](#import-forms-portal-components-aem-archetype) ことができます。 読み込んだ後、次の設定を実行します。
* [外部ストレージの設定](#configure-azure-storage-adaptive-forms)
* [フォームポータルコンポーネントを有効にする](#enable-forms-portal-components)
* [フォームポータルコンポーネントの設定](#configure-forms-portal-components)

## フォームポータルコンポーネントの読み込み {#import-forms-portal-components-aem-archetype}

標準搭載のフォームポータルコンポーネントを AEM Forms as a Cloud Service に読み込むには、次の手順を実行します。

1. **ローカル開発インスタンス上に Cloud Manager Git リポジトリーを複製する：** Cloud Manager Git リポジトリーには、デフォルトの AEM プロジェクトが含まれています。[AEM アーキタイプ](https://github.com/adobe/aem-project-archetype/)に基づいています。Cloud Manager UI のセルフサービス Git アカウント管理を使用して Cloud Manager Git リポジトリーを複製し、プロジェクトをローカル開発環境に移行します。リポジトリへのアクセスについて詳しくは、 [リポジトリへのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html?lang=ja) を参照してください。

1. **[!DNL Experience Manager Forms] as a [Cloud Service] プロジェクトの作成：** [AEM アーキタイプ 27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) 以降に基づいて [!DNL Experience Manager Forms] as a [Cloud Service] プロジェクトを作成します。このアーキタイプは、開発者が [!DNL AEM Forms] as a Cloud Service の開発を容易に開始するのに役立ちます。また、すぐに使い始めるのに役立つテーマとテンプレートのサンプルも含まれています。

   [!DNL Experience Manager Forms] as a Cloud Service プロジェクトを作成するには、コマンドプロンプトを開き、以下のコマンドを実行します。[!DNL Forms] に特有の設定、テーマおよびテンプレートを含めるには、`includeForms=y` を設定します。

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   また、上記のコマンドで `appTitle`、`appId`、`groupId` を変更し、環境に反映します。

1. **プレリリースで、次の手順を実行して Forms Portal コンポーネントを使用します。**
   * [プレリリースチャネルを有効にします](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja)。
   * アーキタイププロジェクトのトップレベル `pom.xml` の `<core.forms.components.version>x.y.z</core.forms.components.version>` プロパティを更新して、`Cloud Manager/AEM Archetype` プロジェクトの `core-forms-components-*` バージョンを目的のプレリリースバージョン（例えば、1.0.4-PRERELEASE-20211223）に置き換えます。

1. **プロジェクトをローカル開発環境にデプロイ：** 次のコマンドを使用して、ローカル開発環境にデプロイできます

   `mvn -PautoInstallPackage clean install`

   コマンドの完全なリストについては、 [構築とインストール](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=ja#building-and-installing) を参照してください

1. [ [!DNL AEM Forms]  as a Cloud Service 環境にコードをデプロイします](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=ja#embeddeds)。


## アダプティブフォーム用の Azure ストレージの設定 {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] データ統合](data-integration.md) は、フォームを [!DNL Azure] ストレージサービスと統合するための [!DNL Azure] ストレージ設定を提供します。フォームデータモデルを使用して、[!DNL Azure] サーバーと連携するアダプティブフォームを作成することにより、ビジネスワークフローを使用できるようになります。

### Azure ストレージ設定の作成 {#create-azure-storage-configuration}

これらの手順を実行する前に、Azure ストレージアカウントと、[!DNL Azure] ストレージアカウントへのアクセスを許可するためのアクセスキーがあることを確認してください。

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Azure ストレージ]**&#x200B;に移動します。
1. 設定を作成するフォルダーを選択して、「**[!UICONTROL 作成]**」をタップします。
1. 「**[!UICONTROL タイトル]**」フィールドで設定のタイトルを指定します。
1. 「**[!UICONTROL Azure ストレージアカウント]**」フィールドで [!DNL Azure] ストレージアカウントの名前を指定します。

### フォームポータル用統合ストレージコネクタの設定 {#configure-usc-forms-portal}

AEM ワークフロー用の統合ストレージコネクタを設定するには、次の手順を実行します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Forms]**／**[!UICONTROL 統合ストレージコネクタ]**&#x200B;に移動します。
1. 「**[!UICONTROL フォームポータル]**」セクションで、「**[!UICONTROL ストレージ]**」ドロップダウンリストから「**[!UICONTROL Azure]**」を選択します。
1. 「**[!UICONTROL ストレージ設定パス]**」フィールドで、[Azure ストレージ設定の設定パス](#create-azure-storage-configuration)を指定します。
1. 「**[!UICONTROL 公開]**」をタップしてから、「**[!UICONTROL 保存]**」をタップして設定を保存します。

## フォームポータルコンポーネントを有効にする {#enable-forms-portal-components}

Adobe Experience Manager（AEM）サイトで任意のコアコンポーネント（標準のポータルコンポーネントを含む）を使用するには、プロキシコンポーネントを作成して、サイトに対してそれを有効にする必要があります。プロキシコンポーネントの作成とポータルコンポーネントの有効化については、 [コアコンポーネントの使用](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=ja#create-proxy-components) を参照してください。

ポータルコンポーネントを有効にすると、サイトページのオーサーインスタンスで使用できるようになります。

## フォームポータルコンポーネントの追加と設定 {#configure-forms-portal-components}

ポータルコンポーネントを追加して設定すると、AEM を使用して作成した web サイトでフォームポータルを作成してカスタマイズできます。フォームポータルで使用する前に、 [コンポーネントが有効になっていること](#enable-forms-portal-components) を確認してください。

コンポーネントを追加するには、コンポーネントパネルからページのレイアウトコンテナにコンポーネントをドラッグ＆ドロップするか、レイアウトコンテナ上の追加アイコンをタップして、[!UICONTROL 新規コンポーネントの挿入] ダイアログからコンポーネントを追加します。

### 下書きと送信コンポーネントの設定 {#configure-drafts-submissions-component}

下書きと送信コンポーネントには、後で完成させるために下書きとして保存されているフォームと送信済みのフォームが表示されます。設定するには、コンポーネントをタップしてから ![設定アイコン](assets/configure_icon.png) をタップします。[!UICONTROL 下書きと送信] ダイアログで、フォームを下書きまたは送信済みのフォームとして示すタイトルを指定します。また、下書きのフォームまたは送信済みのフォームを、カード形式またはリスト形式でコンポーネントが一覧表示するかどうかを選択します。

![下書きアイコン](assets/drafts-component.png)

![送信アイコン](assets/submission-listing.png)

### 検索とリスターコンポーネントの設定 {#configure-search-lister-component}

検索とリスターコンポーネントは、ページ上のアダプティブフォームをリスト表示し、リストに表示されたフォームに検索を実装するために使用します。

![検索とリスターアイコン](assets/search-and-lister-component.png)

設定するには、コンポーネントをタップしてから ![設定アイコン](assets/configure_icon.png) をタップします。[!UICONTROL 検索とリスター] ダイアログが開きます。

1. 「[!UICONTROL 表示]」タブで以下を設定します。
   * **[!UICONTROL タイトル]** で、検索とリスターコンポーネントのタイトルを指定します。特徴的なタイトルを使用すると、ユーザーはフォームのリスト全体ですばやく検索を実行できます。
   * **[!UICONTROL レイアウト]** リストで、フォームをカード形式またはリスト形式で表すレイアウトを選択します。
   * 「**[!UICONTROL 検索を非表示]**」および「**[!UICONTROL 並べ替えを非表示]**」を選択し、検索機能と並べ替え機能を非表示にします。
   * **[!UICONTROL ツールヒント]** で、コンポーネントにカーソルを合わせたときに表示されるツールヒントを指定します。
1. 「[!UICONTROL アセットフォルダー]」タブで、フォームを取得してページに一覧表示する場所を指定します。複数のフォルダーの場所を設定できます。
1. 「[!UICONTROL 結果]」タブで、1 ページに表示するフォームの最大数を設定します。デフォルトでは、1 ページに 8 つのフォームです。

### リンクコンポーネントを設定 {#configure-link-component}

リンクコンポーネントを使用すると、ページ上のアダプティブフォームへのリンクを提供できます。設定するには、コンポーネントをタップしてから、 ![設定アイコン](assets/configure_icon.png) をタップします。[!UICONTROL リンクコンポーネントを編集] ダイアログが開きます。

1. リンクで表されたフォームを容易に識別できるように、「[!UICONTROL 表示]」タブでリンクのキャプションとツールヒントを指定します。
1. 「[!UICONTROL アセット情報]」タブで、アセットが保存されているリポジトリパスを指定します。
1.  「[!UICONTROL クエリパラメーター]」タブで、追加のパラメーターをキーと値のペアの形式で指定します。リンクをクリックすると、これらのその他のパラメーターはフォームと共に渡されます。

## Adobe Sign を使用した非同期フォーム送信の設定 {#configure-asynchronous-form-submission-using-adobe-sign}

アダプティブフォームを送信する設定は、すべての受信者が署名行為を完了した場合にのみ行うことができます。Adobe Sign を使用して設定を指定するには、次の手順に従います。

1. オーサーインスタンスで、アダプティブフォームを編集モードで開きます。
1. 左側のウィンドウで「プロパティ」アイコンをタップし、「**[!UICONTROL 電子署名]**」オプションを展開します。
1. 「**[!UICONTROL Adobe Sign を有効にする]**」を選択します。様々な設定オプションが表示されます。
1. 「[!UICONTROL フォームを送信]」セクションで、「**[!UICONTROL すべての受信者が署名行為を完了した後]**」オプションを選択して、「フォームを送信」アクションを設定します。このアクションでは、最初にすべての受信者にフォームが送信されて署名されます。すべての受信者がフォームに署名したときにのみ、そのフォームが送信されます。

## アダプティブフォームを下書きとして保存 {#save-adaptive-forms-as-drafts}

フォームを下書きとして保存し、後で完成させることができます。フォームを下書きとして保存する方法は 2 つあります。
* フォームコンポーネント（ボタンなど）に「フォームを保存」ルールを作成します。このボタンをクリックすると、ルールトリガーとフォームがドラフトとして保存されます。
* 自動保存機能を有効にします。これにより、指定されたイベントごとに、または設定された時間間隔の後にフォームが保存されます。

### アダプティブフォームをドラフトとして保存するためのルールの作成 {#rule-to-save-adaptive-form-as-draft}

フォームコンポーネント（ボタンなど）に「フォームを保存」ルールを作成するには、次の手順に従います。

1. オーサーインスタンスで、アダプティブフォームを編集モードで開きます。
1. 左側のウィンドウで、 ![「コンポーネント」アイコン](assets/components_icon.png) をタップし、「[!UICONTROL ボタン]」コンポーネントをフォームにドラッグします。
1. 「[!UICONTROL ボタン]」コンポーネントをタップしてから、 ![「設定」アイコン](assets/configure_icon.png) をタップします。
1. 「[!UICONTROL ルールを編集]」アイコンをタップして、ルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」をタップし、ルールを設定および作成します。
1. 「[!UICONTROL 条件]」セクションで、「クリック済み」を選択し、「[!UICONTROL 次に]」セクションで「フォームを保存」オプションを選択します。
1. 「**[!UICONTROL 完了]**」をタップして、ルールを保存します。

### 自動保存を有効にする {#enable-auto-save}

アダプティブフォームの自動保存機能は、次のように設定することができます。

1. オーサーインスタンスで、アダプティブフォームを編集モードで開きます。
1. 左側のウィンドウで、 ![プロパティアイコン](assets/configure_icon.png) をクリックし、「[!UICONTROL 自動保存]」オプションを展開します。
1. 「**[!UICONTROL 有効]**」 チェックボックスをオンにし、フォームの自動保存を有効にします。次の項目を設定できます。
* デフォルトでは、[!UICONTROL アダプティブフォームイベント] が「true」に設定されている場合は、イベントのたびにフォームが自動保存されます。
* [!UICONTROL トリガー] で、イベントの発生に基づいて、または特定の時間間隔の経過後に自動保存をトリガーするように設定します。
