---
title: ユニバーサルエディターでフォームのフォームデータモデル（FDM）を統合する方法
description: フォームデータモデル（FDM）に基づいてフォームを作成する方法を説明します。 FDM でデータモデルオブジェクトのサンプルデータを生成し、編集します。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
hide: true
hidefromtoc: true
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 381aad580762fe957e1dc1d5824e4d35098f1ca4
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 11%

---

# ユニバーサルエディターでのフォームとフォームデータモデルの統合

ユニバーサルエディターでフォームをフォームデータモデル（FDM）と統合すると、様々なバックエンドデータソースを使用してフォームデータモデル（FDM）を作成できます。 フォームデータモデル（FDM）を様々なフォームワークフローでスキーマとして使用できます。 データソースを設定し、そのデータソースで使用できるデータモデルオブジェクトとサービスに基づいてフォームデータモデル（FDM）を作成します。

## 考慮事項

* ユニバーサルエディターのフォームの事前入力サービスは、現在サポートされていません。

## 前提条件

ユニバーサルエディターでフォームデータモデルを使用してフォームを設定する前に、次の手順を完了していることを確認してください。

* [Data Sourceの設定 ](/help/forms/configure-data-sources.md)：フォームをバックエンドデータに接続するためのデータソースを設定します。
* [ フォームデータモデル（FDM）の作成 ](/help/forms/create-form-data-models.md)：設定済みデータソースのデータオブジェクトとサービスを使用して、データモデルを作成します。
* [ データモデルオブジェクトとサービスの設定 ](/help/forms/work-with-form-data-model.md)：データモデルオブジェクトとサービスをマッピングして、フォームとデータソース間のデータフローをスムーズにします。

## ユニバーサルエディターでのフォームデータモデルを使用したFormsの作成

