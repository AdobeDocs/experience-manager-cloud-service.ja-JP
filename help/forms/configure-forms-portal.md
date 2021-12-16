---
title: Experience Manager SitesページでForms Portal を作成する方法は？
description: Forms Portal を作成し、標準搭載のコアコンポーネントをAEM Sitesページで使用する方法を説明します。
source-git-commit: 4c42abfe2cc1b11aefb2b298e883406ca5c17fd2
workflow-type: tm+mt
source-wordcount: '1753'
ht-degree: 26%

---


# ポータル上のアダプティブFormsのリスト {#publish-forms-on-portal}

一般的なフォーム中心のポータル展開シナリオでは、フォームの開発とポータルの開発が別々に行われます。フォーム開発者はフォームを設計してリポジトリに保存する一方、Web 開発者は Web アプリケーションを作成してフォームを一覧表示し、フォームの送信を処理します。フォームリポジトリと Web アプリケーション間では通信が行われないため、フォームは Web 層にコピーされます。

このようなシナリオでは、管理問題が発生したり生産が遅延したりすることがよくあります。例えば、リポジトリで新しいバージョンのフォームを利用できる場合、Web 層でフォームを置換し、Web アプリケーションを変更し、公共サイトでフォームを再展開する必要があります。Web アプリケーションの再展開によって、サーバーのダウンタイムが発生する可能性があります。通常、サーバーのダウンタイムは計画的に行われるため、変更を瞬時に公共サイトにプッシュすることはできません。

AEM Formsは、管理のオーバーヘッドと実稼動の遅延を軽減するポータルコンポーネントを提供します。 このコンポーネントにより、Web 開発者は、Adobe Experience Manager(AEM) を使用して作成された Web サイトでForms Portal を作成し、カスタマイズできます。

フォームポータルコンポーネントを使用すると、次の機能を追加できます。

* カスタマイズしたレイアウトによってフォームを一覧表示する。リスト表示およびカード表示レイアウトが標準で用意されています。 独自のカスタムレイアウトを作成する。
* カスタムメタデータとカスタムアクションをリスト表示時に表示できます。
* フォームポータルコンポーネントを使用しているパブリッシュインスタンス上の AEM Forms UI によって発行されたフォームを一覧表示する。
* エンドユーザーがフォームをHTMLおよびPDF形式でレンダリングできるようにする。
* タイトルと説明に基づくフォームの検索を有効にします。
* カスタム CSS を使用してポータルの外観をカスタマイズする。 
* フォームへのリンクを作成する。
* エンドユーザーが作成したアダプティブFormsに関連するドラフトと送信をリストします。

## Forms Portal ページのコンポーネント {#forms-portal-components}

AEM Formsでは、次のポータルコンポーネントをすぐに使用できます。

* Search &amp; Lister:このコンポーネントを使用すると、フォームリポジトリのフォームをポータルページに一覧表示でき、指定した条件に基づいてフォームを一覧表示する設定オプションを提供します。

* ドラフトと送信：Search &amp; Lister コンポーネントには、Formsの作成者が公開したフォームが表示され、Drafts &amp; Submissions コンポーネントには、後で完了するためにドラフトとして保存されたフォームと送信済みのフォームが表示されます。 このコンポーネントはログインユーザーに対してパーソナライズされたエクスペリエンスを提供します。

* Link:このコンポーネントを使用すると、ページの任意の場所にフォームへのリンクを作成できます。

