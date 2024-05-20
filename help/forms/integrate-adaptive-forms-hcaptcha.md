---
title: AEM アダプティブフォームで hCaptcha® を使用する方法
description: hCaptcha® サービスでフォームのセキュリティを簡単に強化します。 ステップバイステップガイドをご用意しております。
topic-tags: Adaptive Forms, author
keywords: hCaptcha® サービス、アダプティブForms、CAPTCHA チャレンジ、ボット防止、フォーム送信セキュリティ、フォームスパム防止
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: a8a31bae0f937aa8941d258af648d6be030a9fac
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 17%

---


# AEM Forms環境と hCaptcha の接続® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> この機能は早期導入プログラムの対象です。 早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

hCaptcha® サービスは、ボット、スパム、自動不正使用からフォームを保護します。 チェックボックスウィジェットの課題を設定し、ユーザーの応答を評価して、フォームを操作しているのが人間かボットかを判断します。 これにより、テストが失敗した場合にユーザーが続行するのを防ぎ、ボットがスパムや悪意のあるアクティビティを投稿するのを防ぐことにより、オンライントランザクションを安全にすることができます。

<!-- ![hCaptcha®](assets/hCaptcha®-challenge.png)-->

AEM Formsas a Cloud Serviceは、アダプティブ Formsの hCaptcha® をサポートします。 これを使用して、フォーム送信時にチェックボックスウィジェットの課題をユーザーに提示できます。

## AEM Forms環境と hCaptcha を統合するための前提条件® {#prerequisite}

AEM Formsで hCaptcha® を設定するには、 [hCaptcha® サイトキーと秘密鍵](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) hCaptcha® web サイトから

## hCaptcha の設定手順® {#steps-to-configure-hcaptcha}

1. AEM Formsas a Cloud Service環境で設定コンテナを作成します。 設定コンテナには、AEM を外部サービスに接続するために使用されるクラウド設定が格納されます。AEM Forms環境を hCaptcha® に接続するための設定コンテナを作成して設定するには：
   1. AEM Forms as a Cloud Service インスタンスを開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定ブラウザーで、既存のフォルダーを選択したり、フォルダーを作成したりできます。 フォルダーを作成し、そのフォルダーに対して「クラウド設定」オプションを有効にするか、既存のフォルダーに対して「クラウド設定」オプションを有効にします。

      * **フォルダーを作成し、そのフォルダーの「クラウド設定」オプションを有効にするには**:
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. 設定を作成ダイアログで、名前とタイトルを指定し、 **[!UICONTROL クラウド設定]** オプション。
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * 既存のフォルダーに対して「クラウド設定」オプションを有効にするには：
         1. 設定ブラウザーで、フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

1. Cloud Service を設定：
   1. AEM オーサーインスタンスで、に移動します。 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** を選択して、 **[!UICONTROL H キャプチャ®]**.
      ![hCaptcha® の ui](assets/hcaptcha-in-ui.png)
   1. 前の節で説明したように、作成または更新された設定コンテナを選択します。 「**[!UICONTROL 作成]**」を選択します。
      ![設定 hCaptcha®](assets/config-hcaptcha.png)
   1. を指定 **[!UICONTROL タイトル]**, **[!UICONTROL 名前]**, **[!UICONTROL サイトキー]**、および **[!UICONTROL 秘密鍵]** hCaptcha® サービスの場合 [前提条件で得られる](#prerequisite). 「**[!UICONTROL 作成]**」を選択します。

      ![AEM FormsCloud Serviceを hCaptcha と接続するための環境を設定する®](assets/create-hcaptcha-config.png)

>[!NOTE]
> ユーザーは変更する必要はありません [クライアントサイド JavaScript 検証 URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) および [サーバーサイド検証 URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side) hCaptcha® 検証用に事前入力されているので、 いくつかの国では、エンドポイントが異なる場合があります。 [hCaptcha® の FAQ](https://docs.hcaptcha.com/faq#does-hcaptcha-support-access-by-users-in-china) を参照してください。

hCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。

## アダプティブフォームでの hCaptcha® の使用{#using-hCaptcha®-foundation-components}

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、以下を選択します。 **[!UICONTROL プロパティ]**. の場合 **[!UICONTROL 設定コンテナ]** 「」オプションを選択し、AEM Formsと hCaptcha® を接続するクラウド設定を含む設定コンテナを選択して、 **[!UICONTROL 保存して閉じる]**.

   そのような設定コンテナがない場合は、の節を参照してください。 [AEM Forms環境と hCaptcha の接続®](#connect-your-forms-environment-with-hcaptcha-service) 設定コンテナの作成方法を説明します。

   ![設定コンテナの選択](/help/forms/assets/captcha-properties.png)

1. アダプティブフォームを選択し、以下を選択します。 **[!UICONTROL 編集]**. アダプティブフォームエディターでアダプティブフォームが開きます。
1. コンポーネントブラウザーから **[!UICONTROL Captcha]** コンポーネントを、アダプティブフォームにドラッグ＆ドロップします。
1. 「」を選択します **[!UICONTROL キャプチャ]** コンポーネントし、「プロパティ」をクリックします。 ![プロパティアイコン](assets/configure-icon.svg) アイコン。 プロパティダイアログが開きます。

   ![代替テキスト](assets/hcaptcha-properties.png)

   次のプロパティを指定します。

   * **[!UICONTROL タイトル]:** Captcha コンポーネントのタイトルを指定すると、フォーム内とルールエディター内の両方で、一意の名前を使用してフォームコンポーネントを簡単に識別できます。
   * **[!UICONTROL 検証メッセージ]:** フォーム送信時の Captcha 検証用の検証メッセージを指定します。
   * **[!UICONTROL Captcha の検証]:** Captcha を検証するオプションの 1 つを選択できます。
      * フォーム送信時
      * ユーザー側のアクション
   * **[!UICONTROL Captcha サービス]:** Captcha サービスを選択します。ここでは、hCaptcha® サービスを選択します。
   * **[!UICONTROL Captcha 設定]:** hCaptcha® 用に設定したクラウド設定を選択します。
     >[!NOTE]
     >同様の目的のために、環境内に複数のクラウド設定を持つことができます。 そのため、サービスは慎重に選択してください。サービスが表示されない場合は、を参照してください。 [AEM Forms環境と hCaptcha の接続®](#connect-your-forms-environment-with-hcaptcha-service) AEM Forms環境と hCaptcha® サービスを接続するCloud Serviceの作成方法について説明します。

   * **エラーメッセージ：** Captcha 送信が失敗した場合にユーザーに表示するエラーメッセージを指定します。
   * **Captcha サイズ：** hCaptcha® チャレンジダイアログの表示サイズを選択します。 の使用 **[!UICONTROL コンパクト]** 小さいサイズのを表示するオプション **[!UICONTROL 標準]** 比較的大きなサイズの hCaptcha® チャレンジダイアログを表示するオプション **[!UICONTROL 非表示]** を使用して® ユーザーインターフェイスでチェックボックスウィジェットを明示的にレンダリングせずに hCaptcha を検証できます。

1. 「**[!UICONTROL 完了]**」を選択します。

現在は、フォームの入力者が hCaptcha® サービスによって発生する課題を正常にクリアした正当なフォームのみがフォーム送信で許可されています。

**hCaptcha® は、Intuition Machines, Inc.の登録商標です。**

## よくある質問

* **Q:1 つのアダプティブフォームで複数の Captcha コンポーネントを使用できますか？**
* **回答：** アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込みのためにマークされたフラグメントまたはパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

{{see-also}}
