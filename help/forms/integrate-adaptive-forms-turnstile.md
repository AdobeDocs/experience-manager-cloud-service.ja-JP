---
title: AEM アダプティブフォームで Turnstile を使用する方法
description: Turnstile サービスでフォームのセキュリティを簡単に強化します。 ステップバイステップガイドをご用意しております。
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: 644c351b-a167-4d18-8b99-b7cae6be48d5
source-git-commit: 914139a6340f15ee77024793bf42fa30c913931e
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 26%

---

# Turnstile CAPTCHA と Adaptive Formsの統合

<span class="preview"> この機能は早期導入プログラムの対象です。 早期導入プログラムに登録し、機能へのアクセスをリクエストするには、公式メール ID から aem-forms-ea@adobe.com にメールを送信してください。</span>

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のある目的を防止することで、オンライントランザクションの安全性を高めます。

AEM Forms as a Cloud Service は、次の CAPTCHA ソリューションをサポートしています。

* [Cloudflare Turnstile](#integrate-aem-forms-environment-with-turnstile-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## AEM Forms環境と Turnstile Captcha の統合

Cloudflare の Turnstile Captcha は、自動ボット、悪意のある攻撃、スパム、不要な自動トラフィックからフォームとサイトを保護することを目的としたセキュリティ対策です。 フォームの送信を許可する前に、人間であることを確認するためのチェックボックスがフォーム送信時に表示されます。 AEM Forms as a Cloud Serviceは、アダプティブFormsでの Turnstile Captcha をサポートします。

<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

### AEM Forms環境と Turnstile Captcha を統合するための前提条件 {#prerequisite}

AEM Forms用に Turnstile を設定するには、Turnstile Web サイトから [Turnstile サイトキーと秘密鍵 &#x200B;](https://developers.cloudflare.com/turnstile/get-started/) を取得する必要があります。

### AEM Forms用の Turnstile を設定する手順{#steps-to-configure-turnstile}

1. AEM Forms as a Cloud Service環境に設定コンテナを作成します。 設定コンテナには、AEM を外部サービスに接続するために使用されるクラウド設定が格納されます。AEM Forms環境を Turnstile と接続するための設定コンテナを作成および設定するには：
   1. AEM Forms as a Cloud Service インスタンスを開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定ブラウザーで、既存のフォルダーを選択したり、フォルダーを作成したりできます。 フォルダーを作成し、そのフォルダーに対して「クラウド設定」オプションを有効にするか、既存のフォルダーに対して「クラウド設定」オプションを有効にします。

      * **フォルダーを作成し、そのフォルダーの「クラウド設定」オプションを有効にするには**:
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. 設定を作成ダイアログで、名前とタイトルを指定し、「**[!UICONTROL クラウド設定]**」オプションを選択します。
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * 既存のフォルダーに対して「クラウド設定」オプションを有効にするには：
         1. 設定ブラウザーで、フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

1. Cloud Service を設定：
   1. AEM オーサーインスタンスで、![tools-1](assets/tools-1.png)/**[!UICONTROL Cloud Services]** に移動し、「**[!UICONTROL Turnstile]**」を選択します。

      ![UI でのターンスタイル &#x200B;](assets/turnstile-in-ui.png)
   1. 前の節で説明したように、作成または更新された設定コンテナを選択します。 「**[!UICONTROL 作成]**」を選択します。

      ![&#x200B; 設定ターンスタイル &#x200B;](assets/config-hcaptcha.png)
   1. **[!UICONTROL ウィジェットタイプ]** を管理対象として指定します。ウィジェットタイプは、前提条件で取得したキー **[!UICONTROL タイトル]**、**[!UICONTROL 名前]**、**[!UICONTROL サイトキー]**、**[!UICONTROL 秘密鍵]** に応じて変わることがあります [&#x200B; 前提条件で取得 &#x200B;](#prerequisite)。 「**[!UICONTROL 作成]**」を選択します。

      ![AEM Forms環境を Turnstile と連携させるためのCloud Serviceの設定 &#x200B;](assets/config-turntstile.png)

>[!NOTE]
> 自動スタイル検証用に既にクライアントサイドのJavaScript検証 URL とサーバーサイドの検証 URL が入力されているので、変更する必要はありません。

Turnstile Captcha サービスを設定すると、アダプティブフォームで使用できるようになります。

## アダプティブフォームでの Turnstile の使用{#using-turnstile-foundation-components}

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、**[!UICONTROL プロパティ]** を選択します。 **[!UICONTROL Configuration Container]** オプションについては、AEM Formsと Turnstile を接続するクラウド設定が含まれている Configuration Container を選択して、「保存して閉じる **[!UICONTROL を選択します]**。

   そのような設定コンテナがない場合は、設定コンテナの作成方法について [AEM Forms環境の自動インストールへの接続 &#x200B;](#connect-your-forms-environment-with-turnstile-service) の節を参照してください。

   ![設定コンテナの選択](/help/forms/assets/captcha-properties.png)

1. アダプティブフォームを選択し、「**[!UICONTROL 編集]**」を選択します。 アダプティブフォームエディターでアダプティブフォームが開きます。
1. コンポーネントブラウザーから **[!UICONTROL Captcha]** コンポーネントを、アダプティブフォームにドラッグ＆ドロップします。
1. **[!UICONTROL Captcha]** コンポーネントを選択し、プロパティ ![&#x200B; プロパティアイコン &#x200B;](assets/configure-icon.svg) アイコンをクリックします。 プロパティダイアログが開きます。

   ![設定](assets/turnstile-setting-v1.png)

   次のプロパティを指定します。

   * **[!UICONTROL タイトル &#x200B;]:** Captcha コンポーネントのタイトルを指定すると、フォーム内とルールエディター内の両方で一意の名前を使用して、フォームコンポーネントを簡単に識別できます。
   * **[!UICONTROL 検証メッセージ &#x200B;]:** フォーム送信時に Captcha を検証するための検証メッセージを提供します。
   * **[!UICONTROL Captcha を検証 &#x200B;]:** いずれかのオプションを選択して、Captcha を検証できます。
      * フォーム送信時
      * ユーザー側のアクション
   * **[!UICONTROL Captcha サービス &#x200B;]:** Captcha サービスを選択します。ここでは、Cloudfare Turnstile Captcha サービスを選択します。
   * **[!UICONTROL Captcha 設定 &#x200B;]:** Turnstile 用に設定されたクラウド設定を選択します。 例えば、ここでは **管理キー** を選択します。

     >[!NOTE]
     >
     > 同様の目的のために、環境内に複数のクラウド設定を持つことができます。 そのため、サービスは慎重に選択してください。サービスがリストに表示されない場合は、AEM Forms環境と Turnstile サービスを接続するCloud Serviceの作成方法について、[AEM Forms環境と Turnstile の接続 &#x200B;](#connect-your-forms-environment-with-turnstile-service) を参照してください。

   * **エラーメッセージ：** Captcha 送信が失敗した場合にユーザーに表示するエラーメッセージを指定します。
   * **Captcha サイズ：** 回転式チャレンジダイアログの表示サイズを選択します。 「**[!UICONTROL コンパクト]**」オプションを使用すると小さいサイズを表示し、「**[!UICONTROL 標準]**」オプションを使用すると比較的大きいサイズの回転式チャレンジダイアログを表示します。


     >[!NOTE]
     >これは、ウィジェットタイプの管理対象および非インタラクティブに適用できます。 ウィジェットタイプが非表示の場合、size プロパティは不要で、無効になります。

1. 「**[!UICONTROL 完了]**」を選択します。

現在は、フォームの入力者が Turnstile サービスによって発生する課題を正常にクリアした正当なフォームのみがフォーム送信に許可されています。

![&#x200B; 回転式チャレンジ &#x200B;](assets/turnstile-challenge.png)

## よくある質問

* **Q:1 つのアダプティブフォームで複数の Captcha コンポーネントを使用できますか？**
* **A:** アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込みのためにマークされたフラグメントまたはパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

{{see-also}}
