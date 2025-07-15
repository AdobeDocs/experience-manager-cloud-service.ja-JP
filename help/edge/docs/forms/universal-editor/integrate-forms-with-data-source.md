---
title: ユニバーサルエディターでフォームのフォームデータモデル（FDM）を統合する方法
description: フォームデータモデル（FDM）に基づいたフォームの作成方法について説明します。FDM でデータモデルオブジェクトのサンプルデータを生成し、編集します。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 94%

---

# ユニバーサルエディターでのフォームとフォームデータモデルの統合

ユニバーサルエディターでフォームをフォームデータモデル（FDM）と統合すると、様々なバックエンドデータソースを使用してフォームデータモデル（FDM）を作成できます。フォームデータモデル（FDM）を様々なフォームワークフローのスキーマとして使用できます。データソースを設定し、データソースで使用可能なデータモデルオブジェクトとサービスに基づいて、フォームデータモデル（FDM）を作成します。

## 考慮事項

* ユニバーサルエディターインターフェイスの「**データソース**」アイコンや、右側のプロパティパネルの&#x200B;**連結参照**&#x200B;プロパティが表示されない場合は、**Extension Manager** で&#x200B;**データソース**&#x200B;拡張機能を有効にします。

  ![ フォーム統合を有効にできるデータソース拡張機能など、使用可能な拡張機能を示すユニバーサルエディターExtension Manager インターフェイスのスクリーンショット ](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

  ユニバーサルエディターで拡張機能を有効または無効にする方法については、[&#128279;](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)Extension Manager 機能のハイライトの記事を参照してください。

* ユニバーサルエディターのフォームの事前入力サービスは、現在サポートされていません。

## 前提条件

ユニバーサルエディターでフォームデータモデルを使用してフォームを設定する前に、次の手順が完了していることを確認します。

* [データソースを設定](/help/forms/configure-data-sources.md)：フォームをバックエンドデータに接続するデータソースを設定します。
* [フォームデータモデル（FDM）を作成](/help/forms/create-form-data-models.md)：設定したデータソースのデータオブジェクトとサービスを使用してデータモデルを作成します。
* [データモデルオブジェクトとサービスを設定](/help/forms/work-with-form-data-model.md)：データモデルオブジェクトとサービスをマッピングして、フォームとデータソース間のスムーズなデータフローを確保します。

## ユニバーサルエディターでのフォームデータモデルを使用したフォームの作成

ユニバーサルエディターでは、次の項目を作成できます。

* [スキーマベースのフォーム](#schema-based-form)：スキーマベースのフォームでは、フォーム作成時に「**データ**」タブで設定したデータソースが使用され、データがフォームフィールドに自動的にバインドされます。
* [スキーマベース以外のフォーム](#non-schema-based-form)：スキーマベース以外のフォームでは、データソースを手動で追加し、コンテンツツリーから各フィールドをバインドする必要があります。

![ユニバーサルエディターのフォームのタイプ](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

これらの方法により、必要に応じてデータモデルをフォームに柔軟に接続できます。

### スキーマベースのフォーム

スキーマベースのフォームを作成すると、データソースを使用して自動的に設定され、フォームフィールドはデータバインディングを通じて既にデータにリンクされています。フォーム作成ウィザードを使用してスキーマベースのフォームを作成するには、次の手順を実行します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
1. Experience Manager のログインページに資格情報を入力します。 ログイン後、左上隅の **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 ウィザードが開きます。 「**ソース**」タブで、テンプレートを選択します。

   ![Edge Delivery Services テンプレート](/help/edge/assets/create-eds-forms.png)

   Edge Delivery Services ベースのテンプレートを選択すると、「**[!UICONTROL 作成]**」ボタンが有効になります。「**[!UICONTROL データソース]**」タブまたは「**[!UICONTROL 送信]**」タブに移動して、データソースを選択したり、アクションを送信したりできます。

1. 「**データ**」タブで、次のいずれかのデータモデルを選択できます。

   * **フォームデータモデル（FDM）**：データソースからのデータモデルオブジェクトとサービスをフォームに統合します。フォームで複数のソースからのデータの読み取りと書き込みが必要な場合は、フォームデータモデル（FDM）を選択します。

   * **JSON スキーマ**：データ構造を定義する JSON スキーマを関連付けることで、フォームをバックエンドシステムと統合します。これにより、スキーマ要素を使用して動的コンテンツを追加できます。

     例えば、「ペットフォームデータモデル」という名前の作成済みフォームデータモデルを選択します。

     ![フォームデータモデルを選択](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     デフォルトでは、関連付けられた JSON スキーマまたはフォームデータモデル（FDM）のすべてのフィールドが自動的に選択され、対応するフォームコンポーネントに変換されるので、オーサリングプロセスが簡素化されます。また、ウィザードでは、チェックボックスを使用して、フォームに含めるフィールドを個別に選択することもできます。

1. 「**[!UICONTROL 作成]**」をクリックすると、**フォームを作成**&#x200B;ウィザードが表示されます。
1. 「**名前**」と「**タイトル**」を指定します。
1. **GitHub URL** を指定します。例えば、GitHub リポジトリの名前が `edsforms` で、アカウント `wkndforms` の下にある場合、URL は次のようになります。
   `https://github.com/wkndforms/edsforms`
1. 「**[!UICONTROL 作成]**」をクリックします。

   ![スキーマベースのフォームを作成](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   「**[!UICONTROL 作成]**」をクリックするとすぐに、フォームがオーサリング用のユニバーサルエディターで開きます。

   ![ 事前入力されたフォームフィールドを含むスキーマベースのフォームと、使用可能なデータソース要素を表示するコンテンツブラウザーを示すユニバーサルエディターのスクリーンショット ](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   フォームは、関連付けられたデータソースのデータ要素を使用して作成され、フォームフィールドには、事前設定済みのデータバインディングが含まれています。

   ![自動データバインディング](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   これで、フォームに[送信アクション](/help/edge/docs/forms/universal-editor/submit-action.md)を追加して設定できるようになりました。

### スキーマベース以外のフォーム

スキーマベース以外のフォームを作成した場合、データソースは設定されません。後でフォームのプロパティを編集してデータソースを追加し、フォームフィールドのデータバインディングを手動で設定できます。次の手順を実行して、フォームのプロパティを編集し、データソースを追加します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
1. Experience Manager のログインページに資格情報を入力します。 ログイン後、左上隅の **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. データソースを追加するフォームを選択し、「**[!UICONTROL プロパティ]**」をクリックします。
   ![フォームのプロパティを開く](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   フォームプロパティが開きます。
1. 「**フォームモデル**」タブをクリックして開き、**次から選択**&#x200B;ドロップダウンメニューから選択します。次のいずれかのオプションを選択できます。

   * **フォームデータモデル（FDM）**：フォームデータモデルを使用してフォームを作成します。
   * **コネクタ**：Adobe Marketo データソースを使用してフォームを作成します。
   * **スキーマ**：AEM Forms にアップロードされた JSON スキーマを使用してフォームを作成します。
   * **なし**：フォームモデルを使用しないで最初からフォームを作成します。

     例えば、フォームデータモデル（FDM）を選択します

     ![「フォームモデル」タブを選択](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. ドロップダウンリストから、作成したフォームデータモデル（FDM）を選択します。例えば、ドロップダウンリストから、ペットフォームデータモデルという名前の作成済みフォームデータモデルを選択します。

   ![FDM の選択](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   フォームデータモデル（FDM）を選択すると、警告ダイアログが表示されます。「**OK**」をクリックして、ダイアログを閉じます。

   ![フォームモデルウィザード](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。
1. フォームを編集用に開きます。オーサリング用にユニバーサルエディターでフォームを開きます。

   ![スキーマベース以外のフォームオーサリング](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   関連するフォームデータモデル（FDM）に存在するフォーム要素は、**プロパティパネル**&#x200B;の&#x200B;**[!UICONTROL コンテンツブラウザー]**&#x200B;の「**[!UICONTROL データソース]**」タブに表示されます。

   ![フォームデータソース](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. 「**[!UICONTROL データソース]**」タブからデータ要素を選択し、「**[!UICONTROL 追加]**」をクリックします。

   ![データ要素の追加](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   これらの要素をドラッグ＆ドロップして、アダプティブフォームを作成することもできます。「**[!UICONTROL 追加]**」をクリックすると、「**[!UICONTROL データソース]**」タブで選択した要素がフォームに追加され、追加した要素の前にチェックマークが表示されます。

   ![ 「データSource」タブからフォーム構造にデータ要素をドラッグ&amp;ドロップして作成された、スキーマ以外のフォームを含むユニバーサルエディターを示すスクリーンショット ](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

データ連結は、**連結参照**&#x200B;プロパティから選択してフォームフィールドに追加できます。例えば、フォームに既に存在する **ID** テキストボックスにデータ連結参照を追加してみましょう。データソースツリーからフォームフィールドのデータ連結を選択するには、次の手順を実行します。

1. データ連結参照を追加するフォームフィールドのプロパティを開きます。
1. **連結参照**&#x200B;プロパティに移動し、「**参照**」アイコンをクリックします。

   ![フォームフィールドのデータ連結を手動で追加](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

1. **連結参照を選択**&#x200B;ウィザードで、データソースツリーからデータ連結参照を選択します。

   ![データ連結参照を選択](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

1. フォームフィールドに連結するデータ要素をデータソースツリーから選択し、「**選択**」をクリックします。

   ![データ要素を選択](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

   フォームフィールドはデータ要素に連結され、**連結参照**&#x200B;プロパティに表示されます。

   ![自動データ連結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   また、フォームフィールドの&#x200B;**連結参照**&#x200B;プロパティを手動で編集することもできます。

これで、フォームに[送信アクション](/help/edge/docs/forms/universal-editor/submit-action.md)を追加して設定できるようになりました。

## 関連トピック

{{universal-editor-see-also}}
