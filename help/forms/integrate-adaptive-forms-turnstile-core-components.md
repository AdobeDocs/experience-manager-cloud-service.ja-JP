---
title: AEM アダプティブフォームのコアコンポーネントでターンスタイルを使用する方法
description: Turnstile サービスでフォームのセキュリティを簡単に強化します。 ステップバイステップガイドをご用意しております。
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
source-git-commit: a8a31bae0f937aa8941d258af648d6be030a9fac
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 23%

---

# AEM Forms環境と Turnstile の連携 {#connect-your-forms-environment-with-turnstile-service}

<span class="preview"> この機能は早期導入プログラムの対象です。 早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

Cloudflare の Turnstile Captcha は、自動ボット、悪意のある攻撃、スパム、不要な自動トラフィックからフォームとサイトを保護することを目的としたセキュリティ対策です。 フォームの送信を許可する前に、人間であることを確認するためのチェックボックスがフォーム送信時に表示されます。 AEM Formsas a Cloud Serviceは、アダプティブ Forms コアコンポーネントでの Turnstile Captcha をサポートします。

<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## AEM Forms環境と Turnstile Captcha を統合するための前提条件 {#prerequisite}

AEM Forms コアコンポーネント用の Turnstile を設定するには、以下を取得する必要があります [ターンスタイルサイトキーと秘密鍵](https://developers.cloudflare.com/turnstile/get-started/) Turnstile のウェブサイトから。

## Turnstile の設定手順 {#steps-to-configure-hcaptcha}

AEM Formsを Turnstile サービスと統合するには、次の手順を実行します。

1. AEM Formsas a Cloud Service環境で設定コンテナを作成します。 設定コンテナには、AEM を外部サービスに接続するために使用されるクラウド設定が格納されます。AEM Forms環境を Turnstile と接続するための設定コンテナを作成および設定するには：
   1. AEM Forms as a Cloud Service インスタンスを開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定ブラウザーで、既存のフォルダーを選択したり、フォルダーを作成したりできます。 フォルダーを作成して、そのフォルダーの「クラウド設定」オプションを有効にしたり、既存のフォルダーの「クラウド設定を有効にする」オプションを有効にしたりできます。

      * フォルダーを作成し、それに対して「クラウド設定」オプションを有効にするには、次の手順を実行します。
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. 設定を作成ダイアログで、名前とタイトルを指定し、 **[!UICONTROL クラウド設定]** オプション。
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * 既存のフォルダーに対して「クラウド設定」オプションを有効にするには：
         1. 設定ブラウザーで、フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

1. Cloud Service を設定：
   1. AEM オーサーインスタンスで、に移動します。 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** を選択して、 **[!UICONTROL 回転式の]**.
      ![Ui でのターンスタイル](assets/turnstile-in-ui.png)
   1. 前の節で説明したように、作成または更新された設定コンテナを選択します。 「**[!UICONTROL 作成]**」を選択します。
      ![回転式の設定](assets/config-hcaptcha.png)
   1. を指定 **[!UICONTROL ウィジェットタイプ]** 管理対象、 **[!UICONTROL タイトル]**, **[!UICONTROL 名前]**, **[!UICONTROL サイトキー]**、および **[!UICONTROL 秘密鍵]** 回転式サービス用 [前提条件で得られる](#prerequisite).
   1. 「**[!UICONTROL 作成]**」をクリックします。

      ![AEM FormsCloud Serviceと Turnstile を連携させる環境の設定](assets/config-turntstile.png)

   >[!NOTE]
   > 自動スタイル検証用に既にクライアントサイドの JavaScript 検証 URL とサーバーサイドの検証 URL が入力されているので、ユーザーは変更する必要はありません。

   Turnstile Captcha サービスを設定すると、 [コアコンポーネントに基づくアダプティブフォーム](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/introduction).

## アダプティブなForms コアコンポーネントでのターンスタイルの使用 {#using-turnstile-core-components}

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、以下を選択します。 **[!UICONTROL プロパティ]**. の場合 **[!UICONTROL 設定コンテナ]** オプションとして、AEM Formsと Turnstile を接続するクラウド設定を含んだ設定コンテナを選択し、次を選択します。 **[!UICONTROL 保存して閉じる]**.

   そのような設定コンテナがない場合は、の節を参照してください。 [AEM Forms環境と Turnstile の連携](#connect-your-forms-environment-with-turnstile-service) 設定コンテナの作成方法を説明します。

   ![設定コンテナの選択](/help/forms/assets/captcha-properties.png)

1. アダプティブフォームを選択し、以下を選択します。 **[!UICONTROL 編集]**. アダプティブフォームエディターでアダプティブフォームが開きます。
1. コンポーネントブラウザーからドラッグ&amp;ドロップするか、 **[!UICONTROL アダプティブフォームのターンスタイル]** コンポーネントをアダプティブフォーム上に配置します。
1. 「」を選択します **[!UICONTROL アダプティブフォームのターンスタイル]** コンポーネントを選択し、「プロパティ」をクリックします ![プロパティアイコン](assets/configure-icon.svg) アイコン。 プロパティダイアログが開きます。次のプロパティを指定します。

   ![ターンスタイル v2](assets/turnstile-settings-v2.png)

   * **[!UICONTROL 名前]:** Captcha コンポーネントの名前を指定すると、フォーム内とルールエディター内の両方で一意の名前を使用して、フォームコンポーネントを簡単に識別できます。
   * **[!UICONTROL タイトル]:** Captcha コンポーネントのタイトルを指定します。
   * **[!UICONTROL 設定]:** Turnstile 用に設定されたクラウド設定を選択します。
   * **[!UICONTROL 検証メッセージ]:** フォーム送信時に Captcha を検証するための検証メッセージを提供します。
   * **[!UICONTROL スクリプト検証メッセージ]**：このオプションを使用すると、スクリプトの検証が失敗した場合に表示するメッセージを入力できます。
     >[!NOTE]
     >同様の目的のために、環境内に複数のクラウド設定を持つことができます。 そのため、サービスは慎重に選択してください。サービスが表示されない場合は、を参照してください。 [AEM Forms環境と Turnstile の連携](#connect-your-forms-environment-with-turnstile-service) AEM Forms環境と Turnstile サービスを接続するCloud Serviceの作成方法について説明します。
   * **エラーメッセージ：** Captcha 送信が失敗した場合にユーザーに表示するエラーメッセージを指定します。

1. 「**[!UICONTROL 完了]**」を選択します。


現在は、フォームの入力者が Turnstile サービスによって発生する課題を正常にクリアした正当なフォームのみがフォーム送信に許可されています。

![回転式チャレンジ](assets/turnstile-challenge.png)


## よくある質問

* **Q:1 つのアダプティブフォームで複数の Captcha コンポーネントを使用できますか？**
* **回答：** アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込みのためにマークされたフラグメントまたはパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

{{see-also}}
