---
title: フォームビルダー：コアコンポーネントを使用したフォームの作成
description: AEM Formsのフォームビルダーを使用して、コアコンポーネントを含むアダプティブフォームを作成する方法を説明します。 情報の収集および処理を合理化するレスポンシブなHTML5 フォームを必要とするフォーム作成者に最適です。
keywords: フォームビルダー，コアコンポーネント，フォームを作成，フォーム作成者，アダプティブフォーム，作成フォーム，AEM forms, レスポンシブフォーム
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '2352'
ht-degree: 88%

---

# フォームビルダー：コアコンポーネントを使用したフォームの作成 {#creating-an-adaptive-form-core-components}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-an-adaptive-form-core-components.html?lang=ja) |
| AEM as a Cloud Service | この記事 |


AEM Formsのフォームビルダーを使用すると、魅力的でレスポンシブ、かつ動的でアダプティブなフォームを作成できます。 プロフェッショナルなフォームを作成するフォーム作成者であっても、レスポンシブフォームをすばやく作成する必要があるフォーム作成者であっても、AEM Formsは使いやすいウィザードを提供します。 このウィザードはクイックタブナビゲーションを備えており、事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択できます。

開始する前に、使用可能な Forms コンポーネントのタイプについて学習します。

* [アダプティブフォームコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)：標準化されたデータキャプチャコンポーネントです。 これらのコンポーネントは、デジタル登録エクスペリエンスのカスタマイズ機能を提供し、開発時間を短縮し、メンテナンスコストを削減します。 開発者は、これらのコンポーネントを簡単にカスタマイズし、スタイルを設定できます。 アドビでは、これらの最新かつ拡張性の高いコンポーネントを活用してアダプティブフォームを開発することをお勧めします。

* [アダプティブフォーム基盤コンポーネント](creating-adaptive-form.md)：従来の（古い）データキャプチャコンポーネントです。 引き続きこれらを使用して、既存の基盤コンポーネントベースのアダプティブフォームを編集できます。 新しいフォームを作成する場合は、[アダプティブフォームコアコンポーネント](creating-adaptive-form-core-components.md)を使用してアダプティブフォームを作成することをお勧めします。

![アダプティブフォームの作成ウィザード](/help/release-notes/assets/wizard.png)


## 前提条件

アダプティブフォームを作成するには、以下が必要です。



* **アダプティブフォームテンプレート**：テンプレートは基本構造を提供し、アダプティブフォームのアピアランス（レイアウトとスタイル）を定義します。 これには、特定のプロパティやコンテンツ構造を有するフォーマット済みのコンポーネントが含まれます。 また、テーマと送信アクションを定義するオプションも提供されます。 テーマは、ルックアンドフィールと送信アクションを定義し、アダプティブフォームの送信時に実行するアクションを定義します。 例えば、収集したデータをデータソースに送信する場合などです。 クラウドサービスでは、空白という名前の OOTB テンプレートが提供されます。

   * `blank` テンプレートは、すべての新しい AEM Forms as a Cloud Service プログラムに含まれています。
   * パッケージマネージャーを使用して参照パッケージをインストールし、AEM Forms as a Cloud Service プログラムに `blank` テンプレートを追加できます。
   * 最初から[アダプティブフォームテンプレート（コアコンポーネント）を作成](/help/forms/template-editor-core-components.md)することもできます。
   * また、[サンプルテンプレート](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=ja)を環境にデプロイできます。 これらは、フォームの作成を迅速に開始するのに役立ちます。

* **アダプティブフォームのテーマ**：テーマには、コンポーネントとパネル向けのスタイル設定の詳細が含まれます。 スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。 テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。  `Canvas` テンプレートは、すべての新しい AEM Forms as a Cloud Service プログラムに含まれています。 また、[サンプルテーマ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=ja)を環境にデプロイできます。 これらは、フォームのスタイル設定を開始できるようサポートし、ビジネス要件に応じてテーマを作成またはカスタマイズするための基本構造を提供します。

  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create an Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **権限**：[!DNL forms-users] グループにユーザーを追加します。 [!DNL forms-users] グループのメンバーには、アダプティブフォームを作成する権限があります。 フォーム専用のユーザーグループの詳細なリストについて詳しくは、[グループと権限](forms-groups-privileges-tasks.md)を参照してください。

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## アダプティブフォームの作成  {#create-an-adaptive-form-core-components}

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。 Cloud インスタンスまたはローカル開発インスタンスの場合があります。

