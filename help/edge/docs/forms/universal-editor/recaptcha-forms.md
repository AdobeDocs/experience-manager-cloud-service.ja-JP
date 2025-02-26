---
title: AEM Forms as a Cloud Service の Edge Delivery Services での reCAPTCHA の使用
description: AEM Forms の Edge Delivery Services 向けフォームでの Google reCAPTCHA の使用
feature: Edge Delivery Services
keywords: フォームの reCAPTCHA、ユニバーサルエディターの reCAPTCHA の使用、フォームの reCAPTCHA の追加
role: Admin, Architect, Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 12%

---


# WYSIWYG オーサリングでの reCAPTCHA の使用

<span class="preview"> この機能は、早期アクセスプログラムを通じて利用できます。 アクセスをリクエストするには、公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に、GitHub の組織名とリポジトリ名を記載したメールを送信します。 例えば、リポジトリ URL がhttps://github.com/adobe/abcの場合、組織名は adobe で、リポジトリ名は abc.</span> です


CAPTCHA （Completely Automated Public Turing test to tell Computers and Humans Apart）は、web サイトを不正行為、スパム、誤用から保護するために使用される一般的なツールです。

例えば、追加の控除と税率に基づいて税金を計算するフォームについて考えてみます。 このような場合は、悪意のあるユーザーがフォームを悪用してフィッシングメールを送信したり、スパムボットを使用して無関係または有害なコンテンツを大量に送信したりするリスクがあります。CAPTCHA の統合により、送信が正規のユーザーによるものであることが確認されるので、スパムエントリを効果的に最小限に抑え、セキュリティを強化できます。

