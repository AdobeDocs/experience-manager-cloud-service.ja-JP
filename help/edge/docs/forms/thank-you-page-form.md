---
title: フォーム送信後にカスタムのお礼のメッセージを表示
description: フォームブロックのお礼のページとリダイレクトを設定して、ユーザーエクスペリエンスを最適化し、ユーザージャーニーを効率化する方法について説明します。
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 25%

---

# フォーム送信後にカスタムのお礼のメッセージを表示

ユーザーがフォームを送信した後は、「ありがとうございます」メッセージを使用してシームレスなエクスペリエンスを提供することが重要です。 送信が成功したことを確認できるだけでなく、ユーザーの満足度を高め、ジャーニーをさらに進められるようになります。

* **ありがとうメッセージ**：ありがとうメッセージは、ユーザーエクスペリエンスの基礎であり、ブランドアイデンティティを強化しながら、重要な情報を安心して伝えます。 ユーザーの行動を直接的に認知し、達成感や満足感を醸成します。

* **リダイレクト**：リダイレクトは、ユーザーを関連する宛先に導き、エンゲージメントを最適化し、最終的にコンバージョン率を高める上で重要な役割を果たします。 リダイレクトは、ジャーニーの次のステップへとユーザーをシームレスに導くことで、スムーズなナビゲーションエクスペリエンスを保証します。 例えば、最初の詳細を収集した後に支払いページにユーザーをリダイレクトするような場合です。

アダプティブフォームブロックのデフォルトの動作では、送信時に次のお礼のメッセージが表示されます。フォーム送信が成功すると、メッセージがフォームの上部に表示されます。

![デフォルトのお礼のメッセージ](/help/edge/assets/thank-you-message.png)

ただし、特定のニーズに合わせて、このエクスペリエンスを柔軟にカスタマイズできます。 次のようなオプションがあります。

* フォーム送信後にカスタムのお礼のメッセージを表示
* 送信後別のページにユーザーをリダイレクトしてアクションを促す

>[!NOTE]
>
> 以下の [ お問い合わせスプレッドシート ](/help/edge/docs/forms/assets/enquiry.xlsx) を参照して、お客様の要件に合わせて「ありがとうございます」メッセージをカスタマイズできます。

## カスタムの「ありがとうございます」メッセージの設定

フォームの送信が成功したときにパーソナライズされたお礼のメッセージを表示する場合は、スプレッドシートを設定して表示することができます。

アダプティブフォームブロックのカスタムのお礼のメッセージを設定するには、次の手順に従います。

