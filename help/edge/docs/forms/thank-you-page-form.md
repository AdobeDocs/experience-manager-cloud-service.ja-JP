---
title: 「ありがとうございます」ページまたはリダイレクトフォームを送信後に設定
description: Forms Block の「ありがとうございます」ページとリダイレクトを設定して、ユーザーエクスペリエンスを最適化し、ユーザージャーニーを合理化する方法について説明します。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---


# 送信後に「ありがとうございます」ページまたはリダイレクトフォームを表示

ユーザーがフォームを送信した後、「ありがとうございました」ページまたはリダイレクトを通じて、シームレスなエクスペリエンスを提供することが重要です。 これらの要素は、送信の成功を確認するだけでなく、ユーザーの満足度を高め、ジャーニーをさらに促進します。

* **「ありがとうございます」ページ**：ありがとうページは、ブランドアイデンティティを強化しながら、安心感を提供し、重要な情報を伝えるユーザーエクスペリエンスの基礎となります。 ユーザーの行動を直接認識し、完了感と満足感を促進する役割を果たします。

* **リダイレクト**：リダイレクトは、ユーザーを関連する宛先に導き、エンゲージメントを最適化し、最終的にコンバージョン率を高めるのに重要な役割を果たします。 ユーザーをジャーニーの次のステップにシームレスに導くことで、リダイレクトによってスムーズなナビゲーションが実現します。 例えば、初期の詳細を収集した後で、ユーザーを支払いページにリダイレクトします。

「アダプティブForms」ブロックでは、デフォルトの動作で「ありがとうございます」ページが表示されます。 ただし、このエクスペリエンスは、特定のニーズに合わせて柔軟に調整できます。 オプションは次のとおりです。

* [ブランドやコミュニケーションの目標に合わせて「ありがとうございます」ページとメッセージを設定する](#configuring-the-thank-you-page-and-message)
* [ユーザーを別のページにリダイレクトして投稿を送信し、さらにアクションを実行する](#redirect-users-to-another-page-post-submission)

## 「ありがとうございます」ページとメッセージの設定

アダプティブFormsブロックのデフォルトの動作では、送信時に「thankyou」ページが表示されます。 アダプティブFormsブロックの「thankyou」ページを設定するには、次の手順に従います。

1. Microsoft SharePointまたはGoogle Workspace のAEM Edge Delivery プロジェクトフォルダーにアクセスします。
1. プロジェクトディレクトリ内に、「thankyou」という名前のMicrosoft Word またはGoogle Docs ファイルを作成します。
1. 「thankyou」ファイルに感謝のメッセージを追加します。 </br>

   ![「ありがとうございます」ページの例](/help/edge/assets/sample-thankyou-page.png)

1. AEM Sidekickを使用して、「thankyou」ファイルをプレビューし、公開します。

アダプティブFormsブロックには、フォーム送信時に「感謝状」ページが表示されます。

## ユーザーを送信後に別のページにリダイレクト

デフォルトでは、アダプティブFormsブロックはユーザーを「感謝祭」ページにリダイレクトします。 デフォルトの「thankyou」ページ以外のページにユーザーをリダイレクトするには、次の 2 つのオプションがあります。

* [「thankyou」ページを別のページに置き換えます。](#replace-the-existing-thankyou-page)
* [「感謝祭」ページのリダイレクトに Web サイトのリダイレクトを使用](#use-website-redirects-for-thankyou-page-redirection)

### 「thankyou」ページを置き換えます。

1. を開きます。[EDS プロジェクト]/blocks/form/form.js&quot;ファイルを編集します。
1. 次を変更： `thankyou` ページを次の行から選択したページに移動します。

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > Microsoft SharePointまたはGoogle Workspace の Edge Delivery Service プロジェクトフォルダーに同じ名前のページが存在することを確認します。 ページが存在しない場合は、作成して公開します。

1. 更新された「form.js」フォルダーとその基になるファイルを、GitHub の Edge 配信サービスプロジェクトにチェックインします。 この更新により、フォームは、指定したとおりに更新されたページにリダイレクトされるようになります。

1. EDS プロジェクトフォルダーにページが存在することを確認し、公開します。


### 「感謝祭」ページのリダイレクトに Web サイトのリダイレクトを使用

フォーム送信後にユーザーを別のページにリダイレクトすると、関連情報を提供し、アクションを確認し、ユーザーを希望する結果に導くことで、ユーザーのエクスペリエンスを向上させることができます。 例：

* ユーザーが購入フォームを完了すると、支払いページにリダイレクトされ、トランザクションを安全に完了します。
* イベントやウェビナーの登録フォームを送信すると、日付、時刻、場所などのイベントの詳細を表示する確認ページにリダイレクトされます。

「感謝状」ページを別のページにリダイレクトするには、 [web サイトのリダイレクト](https://www.aem.live/docs/redirects) スプレッドシート。


## 詳細を表示する

* [フォームコンポーネント](/help/edge/docs/forms/form-components.md)
* [フォームフィールドのプロパティ](/help/edge/docs/forms/eds-form-field-properties)
* [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
* [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
* [サイトページにフォームを発行する](/help/edge/docs/forms/publish-forms.md)
* [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
* [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)