1. Experience Manager のログインページに資格情報を入力します。 ログイン後、左上隅の **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 ウィザードが開きます。 ソースタブで、テンプレートを選択します。

   ![コアコンポーネントテンプレート](/help/forms/assets/core-components-template.png)

   テンプレートを選択すると、テンプレートで指定されたテーマと送信アクションが自動的に選択され、**[!UICONTROL 作成]** ボタンが有効になります。 「**[!UICONTROL スタイル]**」または「**[!UICONTROL 送信]**」タブを使用して、別のテーマや送信アクションを選択することができます。 選択したテンプレートでテーマが指定されていない場合、作成ボタンは無効のままです。 「**[!UICONTROL スタイル]**」タブに進み、テーマを手動で選択することができます。

   >[!NOTE]
   >
   >
   > ご利用の環境に&#x200B;**アダプティブフォーム（コアコンポーネント）**&#x200B;テンプレートがない場合は、[ご利用の環境のアダプティブフォームコアコンポーネントを有効にします](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project)。 ご利用の環境でコアコンポーネントを有効にすると、**アダプティブフォーム（コアコンポーネント）**&#x200B;テンプレートが環境に追加されます。

1. 「**[!UICONTROL スタイル]**」タブで、テーマを選択します。

   * 選択したテンプレートでテーマを指定すると、ウィザードでテーマが自動的に選択されます。 「スタイル」タブから別のテーマを選択することもできます。

   * 選択したテンプレートにテーマが指定されていない場合は、「スタイル」タブを使用してテーマを選択することができます。 この「**[!UICONTROL 作成]**」ボタンは、テーマが選択された後にのみ有効になります。

1. （オプション）「データ」タブで、データモデルを選択します。

   * **フォームデータモデル（FDM）**：[フォームデータモデル](data-integration.md)を使用すると、異なるデータソースのエンティティやサービスをアダプティブフォームに統合することができます。 作成するアダプティブフォームで、複数のデータソースに対するデータの取得と書き込みが必要になる場合は、フォームデータモデル（FDM）を選択します。

   * **JSON スキーマ**：[JSON スキーマ](adaptive-form-json-schema-form-model.md) コアコンポーネントベースのアダプティブフォームは、生成または消費されるデータの構造を表す JSON スキーマを関連付ける機能により、自社のバックエンドシステムとシームレスに統合できます。 この関連付けにより、作成者はスキーマの要素を使用して、アダプティブフォームにコンテンツを動的に追加できます。 スキーマの要素には、オーサリングプロセスでコンテンツブラウザーの「データモデルオブジェクト」タブから容易にアクセスできます。すべてのフィールドは、作成されたアダプティブフォームに自動的に追加されます。

   デフォルトでは、関連付けられた JSON スキーマのすべてのフィールドが自動的に選択され、対応するアダプティブフォームコンポーネントに変換されるので、オーサリングプロセスを合理化できます。 ウィザードでは、チェックボックスを使用してアダプティブフォームに含めるフィールドを選択できる、さらに便利な機能が用意されています。

1. 「**[!UICONTROL 送信]**」タブで、送信アクションを選択します。

   * テンプレートを選択すると、テンプレートで指定された送信アクションが自動選択されます。 「送信」タブから、別の送信アクションを選択することができます。 「**[!UICONTROL 送信]**」タブには、使用可能なすべての送信アクションが表示されます。

   * 選択したテンプレートで送信アクションが指定されていない場合は、「**[!UICONTROL 送信]**」タブを使用して送信アクションを選択することができます

1. （オプション）「**[!UICONTROL 配信]**」タブで、アダプティブフォームの公開日または非公開日を指定することができます。

1. 「**[!UICONTROL 作成]**」を選択します。 アダプティブフォームを保存するためのタイトル、名前および場所を指定するためのダイアログが表示されます。

   * **[!UICONTROL タイトル]**：フォームの表示名を指定します。 タイトルを指定すると、[!DNL Experience Manager Forms] ユーザーインターフェイス内のフォームを特定しやすくなります。
   * **[!UICONTROL 名前：]**&#x200B;フォームの名前を指定します。 指定された名前のノードがリポジトリーに作成されます。 タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。 候補として入力された値は変更可能です。 「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。 無効な入力は、すべてハイフンに置き換えられます。
   * **[!UICONTROL パス]**：アダプティブフォームを保存する場所を指定します。 アダプティブフォームは、`/content/dam/formsanddocuments` に直接保存することができます。または、`/content/dam/formsanddocuments/adaptiveforms` などのフォルダーを作成して、アダプティブフォームを保存することができます。 フォルダーをパスで使用する前に、必ずフォルダーを作成してください。 「**[!UICONTROL パス]**」フィールドでは、フォルダーは自動的には作成されません。

