---
title: プレビューインスタンスまたはパブリッシュインスタンスでフォームを公開または非公開にする方法を教えてください。
description: AEM オーサー環境からフォームの公開または非公開を行って、インスタンスをプレビューまたは公開する方法を説明します。 フォームをステージング環境でテストする場合でも、エンドユーザーにライブでデプロイする場合でも、AEMにはこのプロセスを効率的に管理するための合理化されたツールが用意されています。
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: d3c089dcca80255f53c0888d46ee1b4b6246741e
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 2%

---


# &#x200B;Experience Manager Formsでの公開の管理

Adobe Experience Manager Forms管理者は、オーサーインスタンスからExperience Manager Formsにフォームを公開できます。 フォームまたはフォルダーの公開を後の日時にスケジュールできます。 公開すると、ユーザーはフォームにアクセスして入力できます。

Experience Manager Formsのインターフェイスでは、次を使用してフォームを公開できます。
* [Publish オプション ](#publish-forms-using-the-publish-option)
* [「公開を管理」オプション](#publish-forms-using-the-manage-publication-option)

その後、Experience Manager Formsで元のフォームやフォルダーに変更を加えても、その変更は、Experience Manager Formsから再公開するまで **Publish** インスタンスには反映されません。 これにより、処理中の変更は **Publish** インスタンスでは使用できなくなります。 管理者が公開した変更のみが **0}Publish} インスタンスで利用できます。**

## 「Publish」オプションを使用したPublish forms

「**Publish**」オプションを使用すると、フォームをすぐに公開できます。 ツールバーの「**Publish**」ボタンを使用してExperience Managerフォームを公開します。 Publish オプションを使用してフォームを公開するには、次の手順を実行します。

1. Experience Manager Forms コンソールで、親フォルダーに移動し、公開するフォームを選択します。
1. ツールバーの **Publish** オプションをクリックし、フォームと共に公開されるすべての参照アセットを確認します。
1. 「**[!UICONTROL 公開する]**」をクリックします。

   ![Publishとフォームの非公開 ](/help/edge/docs/forms/assets/publish-form-option.png)

   フォームとその関連アセットが正常に公開されると、**成功** ダイアログが表示されます。 **閉じる** をクリックして、ダイアログボックスを閉じます。

   ![成功ダイアログ](/help/forms/assets/publish-success.png)

### フォームを非公開にする

「**Publish**」オプションとその関連アセットを使用してフォームを正常に公開した後、ツールバーの「**[!UICONTROL 非公開]**」ボタンを使用して非公開にすることもできます。 フォームを非公開にするには：

1. フォームとその関連アセットを非公開にするには、フォームを選択し、ツールバーの **[!UICONTROL 非公開]** をクリックします

   **[!UICONTROL 非公開]** ボタンをクリックすると、**アセットを非公開** ダイアログが表示されます。
1. **[!UICONTROL 非公開]** をクリックして、非公開のプロセスを開始します

   ![ ダイアログを解除 ](/help/forms/assets/unpublish-asset.png)

   フォームとその関連アセットが正常に非公開になると、**成功** ダイアログが表示されます。 **閉じる** をクリックして、ダイアログボックスを閉じます。

   ![ 非公開に成功 ](/help/forms/assets/unpublishing-start.png)

## 「公開を管理」オプションを使用したPublish forms

公開を管理を使用すると、選択した宛先にコンテンツを公開または選択した宛先からコンテンツを非公開にしたり、フォームとドキュメントフォルダー全体から公開リストにコンテンツを追加したり、公開する参照を選択したり、後の日時に公開をスケジュールしたりできます。  「公開を管理」オプションを使用してフォームを公開するには、次の手順に従います。

1. Experience Manager Forms コンソールで、親フォルダーに移動し、公開するフォームを選択します。
1. ツールバーの **[!UICONTROL 公開を管理]** オプションをクリックします。

   ![ 「公開を管理」オプション ](/help/forms/assets/manage-publication-option.png)

   **公開を管理** インターフェイスが表示されます。

   ![公開を管理](/help/forms/assets/manage-publication.png)

   **公開を管理**&#x200B;インターフェイスでは次のオプションが使用可能です。

   * **アクション**

      * **Publish**：選択した宛先へのPublish forms
      * **非公開**：宛先からフォームを非公開にします

   * **宛先**

      * **Publish**: Publish forms からExperience Manager Forms （AEM） Publish インスタンスへ。
      * **プレビュー**:Publish forms からExperience Manager Forms（AEM）へのプレビューインスタンス。

   * **スケジュール設定**

      * **今すぐ**:Publish Forms を直ちに使用できます
      * **後**:**アクティベート日** または時刻に基づくPublish forms

