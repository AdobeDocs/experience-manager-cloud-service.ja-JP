---
title: AEM Forms as a Cloud Service の Edge Delivery Services での reCAPTCHA の使用
description: AEM Forms の Edge Delivery Services 向けフォームでの Google reCAPTCHA の使用
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Architect, Developer
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 100%

---


# AEM Forms as a Cloud Service の Edge Delivery Services での reCAPTCHA の使用

<!--
<span>The **reCAPTCHA** feature is under the pre-release program. To request access to the **reCAPTCHA** feature for Edge Delivery Services for AEM Forms, send an email from your work address to mailto:aem-forms-ea@adobe.com.</span>
-->

reCAPTCHA は、web サイトを不正行為、スパムおよび悪用から守るために使用される一般的なツールです。Edge Delivery では、Google reCAPTCHA を追加して人間とボットを区別する機能がアダプティブフォームブロックから提供されます。この機能により、ユーザーは自分の web サイトをスパムや不正使用から保護できます。
例えば、旅行の開始日と終了日、部屋の予算、旅行費用の見積もり、旅行者情報などのデータを収集する問い合わせフォームを考えてみます。このような場合は、悪意のあるユーザーがフォームを悪用してフィッシングメールを送信したり、スパムボットを使用して無関係または有害なコンテンツを大量に送信したりするリスクがあります。reCAPTCHA を統合すると、送信が本物のユーザーからのものであることを確認して、セキュリティを強化し、スパムエントリを最小限に抑える効果を得ることができます。

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

Edge Delivery Services では、アダプティブフォームブロックに&#x200B;**スコアベース（v3）の reCAPTCHA** のみをサポートしています。

![reCAPTCHA v2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


この記事を最後まで読むと、以下の操作を実行できるようになります。
- [1 つのフォームに対する Google reCAPTCHA の有効化](#enable-google-recaptchas-for-a-single-form)
- [サイト上のすべてのフォームに対して reCAPTCHA を有効にする](#enable-recaptcha-for-all-the-forms)

## 前提条件

- [アダプティブフォームブロックを使用したフォームの作成](/help/edge/docs/forms/create-forms.md)で説明される手順に従って、Edge Delivery Services Forms の開発を開始します。
- ドメインを [Google reCAPTCHA に登録し、資格情報を取得します](https://www.google.com/recaptcha/admin/create)。

## 1 つのフォームに対する Google reCAPTCHA の有効化 {#enable-google-recaptchas-for-a-single-form}

1 つのフォームに対して Google reCAPTCHA を有効にするには、Google の reCAPTCHA サービスを特定の web フォームに統合して、自動化された不正使用やスパム送信を防ぐ必要があります。

1 つのフォームに対して Google reCAPTCHA を有効にするには：

1. [プロジェクト設定ファイルの reCAPTCHA 秘密鍵の設定](#configure-secret-key)
1. [reCAPTCHA サイトキーのフォームへの追加](#add-site-key)

Edge Delivery Services Forms で reCAPTCHA の設定を開始するには、フォームの定義を含む次の[スプレッドシート](/help/edge/docs/forms/assets/recaptcha.xlsx)を参照してください。

### プロジェクト設定ファイルの reCAPTCHA 秘密鍵の設定 {#configure-secret-key}

Google reCAPTCHA に登録されているドメインのサイトシークレットが、Microsoft SharePoint または Google Drive の AEM プロジェクトフォルダーで設定ファイル（`.helix/config`）に追加されます。サイトシークレットを設定ファイルに追加するには：

1. Microsoft® SharePoint または Google Drive 上の AEM プロジェクトフォルダーに移動します。
1. Microsoft SharePoint サイトの AEM プロジェクトフォルダーに `.helix/config.xlsx` ファイル、または Google ドライブ内の AEM プロジェクトフォルダーに `.helix/config` ファイルを作成します。

   >[!NOTE]
   >
   > [プロジェクト設定ファイル](https://www.aem.live/docs/configuration)は、`/.helix/config` にあるスプレッドシートです。ファイルが存在しない場合は作成します。

1. `config` ファイルを開き、次のキーと値のペアを追加します。

   - **captcha.secret**：Google reCAPTCHA 秘密鍵の値
   - **captcha.type**：reCAPTCHA v2

   >[!NOTE]
   >
   >  - reCAPTCHA キーは、[Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin) から取得できます。
   >  - `config` ファイルで **captcha.type** の値を **reCAPTCHA v2** として指定する必要があります。

   以下のプロジェクト設定ファイルのスクリーンショットを参照してください。

   ![プロジェクト設定ファイル](/help/forms/assets/recaptcha-config-file.png)

1. `config` ファイルを保存します。

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用して `config` ファイルをプレビューし公開します。

### reCAPTCHA サイトキーのフォームへの追加 {#add-site-key}

Google reCAPTCHA に登録されているドメインのサイトキーが、保護するフォームのスプレッドシートに追加されます。サイトキーをフォームに追加するには：

1. Microsoft® SharePoint または Google ドライブ上の AEM プロジェクトフォルダーに移動し、スプレッドシートを開きます。 また、フォーム用の新しいスプレッドシートを作成することもできます。
1. スプレッドシートに行を挿入して、次の詳細を含む、新しいフィールドを CAPTCHA として追加します。
   - **タイプ**：captcha
   - **値**：Google reCAPTCHA サイトキーの値

   以下のスクリーンショットを参照してください。新しい行タイプが CAPTCHA であるスプレッドシートが示されています。

   ![reCAPTCHA スプレッドシート](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  reCAPTCHA キーは、[Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin) から取得できます。

1. スプレッドシートを保存します。
1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用してシートをプレビューし、公開します。

フォーム定義に新しい行を追加すると、フォームの右下隅に reCAPTCHA バッジが表示されます。これにより、フォームが不正行為、スパムおよび悪用から保護されるようになります。

![recaptcha フォーム](/help/edge/docs/forms/assets/recaptcha-form.png)

## サイト上のすべてのフォームに対して reCAPTCHA を有効にする{#enable-recaptcha-for-all-the-forms}

アダプティブフォームブロックを使用するサイト上のすべてのフォームに Google reCAPTCHA を適用するには、前の手順をスキップし、`sitekey` 値を `recaptcha.js` ファイルに直接埋め込みます。`recaptcha.js` ファイルにサイトキー値を含めるには：

1. [recaptcha.js ファイルの Google reCAPTCHA サイトキーを更新](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [ファイルをデプロイしてプロジェクトをビルド](#2-deploy-the-file-and-build-the-project)
1. [AEM Sidekick を使用してサイトをプレビュー](#3-preview-the-site-using-the-aem-sidekick)

### recaptcha.js ファイルの Google reCAPTCHA サイトキーを更新

1. ローカルマシン上で、対応する GitHub リポジトリを開きます。
1. `[../Form Block/integrations]` フォルダーに移動し、`recaptcha.js` ファイルを開きます。
1. `siteKey` を Google reCAPTCHA サイトキー値に置き換えます。

   ![reCAPTCHA をすべてのフォームに適用](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  reCAPTCHA キーは、[Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin) から取得できます。

1. `recaptcha.js` ファイルを保存します。

### ファイルをデプロイしてプロジェクトをビルド

更新された `recaptcha.js` ファイルを GitHub プロジェクトにデプロイし、ビルドが成功したことを確認します。

### AEM Sidekick を使用してサイトをプレビュー

[AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用してサイトをプレビューし、公開します。

reCAPTCHA バッジが、サイト上のすべてのフォームに表示され始めます。

