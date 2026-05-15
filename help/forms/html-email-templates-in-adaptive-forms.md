---
title: Forms as a Cloud Service上のアダプティブFormsのHTML電子メールテンプレート
description: アダプティブフォームでメールテンプレートを使用する方法を説明します。
feature: Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 640130c0-e5d2-4af1-8ed9-c3bdde31d958
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 13%

---

# アダプティブフォームのメールテンプレート

アダプティブ Formsでは、HTMLとプレーンテキストのメールテンプレートを使用できます。 HTML メールテンプレートを使用すると、フォームの送信時に、リッチでパーソナライズされた、魅力的な外観のメールを送信できます。 これらのメールは、フォームデータでカスタマイズしたり、画像やリンクなどの様々なメールタグを使用して強化したりできます。 アダプティブフォームでは、HTML テンプレートを含むファイルをアップロードするか、プレーンテキストエディターを使用してこれらのテンプレートを作成できます。

![HTML メールテンプレート](/help/forms/assets/html-email.png)

この記事では、Adaptive Formsでメールテンプレートを設定および使用する方法を説明します。 最終的には、次のことが可能になります。

* [アダプティブフォーム用のHTML テンプレートの設定](#configure-an-html-template-for-an-adaptive-form)
* [アダプティブフォームのプレーンテキストメールテンプレートの設定](#configure-a-plain-text-template-for-an-adaptive-form)
* [メールテンプレートでのフォームデータの使用](#use-form-data-in-your-email-templates)


手順の概要を以下に示します。

1. アダプティブフォームを編集用に開きます。
1. [ メール送信](/help/forms/configure-submit-action-send-email.md)送信アクションを設定します。
1. HTML テンプレートを選択またはアップロードするか、電子メールテンプレートを手動で入力します。
1. メール設定をテストします。

## アダプティブフォーム用のHTML テンプレートの設定

アダプティブフォームを設定して、[**電子メールを送信**&#x200B;送信アクション ](/help/forms/configure-submit-action-send-email.md)を使用して、送信時に電子メールを送信できます。 このアクションには、HTML テンプレートを設定するための2つの方法があります。

### オプション 1: HTML テンプレートを含むファイルを選択する

先に進む前に、HTML テンプレートをAEM Forms環境にアップロードしていることを確認してください。

1. アダプティブフォームを編集用に開きます。
1. **コンテンツブラウザー**&#x200B;に移動し、**ガイドコンテナ**&#x200B;を選択して、プロパティアイコンをタップします。 タイトル `Adaptive Form Container`のダイアログボックスが表示されます。
1. **送信** タブに移動し、**メールを送信**&#x200B;送信アクションを選択します。

   ![ メール送信アクション ](/help/forms/assets/send-email-action.png)

1. **外部テンプレートを使用** オプションを有効にします。
1. 「**HTML テンプレートを使用**」オプションを有効にします。
1. 「外部テンプレートパス」オプションのフォルダーアイコンをクリックし、参照してHTML テンプレートを選択します。
1. **完了**&#x200B;をクリックして、設定を保存します。

これで、HTML テンプレートがアダプティブフォーム用に設定されました。

### 方法2:HTML テンプレートを手動で入力またはペーストする

1. アダプティブフォームを編集用に開きます。
1. **コンテンツブラウザー**&#x200B;に移動し、**ガイドコンテナ**&#x200B;を選択して、プロパティアイコンをタップします。 タイトル `Adaptive Form Container`のダイアログボックスが表示されます。
1. **送信** タブに移動し、**メールを送信**&#x200B;送信アクションを選択します。
1. 「**HTML テンプレートを使用**」オプションを有効にします。
1. HTML コードを入力するか、指定された&#x200B;**電子メールテンプレート** ボックスに直接貼り付けます。


## アダプティブフォームのプレーンテキストテンプレートの設定

アダプティブフォームを設定して、[**電子メールを送信**&#x200B;送信アクション ](/help/forms/configure-submit-action-send-email.md)を使用して、送信時に電子メールを送信できます。 このアクションには、プレーンテキストテンプレートを設定するための2つの方法があります。

### オプション 1: テンプレートを含むファイルを選択する

先に進む前に、HTML テンプレートをAEM Forms環境にアップロードしていることを確認してください。

1. アダプティブフォームを編集用に開きます。
1. **コンテンツブラウザー**&#x200B;に移動し、**ガイドコンテナ**&#x200B;を選択して、プロパティアイコンをタップします。 タイトル `Adaptive Form Container`のダイアログボックスが表示されます。
1. **送信** タブに移動し、**メールを送信**&#x200B;送信アクションを選択します。
1. **外部テンプレートを使用** オプションを有効にします。
1. **外部テンプレートパス** オプションのフォルダーアイコンをクリックし、参照してプレーンテキストテンプレートを選択します。
1. 「完了」をクリックして、設定を保存します。

これで、テンプレートがアダプティブフォーム用に設定されました。

### 方法2:HTML テンプレートを手動で入力またはペーストする

1. アダプティブフォームを編集用に開きます。
1. **コンテンツブラウザー**&#x200B;に移動し、**ガイドコンテナ**&#x200B;を選択して、プロパティアイコンをタップします。 タイトル `Adaptive Form Container`のダイアログボックスが表示されます。
1. **送信** タブに移動し、**メールを送信**&#x200B;送信アクションを選択します。
1. プレーンテキストテンプレートコードを入力するか、指定された&#x200B;**メールテンプレート** ボックスに直接貼り付けます。

## メールテンプレートでのフォームデータの使用

プレースホルダーを使用して、メールテンプレートにフォームデータを含めることができます。 これらのプレースホルダーは、電子メールの送信時に、実際のフォームフィールド値に動的に置き換えられます。 例：

* ${name}: 「name」という名前のフィールドの値。
* ${email}: 「email」という名前のフィールドの値。
* ${message}: 「message」という名前のフィールドの値。

### HTML電子メールテンプレートのサンプル

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

### プレーンテキストメールテンプレートの例

プレーンテキストのメールテンプレートの例を次に示します。

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

## HTML電子メールテンプレートのベストプラクティス

* メールクライアントとの互換性を高めるために、スタイルがインラインであることを確認します。
* モバイルデバイスでの体験を向上させるために、テンプレートをレスポンシブにする。
* LitmusやEmail on Acidなどのツールを使用して、さまざまなメールクライアントでメールをプレビューします。
* プレースホルダー名がフォームフィールド名と正確に一致していることを確認します。
* HTML テンプレート内のタグが見つからないか、正しくないかを確認します。
* [ メールを送信](/help/forms/configure-submit-action-send-email.md)送信アクションが正しく設定されていることを確認します。
