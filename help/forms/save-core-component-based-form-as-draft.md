---
title: コアコンポーネントベースのアダプティブフォームをドラフトとして保存し、ドラフトと送信コンポーネントを使用してドラフトと送信をリストする方法を教えてください。
description: コアコンポーネントベースのアダプティブフォームをドラフトとして保存する方法を説明します。 また、ドラフトと送信コンポーネントを使用して、ログインしているユーザーのドラフトと送信をリストする方法も理解します。
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer
source-git-commit: bf0a42e1376e4743fe8ce0650e1f807dfba2d050
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 16%

---


# フォームをドラフトとして保存し、Sites ページに一覧表示する

<!--This article provides information about the Auto-save feature, which is currently available as a pre-release feature. The pre-release feature is accessible only through our [pre-release channel](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/prerelease#new-features).-->

フォームへの入力を開始しても、一時停止してから後で戻る必要があるユーザーを考えてみましょう。 AEMには、今後の完成に備えてフォームをドラフトとして保存できる `save-as-draft` オプションが用意されています。 これを容易にするために、AEMには、すぐに使用できる **ドラフトと送信** Forms ポータルコンポーネントが用意されています。このコンポーネントは、AEM Sites ページにドラフトと送信を表示します。 このコンポーネントには、後で完了するためにドラフトとして保存されたフォームと、送信済みのフォームが一覧表示されます。 ログインしているユーザーのみが、自分の下書きを編集したり、送信されたフォームを表示したりできます。 ただし、匿名ユーザーが **検索とリスター** コンポーネントを使用してフォームのリストを移動し、フォームをドラフトとして保存した場合、そのドラフトは **ドラフトと送信** コンポーネントに表示されません。 ドラフトと送信を表示するには、フォームの送信時にユーザーがログインしている必要があります。

![下書きアイコン](assets/drafts-component.png)

## 前提条件

* お使いの AEM Cloud Service 環境でアダプティブフォームコアコンポーネントを有効にするには、最新版をインストールします。

  最新のコアコンポーネントを環境にデプロイすると、フォームポータルコンポーネントにオーサリング環境でアクセスできます。

* [ ドラフトと送信Forms ポータルコンポーネント用の Azure ストレージコネクタと統合ストレージコネクタの設定 ](#configure-azure-storage-and-unified-storage-connector-for-drafts--submissions-forms-portal-component)

### ドラフトと送信Forms ポータルコンポーネント用の Azure ストレージコネクタと統合ストレージコネクタの設定

**ドラフトと送信** コンポーネントには、AEM Sitesページにドラフトを保存して一覧表示するためのストレージを設定する必要があります。 統合ストレージコネクタは、AEMを外部ストレージとリンクするためのフレームワークを提供します。 フォームをドラフトとして保存するには、Azure ストレージアカウントと、[!DNL Azure] ストレージアカウントへのアクセスを許可するためのアクセスキーがあることを確認します。 Azure ストレージアカウントとアクセスキーを取得したら、次の手順を実行して Azure ストレージ設定を作成します。

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Azure ストレージ]**&#x200B;に移動します。

   ![Azure ストレージカードの選択 ](/help/forms/assets/save-form-as-draft-azure-card.png)

1. 設定フォルダーを選択して設定を作成し、「**[!UICONTROL 作成]**」を選択します。

   ![Azure ストレージ設定フォルダーを選択 ](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. 「**[!UICONTROL タイトル]**」フィールドで設定のタイトルを指定します。
1. 「[!DNL Azure]Azure ストレージアカウント **[!UICONTROL 」フィールドと「]** Azure アクセスキー **[!UICONTROL 」フィールドで]** ストレージアカウントの名前を指定します。

   ![Azure ストレージ設定](/help/forms/assets/save-form-as-draft-azure-storage.png)

   `Connection String` のテキストボックスに `Azure Storage Account` と入力し、`Azure Key` のテキストボックスに `Azure Access key` と入力します。

1. 「**保存**」をクリックします。

   >[!NOTE]
   >
   > **[!UICONTROL Azure ストレージアカウント]** と **[!UICONTROL Azure アクセスキー]** は、[Microsoft Azure Portal](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) から取得できます。

   Azure ストレージ設定が正常に作成されたら、次の手順に従って、Forms Portal 用の統合ストレージコネクタを設定します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Forms]**／**[!UICONTROL 統合ストレージコネクタ]**&#x200B;に移動します。

   ![ 統合コネクタストレージ ](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. 「**[!UICONTROL フォームポータル]**」セクションで、「**[!UICONTROL ストレージ]**」ドロップダウンリストから「**[!UICONTROL Azure]**」を選択します。
1. Azure ストレージ設定の設定パスを「**[!UICONTROL ストレージ設定パス]**」フィールドで指定します。

   ![ 統合コネクタストレージ設定 ](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. 「**[!UICONTROL 保存]**」を選択します。

>[!NOTE]
>
> Azure 以外のストレージオプションを設定する必要がある場合は、公式メールアドレスからaem-forms-ea@adobe.comに詳細な要件を書き込みます。

ドラフトと送信済みフォームを格納するための Azure ストレージコネクタと統合ストレージコネクタの設定が完了したら、AEM Sites ページに **ドラフトと送信** コンポーネントを追加します。

## ドラフト&amp;送信コンポーネントをAEM Sites ページに追加する方法

標準のForms ポータルコンポーネントを使用して、Sites ページ上のドラフトおよび送信を一覧表示できます。 次の手順を実行して、**ドラフトと送信** ポータルコンポーネントを追加します。

1. AEM Sites ページを&#x200B;**編集**&#x200B;モードで開きます。
1. **[!UICONTROL ページ情報]**／**[!UICONTROL テンプレートを編集]**&#x200B;に移動します。
   ![テンプレートポリシーの編集](/help/forms/assets/save-form-as-draft-edit-template.png)

1. **[!UICONTROL ポリシー]** をクリックし、**[!UICONTROL AEM アーキタイププロジェクト名]** - Formsとコミュニケーションポータル **[の下にある ] ドラフトと送信** チェックボックスを選択します。

   ![ポリシーの選択](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. 「**[!UICONTROL 完了]**」をクリックします。
1. 次に、オーサリングモードでAEM Sitesページを再度開きます。
1. ページエディター内で、フォームポータルコンポーネントを追加できるセクションを見つけます。
1. **追加**&#x200B;アイコンをクリックします。アイコンはプラス記号（+）で、新しいコンポーネントを追加するオプションを示します。

   **追加**&#x200B;アイコンをクリックすると、**新規コンポーネントを挿入**&#x200B;ダイアログボックスが表示され、挿入する様々なコンポーネントが表示されます。

   >[!NOTE]
   >
   > または、コンポーネントをドラッグ＆ドロップすることもできます。

1. ダイアログボックスで使用可能なコンポーネントを参照し、リストから目的のコンポーネントを選択します。例えば、リストから **ドラフトと送信** コンポーネントを選択して、**ドラフトと送信** Formsポータルコンポーネントを追加します。

   ![ ドラフトと送信コンポーネントの追加 ](/help/forms/assets/save-form-as-draft-add-dns.png)

次に、要件に従って、**ドラフトと送信** コンポーネントのプロパティを設定します。

## ドラフト&amp;送信コンポーネントのプロパティの設定

以下のように **ドラフトと送信** のプロパティを設定できます。
1. **ドラフトと送信** コンポーネントを選択します。
1. ![ 設定アイコン ](assets/configure_icon.png) をクリックすると、ダイアログボックスが表示されます。
1. **[!UICONTROL ドラフトと送信]** ダイアログで、以下を指定します。
   * **タイトル** Sites ページ内のコンポーネントを識別するために、デフォルトではコンポーネントの上にタイトルが表示されます。
   * **タイプを選択**：フォームを下書きまたは送信済みのフォームとして表示します。 **ドラフトForms** を選択した場合は、ドラフトとして保存されたフォームが表示されます。 または、「**送信済みForms**」を選択すると、ログインユーザーによって送信されたフォームが表示されます。
   * **レイアウト**：下書きのフォームまたは送信済みのフォームをカード形式またはリスト形式で表示します。

   ![ ドラフトおよび送信コンポーネントのプロパティ ](/help/forms/assets/save-form-as-draft-dns-properties.png)

## ドラフトとして保存するフォームの設定

アダプティブFormsは、後で使用するためにドラフトとして保存する次の 2 つの方法で設定できます。
* [ユーザーアクション](#user-action)
* [自動保存](#auto-save)

### ユーザーアクション

>[!NOTE]
>
> [ フォームを保存 ](https://github.com/adobe/aem-core-forms-components) ルールを使用してフォームをドラフトとして保存するには **&#x200B;**&#x200B;コアコンポーネントのバージョンが 3.0.24 以降に設定されていることを確認します。

フォームをドラフトとして保存するには、ボタンなどのフォームコンポーネントに **フォームを保存** ルールを作成します。 ボタンをクリックすると、ルールがトリガーされ、フォームがドラフトとして保存されます。 ボタンコンポーネントに **フォームを保存** ルールを作成するには、次の手順を実行します。

1. アダプティブフォームを編集モードで開きます。
1. 「**[!UICONTROL ルールを編集]**」アイコンを選択して、「**ボタン** コンポーネントのルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」を選択して、ボタンのルールを設定および作成します。
1. 「**[!UICONTROL 条件]**」セクションで「**クリック済み** を選択し、「**[!UICONTROL 次に]**」セクションで「**フォームを保存**」オプションを選択します。
1. 「**[!UICONTROL 完了]**」を選択し、ルールを保存します。

   ![ ボタンのルールを作成 ](/help/forms/assets/save-form-as-drfat-create-rule.png)

アダプティブフォームをプレビューして入力し、「**フォームを保存**」ボタンをクリックすると、フォームはドラフトとして保存されます。

### ドラフト

>[!NOTE]
>
> 自動保存機能を使用してフォームをドラフトとして保存するには、[ コアコンポーネントのバージョンが 3.0.52 以降 ](https://github.com/adobe/aem-core-forms-components) に設定されていることを確認します。

アダプティブフォームを、時間ベースのイベントに基づいて自動的に保存するように設定して、指定された期間の後にフォームが保存されるようにすることもできます。 [ ご利用の環境のForms ポータルコンポーネントを有効にする ](/help/forms/list-forms-on-sites-page.md#enable-forms-portal-components-for-your-existing-environment) と、Forms コンテナのプロパティに **自動保存** タブが表示されます。 アダプティブフォームの自動保存機能を設定できます。

1. オーサーインスタンスで、アダプティブフォームを編集モードで開きます。
1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. 「ガイドコンテナのプロパティ ![ ガイドプロパティ ](/help/forms/assets/configure-icon.svg)」アイコンをクリックし、「**[!UICONTROL ドラフト]**」タブを開きます。

   ![ 自動保存 ](/help/forms/assets/auto-save.png)

1. 「**[!UICONTROL ドラフトを自動的に保存]**」チェックボックスをオンにして、フォームをドラフトとして自動保存できるようにします。
1. **[!UICONTROL 環境設定を保存]** を **一定の間隔でドラフトを保存** として設定し、特定の時間間隔の後にフォーム <!--based on the occurrence of an event or--> ージを自動保存します。
1. 指定した間隔でフォームの自動保存をトリガーにする期間を設定する場合は **[!UICONTROL 時間間隔を]** 保存間隔の頻度（秒）で指定します。
1. 「**[!UICONTROL 完了]**」をクリックします。

## ドラフト&amp;送信コンポーネントを使用して、Sites ページでドラフト/送信済みフォームを表示する

保存されたドラフトまたは送信されたフォームを表示するには、**ドラフトと送信**&#x200B;Forms ポータルコンポーネントを使用します。
**[!UICONTROL ドラフトと送信コンポーネントの設定ダイアログ]** で **タイプを選択** が [ ドラフトForms](#configure-properties-of-the-drafts--submissions-component) として選択されている場合、ドラフトとして保存されたフォームは Sites ページに表示されます。 ドラフトを開くには、省略記号（...）をクリックしてフォームを完成させます。

![下書きアイコン](assets/drafts-component.png)

**[!UICONTROL ドラフト&amp;送信コンポーネントの設定ダイアログ]** で **タイプを選択** が [ 送信済みForms](#configure-properties-of-the-drafts--submissions-component) として選択されている場合、送信済みフォームが表示されます。 送信されたフォームは表示できますが、編集することはできません。

![送信アイコン](assets/submission-listing.png)

フォームの右下隅に表示される省略記号（...）をクリックして、フォームを破棄することもできます。

>[!NOTE]
>
> Forms ポータルでは、ドラフト&amp;送信コンポーネントは、基盤ベースのフォームからの送信のみをサポートしています。

## 次の手順

次の記事では、[Formsポータルのリンクコンポーネントを使用してサイトページ上のフォームに参照を追加する方法 ](/help/forms/add-form-link-to-aem-sites-page.md) について説明します。

## 関連記事

{{forms-portal-see-also}}

## 関連トピック {#see-also}

{{see-also}}