1. 「**次へ**」をクリックして続行します。
1. 「**範囲**」タブで「[ コンテンツを追加 ](#add-content)」オプションを使用して、公開用にさらにコンテンツを追加します。 例えば、Formsやレコードのドキュメントファイルをさらに追加できます。
   ![ 「範囲」タブ ](/help/forms/assets/scope-tab.png)
1. **[!UICONTROL Publish]** をクリックしてフォームおよび関連アセットを公開すると、成功したというメッセージが表示されます。
   ![ 正常なメッセージを公開 ](/help/forms/assets/publish-successful.png)

### コンテンツを追加する

Experience Manager Formsに公開する場合は、公開リストにさらにコンテンツ（フォームやフォルダー）を追加できます。 `formsanddocuments` フォルダーからリストにさらにフォームやフォルダーを追加できます。 ただし、複数のフォルダーからフォームを一度に追加することはできません。 公開用のフォームをさらに追加するには、次の手順に従います。

1. コンテンツをさらに追加するには、「**コンテンツを追加**」ボタンをクリックします。

   ![ コンテンツを追加 ](/help/forms/assets/add-content.png)

1. **パスを選択** 画面からフォームを選択します。 フォルダーから複数のフォームを一度に追加したり、複数のフォルダーを一度に追加したりできます。 ただし、複数のフォルダーからフォームを一度に追加することはできません。

   ![ コンテンツを追加 ](/help/forms/assets/add-assets.png)

1. 参照を公開またはフォームから非公開に設定するには、フォームを選択し、「**[!UICONTROL 公開済みの参照]**」をクリックします。

   ![ 公開済みの参照 ](/help/forms/assets/published-references.png)

1. **公開済みの参照** ダイアログボックスで、公開しないアセットのチェックボックスをオフにして、「**[!UICONTROL 完了]**」をクリックします。
   ![ 公開済みの参照ダイアログ ](/help/forms/assets/published-references-dialog.png)

<!--
### Include Folder Settings
By default, publishing a folder to Experience Manager Forms publishes all the assets, subfolders, and their references. To filter the folder for publishing:

1. Click **[Include Folder Settings]** to filter the folder.

    ![Include folder](/help/forms/assets/include-folder.png)

    The **[UICONTROL Include Folder Settings]** dialog appears. 
    
    ![Include folder dialog](/help/forms/assets/include-folder-dialog.png)
    
    The **[UICONTROL Include Folder Settings]** includes following options:

    * **[!UICONTROL Include folder contents]** checkbox. 
        * If selected, all forms and assets in the chosen folder, its subfolders (including all forms and assets within them), and references are published.
        * If not selected, only the forms and assets in the selected folder are published, while subfolder forms and assets are not.

    * **[!UICONTROL Include only immediate folder contents]** checkbox
        Selecting the **[!UICONTROL Include folder contents]** checkbox enables the **[!UICONTROL Include only immediate folder contents]** checkbox for selection.

        * If you select both options, all the forms and assets of the selected folder, subfolders (empty), and references are published. The forms and assets of the subfolders are not published.
        * -->


### 後でフォームをPublishまたは非公開にする

「後で公開または非公開にする」オプションを使用すると、後でフォームを公開または非公開にできるだけでなく、ワークフローを設定することもできます。 フォームがワークフローの完了後に公開または非公開になります。 フォームを公開または非公開にするようにスケジュールするには：

1. Experience Manager Forms コンソールで、親フォルダーに移動し、公開スケジュールを設定するフォームを選択します。
1. ツールバーの **[!UICONTROL 公開を管理]** オプションをクリックします。

   ![公開を管理](/help/forms/assets/manage-publication.png)

1. **[!UICONTROL アクション]** で **Publish** または **非公開** をクリックし、コンテンツを公開または非公開にする **[!UICONTROL 宛先]** を選択します。
   * **プレビュー**:「**プレビュー**」オプションを使用して、Experience Manager Forms プレビュー環境に公開または非公開にします。 Experience Manager Forms プレビュー環境は、開発フォームでテストするために使用します。
   * **Publish**: フォームが実稼動環境で使用できる状態になったら、「Experience Manager Forms Publish」オプションを使用して、フォームをExperience Manager Forms パブリッシュ環境に送信します。

1. 「スケジュール」から「**[!UICONTROL 後で]**」を選択します。

   ![ 後で公開を管理 ](/help/forms/assets/manage-publication-later.png)

1. 「**[!UICONTROL アクティベート日]**」を選択し、日時を指定します。
1. **[!UICONTROL 次へ]** をクリックします。
1. 「**範囲**」タブで、**[!UICONTROL コンテンツを追加]** します（必要な場合）。
   ![ 公開を管理してコンテンツを後で追加 ](/help/forms/assets/publish-later-add-content.png)
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. （オプション）「**ワークフロー**」タブで、**[!UICONTROL ワークフロータイトル]** を指定します。
1. 「**[!UICONTROL Publishを後で]**」をクリックします。

   ![「公開を管理」ワークフロー](/help/forms/assets/manage-publication-workflows.png)

## 公開ステータスの判別

公開ステータスを判断する方法は複数あります。

* 公開先のインスタンスにログインして、公開されたフォームやその他のアセットを（スケジュールを設定した日時に応じて）確認します。

* タイムライン表示を使用して、公開ステータスを判断します。

* アダプティブFormsエディターでページ情報メニューを使用します。