1. 「**[!UICONTROL 作成]**」を選択します。 アダプティブフォームが作成され、アダプティブフォームエディターで開きます。 エディターに、テンプレートで使用可能なコンテンツが表示されます。  アダプティブフォームのタイプに応じて、関連する <!--XFA form template, XML schema or --> JSON スキーマまたはフォームデータモデル（FDM）に存在するフォーム要素が、サイドバーの&#x200B;**[!UICONTROL コンテンツブラウザー]**&#x200B;の「**[!UICONTROL データモデルオブジェクト]**」タブに表示されます。 これらの要素もドラッグ＆ドロップしてアダプティブフォームを作成できます。

これで、[アダプティブフォームのコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)をアダプティブフォームのコンテナにドラッグ＆ドロップし、フォームをデザインおよび作成できます。 また、[https://aemcomponents.dev/](https://aemcomponents.dev/) では、使用可能なコアコンポーネントの動作を確認できます。

>[!NOTE]
>
> また、[XFA フォームテンプレート（*.XDP ファイル）を使用してアダプティブフォームを作成](/help/forms/create-adaptive-form-using-xfa-templates.md)することもできます。 これにより、XDP ファイルのフィールドをアダプティブフォームで直接再利用して、時間を節約できます。

## アダプティブフォームの送信アクションの設定 {#configure-submit-action-for-form}

送信アクションを使用すると、アダプティブフォーム経由で取り込んだデータの送信先を選択できます。 送信アクションは、ユーザーがアダプティブフォームの「送信」ボタンをクリックするとトリガーされます。 アダプティブフォームには、すぐに使用できる送信アクションがいくつか含まれています。 デフォルトの送信アクションを拡張して、独自のカスタム送信アクションを作成することもできます。 フォームの送信アクションを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。

1. 「**[!UICONTROL 送信]**」タブをクリックします。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、送信アクションを設定します](/help/forms/assets/adaptive-forms-submit-message.png)

1. 必要に応じて、**[!UICONTROL 送信アクション]**&#x200B;を選択して設定します。 送信アクションについて詳しくは、[アダプティブフォームの送信アクション](/help/forms/configuring-submit-actions.md)を参照してください。

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## ユーザーをページにリダイレクトするか、フォーム送信時にお礼のメッセージを表示

フォームの送信時に、ユーザーを別の web ページまたはメッセージにリダイレクトできます。 ユーザーをリダイレクトするか、お礼のメッセージを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブを開きます。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、リダイレクトページまたはお礼のメッセージを設定](/help/forms/assets/adaptive-forms-redirect-message.png)

   * リダイレクト URL を設定するには、「送信」オプションで、「**[!UICONTROL URL にリダイレクト]**」オプションを選択し、AEM Sites ページを参照して選択するか、外部ページの URL を指定します。

   * カスタムメッセージまたはお礼のメッセージを設定するには、「送信」オプションで「**[!UICONTROL メッセージを表示]**」オプションを選択し、**[!UICONTROL メッセージコンテンツ]**&#x200B;ボックスにメッセージを入力します。 これはリッチテキストボックスで、全画面表示オプションを使用して、使用可能なすべてのリッチテキスト項目を表示できます。

## アダプティブフォームのスキーマまたはフォームデータモデル（FDM）の設定{#configure-schema-or-data-model-for-form}

フォームデータモデル（FDM）を使用してフォームをデータソースに接続し、ユーザーのアクションに基づいてデータを送受信することができます。 また、フォームを JSON スキーマに接続して、送信されたデータを事前に定義した形式で受信することもできます。 要件に基づいて、次のようにフォームを JSON スキーマまたはフォームデータモデル（FDM）に接続します。

* [JSON スキーマを作成して環境にアップロード](/help/forms/adaptive-form-json-schema-form-model.md)
* [フォームデータモデル（FDM）の作成](/help/forms/create-form-data-models.md)

### フォームの JSON スキーマまたはフォームデータモデル（FDM）の設定