![Google recaptcha](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

Edge Delivery Services Formsでは、フォームブロックを使用すると、[Captcha （非表示） **コンポーネントを使用して ](#connect-forms-with-recaptcha-service-by-google)Google reCAPTCHA をフォームに** 接続）して、人間とボットを区別できます。 この機能は、作成者がフォームをスパムや誤用から保護するのに役立ちます。

## GoogleによるFormsと reCAPTCHA サービスの接続

Edge Delivery Services Formsをオーサリングして、Googleが提供する reCAPTCHA サービスを実装できます。 必要に応じて、Edge Delivery Services Formsに対して、次のいずれかの reCAPTCHA サービスを設定できます。

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> reCAPTCHA の仕組みについて詳しくは、[Google reCAPTCHA](https://developers.google.com/recaptcha/) を参照してください。

### reCAPTCHA Enterprise の設定

reCAPTCHA Enterprise は、Googleが提供する、プレミアムでエンタープライズクラスの不正検知および防止サービスです。 reCAPTCHA （スコアベース）の基盤の上に構築されますが、ビジネスの複雑なニーズを満たすための追加の機能、スケーラビリティ、カスタマイズを提供します。

#### 始める前に

Edge Delivery Services Forms用にGoogle reCAPTCHA Enterprise を設定する前に、次の手順を完了していることを確認してください。

1. [Google Cloud プロジェクトを作成または選択し ](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin)[ プロジェクト ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) を取得します。

1. Google Cloud プロジェクトの [reCAPTCHA Enterprise API を有効にする ](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) と [API キーを作成する ](https://console.cloud.google.com/apis/credentials) を行います。

1. Google Cloud プロジェクトの [ サイトキー ](https://console.cloud.google.com/security/recaptcha) を作成し、サイトキーをコピーします。

これらの資格情報を取得したら、フォームの reCAPTCHA Enterprise の設定に進むことができます。

1. [クラウド設定コンテナの作成](#1-create-cloud-configuration-container)
1. [reCAPTCHA Enterprise のクラウドサービス設定の作成](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. クラウド設定コンテナの作成

クラウド設定コンテナを作成するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. **[!UICONTROL ツール]** ![tools-1](/help/forms/assets/tools-1.png)/**[!UICONTROL 一般]**/**[!UICONTROL 設定ブラウザー]** に移動します。

   ![ クラウド設定コンテナ ](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. **[!UICONTROL 設定ブラウザー]** でフォームに移動し、「**[!UICONTROL プロパティ]**」を選択します。

   ![ クラウド設定プロパティ ](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. **[!UICONTROL 設定プロパティ]**&#x200B;ダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。

1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

   ![ クラウド設定プロパティの有効化 ](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
&#39;
クラウド設定コンテナを作成したら、それを公開します。

   ![ パブリッシュクラウド設定 ](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. reCAPTCHA Enterprise のクラウドサービス設定を作成する

reCAPTCHA Enterprise のクラウドサービス設定を作成するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. **[!UICONTROL Tools]** ![tools-1](/help/forms/assets/tools-1.png) / **[!UICONTROL Cloud Services]** / **[!UICONTROL reCAPTCHA]** に移動します。

   ![Recaptcha クラウド設定 ](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   **設定** ダイアログが開きます。

1. フォームに移動し、「**[!UICONTROL 作成]**」を選択します。

   ![Captcha 設定 ](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   **[!UICONTROL reCAPTCHA 設定を作成]** ダイアログが開きます。

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. バージョンを [!DNL ReCAPTCHA Enterprise] として選択し、タイトル、名前、プロジェクト ID、サイトキー、API キーを指定します。

   >[!NOTE]
   >
   > プロジェクト ID、サイトキー、API キーは、reCAPTCHA Enterprise の [ 事前準備 ](#before-you-start) セクションから取得できます。

1. **[!UICONTROL キータイプ]** を **スコアベースのサイトキー** として選択します。
1. を指定します。 [0 ～ 1 の範囲のしきい値スコア](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores). スコアがしきい値スコア以上の場合は、人間による操作が識別され、それ以外の場合は、ボットの操作と見なされます。
1. 「**[!UICONTROL 作成]**」を選択して、クラウドサービス設定を作成します。

   reCAPTCHA クラウド設定を作成したら、公開します。

   ![Recaptcha 設定の公開 ](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

これで、フォームを作成または編集し、WYSIWYG ベースのオーサリングを使用して reCAPTCHA コンポーネントを追加できます。 Google reCAPTCHA をフォームに統合する手順について詳しくは、[ フォームでの reCAPTCHA の使用 ](#use-recaptcha-in-your-form) を参照してください。

## reCAPTCHA の設定

reCAPTCHA は、web サイトがボットやスパムなどの悪用されるトラフィックを検出して防ぐためにGoogleが提供する無料サービスです。 バックグラウンドで動作し、各ユーザーインタラクションにリスクスコア（0.0 ～ 1.0 の範囲）を割り当てるスコアベースバージョンをサポートしています。 スコアがしきい値スコア以上の場合は、人間による操作が識別され、それ以外の場合は、ボットの操作と見なされます。

#### 始める前に

Edge Delivery Services Forms用にGoogle reCAPTCHA を設定する前に、[reCAPTCHA API キーペアをGoogle コンソールから取得 ](https://www.google.com/recaptcha/admin) ます。 ペアには、サイトキーと秘密鍵が含まれます。

>[!NOTE]
>
> * Edge Delivery Services Formsは、**reCAPTCHA スコアベース** バージョンのみをサポートします。

API キーペアを取得したら、フォームの reCAPTCHA の設定に進むことができます。

1. [クラウド設定コンテナの作成](#1-create-cloud-configuration-container-1)
1. [reCAPTCHA のクラウドサービス設定の作成](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. クラウド設定コンテナの作成

クラウド設定コンテナを作成するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. **[!UICONTROL ツール]** ![tools-1](/help/forms/assets/tools-1.png)/**[!UICONTROL 一般]**/**[!UICONTROL 設定ブラウザー]** に移動します。

   ![ クラウド設定コンテナ ](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. **[!UICONTROL 設定ブラウザー]** でフォームに移動し、「**[!UICONTROL プロパティ]**」を選択します。

   ![ クラウド設定プロパティ ](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. **[!UICONTROL 設定プロパティ]**&#x200B;ダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。

1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

   ![ クラウド設定プロパティの有効化 ](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   クラウド設定コンテナを作成したら、それを公開します。

   ![ パブリッシュクラウド設定 ](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. reCAPTCHA のクラウドサービス設定を作成する

reCAPTCHA のクラウドサービス設定を作成するには、次の手順を実行します。

1. オーサーインスタンスにログインします。
1. **[!UICONTROL Tools]** ![tools-1](/help/forms/assets/tools-1.png) / **[!UICONTROL Cloud Services]** / **[!UICONTROL reCAPTCHA]** に移動します。

   ![Recaptcha クラウド設定 ](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   **設定** ダイアログが開きます。

1. フォームに移動し、「**[!UICONTROL 作成]**」を選択します。

   ![Captcha 設定 ](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   **[!UICONTROL reCAPTCHA 設定を作成]** ダイアログが開きます。

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. バージョンを [!DNL ReCAPTCHA v2] として選択し、タイトルと名前を指定します。
1. サイトキーと秘密鍵を指定します。

   >[!NOTE]
   >
   > サイトキーと秘密鍵は、reCAPTCHA の [ 始める前に ](#before-you-begin) セクションから取得できます。

1. 「**[!UICONTROL 作成]**」を選択して、クラウドサービス設定を作成します。

   reCAPTCHA クラウド設定を作成したら、公開します。

   ![Recaptcha 設定の公開 ](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

これで、フォームを作成および編集し、WYSIWYG ベースのオーサリングを使用して reCAPTCHA コンポーネントを追加できます。 Google reCAPTCHA をフォームに統合する手順について詳しくは、[ フォームでの reCAPTCHA の使用 ](#use-recaptcha-in-your-form) を参照してください。

### フォームでの reCAPTCHA の使用

フォームを作成して reCAPTCHA （非表示）コンポーネントを追加するには、次の手順を実行します。

1. 編集用にユニバーサルエディターでフォームを開きます。
1. コンテンツツリーで、追加した「アダプティブフォーム」セクションに移動します。
1. **[!UICONTROL 追加]** アイコンをクリックし、**[!UICONTROL アダプティブフォームコンポーネント** リストから ]**Captcha （非表示）** コンポーネントを追加します。

   ![reCaptcha コンポーネントの追加 ](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   ユニバーサルエディターには直感的なドラッグ&amp;ドロップ機能があるので、必要なアダプティブ Forms コンポーネントをドラッグ&amp;ドロップすることもできます。

1. **公開** をクリックして、**[!UICONTROL Captcha （非表示）]** コンポーネントを追加した後でフォームを再度公開します。

   ![ フォームの再公開 ](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

次の URL で、reCAPTCHA サービスを使用してフォームを表示できるようになりました。
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`。

![reCAPTCHA を使用したフォーム ](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## よくある質問

* **ユーザーが reCAPTCHA クラウド設定を作成しない場合はどうなりますか？**

  **A**：ユーザーが reCAPTCHA クラウド設定を作成しない場合、AEM サーバーはグローバル設定コンテナで reCAPTCHA クラウド設定を検索します。 グローバル設定コンテナに設定が存在しない場合、AEM サーバーはエラーをスローします。

* **ユーザーが複数の reCAPTCHA クラウド設定を作成するとどうなりますか？**
  **A**：ユーザーが複数の reCAPTCHA クラウド設定を作成した場合、最初に作成された reCAPTCHA 設定が自動的に選択されます。

* **公開済みの URL に変更や変更が表示されないのはなぜですか？**
公開済み URL に変更や変更が表示されない場合は、フォームが再公開されていることを確認して更新を適用してください。

* **Edge Delivery Services Formsがサポートする reCAPTCHA サービスはどれですか？**
  **A**:Edge Delivery Services Formsは、Googleが提供するスコアベースの reCAPTCHA サービスのみをサポートします。


## 関連トピック

{{universal-editor-see-also}}

