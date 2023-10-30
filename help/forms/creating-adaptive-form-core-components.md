---
title: コアコンポーネントに基づくアダプティブフォームの作成方法
description: ' [!DNL Experience Manager Forms] を使用したアダプティブフォームの作成方法を説明します。アダプティブフォームは、情報の収集および処理を合理化するレスポンシブ HTML5 フォームです。フォームデータモデルと XML または JSON スキーマに基づいてアダプティブフォームを作成する方法について詳しく調べます。'
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 397e7d4f23202b8ae7419b0ad5436a6a10e2efb8
workflow-type: tm+mt
source-wordcount: '2303'
ht-degree: 75%

---

# アダプティブフォームを作成 {#creating-an-adaptive-form-core-components}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-an-adaptive-form-core-components.html) |
| AEM as a Cloud Service | この記事 |


アダプティブフォームを使用すると、魅力的でレスポンシブ、かつ動的でアダプティブなフォームを作成できます。AEM Formsは、アダプティブFormsをすばやく作成するための、ビジネスに適したウィザードを提供します。 このウィザードはクイックタブナビゲーションを備えており、アダプティブフォームを作成するための事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択することができます。

開始する前に、使用可能な Forms コンポーネントのタイプについて学習します。

* [アダプティブフォームコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)：標準化されたデータキャプチャコンポーネントです。これらのコンポーネントは、デジタル登録エクスペリエンスのカスタマイズ機能を提供し、開発時間を短縮し、メンテナンスコストを削減します。開発者は、これらのコンポーネントを簡単にカスタマイズし、スタイルを設定できます。これらの最新かつ拡張性の高いコンポーネントを活用してアダプティブフォームを開発することをお勧めします。

* [アダプティブフォーム基盤コンポーネント](creating-adaptive-form.md)：従来の（古い）データキャプチャコンポーネントです。引き続きこれらを使用して、既存の基盤コンポーネントベースのアダプティブフォームを編集できます。 新しいフォームを作成する場合は、[アダプティブフォームコアコンポーネント](creating-adaptive-form-core-components.md)を使用してアダプティブフォームを作成することをお勧めします。

![アダプティブフォームの作成ウィザード](/help/release-notes/assets/wizard.png)


## 前提条件

アダプティブフォームを作成するには、以下が必要です。

* **お使いの環境でアダプティブフォームズコアコンポーネントを有効化**：新しいプログラムを作成すると、アダプティブコアコンポーネントはお使いの環境で既に有効になっています。アーキタイプ 39 以前に基づくFormsas a Cloud Service環境がある場合、 [環境でのアダプティブFormsコアコンポーネントの有効化](enable-adaptive-forms-core-components.md). ご利用の環境でコアコンポーネントを有効にすると、**アダプティブフォーム（コアコンポーネント）**&#x200B;のテンプレートとキャンバステーマが環境に追加されます。AEM SDK バージョンが 2023.02.0 より前の場合は、2023.02.0 リリースより前にアダプティブフォームのコアコンポーネントがプレリリースの一部であったので、[お使いの環境で `prerelease` フラグが有効になっていることを確認してください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features)。

* **アダプティブフォームテンプレート**：テンプレートは基本構造を提供し、アダプティブフォームのアピアランス（レイアウトとスタイル）を定義します。これには、特定のプロパティやコンテンツ構造を有するフォーマット済みのコンポーネントが含まれます。また、テーマと送信アクションを定義するオプションも提供されます。 テーマは、ルックアンドフィールと送信アクションを定義し、アダプティブフォームの送信時に実行するアクションを定義します。 例えば、収集したデータをデータソースに送信する場合などです。 クラウドサービスでは、空白という名前の OOTB テンプレートが提供されます。

   * `blank` テンプレートは、すべての新しい AEM Forms as a Cloud Service プログラムに含まれています。
   * パッケージマネージャーを使用して参照パッケージをインストールし、AEM Forms as a Cloud Service プログラムに `blank` テンプレートを追加できます。
   * 最初から[新しいアダプティブフォームテンプレート（コアコンポーネント）を作成する](/help/forms/template-editor-core-components.md)こともできます。
   * また、 [サンプルテンプレート](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) を環境に追加します。 これらは、フォームの作成を迅速に開始するのに役立ちます。

