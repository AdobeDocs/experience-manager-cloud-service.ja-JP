---
title: AEM Forms as a Cloud Service の Edge Delivery Services での reCAPTCHA の使用
description: AEM Forms の Edge Delivery Services 向けフォームでの Google reCAPTCHA の使用
feature: Edge Delivery Services
keywords: フォームの reCAPTCHA, ユニバーサルエディターでの reCAPTCHA の使用, フォームでの reCAPTCHA の追加
role: Admin, Architect, Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 96%

---


# WYSIWYG オーサリングでの reCAPTCHA の使用

<span class="preview"> この機能は、早期アクセスプログラムを通じて利用できます。 アクセスをリクエストするには、公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に、GitHub の組織名とリポジトリ名を記載したメールを送信します。 例えば、リポジトリ URL がhttps://github.com/adobe/abcの場合、組織名は adobe で、リポジトリ名は abc.</span> です


CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、web サイトを不正行為、スパムおよび不正使用からの保護に使用される一般的なツールです。

例えば、追加控除と税率に基づいて税金を計算するフォームを考えます。このような場合は、悪意のあるユーザーがフォームを悪用してフィッシングメールを送信したり、スパムボットを使用して無関係または有害なコンテンツを大量に送信したりするリスクがあります。CAPTCHA を統合すると、送信が本物のユーザーからのものであることを確認して、セキュリティを強化し、スパムエントリを最小限に抑える効果を得ることができます。