1. Microsoft SharePoint または Google Workspace 上の Edge 配信プロジェクトフォルダーに移動し、スプレッドシートを開きます。
1. スプレッドシートの `submit` フィールドタイプの `value` 列に、カスタマイズした「ありがとうございます」メッセージを追加します。

   ![ カスタマイズされた感謝のメッセージ ](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   例えば、`submit` フィールドタイプ `Submission Successful!` 対して、「`value`」列にメッセージを追加します。

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用して、シートをプレビューし公開します。

   ![ カスタマイズされた感謝のメッセージ ](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## 送信後別ページにユーザーをリダイレクト

フォームの送信後にユーザーを別のページにリダイレクトすると、関連情報を提供し、アクションを確認し、ユーザーを目的の結果に導くことで、ユーザーエクスペリエンスを向上させることができます。 例：

* ユーザーが購入フォームを完了すると、支払いページにリダイレクトされ、トランザクションを安全に完了できます。
* イベントまたはウェビナーの登録フォームを送信すると、ユーザーは日付、時間、場所などのイベントの詳細が表示される確認ページにリダイレクトされます。

ユーザーを別のページにリダイレクトするには、次の手順に従います。

1. Microsoft SharePoint または Google Workspace 上の Edge 配信プロジェクトフォルダーに移動し、スプレッドシートを開きます。
1. スプレッドシートの `submit` フィールドタイプの `value` 列に URL を貼り付けて、フォームが正常に送信されたときにユーザーをリダイレクトします。
ページを別のページにリダイレクトするには、[Edge Delivery ドキュメント ](https://www.aem.live/docs/) ページの URL を使用します。

   ![ リダイレクト URL](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用して、シートをプレビューし公開します。

   ![ 感謝のメッセージをリダイレクト ](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

新しいドキュメントファイルを作成し、そのプレビュー URL を `submit` フィールドタイプの「`value`」列に追加することもできます。

ユーザーがフォームを送信した後は、明確な「ありがとうございます」メッセージを提供することが重要です。 送信が成功したことを確認し、ユーザーの満足度を向上させます。

## 関連トピック

{{see-more-forms-eds}}

<!--
## Configuring a custom thank you message

The default behavior of Adaptive Forms Block is to display the following thank you message on submission. The message is displayed on the top of the form. 

![default thank you message](/help/edge/assets/thank-you-message.png)


Follow the below steps to configure a custom thank you message for your Adaptive Forms Block:

1. Access your AEM Project on your local machine or GitHub repository.

2. Navigate to [AEM Project Folder]\blocks\form\submit.js file for editing.

3. Locate the following code 

    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Thanks for your submission';

    ```

4. Replace the default message with your custom message. For example, 


    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Your submission has been received and noted.';

    ```


1. Save the file. Commit the updated file to your GitHub Repository. Now, when you submit a form, the custom thank you message is displayed. For example,

![Custom thank you message](/help/edge/assets/custom-thank-you-message.png)

* **Thank you message**: A thank you message is a cornerstone of user experience, offering reassurance and conveying important information while reinforcing brand identity. It serves as a direct acknowledgment of the user's action, fostering a sense of completion and satisfaction.

* **Redirect**: A redirect plays a pivotal role in steering users towards relevant destinations, optimizing engagement, and ultimately boosting conversion rates. By seamlessly guiding users to the next step in their journey, a redirect ensures a smooth navigation experience. For example, redirecting user to payments page after collecting initial details. 

In the Adaptive Forms Block, the default behavior is to display a thank you message. However, you have the flexibility to tailor this experience to meet your specific needs. Options include:

* [Configuring a custom thank you message to align with your brand and communication goals](#configuring-the-thank-you-page-and-message) 
* [Redirecting users to another page post-submission for further action](#redirect-users-to-another-page-post-submission)

## Redirect users to another page post-submission

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 





1. Access your AEM Edge Delivery project folder on Microsoft SharePoint or Google Workspace.
1. Create a Microsoft Word or Google Docs file named "thankyou" within your project directory.
1. Add your thank you message to the "thankyou" file. </br>
   
    ![Example thank you page](/help/edge/assets/sample-thankyou-page.png) 

1. Use AEM Sidekick to preview and publish the "thankyou" file.

 Your Adaptive Forms Block displays the "thankyou" page on form submission. 

## Redirect users to another page post-submission

By default, the Adaptive Forms Block redirects the users to the "thankyou" page. To redirect users to a page other than the default "thankyou" page, you have two options: 

* [Replace the "thankyou" page with a different page](#replace-the-existing-thankyou-page) 
* [Use website redirects for "thankyou" page redirection](#use-website-redirects-for-thankyou-page-redirection) 

### Replace the "thankyou" page

1. Open the "[EDS Project]/blocks/form/form.js" file for editing.
1. Change the `thankyou` page in the following line to page of your choice:

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'thankyou';

    ```

    For example,

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'payment';
        
    ```
    
    >[!NOTE]
    >
    > Ensure that a page with the same name exists in your Edge Delivery Services project folder on either Microsoft SharePoint or Google Workspace. If the page does not exist, proceed to create and publish it.  

1. Proceed to check in the updated 'form.js' folder and its underlying files to your Edge Delivery Services project on GitHub. This update ensures that the form now redirects to the updated page as specified.

1. Ensure that the page exists in your EDS project folder and publish it.


### Use website redirects for "thankyou" page redirection

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 



## See also

{{see-more-forms-eds}}