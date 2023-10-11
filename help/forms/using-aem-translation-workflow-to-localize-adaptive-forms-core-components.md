---
title: コアコンポーネントベースのアダプティブフォームを翻訳するにはどうすればよいですか？
description: AEM Formsでフォームデータモデルを作成し、サンプルデータとサービスを使用してモデルをテストし、モデルの様々なオプションを設定する方法を説明します。
feature: Adaptive Forms
exl-id: ad46bf0f-e6ec-4c52-9695-5768a9968e16
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 17%

---

# 機械翻訳または人間翻訳を使用した、コアコンポーネントベースのアダプティブフォームの翻訳 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

フォームのローカライズにより、様々な地域の幅広い対象者に向けてフォームを提供できるようになります。アダプティブフォームおよびレコードのドキュメントをローカライズするには、Adobe Experience Manager 翻訳ワークフローが役立ちます。アダプティブフォームのローカライズには、**機械翻訳**&#x200B;または&#x200B;**人による翻訳**&#x200B;を使用できます。

## 機械翻訳を使用したアダプティブフォームとレコードのドキュメントの翻訳 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機械翻訳サービスは、アダプティブフォームのコンテンツを直ちに翻訳し、 [レコードのドキュメント](/help/forms/generate-document-of-record-core-components.md). AEM Forms as a Cloud Serviceは、機械翻訳にMicrosoft Translator の体験版を使用するように事前に設定されています。 アダプティブフォームおよびレコードのドキュメントの機械翻訳を有効にするには、以下の手順を実行します。

1. AEM Forms UI 上でフォームを選択し、「**[!UICONTROL 辞書の追加]**」オプションをタップします。
1. 辞書を翻訳プロジェクトに追加画面で、 **[!UICONTROL プロジェクト]** オプション

   * 翻訳プロジェクトを作成するには、「 **[!UICONTROL 新しい翻訳プロジェクトを作成]** オプションと **プロジェクトタイトル** 「 」フィールドで、タイトルを指定します。 例：`Government Reference Site - German locale.`
   * 既存の翻訳プロジェクトに新しい辞書を追加するには、 **[!UICONTROL 既存の翻訳プロジェクトに追加]** オプションを選択し、 **[!UICONTROL 既存の翻訳プロジェクト]**.
1. Adobe Analytics の **ターゲット言語** フィールドにロケールを指定します ( 例： `German(de)`) をクリックします。 複数のロケールを指定できます。 フォームは、 **ターゲット言語** フィールドに入力します。 「**完了**」をクリックします。
1. 辞書が追加されましたダイアログボックスで、 **プロジェクトを開く**.
1. プロジェクト画面で、新しく作成したプロジェクトをクリックします。 例えば、 **政府リファレンスサイト — ドイツ語ロケール** タイル。
1. **翻訳ジョブ**&#x200B;タイルで ![aem62forms_downarrow](assets/aem62forms_downarrow.png) アイコンをクリックし、「**開始**」をクリックします。タイルのステータスがドラフトに変わります。 翻訳が完了すると、ステータスは「 **承認済み**. 数分後にページを更新し、ステータスを確認します。

   ![翻訳を開始](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. ステータスが「 **承認済み** の **翻訳ジョブ** タイルで、 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) アイコンをクリックし、 **完了**.

1. ローカライズされたフォームをプレビューするには、AEM Forms UI で、ローカライズされたフォームを選択します。 クリック **[!UICONTROL プレビュー]** >**[!UICONTROL プレビューをHTML]**. を追加した後でフォームを再度開く `afAcceptLang=<locale code>` をフォームの URL に追加します。 例えば、 `afAcceptLang=de`をクリックして、ドイツ語版のフォームを開きます。


   >[!NOTE]
   >
   >* ブラウザーウィンドウでローカライズ版のフォームを開く前に、ブラウザーのロケールがフォームのロケールと一致するように設定されていることを確認します。 例えば、フォームがドイツ語 (de) に翻訳されている場合は、ブラウザーのロケールをドイツ語 (de) に設定します。
   >* アダプティブフォームコンポーネントは、右から左に筆記する言語（RTL）をサポートしていません。（例：ヘブライ語）。

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, tap Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## 人間による翻訳を使用したアダプティブフォームとそのレコードのドキュメントのローカライズ {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

