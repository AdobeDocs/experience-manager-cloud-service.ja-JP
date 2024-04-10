---
title: AEM Forms Edge Delivery ServicesForm の翻訳とローカライズ
description: AEM Forms Edge Delivery ServicesForm の翻訳とローカライズ
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 6%

---


# AEM Forms Edge Delivery ServicesForm の翻訳とローカライズ

Edge Delivery Servicesでは、フォーム翻訳において、正確性、明確さ、一貫性に重点を置いて、フォームコンテンツを別の言語に変換します。 翻訳またはローカライズされたフォームを使用すると、異なる地理的な場所をまたいで幅広いオーディエンスにリーチできます。これにより、ユーザーエクスペリエンスが向上し、様々な言語の環境設定をまたいでコミュニケーションを容易にすることができます。


この記事を読むことで、次の内容を学ぶことができます。

* [Google Drive 内のフォームの翻訳](#translate-form-google-drive)
* [SharePoint サイト内のフォームの翻訳](#translate-form-sharepoint)

## Google Drive 内のフォームの翻訳 {#translate-form-google-drive}

この `GOOGLETRANSLATE` Google シートの機能では、組み込みの翻訳ツールをタップしてフォームを翻訳し、Google シート内でテキストを別の言語に直接変更します。 Google Drive 内でフォームを翻訳するには：

1. Google ドライブのAEM プロジェクトフォルダーに移動し、Google シートを開きます。
2. 既存のシートの名前を変更します（`shared-default`） ～ `shared-en`.
3. という名前のシートを追加します `shared-default`. この `shared-default` シートには、特定の言語にローカライズするコンテンツが含まれています。
4. ローカライズされたコンテンツの追加： `shared-default` を使用したシート `GOOGLETRANSLATE` 関数。
数式を使用して、セル D2 の内容を `shared-en` 内でフランス語にシート `shared-default` シート。 使用する式を次に示します。
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Inquiry Translate スプレッドシート](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. を使用したシートのプレビューとパブリッシュ [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

以下を参照してください [spreadsheet](/help/forms/assets/enquirytranslate.xlsx) のフォーム定義を含む `enquiry` フォームは英語からフランス語に翻訳されています。

![お問い合わせ翻訳済みフォーム](/help/forms/assets/translate-form-french.png)

以下の URL を参照すると、フランス語翻訳でフォームを表示できます（https://main--portal--wkndforms.hlx.live/enquirytranslate）。

## SharePoint サイト内のフォームの翻訳{#translate-form-sharepoint}

Microsoft® SharePoint サイトのフォームを翻訳するには、翻訳サービスを使用してフィールドのラベルを手動で変更する必要があります。 SharePoint サイト内のフォームを翻訳するには：

1. Microsoft®SharePointのAEM プロジェクトフォルダーに移動し、スプレッドシートを開きます。
2. 既存のシートの名前を変更します（`shared-default`） ～ `shared-en`.
3. という名前のシートを追加します `shared-default`. この `shared-default` シートには、特定の言語にローカライズするコンテンツが含まれています。
4. ローカライズされたコンテンツの追加： `shared-default` 手動でシート化する。

   ![Inquiry Translate スプレッドシート](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. を使用したシートのプレビューとパブリッシュ [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

を参照してください。 [spreadsheet](/help/forms/assets/enquirytranslate-sp.xlsx) のフォーム定義を含む `enquiry` フォームは英語からフランス語に翻訳されています。

![お問い合わせ翻訳済みフォーム](/help/forms/assets/translate-form-french.png)

以下の URL を参照すると、フランス語翻訳でフォームを表示できます（https://main--wefinance--wkndforms.hlx.live/enquirytranslate）。

## 既知の問題 {#known-issues}

* フォームのラベルは、で指定されたローカライズされた言語に翻訳されます。 `shared-default` シートに表示されますが、エラーメッセージはブラウザーのデフォルト言語で表示されます。

  ![エラーメッセージ](/help/forms/assets/translate-error-message.png)

* カレンダーを開くと、ブラウザーのデフォルト言語でカレンダードロップダウンが表示されます。

  ![エラーメッセージ](/help/forms/assets/translate-calender-display.png)


## よくある質問 {#faq}

**第四半期**：フォーム内で指定されたローカライズされた言語で入力を入力するにはどうすればよいですか？

**A**：特定のローカライズされた言語でテキストを入力するには、デバイスのキーボード設定を調整します。 その方法については、次のリンクを参照してください。

* [他の言語で入力できるようにMacを設定する](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
* [別の言語で入力できるように Windows をセットアップします](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
* [別の言語で入力できるように Android または iPhone/iPad を設定します](https://support.google.com/gboard/answer/7068494?hl=en&amp;co=GENIE.Platform%3DAndroid)


**第四半期**：で使用されているロケールのリストを取得する方法 `GOOGLETRANSLATE` 機能？

**A**：次を参照してください [Googleの公式ドキュメント](https://cloud.google.com/translate/docs/languages) GOOGLETRANSLATE で使用されるロケールの包括的なリスト。

## 関連トピック

{{see-more-forms-eds}}