* **アダプティブフォームのテーマ**：テーマには、コンポーネントとパネル向けのスタイル設定の詳細が含まれます。 スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。`Canvas` テンプレートは、すべての新しい AEM Forms as a Cloud Service プログラムに含まれています。また、 [サンプルテーマ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) を環境に追加します。 これらは、フォームのスタイル設定を開始し、ビジネス要件に応じてテーマを作成またはカスタマイズするための基本構造を提供します。

  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **権限**：[!DNL forms-users] グループにユーザーを追加します。[!DNL forms-users] グループのメンバーには、アダプティブフォームを作成する権限があります。フォーム固有のユーザーグループの詳細なリストについては、 [グループと権限](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## アダプティブフォームを作成  {#create-an-adaptive-form-core-components}

1. にログインします。 [!DNL Experience Manager Forms] オーサーインスタンス。 Cloud インスタンスまたはローカル開発インスタンスの場合があります。

1. Experience Manager のログインページに資格情報を入力します。ログイン後、左上隅の **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;をタップします。

1. 「**[!UICONTROL 作成]**」をタップして、「**[!UICONTROL アダプティブフォーム]**」を選択します。ウィザードが開きます。ソースタブで、テンプレートを選択します。

   ![コアコンポーネントテンプレート](/help/forms/assets/core-components-template.png)

   テンプレートを選択すると、テンプレートで指定されたテーマと送信アクションが自動的に選択され、**[!UICONTROL 作成]** ボタンが有効になります。「**[!UICONTROL スタイル]**」または「**[!UICONTROL 送信]**」タブを使用して、別のテーマや送信アクションを選択することができます。 選択したテンプレートでテーマが指定されていない場合、作成ボタンは無効のままです。「**[!UICONTROL スタイル]**」タブに進み、テーマを手動で選択することができます。

   >[!NOTE]
   >
   >
   > ご利用の環境に&#x200B;**アダプティブフォーム（コアコンポーネント）**&#x200B;テンプレートがない場合は、[ご利用の環境のアダプティブフォームコアコンポーネントを有効にします](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project)。ご利用の環境でコアコンポーネントを有効にすると、**アダプティブフォーム（コアコンポーネント）**&#x200B;テンプレートが環境に追加されます。

1. 「**[!UICONTROL スタイル]**」タブで、テーマを選択します。

   * 選択したテンプレートでテーマを指定すると、ウィザードでテーマが自動的に選択されます。 「スタイル」タブから別のテーマを選択することもできます。

   * 選択したテンプレートにテーマが指定されていない場合は、「スタイル」タブを使用してテーマを選択することができます。 この「**[!UICONTROL 作成]**」ボタンは、テーマが選択された後にのみ有効になります。

1. （オプション）「データ」タブで、データモデルを選択します。

   * **フォームデータモデル**：[フォームデータモデル](data-integration.md)を使用すると、異なるデータソースのエンティティやサービスをアダプティブフォームに統合することができます。 作成するアダプティブフォームで、複数のデータソースに対するデータの取得と書き込みが必要になる場合は、フォームデータモデルを選択します。

   * **JSON スキーマ**：[JSON スキーマ](adaptive-form-json-schema-form-model.md) コアコンポーネントベースのアダプティブフォームは、生成または消費されるデータの構造を表す JSON スキーマを関連付ける機能により、自社のバックエンドシステムとシームレスに統合できます。この関連付けにより、作成者はスキーマの要素を使用して、アダプティブフォームにコンテンツを動的に追加できます。スキーマの要素には、オーサリングプロセス中にコンテンツブラウザーの「データモデルオブジェクト」タブから簡単にアクセスでき、すべてのフィールドが新しく作成されたアダプティブフォームに自動的に追加されます。

   デフォルトでは、関連付けられた JSON スキーマのすべてのフィールドが自動的に選択され、対応するアダプティブフォームコンポーネントに変換されるので、オーサリングプロセスを合理化できます。ウィザードでは、チェックボックスを使用してアダプティブフォームに含めるフィールドを選択できる、さらに便利な機能が用意されています。

1. 「**[!UICONTROL 送信]**」タブで、送信アクションを選択します。

   * テンプレートを選択すると、テンプレートで指定された送信アクションが自動選択されます。 「送信」タブから、別の送信アクションを選択することができます。 「**[!UICONTROL 送信]**」タブには、使用可能なすべての送信アクションが表示されます。

   * 選択したテンプレートで送信アクションが指定されていない場合は、「**[!UICONTROL 送信]**」タブを使用して送信アクションを選択することができます

1. （オプション）「**[!UICONTROL 配信]**」タブで、アダプティブフォームの公開日または非公開日を指定することができます。

1. 「**[!UICONTROL 作成]**」をタップします。アダプティブフォームを保存するためのタイトル、名前および場所を指定するためのダイアログが表示されます。

   * **[!UICONTROL タイトル]**：フォームの表示名を指定します。タイトルを指定すると、[!DNL Experience Manager Forms] ユーザーインターフェイス内のフォームを特定しやすくなります。
   * **[!UICONTROL 名前：]**&#x200B;フォームの名前を指定します。指定された名前のノードがリポジトリーに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。無効な入力は、すべてハイフンに置き換えられます。
   * **[!UICONTROL パス]**：アダプティブフォームを保存する場所を指定します。 アダプティブフォームは、`/content/dam/formsanddocuments` に直接保存することができます。または、`/content/dam/formsanddocuments/adaptiveforms` などのフォルダーを作成して、アダプティブフォームを保存することができます。フォルダーをパスで使用する前に、必ずフォルダーを作成してください。 「**[!UICONTROL パス]**」フィールドでは、フォルダーは自動的には作成されません。

1. 「**[!UICONTROL 作成]**」をタップします。アダプティブフォームが作成され、アダプティブフォームエディターで開かれます。 エディターに、テンプレートで使用可能なコンテンツが表示されます。 アダプティブフォームのタイプに応じて、関連する <!--XFA form template, XML schema or --> JSON スキーマまたはフォームデータモデルに存在するフォーム要素が、サイドバーの&#x200B;**[!UICONTROL コンテンツブラウザ]**&#x200B;の「**[!UICONTROL データモデルオブジェクト]**」タブに表示されます。これらの要素もアドラッグ＆ドロップしてダプティブフォームを作成できます。

これで、 [アダプティブFormsコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) をアダプティブFormsコンテナに追加して、フォームをデザインし作成します。 また、[https://aemcomponents.dev/](https://aemcomponents.dev/) では、使用可能なコアコンポーネントの動作を確認できます。

## アダプティブフォームの送信アクションの設定 {#configure-submit-action-for-form}

送信アクションを使用すると、アダプティブフォームから取り込んだデータの送信先を選択できます。 送信アクションは、ユーザーがアダプティブフォームの「送信」ボタンをクリックするとトリガーされます。アダプティブフォームには、すぐに使用できる送信アクションがいくつか含まれています。デフォルトの送信アクションを拡張して、独自のカスタム送信アクションを作成することもできます。フォームの送信アクションを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、「 **[!UICONTROL ガイドコンテナ]** アダプティブフォームのコンポーネント
1. ガイドコンテナのプロパティをクリックします。 ![ガイドのプロパティ](/help/forms/assets/configure-icon.svg) アイコン。 アダプティブフォームコンテナダイアログボックスが開きます。

1. 次をクリック：  **[!UICONTROL 送信]** タブをクリックします。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、送信アクションを設定します](/help/forms/assets/adaptive-forms-submit-message.png)

1. を選択して設定します。 **[!UICONTROL 送信アクション]**、要件に応じて。 送信アクションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configuring-submit-actions.md)を参照してください。

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## フォーム送信時に、ユーザーをページにリダイレクトする、またはお礼のメッセージを表示する

