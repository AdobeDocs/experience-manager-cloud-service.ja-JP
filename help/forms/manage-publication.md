---
title: プレビューインスタンスまたはパブリッシュインスタンスでフォームを公開または非公開にするにはどうすればよいですか？
description: AEM オーサー環境からフォームの公開または非公開を学んで、インスタンスをプレビューまたは公開します。 フォームをステージング環境でテストする場合でも、エンドユーザー向けにライブでデプロイする場合でも、AEMには、このプロセスを効率的に管理するための合理化されたツールが用意されています。
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 6ade40f1-bad5-4f5e-aa0e-84b7c6a82e02
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 7%

---


# Experience Manager Forms での公開の管理

Adobe Experience Manager（AEM）Forms管理者は、オーサーインスタンスからExperience Manager Formsにフォームを公開できます。 また、後の日時に対してフォームまたはフォルダーの公開をスケジュールするオプションもあります。 公開したフォームにアクセスして入力できるようになります。

Experience Manager Formsでは、次のいずれかの方法を使用してフォームを公開できます。

* [公開オプション ](#publish-forms-using-the-publish-option)
* [「公開を管理」オプション](#publish-forms-using-the-manage-publication-option)

## 留意すべき点

* `forms-users` グループのメンバーのみが&#x200B;**公開を管理** オプションを使用してフォームを公開できます。
* Experience Manager Formsでフォームまたはフォルダーに加えた変更は、再公開するまで&#x200B;**公開** インスタンスには表示されません。 これにより、進行中の更新は&#x200B;**パブリッシュ** インスタンスで利用できなくなります。 管理者が明示的に公開した変更のみが&#x200B;**公開** インスタンスに反映されます。

## 「公開」オプションを使用したフォームの公開

**公開** オプションを使用すると、フォームをすぐに公開できます。 Experience Manager フォームを公開するには、ツールバーの「**公開**」ボタンを使用します。 「公開」オプションを使用してフォームを公開するには、次の手順を実行します。

1. Experience Manager Forms コンソールで、親フォルダーに移動し、公開するフォームを選択します。
1. ツールバーの「**公開**」オプションをクリックし、フォームで公開されるすべての参照アセットを確認します。
1. 「**[!UICONTROL 公開する]**」をクリックします。

   ![ フォームの公開と非公開](/help/edge/docs/forms/assets/publish-form-option.png)

   フォームとその関連アセットが正常に公開されると、**成功** ダイアログが表示されます。
1. 「**閉じる**」をクリックします。

   ![成功ダイアログ](/help/forms/assets/publish-success1.png)

### フォームを非公開にする

**公開** オプションとその関連アセットを使用してフォームを正常に公開した後、ツールバーの「**[!UICONTROL 非公開]**」ボタンを使用してフォームを非公開にすることもできます。 フォームを非公開にするには：

1. フォームとその関連アセットを非公開にするには、フォームを選択し、ツールバーの「**[!UICONTROL 非公開]**」をクリックします

   **[!UICONTROL 非公開]** ボタンをクリックすると、**アセットの非公開** ダイアログが表示されます。
1. **[!UICONTROL 非公開]**&#x200B;をクリックして、非公開プロセスを開始します

   ![ ダイアログを展開](/help/forms/assets/unpublish-asset.png)

   フォームとその関連アセットが正常に非公開になると、**成功** ダイアログが表示されます。
1. 「**閉じる**」をクリックします。

   ![非公開が成功しました](/help/forms/assets/unpublishing-start.png)

## 「公開を管理」オプションを使用したフォームの公開

公開を管理すると、選択した宛先との間でコンテンツを公開または非公開にしたり、`forms&documents` フォルダー全体から公開リストにコンテンツを追加したり、公開する参照を選択したり、公開を後の日時にスケジュールしたりできます。  **公開を管理** オプションを使用してフォームを公開するには、次の手順を実行します。

1. Experience Manager Forms コンソールで、親フォルダーに移動し、公開するフォームを選択します。
1. ツールバーの「**[!UICONTROL 公開を管理]**」オプションをクリックします。

   ![公開の管理オプション ](/help/forms/assets/manage-publication-option.png)

   **公開を管理** UIが表示されます。

   ![公開を管理](/help/forms/assets/manage-publication.png)

   **公開を管理** UIでは、次のオプションを使用できます。

   * **アクション**

      * **公開**：選択した宛先へのフォームの公開
      * **非公開**：宛先からフォームを非公開にする

   * **宛先**

      * **公開**: Experience Manager Forms （AEM）公開インスタンスにフォームを公開します。
      * **Preview**: Experience Manager Forms（AEM）プレビューインスタンスへのフォームの公開。

   * **スケジュール設定**

      * **今**：すぐにフォームを公開
      * **以降**: **アクティベーション日**&#x200B;または時間に基づいてフォームを公開します

1. **次へ**&#x200B;をクリックして続行します。
1. （オプション）「**スコープ**」タブで、「[ コンテンツを追加](#add-content)」オプションを使用して、公開用のコンテンツをさらに追加します。 例えば、Forms ファイルまたはレコードのドキュメント ファイルを追加できます。
   ![範囲タブ ](/help/forms/assets/scope-tab.png)
1. 「**[!UICONTROL 公開]**」をクリックして、フォームと関連アセットを公開すると、成功したメッセージが表示されます。
   ![成功したメッセージを公開](/help/forms/assets/publish-successful.png)

### コンテンツを追加する

Experience Manager Formsに公開すると、公開リストにさらにコンテンツ（フォーム）を追加できます。
公開用のフォームをさらに追加するには：

1. 「**コンテンツを追加**」ボタンをクリックして、さらにコンテンツを追加します。

   ![ コンテンツを追加](/help/forms/assets/add-content.png)

2. 「**パスを選択**」画面からフォームを選択します。

   ![ コンテンツを追加](/help/forms/assets/add-assets.png)

   >[!NOTE]
   >
   > リストに追加するフォームまたはフォルダーは、`formsanddocuments` フォルダーから選択できます。 ただし、一度に複数のフォルダーからフォームを追加することはできません。

3. フォームの公開または非公開の参照を設定するには、フォームを選択し、**[!UICONTROL 公開済み参照]**&#x200B;をクリックします。

   ![公開された参照](/help/forms/assets/published-references.png)

4. **公開済み参照** ダイアログボックスで、非公開にするアセットのチェックを外し、**[!UICONTROL 完了]**をクリックします。
   ![公開された参照ダイアログ ](/help/forms/assets/published-references-dialog.png)

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
        *
        -->


### 後でフォームを公開または非公開にする

後でフォームを公開または非公開にできるだけでなく、「後で公開」または「非公開」オプションを使用してワークフローを設定することもできます。 フォームは、ワークフローの完了後に公開または非公開になります。

フォームの公開または非公開をスケジュールするには、次の手順に従います。

1. Experience Manager Forms コンソールから、親フォルダーに移動し、公開をスケジュールするフォームを選択します。
1. ツールバーの「**[!UICONTROL 公開を管理]**」オプションをクリックします。

   ![公開を管理](/help/forms/assets/manage-publication.png)

1. **アクション**&#x200B;から&#x200B;**公開**&#x200B;または&#x200B;**[!UICONTROL 非公開]**&#x200B;をクリックします。
1. コンテンツを公開または非公開にする&#x200B;**[!UICONTROL 宛先]**&#x200B;を選択します。
   * **Preview**: **Preview** オプションを使用して、Experience Manager Forms プレビュー環境に公開または非公開にします。 Experience Manager Formsのプレビュー環境は、開発フォームでテストするために使用されます。
   * **公開**: Experience Manager Forms **公開** オプションを使用して、実稼動環境でフォームを使用する準備が整った後にExperience Manager Forms パブリッシュ環境にフォームを送信します。

1. **[!UICONTROL スケジューリング]**&#x200B;から&#x200B;**後**&#x200B;を選択します。

   ![後で公開を管理](/help/forms/assets/manage-publication-later.png)

1. **[!UICONTROL ライセンス認証日]**&#x200B;を選択し、日時を指定します。
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. （オプション）「**スコープ**」タブで、「**[!UICONTROL コンテンツを追加]**」を使用してコンテンツを追加します。
   ![後でコンテンツを追加する公開を管理](/help/forms/assets/publish-later-add-content.png)
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. 「**ワークフロー**」タブで、**[!UICONTROL ワークフローのタイトル]**&#x200B;を指定します。
1. 「**[!UICONTROL 後で公開]**」をクリックします。

   ![「公開を管理」ワークフロー](/help/forms/assets/manage-publication-workflows.png)

## 公開ステータスの決定

公開ステータスを決定する方法は複数あります。

* 宛先インスタンスにログインして、公開されたフォームやその他のアセットを確認します（スケジュールされた日時によって異なります）。

* タイムラインビューを使用して、公開ステータスを決定します。

* アダプティブ Forms エディターのページ情報メニューを使用します。
