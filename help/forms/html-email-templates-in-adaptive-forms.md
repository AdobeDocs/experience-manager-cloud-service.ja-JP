---
title: Forms as a Cloud Service上のアダプティブFormsのHTML メールテンプレート
description: アダプティブフォームでのメールテンプレートの使用方法を説明します。
feature: Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 640130c0-e5d2-4af1-8ed9-c3bdde31d958
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 13%

---

# アダプティブフォームのメールテンプレート

アダプティブFormsでは、HTMLとプレーンテキストのメールテンプレートを使用できます。 HTML メールテンプレートを使用すると、フォームの送信時に、リッチでパーソナライズされた、魅力的な外観のメールを送信できます。これらのメールは、フォームデータでカスタマイズしたり、画像やリンクなどの様々なメールタグを使用して強化したりできます。アダプティブフォームでは、HTML テンプレートを含むファイルをアップロードするか、プレーンテキストエディターを使用してこれらのテンプレートを作成できます。

![HTML メールテンプレート](/help/forms/assets/html-email.png)

この記事では、アダプティブFormsでメールテンプレートを設定して使用する方法を説明します。 最終的には、次のことが可能になります。

* [アダプティブフォームのHTML テンプレートの設定](#configure-an-html-template-for-an-adaptive-form)
* [アダプティブフォームのプレーンテキストのメールテンプレートを設定する](#configure-a-plain-text-template-for-an-adaptive-form)
* [メールテンプレートでのフォームデータの使用](#use-form-data-in-your-email-templates)


関連する手順の概要を次に示します。

1. アダプティブフォームを編集用に開きます。
1. [ メールを送信 ](/help/forms/configure-submit-action-send-email.md) 送信アクションを設定します。
1. HTML テンプレートを選択またはアップロードするか、メールテンプレートを手動で入力します。
1. メール設定をテストします。

## アダプティブフォームのHTML テンプレートの設定

[**メールを送信** 送信アクション ](/help/forms/configure-submit-action-send-email.md) を使用して、送信時にメールを送信するアダプティブフォームを設定できます。 このアクションにより、HTML テンプレートを設定する 2 つの方法が提供されます。

### オプション 1:HTMLテンプレートを含むファイルを選択する

先に進む前に、HTML テンプレートがAEM Forms環境にアップロードされていることを確認します。

1. アダプティブフォームを編集用に開きます。
1. **コンテンツブラウザー** に移動し、**ガイドコンテナ** を選択して、プロパティアイコンをタップします。 タイトルが「`Adaptive Form Container`」のダイアログボックスが表示されます。
1. 「**送信**」タブに移動し、「**メールを送信**」送信アクションを選択します。

   ![ メール送信アクション ](/help/forms/assets/send-email-action.png)

1. 「**外部テンプレートを使用** オプションを有効にします。
1. 「**HTML テンプレートを使用** オプションを有効にします。
1. 「外部テンプレートパス」オプションのフォルダーアイコンをクリックし、HTML テンプレートを参照して選択します。
1. 「**完了**」をクリックして、設定を保存します。

これで、HTML テンプレートがアダプティブフォーム用に設定されました。

### 方法 2:HTML テンプレートを手動で入力または貼り付ける

1. アダプティブフォームを編集用に開きます。
1. **コンテンツブラウザー** に移動し、**ガイドコンテナ** を選択して、プロパティアイコンをタップします。 タイトルが「`Adaptive Form Container`」のダイアログボックスが表示されます。
1. 「**送信**」タブに移動し、「**メールを送信**」送信アクションを選択します。
1. 「**HTML テンプレートを使用** オプションを有効にします。
1. 提供された **メールテンプレート** ボックスにHTML コードを直接入力または貼り付けます。


## アダプティブフォームのプレーンテキストテンプレートの設定

[**メールを送信** 送信アクション ](/help/forms/configure-submit-action-send-email.md) を使用して、送信時にメールを送信するアダプティブフォームを設定できます。 このアクションには、プレーンテキストテンプレートを設定する 2 つの方法が用意されています。

### オプション 1：テンプレートを含むファイルを選択する

先に進む前に、HTML テンプレートがAEM Forms環境にアップロードされていることを確認します。

1. アダプティブフォームを編集用に開きます。
1. **コンテンツブラウザー** に移動し、**ガイドコンテナ** を選択して、プロパティアイコンをタップします。 タイトルが「`Adaptive Form Container`」のダイアログボックスが表示されます。
1. 「**送信**」タブに移動し、「**メールを送信**」送信アクションを選択します。
1. 「**外部テンプレートを使用** オプションを有効にします。
1. 「**外部テンプレートパス**」オプションのフォルダーアイコンをクリックし、プレーンテキストテンプレートを参照して選択します。
1. 「完了」をクリックして、設定を保存します。

これで、テンプレートがアダプティブフォーム用に設定されました。

### 方法 2:HTML テンプレートを手動で入力または貼り付ける

1. アダプティブフォームを編集用に開きます。
1. **コンテンツブラウザー** に移動し、**ガイドコンテナ** を選択して、プロパティアイコンをタップします。 タイトルが「`Adaptive Form Container`」のダイアログボックスが表示されます。
1. 「**送信**」タブに移動し、「**メールを送信**」送信アクションを選択します。
1. 入力した **メールテンプレート** ボックスにプレーンテキストテンプレートのコードを直接入力または貼り付けます。

## メールテンプレートでのフォームデータの使用

プレースホルダーを使用することで、メールテンプレートにフォームデータを含めることができます。 これらのプレースホルダーは、メールの送信時に、実際のフォームフィールド値に動的に置き換えられます。 例：

* ${name}: 「name」という名前のフィールドの値。
* ${email}: 「email」という名前のフィールドの値。
* ${message}: 「message」という名前のフィールドの値。

### HTML メールテンプレートのサンプル

フォームデータプレースホルダーを使用するHTML メールテンプレートの例を次に示します。

```HTML
    <!DOCTYPE html>
    <html>
    <head>
        <title>Form Submission</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                line-height: 1.6;
                color: #333;
            }
            h2 {
                color: #0056b3;
            }
        </style>
    </head>
    <body>
        <h2>Thank You for Your Submission</h2>
        <p>Dear ${name},</p>
        <p>We have received your submission with the following details:</p>
        <ul>
            <li><strong>Email:</strong> ${email}</li>
            <li><strong>Phone Number:</strong> ${phone_number}</li>
            <li><strong>Message:</strong> ${message}</li>
        </ul>
        <p>We will get back to you soon!</p>
        <p>Best regards,</p>
        <p>Your Team</p>
    </body>
    </html>
```

### プレーンテキストのメールテンプレートのサンプル

次に、プレーンテキストのメールテンプレートの例を示します。

```TXT
    
    Subject: Thank You for Your Submission
    
    Dear ${name},
    
    We have received your submission with the following details:
    
    - Email: ${email}
    - Phone Number: ${phone_number}
    - Message: ${message}
    
    We will get back to you soon!
    
    Best regards,
    Your Team
```

## HTMLのメールテンプレートのベストプラクティス

* メールクライアントとの互換性を高めるために、スタイルがインラインであることを確認します。
* テンプレートをレスポンシブにして、モバイルデバイスでのエクスペリエンスを向上させます。
* Litmus や Acid でのメールなどのツールを使用して、様々なメールクライアントでメールをプレビューします。
* プレースホルダーの名前がフォームフィールドの名前と完全に一致するようにします。
* HTML テンプレートにタグがないか、またはタグが正しくないかを確認します。
* [ メールを送信 ](/help/forms/configure-submit-action-send-email.md) 送信アクションが正しく設定されていることを確認します。