以下が可能です。 [標準搭載のForms Portal コンポーネントの読み込み](#import-forms-portal-components-aem-archetype) をAEM Project Archetype から取得します。 読み込み後、次の設定を実行します。
* [外部ストレージの設定](#configure-azure-storage-adaptive-forms)
* [Forms Portal コンポーネントの有効化](#enable-forms-portal-components)
* [Forms Portal コンポーネントの設定](#configure-forms-portal-components)

## Forms Portal コンポーネントを読み込む {#import-forms-portal-components-aem-archetype}

標準搭載のForms Portal コンポーネントをAEM Forms as a Cloud Serviceに読み込むには、次の手順を実行します。

1. **ローカル開発インスタンス上に Cloud Manager Git リポジトリーを複製する：** Cloud Manager Git リポジトリーには、デフォルトの AEM プロジェクトが含まれています。[AEM アーキタイプ](https://github.com/adobe/aem-project-archetype/)に基づいています。Cloud Manager UI のセルフサービス Git アカウント管理を使用して Cloud Manager Git リポジトリーを複製し、プロジェクトをローカル開発環境に移行します。リポジトリへのアクセスについて詳しくは、 [リポジトリへのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html?lang=ja).

1. **作成 [!DNL Experience Manager Forms] as a [Cloud Service] プロジェクト：** 作成 [!DNL Experience Manager Forms] as a [Cloud Service] ～に基づくプロジェクト [AEM Archetype 27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) または後で。 このアーキタイプは、開発者が [!DNL AEM Forms] as a Cloud Service の開発を容易に開始するのに役立ちます。また、すぐに使い始めるのに役立つサンプルのテーマとテンプレートも含まれています。

   次の手順で [!DNL Experience Manager Forms] as a Cloud Serviceプロジェクトで、コマンドプロンプトを開き、次のコマンドを実行します。 [!DNL Forms] に特有の設定、テーマおよびテンプレートを含めるには、`includeForms=y` を設定します。

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   また、上記のコマンドで `appTitle`、`appId`、`groupId` を変更し、環境に反映します。

1. **プロジェクトをローカル開発環境にデプロイします。** 次のコマンドを使用して、環境にデプロイできます。ローカル開発

   `mvn -PautoInstallPackage clean install`

   コマンドの完全なリストについては、「[構築とインストール](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=ja#building-and-installing)」を参照してください

1. [コアコンポーネントのアーティファクトを含める](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds) 依存関係は次のようになります。

   ```shell
   <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>{TBD}</artifactId>
               <type>content-package</type>
               <version>{TBD}</version>
   </dependency>
   ```

1. [ [!DNL AEM Forms]  as a Cloud Service 環境にコードをデプロイします](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds)。


## アダプティブForms用の Azure ストレージの設定 {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] データ統合](data-integration.md) 提供 [!DNL Azure] フォームをと統合するためのストレージ設定 [!DNL Azure] ストレージサービス。 フォームデータモデルを使用して、[!DNL Azure] サーバーと連携するアダプティブフォームを作成することにより、ビジネスワークフローを使用できるようになります。

### Azure ストレージ設定の作成 {#create-azure-storage-configuration}

これらの手順を実行する前に、 [!DNL Azure] ストレージアカウントと、 [!DNL Azure] ストレージアカウント。

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Azure ストレージ]**&#x200B;に移動します。
1. 設定を作成するフォルダーを選択して、「**[!UICONTROL 作成]**」をタップします。
1. 「**[!UICONTROL タイトル]**」フィールドで設定のタイトルを指定します。
1. 「**[!UICONTROL Azure ストレージアカウント]**」フィールドで [!DNL Azure] ストレージアカウントの名前を指定します。

### Forms Portal 用統合ストレージコネクタの設定 {#configure-usc-forms-portal}

AEM ワークフロー用の統合ストレージコネクタを設定するには、次の手順を実行します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Forms]**／**[!UICONTROL 統合ストレージコネクタ]**&#x200B;に移動します。
1. 内 **[!UICONTROL Forms Portal]** セクション、選択 **[!UICONTROL Azure]** から **[!UICONTROL ストレージ]** 」ドロップダウンリストから選択できます。
1. 「**[!UICONTROL ストレージ設定パス]**」フィールドで、[Azure ストレージ設定の設定パス](#create-azure-storage-configuration)を指定します。
1. 「**[!UICONTROL 公開]**」をタップしてから、「**[!UICONTROL 保存]**」をタップして設定を保存します。

## Forms Portal コンポーネントの有効化 {#enable-forms-portal-components}

Adobe Experience Manager(AEM) サイトで任意のコアコンポーネント（標準のポータルコンポーネントを含む）を使用するには、プロキシコンポーネントを作成して、サイトで有効にする必要があります。 プロキシコンポーネントの作成とポータルコンポーネントの有効化については、 [コアコンポーネントの使用](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components).

ポータルコンポーネントを有効にすると、サイトページのオーサーインスタンスで使用できるようになります。

## Forms Portal コンポーネントの追加と設定 {#configure-forms-portal-components}

ポータルコンポーネントを追加および設定することで、AEMを使用して作成した Web サイトでForms Portal を作成し、カスタマイズできます。 次を確認します。 [コンポーネントが有効](#enable-forms-portal-components) Forms Portal で使用する前に、

コンポーネントを追加するには、コンポーネントパネルからページのレイアウトコンテナにコンポーネントをドラッグ&amp;ドロップするか、レイアウトコンテナ上の追加アイコンをタップして、 [!UICONTROL 新規コンポーネントを挿入] ダイアログ。

### ドラフトと送信コンポーネントを設定 {#configure-drafts-submissions-component}

ドラフトと送信コンポーネントには、後で完了するためにドラフトとして保存され、送信されたフォームが表示されます。 設定するには、コンポーネントをタップしてから ![設定アイコン](assets/configure_icon.png). 内 [!UICONTROL ドラフトと送信] ダイアログで、フォームのリストをドラフトまたは送信済みのフォームとして示すタイトルを指定します。 また、コンポーネントでドラフトフォームを一覧表示するか、送信済みのフォームをカード形式またはリスト形式で表示するかを選択します。

![ドラフトアイコン](assets/drafts-component.png)

![送信アイコン](assets/submission-listing.png)

### Search &amp; Lister コンポーネントを設定 {#configure-search-lister-component}

Search &amp; Lister コンポーネントは、ページ上のアダプティブフォームのリストを表示し、リストに表示されたフォームに検索を実装するために使用します。

![Search &amp; Lister アイコン](assets/search-and-lister-component.png)

設定するには、コンポーネントをタップしてから ![設定アイコン](assets/configure_icon.png). この [!UICONTROL Search &amp; Lister] ダイアログが開きます。

1. 内 [!UICONTROL 表示] 「 」タブで、以下を設定します。
   * In **[!UICONTROL タイトル]**「 Search &amp; Lister 」コンポーネントのタイトルを指定します。 目安のタイトルを使用すると、ユーザーはフォームのリスト全体ですばやく検索を実行できます。
   * 次の **[!UICONTROL レイアウト]** リストで、フォームをカード形式またはリスト形式で表すレイアウトを選択します。
   * 選択 **[!UICONTROL 検索を非表示]** および **[!UICONTROL 並べ替えを非表示にする]** 検索を非表示にし、機能で並べ替えるには、次の手順に従います。
   * In **[!UICONTROL ツールチップ]**&#x200B;で、コンポーネントにカーソルを合わせたときに表示されるツールチップを指定します。
1. 内 [!UICONTROL アセットフォルダー] 「 」タブで、フォームの取り込み元とページ上のリスト表示元を指定します。 複数のフォルダーの場所を設定できます。
1. 内 [!UICONTROL 結果] 「 」タブで、1 ページに表示するフォームの最大数を設定します。 デフォルトでは、1 ページに 8 つのフォームがあります。

### リンクコンポーネントを設定 {#configure-link-component}

リンクコンポーネントを使用すると、ページ上のアダプティブフォームへのリンクを提供できます。 設定するには、コンポーネントをタップしてから ![設定アイコン](assets/configure_icon.png). この [!UICONTROL リンクコンポーネントを編集] ダイアログが開きます。

1. 内 [!UICONTROL 表示] タブにリンクのキャプションとツールチップを入力して、リンクで表されるフォームを簡単に識別できるようにします。
1. 内 [!UICONTROL アセット情報] 「 」タブで、アセットが保存されるリポジトリのパスを指定します。
1. 内 [!UICONTROL クエリのパラメータ] 「 」タブで、追加のパラメーターをキーと値のペアの形式で指定します。 リンクをクリックすると、これらのその他のパラメーターはフォームと共に渡されます。

## Adobe Signを使用した非同期フォーム送信の設定 {#configure-asynchronous-form-submission-using-adobe-sign}

アダプティブフォームを送信する設定は、すべての受信者が署名式を完了した場合にのみ行うことができます。 Adobe Signを使用して設定を構成するには、次の手順に従います。

1. オーサーインスタンスで、アダプティブフォームを編集モードで開きます。
1. 左側のウィンドウで、「プロパティ」アイコンをタップし、 **[!UICONTROL 電子署名]** オプション。
1. 選択 **[!UICONTROL Adobe Signを有効にする]**. 様々な設定オプションが表示されます。
1. 内 [!UICONTROL フォームを送信] セクションで、 **[!UICONTROL すべての受信者が署名式を完了した後]** 「フォームを送信」アクションを設定するオプション。このアクションでは、すべての受信者に最初に署名用のフォームが送信されます。 すべての受信者がフォームに署名したら、そのフォームのみが送信されます。

## アダプティブFormsをドラフトとして保存 {#save-adaptive-forms-as-drafts}

フォームをドラフトとして保存し、後で完了することができます。 フォームをドラフトとして保存する方法は 2 つあります。
* フォームコンポーネント（ボタンなど）に「フォームを保存」ルールを作成します。 このボタンをクリックすると、ルールトリガーとフォームがドラフトとして保存されます。
* 自動保存機能を有効にします。指定したイベントごと、または設定した時間間隔でフォームが保存されます。

### アダプティブフォームをドラフトとして保存するためのルールの作成 {#rule-to-save-adaptive-form-as-draft}

フォームコンポーネント（ボタンなど）に「フォームを保存」ルールを作成するには、次の手順に従います。

1. オーサーインスタンスで、アダプティブフォームを編集モードで開きます。
1. 左側のウィンドウで、 ![コンポーネントアイコン](assets/components_icon.png) をクリックし、 [!UICONTROL ボタン] コンポーネントをフォームに追加します。
1. 次をタップします。 [!UICONTROL ボタン] コンポーネントをタップしてから、 ![設定アイコン](assets/configure_icon.png).
1. 次をタップします。 [!UICONTROL ルールを編集] アイコンをクリックして、ルールエディターを開きます。
1. タップ **[!UICONTROL 作成]** をクリックし、ルールを設定および作成します。
1. 内 [!UICONTROL 条件] 」セクションで、「クリック済み」を選択し、 [!UICONTROL 次に、] セクションで、「フォームを保存」オプションを選択します。
1. 「**[!UICONTROL 完了]**」をクリックして、ルールを保存します。

### 自動保存を有効にする {#enable-auto-save}

アダプティブフォームの自動保存機能は、次のように設定することができます。

1. オーサーインスタンスで、アダプティブフォームを編集モードで開きます。
1. 左側のウィンドウで、 ![プロパティアイコン](assets/configure_icon.png) をクリックし、 [!UICONTROL 自動保存] オプション。
1. を選択します。 **[!UICONTROL 有効にする]** フォームの自動保存を有効にするには、チェックボックスをオンにします。 次の項目を設定できます。
* デフォルトでは、 [!UICONTROL アダプティブフォームイベント] が「true」に設定されている場合は、イベントのたびにフォームが自動保存されます。
* In [!UICONTROL トリガー]、イベントの発生に基づいて、または特定の時間間隔の経過後に自動保存をトリガーするように設定します。