フォームの送信時に、ユーザーを別の web ページまたはメッセージにリダイレクトできます。ユーザーをリダイレクトするか、お礼のメッセージを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、「 **[!UICONTROL ガイドコンテナ]** アダプティブフォームのコンポーネント
1. ガイドコンテナのプロパティをクリックします。 ![ガイドのプロパティ](/help/forms/assets/configure-icon.svg) アイコン。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブを開きます。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、リダイレクトページまたは「ありがとうございます」メッセージを設定します。](/help/forms/assets/adaptive-forms-redirect-message.png)

   * リダイレクト URL を設定するには、「送信時」オプションで、 **[!UICONTROL URL にリダイレクト]** 」オプションを選択し、AEM Sitesページを参照して選択するか、外部ページの URL を指定します。

   * カスタムメッセージまたは「ありがとうございます」メッセージを設定するには、「送信」オプションで、 **[!UICONTROL メッセージを表示]** オプションを選択し、 **[!UICONTROL メッセージの内容]** ボックス。 これはリッチテキストボックスで、全画面表示オプションを使用して、使用可能なすべてのリッチテキスト項目を表示できます。

## アダプティブフォームのスキーマまたはフォームデータモデルの設定{#configure-schema-or-data-model-for-form}

フォームデータモデルを使用してフォームをデータソースに接続し、ユーザーのアクションに基づいてデータを送受信することができます。また、フォームを JSON スキーマに接続して、送信されたデータを事前定義済みの形式で受信することもできます。必要に応じて、フォームを JSON スキーマまたはフォームデータモデルに接続します。

