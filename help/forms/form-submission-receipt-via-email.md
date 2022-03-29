---
title: 電子メールによるフォーム送信確認の送信
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms では、フォームの送信時にユーザーに確認を送信する電子メール送信アクションを設定できます。
seo-description: AEM Forms allows you to configure the email Submit Action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 100%

---


# 電子メールによるフォーム送信確認の送信 {#sending-a-form-submission-acknowledgement-via-email}

## アダプティブフォームデータ送信 {#adaptive-form-data-submission}

アクティビティフォームには、いくつかのすぐに使用できる[送信アクション](configuring-submit-actions.md)ワークフローが用意されており、フォームデータを複数のエンドポイントに送信できます。

例えば、**[!UICONTROL 電子メールを送信]**&#x200B;送信アクションは、アクティビティフォームの送信に成功したときに、電子メールを送信します。これは、フォームデータと PDF を電子メールで送信するように設定することもできます。

この記事では、アダプティブフォームで電子メールアクションを有効にする手順や、様々な設定について詳しく説明します。

>[!NOTE]
>
>「**[!UICONTROL 電子メールで PDF を送信]**」オプションを使用すると、完了したフォームを PDF 添付ファイルとして電子メールで送信することもできます。このアクションで使用できる設定オプションは、**[!UICONTROL 電子メールを送信]**&#x200B;アクションで使用できるオプションと同じです。PDF の電子メールアクションは、XFA ベースのアダプティブフォームに対してのみ使用できます。

## 電子メールを送信アクション {#email-action}

電子メールを送信アクションを使用すると、作成者は、アダプティブフォームの送信に成功したときに、1 人または複数の受信者に自動的に電子メールを送信できます。

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, tap **[!UICONTROL Form Container]** and tap ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an end user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### アダプティブフォームのフィールド名を使用した電子メールコンテンツの動的作成 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

アダプティブフォームのフィールド名は、プレースホルダーと呼ばれ、ユーザーがフォームを送信した後にそのフィールドの値で置き換えられます。

**[!UICONTROL 電子メールを送信]**&#x200B;アクションでは、アクションを実行する際に処理されるプレースホルダーを使用できます。これは、ユーザーがフォームを送信する際に、電子メールのヘッダー（**[!UICONTROL 宛先]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL 件名]**&#x200B;など）が生成されることを意味します。

プレースホルダーを定義するには、送信アクションとして「**[!UICONTROL 電子メールを送信]**」を選択してから、フィールドに `${<field name>}` を指定します。

例えば、フォームに `email_addr` という名前の「**[!UICONTROL 電子メールアドレス]**」フィールドが含まれる場合、ユーザーの電子メール ID を取得するために、「**[!UICONTROL 宛先]**」、「**[!UICONTROL CC]**」または「**[!UICONTROL BCC]**」フィールドに以下を指定できます。

`${email_addr}`

ユーザーがフォームを送信すると、フォームの `email_addr` フィールドに入力された電子メール ID に電子メールが送信されます。

>[!NOTE]
>
>フィールドの&#x200B;**[!UICONTROL 編集]**&#x200B;ダイアログにフィールドの名前があります。

また、変数プレースホルダーは、「**[!UICONTROL 件名]**」および「**[!UICONTROL 電子メールテンプレート]**」フィールドにも使用できます。

次に例を示します。

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>繰り返し可能なパネル内のフィールドは、変数プレースホルダーとして使用することはできません。

