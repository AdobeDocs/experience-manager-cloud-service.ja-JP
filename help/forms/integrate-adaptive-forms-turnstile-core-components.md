---
title: AEM アダプティブフォームのコアコンポーネントでターンスタイルを使用する方法
description: Turnstile サービスでフォームのセキュリティを簡単に強化します。 ステップバイステップガイドをご用意しております。
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
exl-id: e9c13228-0857-4936-9c39-12ed2bddf429
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 31%

---

# AEM Forms環境と Turnstile の連携 {#connect-your-forms-environment-with-turnstile-service}

<span class="preview"> この機能は早期導入プログラムの対象です。 早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式メール ID から aem-forms-ea@adobe.com にメールを送信してください。</span>

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のある目的を防止することで、オンライントランザクションの安全性を高めます。

AEM Forms as a Cloud Service は、次の CAPTCHA ソリューションをサポートしています。


* [Cloudflare Turnstile](#integrate-aem-forms-environment-with-turnstile-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)



<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## AEM Forms環境と Turnstile Captcha の統合

Cloudflare の Turnstile Captcha は、自動ボット、悪意のある攻撃、スパム、不要な自動トラフィックからフォームとサイトを保護することを目的としたセキュリティ対策です。 フォームの送信を許可する前に、人間であることを確認するためのチェックボックスがフォーム送信時に表示されます。 AEM Formsas a Cloud Serviceは、アダプティブ Forms コアコンポーネントでの Turnstile Captcha をサポートしています。

### AEM Forms環境と Turnstile Captcha を統合するための前提条件 {#prerequisite}

AEM Forms コアコンポーネントの Turnstile を設定するには、Turnstile の Web サイトから [Turnstile sitekey and secret key](https://developers.cloudflare.com/turnstile/get-started/) を取得する必要があります。

### ターンスタイルを設定 {#steps-to-configure-hcaptcha}

AEM Formsを Turnstile サービスと統合するには、次の手順を実行します。

1. AEM Formsas a Cloud Service環境で設定コンテナを作成します。 設定コンテナには、AEM を外部サービスに接続するために使用されるクラウド設定が格納されます。AEM Forms環境を Turnstile と接続するための設定コンテナを作成および設定するには：
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
   1. AEM オーサーインスタンスで、![tools-1](assets/tools-1.png)/**[!UICONTROL Cloud Service]** に移動し、「**[!UICONTROL Turnstile]**」を選択します。
      ![UI でのターンスタイル ](assets/turnstile-in-ui.png)
   1. 前の節で説明したように、作成または更新された設定コンテナを選択します。 「**[!UICONTROL 作成]**」を選択します。
      ![ 設定ターンスタイル ](assets/config-hcaptcha.png)
   1. 自動スタイルサービス用の **[!UICONTROL ウィジェットタイプ]** を管理対象、**[!UICONTROL タイトル]**、**[!UICONTROL 名前]**、**[!UICONTROL サイトキー]**、**[!UICONTROL 秘密鍵]** に指定します [ 前提条件で取得 ](#prerequisite)。
   1. 「**[!UICONTROL 作成]**」をクリックします。

      ![AEM Forms環境を Turnstile と連携させるためのCloud Serviceの設定 ](assets/config-turntstile.png)

   >[!NOTE]
   > 自動スタイル検証用に既にクライアントサイドのJavaScript検証 URL とサーバーサイドの検証 URL が入力されているので、変更する必要はありません。

   Turnstile Captcha サービスを設定すると、[ コアコンポーネントに基づくアダプティブフォーム ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/introduction) で使用できるようになります。

## アダプティブフォームでの Turnstile の使用 {#using-turnstile-core-components}

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、**[!UICONTROL プロパティ]** を選択します。 **[!UICONTROL 設定コンテナ]** オプションについては、AEM Formsと Turnstile を接続するクラウド設定を含んだ設定コンテナを選択し、「**[!UICONTROL 保存して閉じる]**」を選択します。

   そのような設定コンテナがない場合は、設定コンテナの作成方法について [AEM Forms環境の自動インストールへの接続 ](#connect-your-forms-environment-with-turnstile-service) の節を参照してください。

   ![設定コンテナの選択](/help/forms/assets/captcha-properties.png)

1. アダプティブフォームを選択し、「**[!UICONTROL 編集]**」を選択します。 アダプティブフォームエディターでアダプティブフォームが開きます。
1. コンポーネントブラウザーから **[!UICONTROL アダプティブフォームターンスタイル]** コンポーネントを、アダプティブフォームにドラッグ&amp;ドロップまたは追加します。
1. **[!UICONTROL アダプティブフォームターンスタイル]** コンポーネントを選択し、「プロパティ ![ プロパティアイコン ](assets/configure-icon.svg) アイコンをクリックします。 プロパティダイアログが開きます。次のプロパティを指定します。

   ![ ターンスタイル v2](assets/turnstile-settings-v2.png)

   * **[!UICONTROL 名前 ]:** Captcha コンポーネントの名前を指定すると、フォーム内とルールエディター内の両方で一意の名前を使用して、フォームコンポーネントを簡単に識別できます。
   * **[!UICONTROL タイトル ]:** Captcha コンポーネントのタイトルを指定します。
   * **[!UICONTROL 設定 ]:** 自動で設定するクラウド設定を選択します。
   * **[!UICONTROL 検証メッセージ ]:** フォーム送信時に Captcha を検証するための検証メッセージを提供します。
   * **[!UICONTROL スクリプト検証メッセージ]**：このオプションを使用すると、スクリプトの検証が失敗した場合に表示するメッセージを入力できます。
     >[!NOTE]
     >同様の目的のために、環境内に複数のクラウド設定を持つことができます。 そのため、サービスは慎重に選択してください。サービスがリストに表示されない場合は、AEM Forms環境と Turnstile サービスを接続するCloud Serviceの作成方法について、[AEM Forms環境と Turnstile の接続 ](#connect-your-forms-environment-with-turnstile-service) を参照してください。
   * **エラーメッセージ：** Captcha 送信が失敗した場合にユーザーに表示するエラーメッセージを指定します。

1. 「**[!UICONTROL 完了]**」を選択します。


現在は、フォームの入力者が Turnstile サービスによって発生する課題を正常にクリアした正当なフォームのみがフォーム送信に許可されています。

![ 回転式チャレンジ ](assets/turnstile-challenge.png)


## よくある質問

* **Q:1 つのアダプティブフォームで複数の Captcha コンポーネントを使用できますか？**
* **A:** アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込みのためにマークされたフラグメントまたはパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

{{see-also}}
