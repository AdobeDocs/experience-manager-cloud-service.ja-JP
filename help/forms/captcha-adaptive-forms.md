---
title: アダプティブフォームでの CAPTCHA の使用
seo-title: Using CAPTCHA in Adaptive Forms
description: アダプティブフォームで AEM CAPTCHA または Google reCAPTCHA サービスを設定する方法を説明します。
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in Adaptive Forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: 580ab2731bc277bcd53c4863b3b22f5e44dc8406
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 94%

---

# アダプティブフォームでの CAPTCHA の使用 {#using-captcha-in-adaptive-forms}

CAPTCHA（Completely Automated Public Turing test to tell Computers and Humans Apart）は、オンライントランザクションにおいて人間と自動プログラムやボットとを区別するために一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。これにより、テストに失敗した場合ユーザーは続行できないため、ボットによるスパムの投稿や悪意のある目的を防止し、オンライントランザクションを安全に保ちます。

[!DNL AEM Forms] は、アダプティブフォームでの CAPTCHA をサポートします。Google が提供する reCAPTCHA サービスを使用して、CAPTCHA を実装できます。

>[!NOTE]
>
>* [!DNL AEM Forms] は reCaptcha v2 のみをサポートします。その他のバージョンはサポートされません。
>* アダプティブフォームの CAPTCHA は、[!DNL AEM Forms] アプリのオフラインモードではサポートされていません。
>


## Google が提供する reCAPTCHA サービスの設定 {#google-recaptcha}