![Google reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

Edge Delivery Services Forms では、フォームブロックにより、**CAPTCHA（非表示）**&#x200B;コンポーネントを使用して [Google reCAPTCHA をフォームに接続](#connect-forms-with-recaptcha-service-by-google)し、人間とボットを区別できます。この機能は、作成者がフォームをスパムや不正使用から保護するのに役立ちます。

## Forms と Google による reCAPTCHA サービスとの接続

Edge Delivery Services フォームを作成して、Google が提供する reCAPTCHA サービスを実装できます。必要に応じて、Edge Delivery Services Forms に次のいずれかの reCAPTCHA サービスを設定できます。

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> reCAPTCHA の仕組みについて詳しくは、[Google reCAPTCHA](https://developers.google.com/recaptcha/) を参照してください。

### reCAPTCHA Enterprise の設定

reCAPTCHA Enterprise は、Google が提供するプレミアムなエンタープライズグレードの不正検出および防止サービスです。これは、reCAPTCHA（スコアベース）の基盤に基づいて作成されていますが、ビジネスの複雑なニーズに合わせて、追加機能、スケーラビリティ、カスタマイズを提供します。

#### 始める前に

Edge Delivery Services Forms 用に Google reCAPTCHA Enterprise を設定する前に、次の手順が完了していることを確認します。

1. [Google Cloud プロジェクト](https://cloud.google.com/recaptcha/docs/prepare-environment?hl=ja#before-you-begin)を作成または選択し、[プロジェクト ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) を取得します。

1. Google Cloud プロジェクトで [reCAPTCHA Enterprise API を有効](https://cloud.google.com/recaptcha/docs/prepare-environment?hl=ja#enable-api)にし、[API キーを作成](https://console.cloud.google.com/apis/credentials)します。

1. [Google Cloud プロジェクトのサイトキー](https://console.cloud.google.com/security/recaptcha)を作成し、そのサイトキーをコピーします。

これらの資格情報を取得したら、フォームの reCAPTCHA Enterprise の設定に進むことができます。

1. [クラウド設定コンテナの作成](#1-create-cloud-configuration-container)
1. [reCAPTCHA Enterprise のクラウドサービス設定を作成](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. クラウド設定コンテナを作成

クラウド設定コンテナを作成するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. **[!UICONTROL ツール]** ![tools-1](/help/forms/assets/tools-1.png)／**[!UICONTROL 一般]**／**[!UICONTROL 設定ブラウザー]**&#x200B;に移動します。

   ![クラウド設定コンテナ](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. **[!UICONTROL 設定ブラウザー]**&#x200B;で、フォームに移動し、「**[!UICONTROL プロパティ]**」を選択します。

   ![クラウド設定プロパティ](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. **[!UICONTROL 設定プロパティ]**&#x200B;ダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。

1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

   ![クラウド設定プロパティを有効にする](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
&#39;
クラウド設定コンテナを作成したら、公開します。

   ![クラウド設定を公開](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. reCAPTCHA Enterprise のクラウドサービス設定を作成

reCAPTCHA Enterprise のクラウドサービス設定を作成するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. **[!UICONTROL ツール]** ![tools-1](/help/forms/assets/tools-1.png)／**[!UICONTROL Cloud Services]**／**[!UICONTROL reCAPTCHA]** に移動します。

   ![reCAPTCHA クラウド設定](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   **設定**&#x200B;ダイアログが開きます。

1. フォームに移動し、「**[!UICONTROL 作成]**」を選択します。

   ![CAPTCHA 設定](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   **[!UICONTROL reCAPTCHA 設定を作成]**&#x200B;ダイアログが開きます。

   ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. [!DNL ReCAPTCHA Enterprise] としてバージョンを選択し、タイトル、名前、プロジェクト ID、サイトキー、API キーを指定します。

   >[!NOTE]
   >
   > プロジェクト ID、サイトキー、API キーは、reCAPTCHA Enterprise の[事前準備](#before-you-start)の節から取得できます。

1. **スコアベースのサイトキー**&#x200B;として&#x200B;**[!UICONTROL キータイプ]**&#x200B;を選択します。
1. [0 ～ 1 の範囲のしきい値スコア](https://cloud.google.com/recaptcha/docs/interpret-assessment-website?hl=ja#interpret_scores)を指定します。スコアがしきい値以上になると、人間のインタラクションを識別し、それ以外の場合はボットのインタラクションとみなされます。
1. 「**[!UICONTROL 作成]**」を選択して、クラウドサービス設定を作成します。

   reCAPTCHA クラウド設定を作成したら、公開します。

   ![reCAPTCHA 設定を公開](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

これで、フォームを作成または編集し、WYSIWYG ベースのオーサリングを使用して reCAPTCHA コンポーネントを追加できます。Google reCAPTCHA をフォームに統合する手順について詳しくは、[フォームでの reCAPTCHA の使用](#use-recaptcha-in-your-form)を参照してください。

## reCAPTCHA の設定

reCAPTCHA は、ボットやスパムなどの不正なトラフィックを web サイトが検出して防止するのに役立つ、Google が提供する無料サービスです。背景で動作し、各ユーザーインタラクションにリスクスコア（0.0～1.0 の範囲）を割り当てるスコアベースのバージョンをサポートします。スコアがしきい値以上になると、人間のインタラクションを識別し、それ以外の場合はボットのインタラクションとみなされます。

#### 始める前に

Edge Delivery Services Forms 用に Google reCAPTCHA を設定する前に、[Google Console から reCAPTCHA API キーペア](https://www.google.com/recaptcha/admin)を取得します。ペアには、サイトキーと秘密鍵が含まれます。

>[!NOTE]
>
> * Edge Delivery Services Forms では、**reCAPTCHA スコアベース**&#x200B;のバージョンのみをサポートしています。

API キーペアを取得したら、フォームの reCAPTCHA の設定に進むことができます。

1. [クラウド設定コンテナの作成](#1-create-cloud-configuration-container-1)
1. [reCAPTCHA のクラウドサービス設定を作成](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. クラウド設定コンテナを作成

クラウド設定コンテナを作成するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. **[!UICONTROL ツール]** ![tools-1](/help/forms/assets/tools-1.png)／**[!UICONTROL 一般]**／**[!UICONTROL 設定ブラウザー]**&#x200B;に移動します。

   ![クラウド設定コンテナ](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. **[!UICONTROL 設定ブラウザー]**&#x200B;で、フォームに移動し、「**[!UICONTROL プロパティ]**」を選択します。

   ![クラウド設定プロパティ](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. **[!UICONTROL 設定プロパティ]**&#x200B;ダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。

1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

   ![クラウド設定プロパティを有効にする](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   クラウド設定コンテナを作成したら、公開します。

   ![クラウド設定を公開](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. reCAPTCHA のクラウドサービス設定を作成

reCAPTCHA のクラウドサービス設定を作成するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. **[!UICONTROL ツール]** ![tools-1](/help/forms/assets/tools-1.png)／**[!UICONTROL Cloud Services]**／**[!UICONTROL reCAPTCHA]** に移動します。

   ![reCAPTCHA クラウド設定](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   **設定**&#x200B;ダイアログが開きます。

1. フォームに移動し、「**[!UICONTROL 作成]**」を選択します。

   ![CAPTCHA 設定](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   **[!UICONTROL reCAPTCHA 設定を作成]**&#x200B;ダイアログが開きます。

   ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. [!DNL ReCAPTCHA v2] としてバージョンを選択し、タイトルと名前を指定します。
1. サイトキーと秘密鍵を指定します。

   >[!NOTE]
   >
   > サイトキーと秘密鍵は、reCAPTCHA の [始める前に](#before-you-begin)の節から取得できます。

1. 「**[!UICONTROL 作成]**」を選択して、クラウドサービス設定を作成します。

   reCAPTCHA クラウド設定を作成したら、公開します。

   ![reCAPTCHA 設定を公開](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

これで、フォームを作成および編集し、WYSIWYG ベースのオーサリングを使用して reCAPTCHA コンポーネントを追加できます。Google reCAPTCHA をフォームに統合する手順について詳しくは、[フォームでの reCAPTCHA の使用](#use-recaptcha-in-your-form)を参照してください。

### フォームでの reCAPTCHA の使用

フォームを作成して reCAPTCHA（非表示）コンポーネントを追加するには、次の手順を実行します。

1. 編集用にユニバーサルエディターでフォームを開きます。
1. コンテンツツリーで、追加した「アダプティブフォーム」セクションに移動します。
1. 「**[!UICONTROL 追加]**」アイコンをクリックし、**アダプティブフォームコンポーネント**&#x200B;リストから **[!UICONTROL CAPTCHA（非表示）]**&#x200B;を追加します。

   ![reCaptcha コンポーネントを追加](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   また、ユニバーサルエディターには直感的なドラッグ＆ドロップ機能が用意されているので、必要なアダプティブフォームコンポーネントをドラッグ＆ドロップすることもできます。

1. **[!UICONTROL CAPTCHA（非表示）]**&#x200B;コンポーネントを追加した後、「**公開**」をクリックしてフォームを再度公開します。

   ![フォームを再公開](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

次の URL で、reCAPTCHA サービスを使用してフォームを表示できるようになりました。
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`。

![reCAPTCHA を使用したフォーム](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## よくある質問

* **ユーザーが reCAPTCHA クラウド設定を作成しない場合はどうなりますか？**

  **回答**：ユーザーが reCAPTCHA クラウド設定を作成しない場合、AEM サーバーはグローバル設定コンテナで reCAPTCHA クラウド設定を検索します。グローバル設定コンテナに設定が存在しない場合、AEM サーバーはエラーをスローします。

* **ユーザーが複数の reCAPTCHA クラウド設定を作成するとどうなりますか？**
  **回答**：ユーザーが複数の reCAPTCHA クラウド設定を作成した場合、最初に作成した reCAPTCHA 設定が自動的に選択されます。

* **公開済みの URL に修正や変更が表示されないのはなぜですか？**
公開済みの URL に修正や変更が表示されない場合は、フォームを再公開して更新を適用します。

* **Edge Delivery Services Forms がサポートする reCAPTCHA サービスはどれですか？**
  **回答**：Edge Delivery Services Forms は、Google が提供するスコアベースの reCAPTCHA サービスのみをサポートします。


## 関連トピック

{{universal-editor-see-also}}

