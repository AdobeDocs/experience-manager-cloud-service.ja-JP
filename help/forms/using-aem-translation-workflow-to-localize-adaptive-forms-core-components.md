---
title: コアコンポーネントベースのアダプティブフォームを翻訳するにはどうすればよいですか？
description: AEM Forms でフォームデータモデル（FDM）を作成し、サンプルデータとサービスを使用してモデルをテストし、モデルの様々なオプションを設定する方法を説明します。
feature: Adaptive Forms, Core Components
exl-id: ad46bf0f-e6ec-4c52-9695-5768a9968e16
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: ht
source-wordcount: '885'
ht-degree: 100%

---

# 機械翻訳または人間による翻訳を使用した、コアコンポーネントベースのアダプティブフォームの翻訳 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

フォームのローカライズにより、様々な地域の幅広い対象者に向けてフォームを提供できるようになります。アダプティブフォームおよびレコードのドキュメントをローカライズするには、Adobe Experience Manager 翻訳ワークフローが役立ちます。アダプティブフォームのローカライズには、**機械翻訳**&#x200B;または&#x200B;**人による翻訳**&#x200B;を使用できます。

## 機械翻訳によるアダプティブフォームおよびレコードのドキュメントの翻訳 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機械翻訳サービスを使用すると、アダプティブフォームおよび[レコードのドキュメント](/help/forms/generate-document-of-record-core-components.md)を即座に翻訳できます。AEM Forms as a Cloud Service では、機械翻訳に Microsoft Translator の体験版を使用することが事前に定義されています。アダプティブフォームおよびレコードのドキュメントの機械翻訳を有効にするには、以下の手順を実行します。

1. AEM Forms UI 上でフォームを選択し、「**[!UICONTROL 辞書を追加]**」オプションをクリックします。
1. 辞書を翻訳プロジェクトに追加画面の、「**[!UICONTROL プロジェクト]**」オプション

   * 翻訳プロジェクトを作成するには、「**[!UICONTROL 新しい翻訳プロジェクトを作成]**」オプションを選択し、「**プロジェクトタイトル**」フィールドでタイトルを指定します。例：`Government Reference Site - German locale.`
   * 新しい辞書を既存の翻訳プロジェクトに追加するには、「**[!UICONTROL 既存の翻訳プロジェクトに追加]**」オプションを選択し、「**[!UICONTROL 既存の翻訳プロジェクト]**」を選択します。
