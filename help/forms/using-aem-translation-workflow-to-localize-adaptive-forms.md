---
title: AEM翻訳ワークフローを使用してアダプティブFormsとレコードのドキュメントをローカライズするにはどうすればよいですか？
description: AEM 翻訳ワークフローを使用してアダプティブフォームとレコードのドキュメントをローカライズする方法について説明します。
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 90%

---


# アダプティブFormsとレコードのドキュメントのローカライズ{#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

フォームのローカライズにより、様々な地域の幅広い対象者に向けてフォームを提供できるようになります。アダプティブフォームおよびレコードのドキュメントをローカライズするには、Adobe Experience Manager 翻訳ワークフローが役立ちます。アダプティブフォームのローカライズには、**機械翻訳**&#x200B;または&#x200B;**人による翻訳**&#x200B;を使用できます。

この記事では、アダプティブフォームおよびレコードのドキュメントに対する AEM 翻訳ワークフローの使用手順を説明します。

## 機械翻訳によるアダプティブフォームおよびレコードのドキュメントのローカライズ {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機械翻訳サービスを使用すると、アダプティブフォームおよびレコードのドキュメントを即座に翻訳できます。[!DNL AEM Forms] では、機械翻訳に [!DNL Microsoft Translator] の体験版を使用するように事前設定されています。アダプティブフォームおよびレコードのドキュメントの機械翻訳を有効にするには、以下の手順を実行します。

1. 次の日： [!DNL AEM Forms] UI、フォームを選択し、 **辞書を追加** オプション。
1. **辞書を翻訳プロジェクトに追加** 画面で、「**新しい翻訳プロジェクトを作成**」または「**既存の翻訳プロジェクトを追加**」オプションを選択します。
1. 「**プロジェクトタイトル**」フィールドでタイトルを指定します。例：`Government Reference Site - German locale.`
1. 「**ターゲット言語**」フィールドでロケールを指定し（例えば `German(de)` と入力します）、「**完了**」をクリックします。複数のロケールを指定できます。フォームは、**ターゲット言語**&#x200B;フィールドに指定されたすべてのロケールに翻訳されます。
1. 辞書が追加された際のダイアログボックスで、「**プロジェクトを開く**」をクリックします。プロジェクト画面で、作成したプロジェクトを開きます。
1. 「**翻訳の概要**」タイルの下部にある&#x200B;**省略記号**&#x200B;をクリックします。翻訳の概要画面が開きます。
1. **翻訳の概要**&#x200B;の上部にある&#x200B;**編集**&#x200B;アイコンをクリックします。「**翻訳**」タブを開き、 **翻訳方法** 画面で機械翻訳を選択します。適切な **翻訳プロバイダー** と **クラウド設定** を選択します。画面の上部にある「**完了**」アイコンをクリックします。
1. **翻訳ジョブ**&#x200B;タイルで ![aem62forms_downarrow](assets/aem62forms_downarrow.png) アイコンをクリックし、「**開始**」をクリックします。タイルのステータスがドラフトに変わります。翻訳が完了すると、ステータスは「**レビューへの準備完了**」に変わります。数分後にページを更新し、ステータスを確認します。
1. **翻訳ジョブ**&#x200B;タイルのステータスが&#x200B;**レビューへの準備完了**&#x200B;に変わったことを確認できたら、ブラウザーウィンドウでフォームを開きます。フォームのローカライズ版が表示されます。

   >[!NOTE]
   >
   >* ブラウザーウィンドウでローカライズ版のフォームを開く前に、ブラウザーのロケールがフォームのロケールと一致するように設定されていることを確認します。例えば、フォームがドイツ語（de）に翻訳されている場合は、ブラウザーのロケールをドイツ語（de）に設定します。
   >* アダプティブフォームコンポーネントは、右から左（RTL）言語をサポートしていません（例：ヘブライ語）。

   アダプティブフォームと共に、自動生成されるレコードのドキュメントもローカライズされます。

   レコードのドキュメントの設定と構成について詳しくは、以下を参照してください。

[レコードのドキュメントのテンプレート設定](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[レコードのドキュメントの設定](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [レコードのドキュメントのブランディング情報をカスタマイズ](generate-document-of-record-for-non-xfa-based-adaptive-forms.md)し、ブラウザーのロケールを、機械語を使用してアダプティブフォームをローカライズしたのと同じ言語に設定します。ブラウザーのロケールは、レコードのドキュメントにあるブランディング情報のローカライズに役立ちます。
1. ローカライズされたレコードのドキュメントを表示するには、「プレビューを生成」を選択します。 レコードのドキュメントの PDF が生成され、ブラウザーの新しいタブに表示されます。

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that is displayed to the end users and placeholders for the corresponding localized text.

Perform the following steps to localize a form and its Document of Record using Human Translators:

1. [Connect AEM with your translation service provider](/help/sites-administering/tc-tic.md) and [create translation integration framework configurations](/help/sites-administering/tc-tic.md).

1. [Associate the pages of your language master](/help/sites-administering/tc-tic.md) with the translation service and framework configurations.

1. [Identify the type of content](/help/sites-administering/tc-rules.md) to translate.

1. [Prepare the content for translation](/help/sites-administering/tc-prep.md) by authoring the language master and creating the root pages of language copies.

1. [Create translation projects](/help/sites-administering/tc-manage.md) to gather the content to translate and to prepare the translation process.

1. Use the translation projects to [manage the content translation process](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Adaptive Form components do not support right to left (RTL) languages. For example, Hebrew.
> -->