フォームの作成者は、Google による reCAPTCHA サービスを使用してアダプティブフォームに CAPTCHA を実装できます。これにより、サイトを保護する高度な CAPTCHA 機能が提供されます。reCAPTCHA の仕組みについて詳しくは、「[Google reCAPTCHA](https://developers.google.com/recaptcha/)」を参照してください。

![reCAPTCHA](assets/recaptcha_new.png)

[!DNL AEM Forms]で reCAPTCHA サービスを実装するには、以下の手順を実行します。

1. Google から [reCAPTCHA API キーペア](https://www.google.com/recaptcha/admin)を取得します。これにはサイトキーと秘密鍵が含まれます。
1. クラウドサービス用の設定コンテナを作成します。

   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
      * 詳しくは、 [設定ブラウザー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=ja#introduction) のドキュメントを参照してください。
   1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

      1. 設定ブラウザーで、**[!UICONTROL global]** フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。

      1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
      1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。
   1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
   1. 設定を作成ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
   1. 「**[!UICONTROL 作成]**」をタップします。これで、クラウドサービス設定が有効になったフォルダーが作成されました。


1. reCAPTCHA のクラウドサービスを設定します。

   1. Experience Managerオーサーインスタンスで、に移動します。 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. 「**[!UICONTROL reCAPTCHA]**」をタップします。設定ページが表示されます。上記の手順で作成した設定コンテナを選択し、「**[!UICONTROL 作成]**」をタップします。
   1. reCAPTCHA サービスの名前、サイトキー、秘密鍵を指定し、「**[!UICONTROL 作成]**」をタップして、クラウドサービスの設定を作成します。
   1. コンポーネントを編集ダイアログで、サイトおよび手順 1 で取得した秘密鍵を指定します。「**[!UICONTROL 設定を保存]**」をタップしてから、「**[!UICONTROL OK]**」をタップして設定を完了します。

   reCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。詳しくは、「[アダプティブフォームでの CAPTCHA の使用](#using-captcha)」を参照してください。

## アダプティブフォームでの CAPTCHA の使用 {#using-captcha}

アダプティブフォームで CAPTCHA を使用するには、以下を実行します。

1. アダプティブフォームを編集モードで開きます。

   >[!NOTE]
   >
   >アダプティブフォームの作成時に選択した設定コンテナに、reCAPTCHA クラウドサービスが含まれていることを確認してください。アダプティブフォームのプロパティを編集して、そのアダプティブフォームに関連付けられている設定コンテナを変更することもできます。

1. コンポーネントブラウザーから **[!UICONTROL Captcha]** コンポーネントを、アダプティブフォームにドラッグ＆ドロップします。

   >[!NOTE]
   >
   >アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。また、遅延読み込みとしてマークされているパネルやフラグメント内のパネルで CAPTCHA を使用することはお勧めしません。

   >[!NOTE]
   >
   >Captcha は、約 1 分間で期限切れになります。そのため、アダプティブフォームに「送信」ボタンを配置する直前に Captcha コンポーネントを配置することをお勧めします。

1. 追加した Captcha コンポーネントを選択して、![cmppr](assets/configure-icon.svg) をタップし、プロパティを編集します。
1. CAPTCHA ウィジェットのタイトルを指定します。デフォルト値は **[!UICONTROL Captcha]** です。タイトルを表示しない場合は、「**[!UICONTROL タイトルを非表示にする]**」を選択します。
1. **[!UICONTROL Captcha サービス]**&#x200B;ドロップダウンで「**[!UICONTROL reCaptcha]**」を選択して、reCAPTCHA サービスを有効にします（「[Google による reCAPTCHA サービス](#google-recaptcha)」に記載されている手順に従って reCAPTCHA サービスが設定されている場合）。設定ドロップダウンから設定を選択します。
1. タイプをとして選択します。 **[!UICONTROL 標準]** または **[!UICONTROL コンパクト]** reCAPTCHA ウィジェット用。 また、 **[!UICONTROL 非表示]** オプションを使用して、疑わしいアクティビティの場合にのみ CAPTCHA チャレンジを表示できます。 以下に示す reCAPTCHA バッジによって保護されたが、保護されたフォームに表示されます。

   ![reCAPTCHA バッジによって処理されたGoogle](assets/google-recaptcha-v2.png)

   >[!NOTE]
   >
   >選択しない **[!UICONTROL デフォルト]** を「 Captcha サービス」ドロップダウンから選択します。これは、デフォルトのExperience ManagerCAPTCHA サービスが非推奨（廃止予定）になったためです。

1. 各プロパティを保存します。

アダプティブフォーム上で reCAPTCHA サービスが有効になります。フォームをプレビューして、CAPTCHA が機能していることを確認できます。

### ルールに基づいた CAPTCHA コンポーネントの表示／非表示 {#show-hide-captcha}

アダプティブフォームのコンポーネントに適用するルールに基づいて、CAPTCHA コンポーネントの表示／非表示を切り替えることができます。コンポーネントをタップして、「![ルールを編集](assets/edit-rules-icon.svg)」を選択し、「**[!UICONTROL 作成]**」をタップしてルールを作成します。ルールの作成について詳しくは、「[ルールエディター](rule-editor.md)」を参照してください。

例えば、CAPTCHA コンポーネントは、フォームの「通貨の値」フィールドの値が 25000 を超える場合にのみ、アダプティブフォームに表示する必要があります。

フォームの「**[!UICONTROL 通貨の値]**」フィールドをタップして、以下のルールを作成します。

![ルールの表示／非表示](assets/rules-show-hide-captcha.png)

### CAPTCHA の検証 {#validate-captcha}

アダプティブフォーム内の CAPTCHA は、フォームを送信するとき、またはユーザーの操作や条件に基づいて CAPTCHA 検証を行うときに検証できます。

#### フォーム送信時の CAPTCHA の検証 {#validation-form-submission}

アダプティブフォームの送信時に CAPTCHA を自動的に検証するには、以下の手順を実行します。

1. CAPTCHA コンポーネントをタップし、![cmppr](assets/configure-icon.svg) を選択して、コンポーネントのプロパティを表示します。
1. 「**[!UICONTROL CAPTCHA を検証]**」セクションで、「**[!UICONTROL フォーム送信時に CAPTCHA を検証]**」を選択します。
1. 「![完了](assets/save_icon.svg)」をタップして、コンポーネントプロパティを保存します。

#### ユーザーの操作と条件に対する CAPTCHA の検証 {#validate-captcha-user-action}

条件とユーザー操作に基づいて CAPTCHA を検証するには、以下の手順を実行します。

1. CAPTCHA コンポーネントをタップし、![cmppr](assets/configure-icon.svg) を選択して、コンポーネントのプロパティを表示します。
1. 「**[!UICONTROL CAPTCHA を検証]**」セクションの、「**[!UICONTROL ユーザーアクションで CAPTCHA を検証する]**」を選択します。
1. 「![完了](assets/save_icon.svg)」をタップして、コンポーネントプロパティを保存します。

[!DNL Experience Manager Forms] は、事前定義済みの条件を使用して CAPTCHA を検証する `ValidateCAPTCHA` API を提供します。この API は、カスタム送信アクションを使用するか、アダプティブフォームのコンポーネントにルールを定義することで呼び出すことができます。

以下の例は、事前定義された条件を使用して CAPTCHA を検証する `ValidateCAPTCHA` API の例です。

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
     GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

この例は、フォームの入力時にユーザーが指定した数値ボックスの桁数が 5 より大きい場合にのみ、`ValidateCAPTCHA` API がフォームの CAPTCHA を検証することを示しています。

**オプション 1：[!DNL Experience Manager Forms] ValidateCAPTCHA API を使用して、カスタム送信アクションを使用して CAPTCHA を検証する**

`ValidateCAPTCHA` API を使用してカスタム送信アクションを使用して CAPTCHA を検証するには、以下の手順を実行します。

1. `ValidateCAPTCHA` API を含むスクリプトをカスタム送信アクションに追加します。カスタム送信アクションについて詳しくは、「[アダプティブフォーム用のカスタム送信アクションの作成](custom-submit-action-form.md)」を参照してください。
1. アダプティブフォームの **[!UICONTROL 送信]** プロパティの **[!UICONTROL 送信アクション]** ドロップダウンリストから、カスタム送信アクションの名前を選択します。
1. 「**[!UICONTROL 送信]**」をタップします。CAPTCHA は、カスタム送信アクションの `ValidateCAPTCHA` API で定義された条件に基づいて検証されます。

**オプション 2：フォームを送信する前に、[!DNL Experience Manager Forms] ValidateCAPTCHA API を使用してユーザーアクションに対する CAPTCHA の検証を行う**

また、アダプティブフォーム内のコンポーネントにルールを適用することで、`ValidateCAPTCHA` API を呼び出すこともできます。

例えば、アダプティブフォームに「**[!UICONTROL CAPTCHA を検証]**」ボタンを追加し、ボタンをクリックするとサービスを呼び出すルールを作成します。

以下の図は、「**[!UICONTROL CAPTCHA を検証]**」ボタンをクリックしてサービスを呼び出す方法を示しています。

![CAPTCHA の検証](assets/captcha-validation1.gif)

`ValidateCAPTCHA` API を含むカスタムサーブレットをルールエディターを使用して呼び出し、検証結果に基づいてアダプティブフォームの送信ボタンを有効または無効にできます。

同様に、ルールエディターを使用して、アダプティブフォーム内の CAPTCHA を検証するカスタムメソッドを含めることができます。

### カスタム CAPTCHA サービスの追加 {#add-custom-captcha-service}

[!DNL Experience Manager Forms] は、CAPTCHA サービスとして reCAPTCHA を提供します。**[!UICONTROL CAPTCHA サービス]**&#x200B;ドロップダウンリストに表示するカスタムサービスを追加できます。

以下は、アダプティブフォームに CAPTCHA サービスを追加するためのインターフェイスの実装例です。

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` は、Sling リポジトリー内の CAPTCHA コンポーネントのリソースパスを参照します。CAPTCHA コンポーネントに特有の詳細を含めるには、このプロパティを使用します。例えば、`captchaPropertyNodePath` には、CAPTCHA コンポーネントで設定された reCAPTCHA クラウド設定に関する情報が含まれます。クラウド設定情報は、reCAPTCHA サービスを実装するための&#x200B;**[!UICONTROL サイトキー]**&#x200B;と&#x200B;**[!UICONTROL 秘密鍵]**&#x200B;の設定を提供します。

`userResponseToken` は、フォームで CAPTCHA を解決した後に生成される `g_recaptcha_response` を指します。

### reCAPTCHA サービスドメインの編集 {#recaptcha-service-domain}

reCAPTCHA サービスは、`https://www.recaptcha.net/` をデフォルトドメインとして使用します。設定を変更して `https://www.google.com/` を設定したり、reCAPTCHA サービスの読み込み、レンダリング、検証を行うカスタムドメイン名を設定したりできます。

**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネル設定]**&#x200B;の **[!UICONTROL af.cloudservices.recaptcha.domain]** プロパティを設定して、`https://www.google.com/` または他のカスタムドメイン名を指定します。以下の JSON ファイルにサンプルが表示されています。

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

設定の値をセットするには、[AEM SDK を使用して OSGi 設定を生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=ja#generating-osgi-configurations-using-the-aem-sdk-quickstart)し、Cloud Service インスタンスに[設定をデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja#deployment-process)します。