人間翻訳では、コンテンツは翻訳プロバイダーに送信され、専門の翻訳者によって翻訳されます。 完了すると、翻訳コンテンツが返され、AEM に読み込まれます。翻訳プロバイダーが AEM と統合されると、AEM と翻訳プロバイダーとの間でコンテンツが自動的に送信されます。

翻訳の場合、XLIFF 形式のファイルを含む辞書は、専門の翻訳者と共有されます。 この辞書には、ロケールごとに個別の XLIFF ファイルが含まれます。 各 XLIFF ファイルには、エンドユーザーに表示されるテキストと、対応するローカライズされたテキストのプレースホルダーが含まれます。

人による翻訳を使用してフォームとレコードのドキュメントをローカライズするには、次の手順を実行します。

1. AEM Forms UI 上でフォームを選択し、「**[!UICONTROL 辞書の追加]**」オプションをタップします。
1. 辞書を翻訳プロジェクトに追加画面で、 **[!UICONTROL プロジェクト]** オプション

   * 翻訳プロジェクトを作成するには、「 **[!UICONTROL 新しい翻訳プロジェクトを作成]** オプションと **プロジェクトタイトル** 「 」フィールドで、タイトルを指定します。 例：`Government Reference Site - German locale.`
   * 既存の翻訳プロジェクトに新しい辞書を追加するには、 **[!UICONTROL 既存の翻訳プロジェクトに追加]** オプションを選択し、 **[!UICONTROL 既存の翻訳プロジェクト]**.
1. Adobe Analytics の **ターゲット言語** フィールドにロケールを指定します ( 例： `German(de)`) をクリックします。 複数のロケールを指定できます。 フォームは、 **ターゲット言語** フィールドに入力します。 「**完了**」をクリックします。
1. 辞書が追加されましたダイアログボックスで、 **プロジェクトを開く**.
1. プロジェクト画面で、新しく作成したプロジェクトをクリックします。 例えば、 **政府リファレンスサイト — ドイツ語ロケール** タイル。
1. の下部に **概要** タイルで、 **省略記号**. 翻訳プロジェクトのプロパティ画面が開きます。
1. を開きます。 **[!UICONTROL 詳細]** タブをクリックします。 **翻訳プロジェクトのプロパティ** 画面。 の **[!UICONTROL 翻訳フィールド]**&#x200B;を選択します。 **[!UICONTROL 人間翻訳]**. クリック **保存して閉じる** をクリックします。
1. 次の日： **翻訳ジョブ** タイルで、 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) アイコンをクリックし、 **書き出し**. [ 書き出し ] ダイアログで、[ 書き出したファイルをダウンロード ] オプションをクリックします。 .zip ファイルをダウンロードします。
   ![翻訳ファイルを書き出し](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. ダウンロードした.zip ファイルを展開します。 抽出されたフォルダーには次の 2 つのファイルが含まれます。
   * translation_export_summary.xml
   * [form-fields-file].xml.
1. を開きます。 [form-fields-file].xml （編集用） フォームフィールドに、ローカライズされた文字列とメッセージを追加します。 ファイルを保存して閉じます。
1. ファイルを translation_export_summary.xml に zip 化し、 [form-fields-file].xml.
1. 次の日： **翻訳ジョブ** タイルで、 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) アイコンをクリックし、 **インポート**. 次を含むアーカイブを選択 [form-fields-file].xml. フォームフィールドのローカライズされた文字列とメッセージを含む

   ![翻訳ファイルをインポート](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. ローカライズされたフォームをプレビューするには、AEM Forms UI で、ローカライズされたフォームを選択します。 クリック **[!UICONTROL プレビュー]** >**[!UICONTROL プレビューをHTML]**. を追加した後でフォームを再度開く `afAcceptLang=<locale code>` をフォームの URL に追加します。 例えば、 `afAcceptLang=de`をクリックして、ドイツ語版のフォームを開きます。
