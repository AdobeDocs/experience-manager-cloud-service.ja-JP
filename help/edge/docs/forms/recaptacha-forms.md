---
title: AEM Forms as a Cloud Service の Edge Delivery Services での reCAPTCHA の使用
description: EDS フォームでの Google reCAPTCHA の使用
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
source-git-commit: 8730383d26c6f4fbe31a25a43d33bf314251d267
workflow-type: ht
source-wordcount: '200'
ht-degree: 100%

---


# AEM Forms as a Cloud Service の Edge Delivery Services での reCAPTCHA の使用

reCAPTCHA は、web サイトを不正行為、スパムおよび悪用から守るために使用される一般的なツールです。Edge Delivery では、Google reCAPTCHA を追加して人間とボットを区別する機能がアダプティブフォームブロックから提供されます。この機能により、ユーザーは自分の web サイトをスパムや不正使用から保護できます。
例えば、旅行の開始日と終了日、部屋の予算、旅行費用の見積もり、旅行者情報などのデータを収集する問い合わせフォームを考えてみます。このような場合は、悪意のあるユーザーがフォームを悪用してフィッシングメールを送信したり、スパムボットを使用して無関係または有害なコンテンツを大量に送信したりするリスクがあります。reCAPTCHA を統合すると、送信が本物のユーザーからのものであることを確認して、セキュリティを強化し、スパムエントリを最小限に抑える効果を得ることができます。

Edge Delivery では、アダプティブフォームブロックに&#x200B;**スコアベース（v3）の reCAPTCHA** のみをサポートしています。

![reCAPTCHA v2](/help/forms/assets/recaptcha-v2-invisible.png)

**reCAPTCHA** 機能はプレリリースプログラムで提供されているものです。AEM Forms Edge Delivery の **reCAPTCHA** 機能の利用を申請するには、職場のアドレスから mailto:aem-forms-ea@adobe.com にメールを送信してください。

<!--
By the end of this article, you learn to:
  * [Enable Google reCAPTCHA's for a single form](#enable-google-recaptchas-for-a-single-form)
  * [Enable reCAPTCHA for all the forms on your Site](#enable-recaptcha-for-all-the-forms)

## Pre-requisite

Register your domain with [Google reCAPTCHA and obtain credentials](https://www.google.com/recaptcha/admin/create).

## Enable Google reCAPTCHA's for a single form {#enable-google-recaptchas-for-a-single-form}

Enabling Google reCAPTCHA for a single form involves integrating Google's reCAPTCHA service into a specific web form to prevent automated abuse or spam submissions.

To enable Google reCAPTCHA's for a single form:
1. [Configure the reCAPTCHA secret key in project configuration file](#configure-secret-key)
1. [Add reCAPTCHA site key to your form](#add-site-key)


### Configure the reCAPTCHA secret key in project configuration file {#configure-secret-key}

The Site Secret for domain registered with Google reCAPTCHA is added to project the configuration file (`.helix/config`) in your AEM Project folder at Microsoft SharePoint or Google Drive. To add the Site Secret to the config file:

1. Go to your AEM Project folder on Microsoft® SharePoint or Google Drive. 
1. Create the `.helix/config.xlsx` file in your AEM Project folder in Microsoft SharePoint Site or the `.helix/config` file in AEM Project folder within your Google Drive. 

    >[!NOTE]
    >
    > The [project configuration file](https://www.aem.live/docs/configuration) is a spreadsheet located at `/.helix/config`. If the file does not exist, create it.

1. Open the `config` file and add the following key and value pairs:

    * **captcha.secret**: Google reCAPTCHA secret key value
    * **captcha.type**: reCAPTCHA v2
  
   Refer to the image for an illustration of a project configuration file:

    ![Project configuration file](/help/forms/assets/recaptcha-config-file.png)

    >[!NOTE]
    >
    >  You can retrieve the reCAPTCHA keys from the [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1.  Preview and publish the `config` file using [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content). 

### Add reCAPTCHA site key to your form {#add-site-key}

The Site Key for domain registered with Google reCAPTCHA is added to the spreadsheet of the form that is to be protected. To add the Site key to a form:

1. Go to your AEM Project folder on Microsoft® SharePoint or Google Drive and open your spreadsheet. You can also create new spreadsheet for a form.
1. Insert a row into the spreadsheet to add new field as CAPTCHA, including the following details:
    * **type**: captcha
    * **value**: Google reCAPTCHA site key value
  
    Refer to the illustration below, depicting the spreadsheet with the new row type as CAPTCHA:
  
   ![Recaptcha spreadsheet](/help/forms/assets/recaptcha-spreadsheet.png)

    >[!NOTE]
    >
    >  You can retrieve the reCAPTCHA keys from the [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) to preview and publish the sheet. 
You can refer to the [spreadsheet](/help/forms/assets/recaptcha-enquiry.xlsx) that includes the form definition for an enquiry form.

After adding new row in the form definition, a reCAPTCHA badge appears at the bottom-right corner of the form. This ensures that the form is now protected from fraudulent activities, spam, and misuse.

![recaptcha-form](/help/forms/assets/recaptcha-form.png)

Refer to the URL below, which showcases the live form with the reCAPTCHA badge:
https://main--wefinance--wkndforms.hlx.live/enquiry

## Enable reCAPTCHA for all the forms on your Site{#enable-recaptcha-for-all-the-forms}

To apply Google reCAPTCHA to all the forms on your Site that use Adaptive Forms Block, skip the previous steps and directly embed the `sitekey` value into the `recaptcha.js` file. To include site key value in the `recaptcha.js` file:

1. Open the corresponding GitHub repository on your local machine. 
1. Navigate to `../blocks/form/integrations/recaptcha.js` file.
1. Replace the `siteKey` with Google reCAPTCHA site key value.

    ![Recaptcha apply to all forms](/help/forms/assets/recaptcha-apply-to-all-forms.png)

    >[!NOTE]
    >
    >  You can retrieve the reCAPTCHA keys from the [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) to preview and publish the site. 

The reCAPTCHA badge starts appearing for all the forms on your Site. 
-->

## 関連トピック

{{see-more-forms-eds}}