ユニバーサルエディターでは、次の項目を作成できます。
* [ スキーマベースのフォーム ](#schema-based-form)：スキーマベースのフォームは、「**データ**」タブでフォームの作成中に設定されたデータソースを使用し、フォームフィールドにデータを自動的にバインドします。
* [ 非スキーマベースのフォーム ](#non-schema-based-form)：非スキーマベースのフォームでは、データソースを手動で追加し、コンテンツツリーから各フィールドをバインドする必要があります。

![ ユニバーサルエディターのフォームのタイプ ](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

これらの方法を使用すると、必要に応じてデータモデルをフォームに柔軟に接続できます。

### スキーマベースのフォーム

スキーマベースのフォームを作成すると、フォームはデータソースで自動的に設定され、フォームフィールドはデータバインディングによって既にデータにリンクされています。 フォーム作成ウィザードを使用してスキーマベースのフォームを作成するには、次の手順を実行します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
2. Experience Manager のログインページに資格情報を入力します。 ログイン後、左上隅の **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
3. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 ウィザードが開きます。 「**Source**」タブで、テンプレートを選択します。

   ![Edge Delivery Services テンプレート ](/help/edge/assets/create-eds-forms.png)

   Edge Delivery Servicesベースのテンプレートを選択すると、「**[!UICONTROL 作成]**」ボタンが有効になります。 「**[!UICONTROL データSource]**」タブまたは「**[!UICONTROL 送信]**」タブに移動して、データソースまたは送信アクションを選択できます。

4. 「**データ**」タブでは、次のいずれかのデータモデルを選択できます。

   * **フォームデータモデル（FDM）**：データソースのデータモデルオブジェクトとサービスをフォームに統合します。 フォームで複数のソースからのデータの読み取りと書き込みが必要な場合は、フォームデータモデル（FDM）を選択します。

   * **JSON スキーマ**：データ構造を定義する JSON スキーマを関連付けて、フォームをバックエンドシステムに統合します。 スキーマ要素を使用して動的コンテンツを追加できます。

     例えば、「Pet フォームデータモデル」という名前の作成済みフォームデータモデルを選択します。

     ![ フォームデータモデルを選択 ](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     デフォルトでは、関連付けられた JSON スキーマまたはフォームデータモデル（FDM）のすべてのフィールドが自動的に選択され、対応するフォームコンポーネントに変換されるので、オーサリングプロセスを簡素化できます。 このウィザードでは、チェックボックスを使用して、フォームに含めるフィールドを選択的に選択することもできます。

5. 「**[!UICONTROL 作成]**」をクリックすると、**フォームを作成**&#x200B;ウィザードが表示されます。
6. **名前** と **タイトル** を指定します。
7. **GitHub URL** を指定します。 例えば、GitHub リポジトリの名前が `edsforms` の場合は、アカウント `wkndforms` の下に配置され、URL はとなります。
   `https://github.com/wkndforms/edsforms`
8. 「**[!UICONTROL 作成]**」をクリックします。

   ![ スキーマベースのフォームを作成 ](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   「**[!UICONTROL 作成]**」をクリックするとすぐに、フォームがオーサリング用のユニバーサルエディターで開きます。

   ![ フォームのオーサリング ](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   関連するデータソースのデータ要素を使用してフォームが作成され、フォームフィールドには事前設定済みのデータバインディングが含まれています。

   ![ 自動データバインディング ](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   これで、フォームに [ 送信アクションの設定 ](/help/edge/docs/forms/universal-editor/submit-action.md) を追加および設定できるようになりました。

### 非スキーマベースのフォーム

非スキーマベースのフォームを作成した場合、データソースは設定されません。 後でフォームのプロパティを編集してデータソースを追加し、フォームフィールドのデータバインディングを手動で設定できます。 次の手順を実行して、フォームのプロパティを編集し、データソースを追加します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
1. Experience Manager のログインページに資格情報を入力します。 ログイン後、左上隅の **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. データソースを追加するフォームを選択して、**[!UICONTROL プロパティ]** をクリックします。
   ![ フォームプロパティを開く ](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   フォームプロパティが開きます。
1. 「**フォームモデル**」タブをクリックして開き、「**次から選択** ドロップダウンメニューから選択します。 次のいずれかのオプションを選択できます。

   * **フォームデータモデル（FDM）**：フォームデータモデルを使用してフォームを作成します。
   * **コネクタ**:Adobe Marketo データソースを使用してフォームを作成します。
   * **スキーマ**:AEM Formsにアップロードされた JSON スキーマを使用してフォームを作成します。
   * **なし**：フォームモデルを使用せずに最初からフォームを作成します。

     例えば、フォームデータモデル（FDM）を選択します

     ![ 「フォームモデルを選択」タブ ](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. ドロップダウンリストから、作成したフォームデータモデル（FDM）を選択します。 例えば、ドロップダウンリストから、Pet フォームデータモデルという名前の作成したフォームデータモデルを選択します。

   ![FDM の選択 ](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   フォームデータモデル（FDM）を選択すると、警告ダイアログが表示されます。 **OK** をクリックして、ダイアログを閉じます。

   ![ フォームモデルウィザード ](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。
1. フォームを編集用に開きます。 フォームがオーサリング用のユニバーサルエディターで開きます。

   ![ 非スキーマベースのフォームオーサリング ](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   関連するフォームデータモデル（FDM）に存在するフォーム要素は、「プロパティ」パネルの **[!UICONTROL コンテンツブラウザー]** の **[!UICONTROL データソース]** タブに表示さ **ます**。

   ![ フォームデータのSource](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. 「**[!UICONTROL データソース]**」タブからデータ要素を選択し、「**[!UICONTROL 追加]**」をクリックします。

   ![ データ要素の追加 ](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   また、これらの要素をドラッグ&amp;ドロップして、アダプティブフォームを作成することもできます。 **[!UICONTROL 追加]** をクリックすると、「**[!UICONTROL データソース]**」タブで選択した要素がフォームに追加され、追加した要素の前にチェックマークが表示されます。

   ![ フォームを作成 ](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

   フォーム要素の **バインド参照** プロパティにデータ連結を指定するには、フォーム要素に手動でデータ連結を追加する必要があります。
例えば、フォームに既に存在する **ペット名** テキストボックスに、データ連結参照を追加します。

   ![ フォームフィールドのデータディニングを手動で追加 ](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

   これで、フォームに [ 送信アクションの設定 ](/help/edge/docs/forms/universal-editor/submit-action.md) を追加および設定できるようになりました。

## 関連トピック

{{universal-editor-see-also}}
