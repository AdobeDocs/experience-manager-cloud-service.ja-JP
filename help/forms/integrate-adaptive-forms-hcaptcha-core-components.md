---
title: AEM アダプティブフォームコアコンポーネントで hCaptcha&reg；を使用する方法
description: hCaptcha® サービスでフォームのセキュリティを容易に強化できます。ステップバイステップガイドをご用意しております。
topic-tags: Adaptive Forms, author
keywords: hCaptcha&reg; サービス、アダプティブForms、CAPTCHA チャレンジ、ボット防止、コアコンポーネント、フォーム送信セキュリティ、フォームスパム防止
feature: Adaptive Forms, Core Components
exl-id: 6c559df2-7b6a-42fe-b44c-29a782570a0c
role: User, Developer
source-git-commit: 76301ca614ae2256f5f8b00c41399298c761ee33
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 42%

---

# AEM Forms環境と hCaptcha の接続® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> この機能は早期導入プログラムの対象です。 早期導入プログラムに登録し、機能へのアクセスをリクエストするには、公式メール ID から aem-forms-ea@adobe.com にメールを送信してください。</span>

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のある目的を防止することで、オンライントランザクションの安全性を高めます。

AEM Forms as a Cloud Service は、次の CAPTCHA ソリューションをサポートしています。
* [hCaptcha](#integrate-aem-forms-environment-with-hcaptcha-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

## AEM Forms環境と hCaptcha Captcha の統合

hCaptcha® サービスは、ボット、スパム、自動化された不正使用からフォームを保護します。チェックボックスウィジェットテストを行ってユーザーの反応を評価し、フォームを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のあるアクティビティを防止することで、オンライントランザクションの安全性を高めます。

AEM Forms as a Cloud Serviceは、アダプティブ Forms コアコンポーネントで hCaptcha® をサポートします。 これを使用して、フォーム送信時にチェックボックスウィジェットの課題を表示できます。

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### AEM Forms環境と hCaptcha を統合するための前提条件® {#prerequisite}

AEM Formsで hCaptcha® を設定するには、hCaptcha® web サイトから [hCaptcha® サイトキーと秘密鍵 ](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) を取得する必要があります。

### hCaptcha の設定® {#steps-to-configure-hcaptcha}

AEM Formsを hCaptcha® サービスと統合するには、次の手順を実行します。

1. AEM Forms as a Cloud Service環境に設定コンテナを作成します。 設定コンテナには、AEM を外部サービスに接続するために使用されるクラウド設定が格納されます。AEM Forms環境を hCaptcha® に接続するための設定コンテナを作成して設定するには：
   1. AEM Forms as a Cloud Service インスタンスを開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定ブラウザーで、既存のフォルダーを選択したり、フォルダーを作成したりできます。 フォルダーを作成して、そのフォルダーの「クラウド設定」オプションを有効にしたり、既存のフォルダーの「クラウド設定を有効にする」オプションを有効にしたりできます。

      * フォルダーを作成し、それに対して「クラウド設定」オプションを有効にするには、次の手順を実行します。
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. 設定を作成ダイアログで、名前とタイトルを指定し、「**[!UICONTROL クラウド設定]**」オプションを選択します。
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * 既存のフォルダーに対して「クラウド設定」オプションを有効にするには：
         1. 設定ブラウザーで、フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

1. Cloud Service を設定：
   1. AEM オーサーインスタンスで、![tools-1](assets/tools-1.png)/**[!UICONTROL Cloud Services]** に移動し、「**[!UICONTROL hCaptcha®]**」を選択します。

      ![hCaptcha® の ui](assets/hcaptcha-in-ui.png)
   1. 前の節で説明したように、作成または更新された設定コンテナを選択します。 「**[!UICONTROL 作成]**」を選択します。

      ![ 設定 hCaptcha®](assets/config-hcaptcha.png)
   1. hCaptcha® サービスの **[!UICONTROL タイトル]**、**[!UICONTROL 名前]**、**[!UICONTROL サイトキー]** および **[!UICONTROL 秘密鍵]** を指定します [ 前提条件で取得 ](#prerequisite)。 「**[!UICONTROL 作成]**」を選択します。

      ![AEM Forms環境を hCaptcha と接続するようにCloud Serviceを設定する®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > [ クライアントサイドのJavaScript検証 URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) および [ サーバーサイドの検証 URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side) は、hCaptcha® 検証用に既に入力されているので、変更する必要はありません。

   hCAPTCHA サービスを設定すると、[ コアコンポーネントに基づくアダプティブフォーム ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/introduction) で使用できるようになります。

## アダプティブなForms コアコンポーネントコン ールでの hCaptcha® の使用 {#using-hCaptcha®-core-components}

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、**[!UICONTROL プロパティ]** を選択します。 **[!UICONTROL Configuration Container]** オプションについては、AEM Formsと hCaptcha を接続するクラウド設定が含まれている Configuration Container を選択して®**[!UICONTROL 保存して閉じる]** を選択します。

   そのような Configuration Container がない場合に Configuration Container を作成する方法については、[AEM Forms環境と hCaptcha® の接続 ](#connect-your-forms-environment-with-hcaptcha-service) の節を参照してください。

   ![設定コンテナの選択](/help/forms/assets/captcha-properties.png)

1. アダプティブフォームを選択し、「**[!UICONTROL 編集]**」を選択します。 アダプティブフォームエディターでアダプティブフォームが開きます。
1. コンポーネントブラウザーから **[!UICONTROL Adaptive Form hCaptcha®]** コンポーネントをアダプティブフォームにドラッグ&amp;ドロップまたは追加します。
1. **[!UICONTROL アダプティブフォーム hCaptcha®]** コンポーネントを選択し、プロパティ ![ プロパティアイコン ](assets/configure-icon.svg) アイコンをクリックします。 プロパティダイアログが開きます。次のプロパティを指定します。

   ![hCaptcha® v2](assets/config-hcaptcha-v2.png)

   * **[!UICONTROL 名前 &#x200B;]:** Captcha コンポーネントの名前を指定すると、フォーム内とルールエディター内の両方で一意の名前を使用して、フォームコンポーネントを簡単に識別できます。
   * **[!UICONTROL タイトル &#x200B;]:** Captcha コンポーネントのタイトルを指定します。
   * **[!UICONTROL 設定]：** hCaptcha® 用に設定されたクラウド設定を選択します。
   * **Captcha サイズ：** hCaptcha® チャレンジダイアログの表示サイズを選択できます。 「**[!UICONTROL コンパクト]**」オプションを選択すると小さいサイズ、「**[!UICONTROL 標準]**」オプションを選択すると比較的大きなサイズの hCaptcha® テストダイアログを表示できます。<!-- or **[!UICONTROL Invisible]** to validate hCaptcha&reg; without explicitly rendering the checkbox widget on the user interface. -->
   * **[!UICONTROL 検証メッセージ &#x200B;]:** フォーム送信時の Captcha 検証の検証メッセージを指定します。
   * **[!UICONTROL スクリプト検証メッセージ]** - スクリプトの検証が失敗した場合に表示するメッセージを入力できます。

     >[!NOTE]
     >同様の目的のために、環境内に複数のクラウド設定を持つことができます。 そのため、サービスは慎重に選択してください。サービスがリストに表示されない場合は、[AEM Forms環境と hCaptcha® の接続 ](#connect-your-forms-environment-with-hcaptcha-service) を参照して、AEM Forms環境と hCaptcha® サービスを接続するCloud Serviceの作成方法を確認してください。

   <!--* **Error Message:** Provide the error message to display to the user when the Captcha submission fails.-->

1. 「**[!UICONTROL 完了]**」を選択します。


現在は、フォームの入力者が hCaptcha® サービスによって発生する課題を正常にクリアした正当なフォームのみがフォーム送信で許可されています。 hCaptcha®

**hCaptcha® は、Intuition Machines, Inc. の登録商標です。**


## よくある質問

* **Q:1 つのアダプティブフォームで複数の Captcha コンポーネントを使用できますか？**
* **A:** アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込みのためにマークされたフラグメントまたはパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

{{see-also}}
