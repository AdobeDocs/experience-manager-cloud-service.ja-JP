---
title: AEM アダプティブフォームのコアコンポーネントでターンスタイルを使用する方法
description: Turnstile サービスでフォームのセキュリティを簡単に強化します。 ステップバイステップガイドをご用意しております。
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 819c376671ee141e1bcf885a22f161b327ce2c15
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 24%

---

# AEM Forms環境と Turnstile の連携 {#connect-your-forms-environment-with-turnstile-service}

<span class="preview">この機能は早期導入プログラムに基づいています。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式メール ID から aem-forms-ea@adobe.com にメールを送信してください。</span>

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のある目的を防止することで、オンライントランザクションの安全性を高めます。

AEM Forms as a Cloud Service は、次の CAPTCHA ソリューションをサポートしています。


* [Turnstile](/help/forms/integrate-adaptive-forms-turnstile-core-components.md)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## AEM Forms環境と Turnstile Captcha の統合

Cloudflare の Turnstile Captcha は、自動ボット、悪意のある攻撃、スパム、不要な自動トラフィックからフォームとサイトを保護することを目的としたセキュリティ対策です。 フォームの送信を許可する前に、人間であることを確認するためのチェックボックスがフォーム送信時に表示されます。 AEM Formsas a Cloud Serviceは、アダプティブ Forms コアコンポーネントでの Turnstile Captcha をサポートしています。

### AEM Forms環境と Turnstile Captcha を統合するための前提条件 {#prerequisite}

AEM Forms コアコンポーネントの Turnstile を設定するには、Turnstile Web サイトから [Turnstile サイトキーと秘密鍵 ](https://developers.cloudflare.com/turnstile/get-started/) を取得する必要があります。

### ターンスタイルを設定 {#steps-to-configure-hcaptcha}

AEM Formsを Turnstile サービスと統合するには、次の手順を実行します。

1. AEM Formsas a Cloud Service環境で設定コンテナを作成します。 設定コンテナには、AEM を外部サービスに接続するために使用されるクラウド設定が格納されます。AEM Formsを Turnstile に接続するための設定コンテナを作成および設定するには、次の手順に従います。
   1. AEM Forms as a Cloud Service インスタンスを開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定ブラウザーで、新しいフォルダーを作成してそのフォルダーのクラウド設定を有効にするか、以下に説明するように既存のフォルダーのクラウド設定を有効にします。

      * **新規フォルダー** を作成し、そのフォルダーのクラウド設定を次の手順に従って有効にするには：
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. 設定を作成ダイアログで、名前とタイトルを指定し、「**[!UICONTROL クラウド設定]**」オプションを選択します。
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * **既存のフォルダー** に対してクラウド設定オプションを有効にするには：
         1. 設定ブラウザーで、既存のフォルダーを選択し、「**[!UICONTROL プロパティ]**」をクリックします。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. **[!UICONTROL 保存して閉じる]** をクリックして、設定を保存して終了します。

1. Cloud Service を設定：
   1. AEM オーサーインスタンスで、![tools-1](assets/tools-1.png)/**[!UICONTROL Cloud Service]** に移動し、「**[!UICONTROL Turnstile]**」をクリックします。
      ![UI でのターンスタイル ](assets/turnstile-in-ui.png)
   1. 前の節で説明したように、作成または更新された設定コンテナを選択します。 「**[!UICONTROL 作成]**」を選択します。
      ![ 設定ターンスタイル ](assets/config-hcaptcha.png)
   1. **[!UICONTROL ウィジェットタイプ]** を管理対象、非インタラクティブ、非表示のいずれかに指定します。 ウィジェットのタイプについて詳しくは、[Turnstile Widget](https://developers.cloudflare.com/turnstile/concepts/widget/) を参照してください。
   1. 自動スタイルサービス用に **[!UICONTROL タイトル]**、**[!UICONTROL 名前]**、**[!UICONTROL サイトキー]** および **[!UICONTROL 秘密鍵]** を指定します [ 前提条件で取得 ](#prerequisite)。
   1. 「**[!UICONTROL 作成]**」をクリックします。

      ![AEM Forms環境を Turnstile と連携させるためのCloud Serviceの設定 ](assets/config-turntstile-cc.png)

   >[!NOTE]
   > 自動スタイル検証用に既にクライアントサイドのJavaScript検証 URL とサーバーサイドの検証 URL が入力されているので、変更する必要はありません。

   Turnstile Captcha サービスを設定すると、[ コアコンポーネントに基づくアダプティブフォーム ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/introduction) で使用できるようになります。

## アダプティブフォームでの Turnstile の使用 {#using-turnstile-core-components}

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、**[!UICONTROL プロパティ]** をクリックします。 **[!UICONTROL 設定コンテナ]** セクションで、AEM Formsと Turnstile を接続するクラウド設定を含む設定コンテナを選択します。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   設定コンテナがない場合は、[ ターンスタイルの設定 ](#steps-to-configure-hcaptcha) の節を参照して、設定コンテナの作成方法を確認してください。

   ![設定コンテナの選択](/help/forms/assets/captcha-properties.png)

1. アダプティブフォームを選択し、**[!UICONTROL 編集]** をクリックして、エディターでフォームを開きます。
1. コンポーネントブラウザーから **[!UICONTROL アダプティブフォームターンスタイル]** コンポーネントを、アダプティブフォームにドラッグ&amp;ドロップまたは追加します。
   ![Turnstile Captcha コンポーネントの追加 ](/help/forms/assets/turnstile-v2.png)
1. **[!UICONTROL アダプティブフォームターンスタイル]** コンポーネントを選択し、「プロパティ ![ プロパティアイコン ](assets/configure-icon.svg) アイコンをクリックします。 プロパティダイアログが開きます。次のプロパティを指定します。

   ![ ターンスタイル v2](assets/turnstile-settings-for-v2.png)

   * **[!UICONTROL 名前 ]:** Captcha コンポーネントの名前を指定すると、フォーム内とルールエディター内の両方で一意の名前を使用して、フォームコンポーネントを簡単に識別できます。
   * **[!UICONTROL タイトル ]:** Captcha コンポーネントのタイトルを指定します。 チェックボックスをオンにすることで、タイトルにリッチテキストを使用したり、タイトルを非表示にしたりできます。
   * **[!UICONTROL 設定 ]:** Turnstile Captcha サービス用に設定されたクラウド設定を選択します。
     >[!NOTE]
     >* 同様の目的のために、環境内に複数のクラウド設定を持つことができます。 そのため、サービスは慎重に選択してください。サービスがリストされない場合は、設定コンテナを作成してAEM Forms環境を Turnstile サービスと接続する方法について、[Turnstile の設定 ](#steps-to-configure-hcaptcha) の節を参照してください。
   * **[!UICONTROL 検証 ]:** Captcha 検証をエラーメッセージの形式で提供します。
      * **エラーメッセージ：** Captcha 送信が失敗した場合にユーザーに表示するエラーメッセージを指定します。
        >[!NOTE]
        >* エラーメッセージが表示されるのは、クライアント側の CAPTCHA が入力された場合のみです。


1. 「**[!UICONTROL 完了]**」を選択します。


現在は、フォームの入力者が Turnstile サービスによって発生する課題を正常にクリアした正当なフォームのみがフォーム送信に許可されています。

![ 回転式チャレンジ ](assets/turnstile-challenge.png)


## よくある質問

* **Q:1 つのアダプティブフォームで複数の Captcha コンポーネントを使用できますか？**
* **A:** アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込みのためにマークされたフラグメントまたはパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

{{see-also}}
