---
title: AEM Formsでメールを使用してフォーム送信確認を送信する方法
description: AEM Forms では、フォームの送信時にユーザーに受信確認を送信するメール送信アクションを設定できます。
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 100%

---


# メールによるフォーム送信確認の送信 {#sending-a-form-submission-acknowledgement-via-email}

## アダプティブフォームデータ送信 {#adaptive-form-data-submission}

アクティビティフォームには、いくつかのすぐに使用できる[送信アクション](configuring-submit-actions.md)ワークフローが用意されており、フォームデータを複数のエンドポイントに送信できます。

例えば、**[!UICONTROL メールを送信]**&#x200B;送信アクションは、アクティビティフォームの送信に成功したときに、メールを送信します。これは、フォームデータと PDF をメールで送信するように設定することもできます。

この記事では、アダプティブフォームでメールアクションを有効にする手順や、様々な設定について詳しく説明します。

>[!NOTE]
>
>「**[!UICONTROL メールで PDF を送信]**」オプションを使用すると、完了したフォームを PDF 添付ファイルとしてメールで送信することもできます。このアクションで使用できる設定オプションは、**[!UICONTROL メールを送信]**&#x200B;アクションで使用できるオプションと同じです。PDF のメールアクションは、XFA ベースのアダプティブフォームに対してのみ使用できます。

## メールを送信アクション {#email-action}

メールを送信アクションを使用すると、作成者は、アダプティブフォームの送信に成功したときに、1 人または複数の受信者に自動的にメールを送信できます。

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, select **[!UICONTROL Form Container]** and select ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### アダプティブフォームのフィールド名を使用したメールコンテンツの動的作成 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

アダプティブフォームのフィールド名は、プレースホルダーと呼ばれ、ユーザーがフォームを送信した後にそのフィールドの値で置き換えられます。

**[!UICONTROL メールを送信]**&#x200B;アクションでは、アクションを実行する際に処理されるプレースホルダーを使用できます。これは、ユーザーがフォームを送信する際に、メールのヘッダー（**[!UICONTROL 宛先]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL 件名]**&#x200B;など）が生成されることを意味します。

プレースホルダーを定義するには、送信アクションとして「**[!UICONTROL メールを送信]**」を選択してから、フィールドに `${<field name>}` を指定します。

例えば、フォームに `email_addr` という名前の「**[!UICONTROL メールアドレス]**」フィールドが含まれる場合、ユーザーのメール ID を取得するために、「**[!UICONTROL 宛先]**」、「**[!UICONTROL CC]**」または「**[!UICONTROL BCC]**」フィールドに以下を指定できます。

`${email_addr}`

ユーザーがフォームを送信すると、フォームの `email_addr` フィールドに入力されたメール ID にメールが送信されます。

>[!NOTE]
>
>フィールドの&#x200B;**[!UICONTROL 編集]**&#x200B;ダイアログにフィールドの名前があります。

また、変数プレースホルダーは、「**[!UICONTROL 件名]**」および「**[!UICONTROL メールテンプレート]**」フィールドにも使用できます。

例：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>繰り返し可能なパネル内のフィールドは、変数プレースホルダーとして使用することはできません。

