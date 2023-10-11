---
title: AEMアダプティブフォームでGoogle reCAPTCHA を使用する方法は？
description: Google reCAPTCHA サービスでフォームのセキュリティを容易に強化できます。 ステップバイステップガイドをご用意しております。
topic-tags: Adaptive Forms, author
keywords: Google reCAPTCHA サービス，アダプティブForms, CAPTCHA の課題，ボットの回避，コアコンポーネント，フォーム送信セキュリティ，フォームスパムの防止
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 19%

---

# コアコンポーネントに基づくAEMアダプティブフォームでのGoogle reCAPTCHA の使用 {#using-reCAPTCHA-in-adaptive-forms}

| 適用先 | 記事リンク |
| -------- | ---------------------------- |
| コアコンポーネントに基づくアダプティブフォーム | この記事 |
| 基盤コンポーネントに基づくアダプティブフォーム | [ここをクリックしてください](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人と自動化されたプログラムまたはボットを区別するためにオンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットがスパムや悪意のある目的の投稿を防ぐことで、オンライントランザクションの安全性を高めます。

[!DNL AEM Forms] as a [!DNL Cloud Service] は、アダプティブFormsでGoogle reCAPTCHA v2 をサポートしています。 これを使用して、フォームの送信時に CAPTCHA の課題を提示できます. アダプティブフォームで reCAPTCHA を使用するには：

1. [Googleによる reCAPTCHA サービスを使用したAEM Forms環境の接続](#connect-your-forms-environment-with-recaptcha-service-by-google)
1. [アダプティブフォームを設定して、フォーム送信時に CAPTCHA の課題を表示する](#using-reCAPTCHA)

## Googleによる reCAPTCHA サービスを使用したAEM Forms環境の接続 {#connect-your-forms-environment-with-recaptcha-service-by-google}

GoogleによるAEM Forms環境を reCAPTCHA サービスに接続するには

1. Google から [reCAPTCHA API キーペア](https://www.google.com/recaptcha/admin)を取得します。これには、**サイトキー**&#x200B;と&#x200B;**秘密鍵**&#x200B;が含まれます。

   ![Googleの Web サイトでGoogle reCAPTCHA 設定を作成して、reCAPTCHA キーを取得する](/help/forms/assets/google-captcha.gif)
1. 設定コンテナをAEM Formsas a Cloud Service環境に作成します。 設定コンテナには、AEMを外部サービスに接続するために使用されるクラウド設定が格納されます。 GoogleでAEM Forms環境を reCAPTCHA サービスに接続するための設定コンテナを作成および設定するには、次の手順を実行します。
   1. AEM Formsas a Cloud Serviceインスタンスを開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。設定ブラウザーでは、次の操作を実行できます。
   1. 既存のフォルダーを選択するか、フォルダーを作成します。 フォルダーを作成して、そのフォルダーの「クラウド設定」オプションを有効にしたり、既存のフォルダーの「クラウド設定を有効にする」オプションを有効にしたりできます。

      * フォルダーを作成し、それに対して「クラウド設定」オプションを有効にするには、次の手順を実行します。
         1. 設定ブラウザーで、 **[!UICONTROL 作成]**.
         1. 設定を作成ダイアログで、名前とタイトルを指定し、 **[!UICONTROL クラウド設定]** オプション。
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * 既存のフォルダーに対して「クラウド設定」オプションを有効にするには：
         1. 設定ブラウザーで、「」フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。

1. Cloud Service を設定する:
   1. AEMオーサーインスタンスで、に移動します。 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** とタップします。 **[!UICONTROL reCAPTCHA]**.
   1. 前の節で作成または更新した設定コンテナを選択します。 「**[!UICONTROL 作成]**」をタップします。
   1. 指定 **[!UICONTROL タイトル]**, **[!UICONTROL 名前]**, **[!UICONTROL サイトキー]**、および **[!UICONTROL 秘密鍵]** reCAPTCHA サービス用（手順 1 で取得）。 「**[!UICONTROL 作成]**」をタップします。

   ![AEM Forms環境をGoogleの reCAPTCHA サービスに接続するためのCloud Serviceの設定](/help/forms/assets/captcha-configuration.gif)

   reCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。 詳しくは、 [アダプティブフォームでのGoogle reCAPTCHA の使用](#using-reCAPTCHA).

## アダプティブフォームでのGoogle reCAPTCHA の使用 {#using-reCAPTCHA}

アダプティブFormsで reCAPTCHA を使用するには：

1. AEM Formsas a Cloud Serviceインスタンスを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブFormsを選択し、 **[!UICONTROL プロパティ]**. の **[!UICONTROL 設定コンテナ]** 」オプションを選択し、AEM FormsをGoogleの reCAPTCHA サービスに接続するクラウド設定を含む設定コンテナを選択してをタップします。 **[!UICONTROL 保存して閉じる]**.

   このような設定コンテナがない場合は、「 [Googleによる reCAPTCHA サービスを使用したAEM Forms環境の接続](#connect-your-forms-environment-with-recaptcha-service-by-google) を参照して、このような設定コンテナを作成する方法を確認してください。

   ![設定コンテナを選択](/help/forms/assets/captcha-properties.png)

1. アダプティブFormsを選択し、 **[!UICONTROL 編集]**. アダプティブフォームがアダプティブFormsエディターで開きます。
1. コンポーネントブラウザーから、 **[!UICONTROL アダプティブフォーム reCAPTCHA]** コンポーネントをアダプティブフォーム上に配置します。

   Google reCAPTCHA 検証は、時間に依存し、約数分で有効期限が切れます。 したがって、Adobeでは、 **[!UICONTROL アダプティブフォーム reCAPTCHA]** 直前のコンポーネント **[!UICONTROL 送信]** 」ボタンをクリックします。

1. を選択します。 **[!UICONTROL アダプティブフォーム reCAPTCHA]** コンポーネントをタップし、プロパティをタップします。 ![プロパティアイコン](assets/configure-icon.svg) アイコン。 プロパティダイアログが開きます。 次の必須プロパティを指定します。
   * **[!UICONTROL 名前]:** フォームコンポーネントは、フォーム内とルールエディター内の両方で一意の名前で簡単に識別できますが、名前にスペースや特殊文字を含めることはできません。
   * **[!UICONTROL CAPTCHA 設定]:** フォームにGoogle reCAPTCHA ダイアログを表示するように設定されたクラウド設定を選択します。 同様の目的で、環境内に複数のクラウド設定を作成することができます。 そのため、サービスは慎重に選択してください。 サービスが表示されない場合は、 [Googleによる reCAPTCHA サービスを使用したAEM Forms環境の接続](#connect-your-forms-environment-with-recaptcha-service-by-google) AEM Forms環境とGoogleの reCAPTCHA サービスを接続するCloud Serviceを作成する方法を説明します。
   * **キャプチャサイズ：** Google reCAPTCHA チャレンジダイアログの表示サイズを選択できます。 以下を使用します。 **[!UICONTROL コンパクト]** 小さいサイズと **[!UICONTROL 標準]** 比較的大きなサイズのGoogle reCAPTCHA チャレンジダイアログを表示するオプション。

1. 「**[!UICONTROL 完了]**」をタップします。

   さて、 **reCAPTCHA で保護** がアダプティブフォームに表示されます。 Google reCAPTCHA サービスを使用するように設定されているすべてのアダプティブFormsに表示されます。

   現在は、フォームの入力者がGoogle reCAPTCHA サービスによって提供される課題を正常にクリアした正規のフォームのみを送信できます。
   ![reCAPTCHA バッジによって保護された Google](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Tap the component, select ![edit rules](assets/edit-rules-icon.svg), and tap **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Tap the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## よくある質問

**Q：アダプティブフォーム内で複数の Captcha コンポーネントを使用できますか。**
**回答：** アダプティブフォーム内での複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込みのマークが付けられたフラグメントやパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック

* [アダプティブフォームの作成](/help/forms/creating-adaptive-form-core-components.md)
* [アダプティブフォームフラグメントを作成する](/help/forms/adaptive-form-fragments-core-components.md)
* [アダプティブフォームをAEM Sitesページまたはエクスペリエンスフラグメントに追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [アダプティブフォームでのGoogle reCAPTCHA の使用](/help/forms/captcha-adaptive-forms-core-components.md)