フォームの JSON スキーマまたはフォームデータモデル（FDM）を設定するには：

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL データモデル]**」タブを開きます。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、JSON スキーマまたはフォームデータモデル（FDM）を設定する](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 要件に応じて、JSON スキーマまたはフォームデータモデル（FDM）を選択し、設定します。

   * 「**[!UICONTROL フォームモデル]**」オプションを選択する場合は、「**[!UICONTROL フォームデータモデルを選択]**」オプションを使用して、事前設定済みのフォームデータモデル（FDM）を選択します。
   * 「**[!UICONTROL スキーマ]**」オプションを選択する場合は、「**[!UICONTROL スキーマ]**」オプションを使用して、フォームの JSON スキーマを選択します。

1. 「**[!UICONTROL 完了]**」をクリックします。

## 事前入力サービスを設定  {#configure-prefill-service-for-form}

事前入力サービスを使用すると、既存のデータを使用してアダプティブフォームのフィールドに自動入力できます。 ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。 次の操作を実行できます。

* [カスタム事前入力サービスを作成](/help/forms/prepopulate-adaptive-form-fields.md)
* [フォームデータモデルの事前入力サービスを使用](#fdm-prefill-service)

### フォームデータモデル事前入力サービスを使用した、アダプティブフォームのフィールドの事前入力 {#fdm-prefill-service}

フォームデータモデルの事前入力サービスでは、フォームデータモデル事前入力サービス、またはカスタムの事前入力サービスを使用して、アダプティブフォームのフィールドに事前入力できます。 フォームデータモデルの事前入力サービスでは、[設定済みのフォームデータモデルのサービスを取得](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)を使用して、データを取得します。 アダプティブフォームでフォームデータモデルの事前入力サービスを使用するには、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/assets/configure-icon.svg)アイコン）をクリックします。 データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、リダイレクトページまたはお礼のメッセージを設定](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. フォームデータモデル（FDM）を選択します。 「**[!UICONTROL 基本]**」タブを開きます。 事前入力サービスで、「**[!UICONTROL フォームデータモデルの事前入力サービス]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。 これで、アダプティブフォームがフォームデータモデルの事前入力を使用するように設定されました。 [ルールエディター](rule-editor.md)を使用して、フォームのフィールドに事前入力するルールを作成できるようになりました。

## アダプティブフォームのフォームモデルプロパティの編集 {#edit-form-model}

1. アダプティブフォームを選択し、![ページ情報](/help/forms/assets/Smock_Properties_18_N.svg)／**[!UICONTROL プロパティを開く]**&#x200B;をクリックします。 フォームプロパティページが開きます。

1. 「**[!UICONTROL フォームモデル]**」タブをクリックし、フォームモデルを選択します。 アダプティブフォームにフォームモデルがない場合は、JSON スキーマまたはフォームデータモデル（FDM）を選択できます。 一方、アダプティブフォームが既にフォームモデルに基づいている場合は、同じタイプの別のフォームモデルに切り替えることもできます。 例えば、フォームが JSON スキーマを使用している場合、別の JSON スキーマに容易に切り替えることができます。同様に、フォームがフォームデータモデル（FDM）を使用している場合は、別のフォームデータモデル（FDM）に切り替えることができます。

1. 「**[!UICONTROL 保存]**」を選択して、プロパティを保存します。


## AEM アダプティブフォームの名前を変更する方法 {#rename-an-AEM-Adaptive-Form}

アダプティブフォームの名前を変更するには、次の手順を実行します。

1. AEM Forms ユーザーインターフェイスでアダプティブフォームを選択します。
1. 上部パネルにある「**プロパティ**」をクリックします。
1. 下の画像に示すように、「**タイトル**」タブでフォームの名前を変更します。
1. 「**保存して閉じる**」をクリックします。

![AEM アダプティブフォームの名前を変更](/help/forms/assets/change-af-name.png)



## 適用性とユースケース

### 保険

## AEM Formsは、顧客向けのプロセスと内部保険プロセスの両方で使用できますか？

はい。AEM Formsは、顧客向けのデジタルフォームに加えて、レビュー、承認、支援を受けたデータキャプチャなど、社内、スタッフ、またはエージェント主導のプロセスをサポートします。

## 保険金請求の送信にAEM Formsを使用できますか？

はい。AEM Formsでは、構造化データの取得やサポートドキュメントの取得など、保険契約者が保険金請求をデジタル送信できる複数ステップのアダプティブフォームをサポートしています。

## AEM Formsはモバイル保険金請求をサポートしていますか？

はい。AEM Formsは、レスポンシブでモバイルに適したフォームをサポートしており、お客様やエージェントがモバイルデバイスから保険情報を送信できます。
