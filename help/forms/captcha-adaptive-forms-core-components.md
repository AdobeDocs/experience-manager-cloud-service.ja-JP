---
title: AEM アダプティブフォームで Google reCAPTCHA を使用する方法は？
description: Google reCAPTCHA サービスでフォームのセキュリティを容易に強化できます。ステップバイステップガイドをご用意しております。
topic-tags: Adaptive Forms, author
keywords: Google reCAPTCHA サービス, アダプティブフォーム, CAPTCHA の課題, ボットの回避, コアコンポーネント, フォーム送信セキュリティ, フォームスパムの防止
feature: Adaptive Forms, Core Components
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 100%

---

# コアコンポーネントに基づく AEM アダプティブフォームでの Google reCAPTCHA の使用 {#using-reCAPTCHA-in-adaptive-forms}

| 適用先 | 記事リンク |
| -------- | ---------------------------- |
| コアコンポーネントに基づくアダプティブフォーム | この記事 |
| 基盤コンポーネントに基づくアダプティブフォーム | [ここをクリックしてください](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のある目的を防止することで、オンライントランザクションの安全性を高めます。

AEM Forms as a Cloud Service は、次の CAPTCHA ソリューションをサポートしています。

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [Cloudflare Turnstile](/help/forms/integrate-adaptive-forms-turnstile-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## AEM Forms 環境と Google reCAPTCHA サービスの接続 {#connect-your-forms-environment-with-recaptcha-service-by-google}

フォームの作成者は、Google による reCAPTCHA サービスを使用してアダプティブフォームに CAPTCHA を実装できます。サイトを保護する高度な CAPTCHA 機能を提供します。reCAPTCHA の仕組みについて詳しくは、[Google reCAPTCHA](https://developers.google.com/recaptcha/) を参照してください。[!DNL AEM Forms] as a [!DNL Cloud Service] は、アダプティブフォームで Google reCAPTCHA v2 をサポートします。これを使用して、フォームの送信時に CAPTCHA の課題を提示できます。AEM Forms 環境を Google による reCAPTCHA サービスに接続するには

1. Google から [reCAPTCHA API キーペア](https://www.google.com/recaptcha/admin)を取得します。これには、**サイトキー**&#x200B;と&#x200B;**秘密鍵**&#x200B;が含まれます。

   ![Google の Web サイトで Google reCAPTCHA 設定を作成して、reCAPTCHA キーを取得する](/help/forms/assets/google-captcha.gif)
1. 設定コンテナを AEM Forms as a Cloud Service 環境に作成します。設定コンテナには、AEM を外部サービスに接続するために使用されるクラウド設定が格納されます。Google で AEM Forms 環境を reCAPTCHA サービスに接続するための設定コンテナを作成および設定するには、次の手順を実行します。
   1. AEM Forms as a Cloud Service インスタンスを開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。設定ブラウザーでは、次の操作を実行できます。
   1. 既存のフォルダーを選択するか、フォルダーを作成します。フォルダーを作成して、そのフォルダーの「クラウド設定」オプションを有効にしたり、既存のフォルダーの「クラウド設定を有効にする」オプションを有効にしたりできます。

      * フォルダーを作成し、それに対して「クラウド設定」オプションを有効にするには、次の手順を実行します。
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. 設定作成ダイアログで、名前とタイトルを指定し、「**[!UICONTROL クラウド設定]**」オプションを選択します。
         1. 「**[!UICONTROL 作成]**」をクリックします
      * 既存のフォルダーに対して「クラウド設定」オプションを有効にするには：
         1. 設定ブラウザーで、フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

1. Cloud Service を設定：
   1. AEM オーサーインスタンスで、![tools-1](assets/tools-1.png)／**[!UICONTROL クラウドサービス]**&#x200B;に移動し、「**[!UICONTROL reCAPTCHA]**」を選択します。
   1. 前の節で作成または更新した設定コンテナを選択します。「**[!UICONTROL 作成]**」を選択します。
   1. reCAPTCHA サービス用（手順 1 で取得）に&#x200B;**[!UICONTROL タイトル]**、**[!UICONTROL 名前]**、**[!UICONTROL サイトキー]**&#x200B;および **[!UICONTROL 秘密鍵]**&#x200B;を指定します。「**[!UICONTROL 作成]**」を選択します。

   ![AEM Forms 環境を Google の reCAPTCHA サービスに接続するよう Cloud Service を設定](/help/forms/assets/captcha-configuration.gif)

   reCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。詳しくは、[アダプティブフォームでの Google reCAPTCHA の使用](#using-reCAPTCHA)を参照してください。

## アダプティブフォームで Google reCAPTCHA を使用 {#using-reCAPTCHA}

アダプティブフォームで reCAPTCHA を使用するには：

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、「**[!UICONTROL プロパティ]**」を選択します。「**[!UICONTROL 設定コンテナ]**」オプションで AEM Forms を Google の reCAPTCHA サービスに接続するクラウド設定を含む設定コンテナを選択し、「**[!UICONTROL 保存して閉じる]**」を選択します。

   このような設定コンテナがない場合は、[Googleによる reCAPTCHA サービスを使用した AEM Forms 環境の接続](#connect-your-forms-environment-with-recaptcha-service-by-google)の節を参照して、設定コンテナを作成する方法を確認してください。

   ![設定コンテナの選択](/help/forms/assets/captcha-properties.png)

1. アダプティブフォームを選択し、「**[!UICONTROL 編集]**」を選択します。アダプティブフォームエディターでアダプティブフォームが開きます。
1. コンポーネントブラウザーから **[!UICONTROL アダプティブフォーム reCAPTCHA]** コンポーネントをアダプティブフォームにドラッグ＆ドロップします。

   Google reCAPTCHA 検証は時間的制約があり、数分で期限切れになります。そのため、**[!UICONTROL アダプティブフォーム reCAPTCHA]** コンポーネントを&#x200B;**[!UICONTROL 送信]**&#x200B;ボタンのすぐ前に配置することをお勧めします。

1. **[!UICONTROL アダプティブフォーム reCAPTCHA]** コンポーネントを選択し、プロパティ ![プロパティアイコン](assets/configure-icon.svg) アイコンを選択します。プロパティダイアログが開きます。次の必須プロパティを指定します。
   * **[!UICONTROL 名前]：** フォームコンポーネントは、フォーム内とルールエディター内の両方で一意の名前で簡単に識別できますが、名前にスペースや特殊文字を含めることはできません。
   * **[!UICONTROL Captcha 設定]：** フォームの Google reCAPTCHA ダイアログを表示するように設定されたクラウド設定を選択します。同様の目的で、環境内に複数のクラウド設定を作成することができます。そのため、サービスは慎重に選択してください。サービスが表示されない場合は、[Googleによる reCAPTCHA サービスを使用した AEM Forms 環境の接続](#connect-your-forms-environment-with-recaptcha-service-by-google)で、AEM Forms 環境と Google の reCAPTCHA サービスを接続する Cloud Service を作成する方法を参照してください。
   * **Captcha サイズ：**「Google reCAPTCHA チャレンジ」ダイアログの表示サイズを選択できます。「**[!UICONTROL コンパクト]**」オプションを選択すると小さいサイズ、「**[!UICONTROL 標準]**」オプションを選択すると比較的大きなサイズの Google reCAPTCHA チャレンジダイアログを表示できます。

1. 「**[!UICONTROL 完了]**」を選択します。

   reCAPTCHA **で保護された** がアダプティブフォームに表示されます。Google reCAPTCHA サービスを使用するように設定されているすべてのアダプティブフォームに表示されます。

   現在、フォームの入力者は Google reCAPTCHA サービスによって提供される課題を正常にクリアした正規のフォームのみを送信できます。
   ![reCAPTCHA バッジによって保護された Google](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Select the component, select ![edit rules](assets/edit-rules-icon.svg), and select **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Select the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## よくある質問

**Q：アダプティブフォーム内で複数の Captcha コンポーネントを使用できますか。**
**A：** アダプティブフォームでは、複数の Captcha コンポーネントを使用することはできません。また、遅延読み込みのマークが付けられたフラグメントやパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

{{see-also}}