* [JSON スキーマの作成と環境へのアップロード](/help/forms/adaptive-form-json-schema-form-model.md)
* [フォームデータモデルを作成](/help/forms/create-form-data-models.md)

### フォームの JSON スキーマまたはフォームデータモデルを設定する

フォームの JSON スキーマまたはフォームデータモデルを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、「 **[!UICONTROL ガイドコンテナ]** アダプティブフォームのコンポーネント
1. ガイドコンテナのプロパティをクリックします。 ![ガイドのプロパティ](/help/forms/assets/configure-icon.svg) アイコン。 アダプティブフォームコンテナダイアログボックスが開きます。
1. を開きます。 **[!UICONTROL データモデル]** タブをクリックします。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、JSON スキーマまたはフォームデータモデルを設定します](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 必要に応じて、JSON スキーマまたはフォームデータモデルを選択し、設定します。

   * 「**[!UICONTROL フォームモデル]**」オプションを選択する場合は、「**[!UICONTROL フォームデータモデルを選択]**」オプションを使用して、事前設定済みのフォームデータモデルを選択します。
   * 「**[!UICONTROL スキーマ]**」オプションを選択する場合は、「**[!UICONTROL スキーマ]**」オプションを使用して、フォームの JSON スキーマを選択します。

1. 「**[!UICONTROL 完了]**」をクリックします。

## 事前入力サービスの設定  {#configure-prefill-service-for-form}

事前入力サービスを使用すると、既存のデータを使用してアダプティブフォームのフィールドに自動入力できます。ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。以下の操作を実行できます。

* [カスタム事前入力サービスを作成](/help/forms/prepopulate-adaptive-form-fields.md)
* [フォームデータモデルの事前入力サービスを使用](#fdm-prefill-service)

### フォームデータモデルの事前入力サービスを使用して、アダプティブフォームのフィールドに事前入力する {#fdm-prefill-service}

フォームデータモデルの事前入力サービスを使用すると、フォームデータモデルまたはカスタム事前入力サービスを使用して、アダプティブフォームのフィールドに事前入力することができます。 フォームデータモデルの事前入力サービスでは、[設定済みのフォームデータモデルのサービスを取得](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)を使用して、データを取得します。アダプティブフォームでフォームデータモデルの事前入力サービスを使用するには、次の手順を実行します。

1. コンテンツブラウザーを開き、「 **[!UICONTROL ガイドコンテナ]** アダプティブフォームのコンポーネント
1. ガイドコンテナのプロパティをクリックします。 ![ガイドのプロパティ](/help/forms/assets/configure-icon.svg) アイコン。 アダプティブフォームコンテナダイアログボックスが開きます。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/assets/configure-icon.svg)アイコン）をクリックします。データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、リダイレクトページまたは「ありがとうございます」メッセージを設定します。](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. フォームデータモデルを選択. 「**[!UICONTROL 基本]**」タブを開きます。事前入力サービスで、「**[!UICONTROL フォームデータモデルの事前入力サービス]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。アダプティブフォームでフォームデータモデルの事前入力を使用するように設定しました。 [ルールエディター](rule-editor.md)を使用して、フォームのフィールドに事前入力するルールを作成できるようになりました。

## アダプティブフォームのフォームモデルプロパティの編集 {#edit-form-model}

1. アダプティブフォームを選択し、![ページ情報](/help/forms/assets/Smock_Properties_18_N.svg)／**[!UICONTROL プロパティを開く]**&#x200B;をタップします。フォームプロパティページが開きます。

1. 「**[!UICONTROL フォームモデル]**」タブをクリックし、フォームモデルを選択します。アダプティブフォームにフォームモデルがない場合は、JSON スキーマまたはフォームデータモデルを自由に選択できます。一方、アダプティブフォームが既にフォームモデルに基づいている場合は、同じタイプの別のフォームモデルに切り替えることもできます。例えば、フォームが JSON スキーマを使用している場合、別の JSON スキーマに容易に切り替えることができます。同様に、フォームがフォームデータモデルを使用している場合は、別のフォームデータモデルに切り替えることができます。

1. 「**[!UICONTROL 保存]**」をタップして、プロパティを保存します。


<!--

## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Add dynamic behavior to forms using the rule editor](rule-editor.md)
* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/responsive-layout.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)

-->

## 関連トピック {#see-also}

{{see-also}}

* [ルールエディターを使用してフォームに動的な動作を追加](rule-editor.md)
* [画面サイズやデバイスタイプに応じてフォームのレイアウトを設定](/help/sites-cloud/authoring/features/responsive-layout.md)

