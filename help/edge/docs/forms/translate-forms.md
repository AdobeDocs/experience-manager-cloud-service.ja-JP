---
title: AEM Forms の Edge Delivery Services の翻訳とローカライズ
description: AEM Forms の Edge Delivery Services の翻訳とローカライズ
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '544'
ht-degree: 100%

---


# AEM Forms の Edge Delivery Services の翻訳とローカライズ

Edge Delivery では、フォーム翻訳の際に、正確さ、明確さおよび一貫性に重点を置いてフォームコンテンツを別の言語に変換する必要があります。フォームを翻訳またはローカライズすると、様々な地域の幅広いオーディエンスにリーチできるので、ユーザーエクスペリエンスが向上し、多様な言語設定でより良いコミュニケーションを促進することができます。


この記事を最後まで読むと、以下を行えるようになります。

- [Google ドライブ内のフォームの翻訳](#translate-form-google-drive)
- [SharePoint サイト内のフォームの翻訳](#translate-form-sharepoint)

## Google ドライブ内のフォームの翻訳 {#translate-form-google-drive}

Google シートの `GOOGLETRANSLATE` 関数では、ビルトインの翻訳ツールを利用してフォームを翻訳し、Google シート内でテキストを別の言語に直接変更します。Google ドライブ内でフォームを翻訳するには、次の手順に従います。

1. Google ドライブの AEM プロジェクトフォルダーに移動し、Google シートを開きます。
2. 既存のシート（`shared-default`）の名前を `shared-en` に変更します。
3. `shared-default` という名前のシートを追加します。`shared-default` シートには、特定の言語にローカライズしたコンテンツが含まれています。
4. `GOOGLETRANSLATE` 関数を使用して、ローカライズされたコンテンツを `shared-default` シートに追加します。
`shared-default` シート内で数式を使用して、`shared-en` シートのセル D2 の内容をフランス語に翻訳することができます。使用する式は次のとおりです。
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![お問い合わせフォーム翻訳スプレッドシート](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用して、シートをプレビューおよび公開します。

英語からフランス語に翻訳された `enquiry` フォームのフォーム定義を含んだ[スプレッドシート](/help/forms/assets/enquirytranslate.xlsx)を参照できます。

![翻訳済みのお問い合わせフォーム](/help/forms/assets/translate-form-french.png)

URL（https://main--portal--wkndforms.hlx.live/enquirytranslate）を参照すると、フランス語翻訳でフォームを表示できます。


## SharePoint サイト内のフォームの翻訳{#translate-form-sharepoint}

Microsoft® SharePoint サイトのフォームを翻訳するには、任意の翻訳サービスを使用してフィールドのラベルを手動で変更する必要があります。SharePoint サイト内のフォームを翻訳するには、次の手順に従います。

1. Microsoft® SharePoint の AEM プロジェクトフォルダーに移動し、スプレッドシートを開きます。
2. 既存のシート（`shared-default`）の名前を `shared-en` に変更します。
3. `shared-default` という名前のシートを追加します。`shared-default` シートには、特定の言語にローカライズしたコンテンツが含まれています。
4. ローカライズされたコンテンツを手動で `shared-default` シートに追加します。

   ![お問い合わせフォーム翻訳スプレッドシート](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用して、シートをプレビューおよび公開します。

英語からフランス語に翻訳された `enquiry` フォームのフォーム定義を含んだ[スプレッドシート](/help/forms/assets/enquirytranslate-sp.xlsx)を参照してください。

![翻訳済みのお問い合わせフォーム](/help/forms/assets/translate-form-french.png)

URL（https://main--wefinance--wkndforms.hlx.live/enquirytranslate）を参照すると、フランス語翻訳でフォームを表示できます。


## 既知の問題 {#known-issues}

- `shared-default` シートで、フォームのラベルは指定のローカライズ先言語に翻訳されますが、エラーメッセージはブラウザーのデフォルト言語で表示されます。

  ![エラーメッセージ](/help/forms/assets/translate-error-message.png)

- カレンダーを開くと、カレンダードロップダウンがブラウザーのデフォルト言語で表示されます。

  ![エラーメッセージ](/help/forms/assets/translate-calender-display.png)


## よくある質問 {#faq}

**Q**：指定のローカライズ先言語でフォームに入力するにはどうすればよいですか？

**A**：特定のローカライズ先言語でテキストを入力するには、お使いのデバイスのキーボード設定を調整します。方法については、次のリンクを参照してください。

- [別の言語で入力できるように Mac を設定する](https://support.apple.com/ja-in/guide/mac-help/mchlp1406/mac)
- [別の言語で入力できるように Windows を設定する](https://support.microsoft.com/ja-jp/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
- [別の言語で入力できるように Android または iPhone／iPad を設定する](https://support.google.com/gboard/answer/7068494?hl=ja&co=GENIE.Platform%3DAndroid)


**Q**：`GOOGLETRANSLATE` 関数で使用されるロケールのリストを取得するにはどうすればよいですか？

**A**：GOOGLETRANSLATE で使用されるロケールの包括的なリストについては、[Google の公式ドキュメント](https://cloud.google.com/translate/docs/languages)を参照してください。