1. 「**ターゲット言語**」フィールドで、ロケール（`German(de)` など）を指定します。複数のロケールを指定できます。フォームは、「**ターゲット言語**」フィールドで指定されたすべてのロケールに翻訳されます。「**完了**」をクリックします。
1. 辞書の追加ダイアログボックスで、「**プロジェクトを開く**」をクリックします。
1. プロジェクト画面で、作成されたプロジェクトをクリックします。例えば、**政府リファレンスサイト - ドイツ語ロケール**&#x200B;タイルをクリックします。
1. **翻訳ジョブ**&#x200B;タイルで ![aem62forms_downarrow](assets/aem62forms_downarrow.png) アイコンをクリックし、「**開始**」をクリックします。タイルのステータスがドラフトに変わります。翻訳を完了すると、ステータスが「**承認済み**」に変わります。数分後にページを更新し、ステータスを確認します。

   ![翻訳を開始](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. **翻訳ジョブ**&#x200B;タイルのステータスが「**承認済み**」に変わったら、「![aem62forms_downarrow](assets/aem62forms_downarrow.png)」アイコンをクリックし、「**完了**」をクリックします。

1. ローカライズされたフォームをプレビューするには、AEM Forms UI で、ローカライズされたフォームを選択します。**[!UICONTROL プレビュー]**／**[!UICONTROL HTML をプレビュー]**&#x200B;をクリックします。フォームの URL に `afAcceptLang=<locale code>` を追加した後、フォームを再度開きます。例えば、ドイツ語版のフォームを開くには `afAcceptLang=de` を追加します。


   >[!NOTE]
   >
   >* ブラウザーウィンドウでローカライズ版のフォームを開く前に、ブラウザーのロケールがフォームのロケールと一致するように設定されていることを確認します。例えば、フォームがドイツ語（de）に翻訳されている場合は、ブラウザーのロケールをドイツ語（de）に設定します。
   >* アダプティブフォームコンポーネントは、右から左に筆記する言語（RTL）をサポートしていません。（例：ヘブライ語）。

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, select Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## 人間による翻訳を使用した、アダプティブフォームおよびレコードのドキュメントのローカライズ {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

人間による翻訳を使用すると、コンテンツは翻訳プロバイダーに送信され、専門の翻訳者によって翻訳が行われます。完了すると、翻訳コンテンツが返され、AEM に読み込まれます。翻訳プロバイダーが AEM と統合されると、AEM と翻訳プロバイダーとの間でコンテンツが自動的に送信されます。

翻訳では、XLIFF 形式のファイルを含む辞書が専門の翻訳者と共有されます。この辞書には、ロケールごとに個別の XLIFF ファイルが含まれます。各 XLIFF ファイルには、エンドユーザーに表示されるテキストと、対応するローカライズ済みテキストのプレースホルダーが含まれています。

人間による翻訳を使用してフォームとレコードのドキュメントをローカライズするには、次の手順を実行します。

1. AEM Forms UI 上でフォームを選択し、「**[!UICONTROL 辞書を追加]**」オプションをクリックします。
1. 辞書を翻訳プロジェクトに追加画面の、「**[!UICONTROL プロジェクト]**」オプション

   * 翻訳プロジェクトを作成するには、「**[!UICONTROL 新しい翻訳プロジェクトを作成]**」オプションを選択し、「**プロジェクトタイトル**」フィールドでタイトルを指定します。例：`Government Reference Site - German locale.`
   * 新しい辞書を既存の翻訳プロジェクトに追加するには、「**[!UICONTROL 既存の翻訳プロジェクトに追加]**」オプションを選択し、「**[!UICONTROL 既存の翻訳プロジェクト]**」を選択します。
1. 「**ターゲット言語**」フィールドで、ロケール（`German(de)` など）を指定します。複数のロケールを指定できます。フォームは、「**ターゲット言語**」フィールドで指定されたすべてのロケールに翻訳されます。「**完了**」をクリックします。
1. 辞書の追加ダイアログボックスで、「**プロジェクトを開く**」をクリックします。
1. プロジェクト画面で、作成されたプロジェクトをクリックします。例えば、**政府リファレンスサイト - ドイツ語ロケール**&#x200B;タイルをクリックします。
1. **概要**&#x200B;タイルの下部にある、**省略記号**&#x200B;をクリックします。翻訳プロジェクトのプロパティ画面が開きます。
1. **翻訳プロジェクトのプロパティ**&#x200B;画面の上部にある「**[!UICONTROL 詳細設定]**」タブを開きます。**[!UICONTROL 翻訳フィールド]**&#x200B;で、「**[!UICONTROL 人間による翻訳]**」を選択します。画面上部の「**保存して閉じる**」をクリックします。
1. **翻訳ジョブ**&#x200B;タイルで「![aem62forms_downarrow](assets/aem62forms_downarrow.png)」アイコンをクリックし、「**書き出し**」をクリックします。書き出しダイアログで、「書き出したファイルをダウンロード」オプションをクリックします。.zip ファイルをダウンロードします。
   ![翻訳ファイルの書き出し](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. ダウンロードした .zip ファイルを解凍します。展開されたフォルダーには次の 2 つのファイルが含まれています。
   * translation_export_summary.xml
   * [form-fields-file].xml.
1. [form-fields-file].xml を開いて編集します。フォームフィールドのローカライズ対象の文字列とメッセージを追加します。ファイルを保存して閉じます。
1. ファイル translation_export_summary.xml および [form-fields-file].xml を zip 形式で圧縮します。
1. **翻訳ジョブ**&#x200B;タイルで「![aem62forms_downarrow](assets/aem62forms_downarrow.png)」アイコンをクリックし、「**読み込み**」をクリックします。[form-fields-file].xml. を含むアーカイブを選択します。フォームフィールドのローカライズ対象の文字列とメッセージを使用します。

   ![翻訳ファイルの読み込み](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. ローカライズされたフォームをプレビューするには、AEM Forms UI で、ローカライズされたフォームを選択します。**[!UICONTROL プレビュー]**／**[!UICONTROL HTML をプレビュー]**&#x200B;をクリックします。フォームの URL に `afAcceptLang=<locale code>` を追加した後、フォームを再度開きます。例えば、ドイツ語版のフォームを開くには、`afAcceptLang=de` を追加します。

## 関連トピック {#see-also}

{{see-also}}