---
title: AEM アダプティブフォームのコアコンポーネントでの hCaptcha&reg；の使用方法
description: hCaptcha® サービスでフォームのセキュリティを容易に強化できます。ステップバイステップガイドをご用意しております。
topic-tags: Adaptive Forms, author
keywords: hCaptcha&reg; service, Adaptive Forms, CAPTCHA challenge, Bot prevention, Core Components, Form submission security, Form spam prevention
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
exl-id: 6c559df2-7b6a-42fe-b44c-29a782570a0c
role: User, Developer
source-git-commit: bba5e5d283da616baa57b788181af73d59d86ee3
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 41%

---

# Connect your AEM Forms environment with hCaptcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview">早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式メール ID から aem-forms-ea@adobe.com にメールを送信してください。</span>

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のある目的を防止することで、オンライントランザクションの安全性を高めます。

AEM Forms as a Cloud Service は、次の CAPTCHA ソリューションをサポートしています。

* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

## AEM Forms環境と hCaptcha Captcha の統合

hCaptcha® サービスは、ボット、スパム、自動化された不正使用からフォームを保護します。チェックボックスウィジェットテストを行ってユーザーの反応を評価し、フォームを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のあるアクティビティを防止することで、オンライントランザクションの安全性を高めます。

AEM Forms as a Cloud Service supports hCaptcha® in Adaptive Forms Core Components. You can use it to present a checkbox widget challenge on form submission.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### Prerequisites to integrate AEM Forms environment with hCaptcha® {#prerequisite}

[](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key)

### Configure hCaptcha® {#steps-to-configure-hcaptcha}

To integrate AEM Forms with hCaptcha® service, perform the following steps:

1. AEM Formsas a Cloud Service環境で設定コンテナを作成します。 設定コンテナには、AEM を外部サービスに接続するために使用されるクラウド設定が格納されます。AEM Forms環境を hCaptcha® に接続するための設定コンテナを作成して設定するには：
   1. AEM Forms as a Cloud Service インスタンスを開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. In the Configuration Browser, you can select an existing folder or create a folder. フォルダーを作成して、そのフォルダーの「クラウド設定」オプションを有効にしたり、既存のフォルダーの「クラウド設定を有効にする」オプションを有効にしたりできます。

      * フォルダーを作成し、それに対して「クラウド設定」オプションを有効にするには、次の手順を実行します。
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. ****
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * 既存のフォルダーに対して「クラウド設定」オプションを有効にするには：
         1. 設定ブラウザーで、フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

1. Cloud Service を設定：
   1. ![](assets/tools-1.png)********
      ![](assets/hcaptcha-in-ui.png)
   1. Select a Configuration Container, created or updated, as described in the previous section. 「**[!UICONTROL 作成]**」を選択します。
      ![](assets/config-hcaptcha.png)
   1. ****************[](#prerequisite)「**[!UICONTROL 作成]**」を選択します。

      ![AEM FormsCloud Serviceを hCaptcha と接続するための環境の設定®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > [ クライアントサイドのJavaScript検証 URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) および [ サーバーサイドの検証 URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side) は、hCaptcha® 検証用に既に入力されているので、変更する必要はありません。

   hCAPTCHA サービスを設定すると、[ コアコンポーネントに基づくアダプティブフォーム ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/introduction) で使用できるようになります。

## アダプティブなForms コアコンポーネントコン {#using-hCaptcha®-core-components} ールでの hCaptcha® の使用

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、**[!UICONTROL プロパティ]** を選択します。 **[!UICONTROL Configuration Container]** オプションについては、AEM Formsと hCaptcha を接続するクラウド設定が含まれている Configuration Container を選択して®**[!UICONTROL 保存して閉じる]** を選択します。

   そのような Configuration Container がない場合に Configuration Container を作成する方法については、[AEM Forms環境と hCaptcha® の接続 ](#connect-your-forms-environment-with-hcaptcha-service) の節を参照してください。

   ![設定コンテナの選択](/help/forms/assets/captcha-properties.png)

1. アダプティブフォームを選択し、「**[!UICONTROL 編集]**」を選択します。 アダプティブフォームエディターでアダプティブフォームが開きます。
1. ****
1. ****![](assets/configure-icon.svg)プロパティダイアログが開きます。Specify the following properties:

   ![](assets/config-hcaptcha-v2.png)

   * ****
   * ****
   * **[!UICONTROL 設定]：** hCaptcha® 用に設定されたクラウド設定を選択します。
   * **Captcha サイズ：** hCaptcha® チャレンジダイアログの表示サイズを選択できます。 「**[!UICONTROL コンパクト]**」オプションを選択すると小さいサイズ、「**[!UICONTROL 標準]**」オプションを選択すると比較的大きなサイズの hCaptcha® テストダイアログを表示できます。<!-- or **[!UICONTROL Invisible]** to validate hCaptcha&reg; without explicitly rendering the checkbox widget on the user interface. -->
   * **[!UICONTROL 検証メッセージ ]:** フォーム送信時の Captcha 検証の検証メッセージを指定します。
   * **[!UICONTROL スクリプト検証メッセージ]** - スクリプトの検証が失敗した場合に表示するメッセージを入力できます。
     >[!NOTE]
     >You can have multiple Cloud Configurations in your environment for a similar purpose. そのため、サービスは慎重に選択してください。[](#connect-your-forms-environment-with-hcaptcha-service)
     <!--* **Error Message:** Provide the error message to display to the user when the Captcha submission fails.-->

1. 「**[!UICONTROL 完了]**」を選択します。


Now, only legitimate forms, in which the form filler successfully clears the challenge posed by the hCaptcha® service are allowed for the form submission. hCaptcha®

**hCaptcha® は、Intuition Machines, Inc. の登録商標です。**


## よくある質問

* **Q:1 つのアダプティブフォームで複数の Captcha コンポーネントを使用できますか？**
* **A:** アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込みのためにマークされたフラグメントまたはパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

{{see-also}}
