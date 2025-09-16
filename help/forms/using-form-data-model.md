---
title: アダプティブフォームのフォームデータモデル（FDM）を作成する方法
description: フォームデータモデル（FDM）に基づいたアダプティブフォームおよびフラグメントの作成方法を説明します。FDM でデータモデルオブジェクトのサンプルデータを生成し、編集します。
feature: Adaptive Forms, Form Data Model
role: Admin, User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 97%

---

# フォームデータモデル（FDM）の使用 {#use-form-data-model}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/using-form-data-model.html?lang=ja) |
| AEM as a Cloud Service | この記事 |


![data-integration](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] のデータ統合機能により、各種のバックエンドデータソースを使用してフォームデータモデル（FDM）を作成できます。作成したデータフォーム（FDM）は、様々なアダプティブフォームの <!--and interactive communications--> ワークフローで、スキーマとして使用できます。そのためには、データソースの設定を行い、データソース内の有効なデータモデルオブジェクトとサービスに基づいて、フォームデータモデル（FDM）を作成する必要があります。詳しくは、以下のトピックを参照してください。

* [[!DNL Experience Manager Forms] データ統合](data-integration.md)
* [データソースの設定](configure-data-sources.md)
* [フォームデータモデル（FDM）の作成](create-form-data-models.md)
* [フォームデータモデル（FDM）の操作](work-with-form-data-model.md)

JSON スキーマの拡張機能であるフォームデータモデル（FDM）を使用して、以下を行うことができます。

* [アダプティブフォームとアダプティブフォームフラグメントの作成](#create-af)
  <!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [サンプルデータを使用したプレビュー](#preview-ic)
* [フォームデータモデルサービスの使用](#prefill)
* [送信されたアダプティブフォームデータのデータソースへの書き戻し](#write-af)
* [アダプティブフォームのルールを使用したサービスの呼び出し](#invoke-services)

## アダプティブフォームとアダプティブフォームフラグメントの作成 {#create-af}

フォームデータモデル（FDM）に基づいて、[アダプティブフォーム](creating-adaptive-form.md)とアダプティブフォームフラグメント <!-- [Adaptive Form Fragments](adaptive-form-fragments.md) --> を作成できます。アダプティブフォームまたはアダプティブフォームフラグメントを作成する際にフォームデータモデル（FDM）を使用するには、以下の手順を実行します。

1. プロパティを追加画面の「フォームモデル」タブで、 **[!UICONTROL 次から選択]** ドロップダウンリストから「**[!UICONTROL フォームデータモデル]**」を選択します。

   ![create-af-1-1](assets/create-af-1-1.png)

2. 「**[!UICONTROL フォームデータモデルを選択]**」を選択して展開します。使用可能なすべてのフォームデータモデル（FDM）がリスト表示されます。

   フォームデータモデルを選択します。

   ![create-af-2-1](assets/create-af-2-1.png)

3. （**アダプティブフォームフラグメントのみ**）フォームデータモデル（FDM）内の 1 つのデータモデルオブジェクトのみに基づいて、アダプティブフォームフラグメントを作成できます。**[!UICONTROL フォームデータモデル定義]**&#x200B;ドロップダウンを展開します。指定したフォームデータモデル（FDM）内のすべてのデータモデルオブジェクトがリスト表示されます。リストからデータモデルオブジェクトを選択します。

   ![create-af-3](assets/create-af-3.png)

   フォームデータモデル（FDM）に基づいてアダプティブフォームまたはアダプティブフォームフラグメントを作成すると、アダプティブフォームビルダーのコンテンツブラウザーの **[!UICONTROL データソース]** タブにフォームデータモデルオブジェクトが表示されます。

   >[!NOTE]
   >
   >アダプティブフォームフラグメントの場合は、オーサリング時に選択したデータモデルオブジェクトと、そのオブジェクトに関連付けられているデータモデルオブジェクトだけが、「データソース」タブに表示されます。

   ![data-model-objects-tab](assets/data-model-objects-tab.png)

   データモデルオブジェクトをアダプティブフォームまたはアダプティブフォームフラグメントにドラッグ＆ドロップすると、フォームフィールドを追加できます。追加されたフォームフィールドには、メタデータのプロパティとデータモデルオブジェクトのプロパティとの連結が保持されます。この連結により、フォームの送信時に対応するデータソース内のフィールド値が更新され、フォームのレンダリング時に対応するデータソース内のフィールドに値が取り込まれます。

<!-- ## Create interactive communications {#create-ic}

You can create an interactive communication based on a Form Data Model that you can use to prefill interactive communication with data from configured data sources. In addition, the building blocks of an interactive communication, such as text, list, and condition document fragments can be based on a form data model.

You can choose a Form Data Model when creating an interactive communication or a document fragment. The following image shows the General tab of the Create Interactive Communication dialog.

![create-ic](assets/create-ic.png)

General tab of Create Interactive Communication dialog

For more information, see:

[Create an interactive communication](create-interactive-communication.md)

[Text in Interactive Communications](texts-interactive-communications.md)

[Conditions in Interactive Communications](conditions-interactive-communications.md)

[List fragments](lists.md) -->

## サンプルデータを使用したプレビュー {#preview-ic}

フォームデータモデルエディターでは、フォームデータモデル（FDM）内のデータモデルオブジェクト用のサンプルデータを生成して編集できます。このデータを使用して、<!--interactive communications and-->アダプティブフォームをプレビューおよびテストできます。プレビュー表示を行う前に、「[フォームデータモデルの操作](work-with-form-data-model.md#sample)」の説明に従って、サンプルデータを生成する必要があります。

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and select **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and select **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

サンプルデータが取り込まれた状態のアダプティブフォームをプレビューするには、オーサーモードでアダプティブフォームを開いて「**[!UICONTROL プレビュー]**」を選択します。

## フォームデータモデルサービスを使用したデータの事前入力 {#prefill}

[!DNL Experience Manager Forms] には、標準のフォームデータモデル事前入力サービスが用意されています。フォームデータモデル（FDM）に基づいて、このサービスをアダプティブフォーム<!--and interactive communications-->で使用することができます。この事前入力サービスは、アダプティブフォーム<!--and interactive communication-->内のデータモデルオブジェクトに対してデータソースのクエリを実行し、フォームまたは通信のレンダリング時にデータを事前入力します。

アダプティブフォームに対してフォームデータモデル事前入力サービスを有効にするには、アダプティブフォームコンテナのプロパティを開き、基本アコーディオンの **[!UICONTROL 事前入力サービス]** ドロップダウンで「**[!UICONTROL フォームデータモデル事前入力サービス]**」を選択します。次に、各プロパティを保存します。

![prefill-service](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## 送信されたアダプティブフォームデータのデータソースへの書き込み {#write-af}

ユーザーがフォームデータモデル（FDM）に基づいてフォームを送信する際には、データモデルオブジェクトの送信データがそのデータソースに書き込まれるようにフォームを設定することができます。この設定を行うために、[!DNL Experience Manager Forms] には、すぐに使用できる[フォームデータモデル送信アクション](configuring-submit-actions.md)が用意されています。これは、フォームデータモデル（FDM）をベースとするアダプティブフォーム専用のアクションです。これにより、データモデルオブジェクトに送信されたデータが、そのデータソースに書き込まれます。

フォームデータモデル送信アクションを設定するには：

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから、「**[!UICONTROL フォームデータモデルを使用して送信]**」を選択します。

   ![アクションの設定](/help/forms/assets/configure-submit-action-invoke-fdm.png)

1. **[!UICONTROL 送信するデータモデル]**&#x200B;を指定します。
1. 「**[!UICONTROL 完了]**」をクリックします。

フォームを送信すると、設定されているデータモデルオブジェクトのデータが、各データソースに書き込まれます。さらに、フォームデータモデル（FDM）とレコードのドキュメント（DoR）を使用して、フォームの添付ファイルをデータソースに送信できます。フォームデータモデル（FDM）について詳しくは、[[!DNL AEM Forms]  のデータ統合機能](data-integration.md)を参照してください。

<!--![data-submission](assets/data-submission.png)-->

>[!NOTE]
>
> AEM as a Cloud Service では、フォーム送信を処理するための様々な送信アクションが標準で提供されます。これらのオプションについて詳しくは、[アダプティブフォームの送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事をご覧ください。

バイナリデータモデルオブジェクトのプロパティを使用して、フォームの添付ファイルをデータソースに送信することもできます。添付ファイルを JDBC データソースに送信するには、次の手順を実行します。

1. バイナリプロパティを含むデータモデルオブジェクトをフォームデータモデル（FDM）に追加します。
1. コンポーネントブラウザーの「**[!UICONTROL 添付ファイル]**」コンポーネントを、アダプティブフォームにドラッグ＆ドロップします。
1. 追加されたコンポーネント、![settings_icon](assets/configure-icon.svg) の順に選択して、そのコンポーネントのプロパティブラウザーを開きます。
1. 「バインド参照」フィールドで ![foldersearch_18](assets/folder-search-icon.svg) を選択し、フォームデータモデル（FDM）に追加したバイナリプロパティに移動してそのプロパティを選択します。必要に応じて、他のプロパティを設定します。

   ![check-button](assets/save_icon.svg) を選択して、プロパティを保存します。これで、添付ファイルフィールドがフォームデータモデル（FDM）のバイナリプロパティに連結されます。

1. アダプティブフォームコンテナプロパティの「送信」セクションで、「**[!UICONTROL フォームの添付ファイルを送信]**」を有効にします。これで、フォーム送信時に、バイナリプロパティフィールド内の添付ファイルがデータソースに送信されます。

## ルールを使用したアダプティブフォーム内のサービスの呼び出し {#invoke-services}

フォームデータモデル（FDM）に基づくアダプティブフォームの場合、[ルールを作成](rule-editor.md)して、フォームデータモデル（FDM）内で設定されているサービスを呼び出すことができます。ルール内の「**[!UICONTROL サービスを起動]**」操作を実行すると、フォームデータモデル（FDM）内のすべての有効なサービスが一覧表示され、サービスの入力フィールドと出力フィールドを選択できます。「**[!UICONTROL 指定値]**」というルールタイプを使用してフォームデータモデルサービスを呼び出し、そのサービスから返された出力に対するフィールドの値を設定することもできます。

例えば以下のルールの場合、従業員 ID を入力として使用する Get サービスが呼び出され、このサービスから返された値が、フォーム内の対応する扶養家族 ID フィールド、姓フィールド、名フィールド、性別フィールドに設定されます。

![invoke-service](assets/invoke-service.png)

また、`guidelib.dataIntegrationUtils.executeOperation` API を使用して、ルールエディターのコードエディターで JavaScript を記述することもできます。<!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->

### カスタム関数を使用したフォームデータモデル（FDM）の呼び出し {#invoke-form-data-model-using-custom-functions}

[カスタム関数を使用してルールエディターからフォームデータモデルを呼び出す](/help/forms/rule-editor.md#custom-functions-in-rule-editor-custom-functions)ことができます。フォームデータモデル（FDM）を呼び出すには、許可リストにフォームデータモデルを追加します。許可リストにフォームデータモデルを追加するには、次の手順を実行します。

1. `https://server:host/system/console/configMgr` で Experience Manager web コンソールに移動します。
1. 「**[!UICONTROL サービス呼び出し用のフォームデータモデルのアダプティブフォームレベルの許可リスト登録 - 設定ファクトリ]**」を見つけます。
1. ![プラスアイコン ](/help/forms/assets/Smock_Add_18_N.svg) をクリックして設定を追加します。
1. **[!UICONTROL コンテンツパスパターン]**&#x200B;を追加して、アダプティブフォームの場所を指定します。デフォルトでは、値は `/content/forms/af/(.*)` で、すべてのアダプティブフォームが含まれています。特定のアダプティブフォームのパスを指定することもできます。
1. **[!UICONTROL フォームデータモデルのパスパターン]**&#x200B;を追加して、フォームデータモデル（FDM）の場所を指定します。デフォルトでは、値は `/content/dams/formsanddocuments-fdm/(.*)` で、すべてのフォームデータモデル（FDM）が含まれています。また、特定のフォームデータモデル（FDM）のパスを指定することもできます。
1. 設定を保存します。

追加した設定は、「**[!UICONTROL サービス呼び出し用のフォームデータモデルのアダプティブフォームレベルの許可リスト登録 - 設定ファクトリ]**」オプションに保存されます。

>[!VIDEO](https://video.tv.adobe.com/v/3423977/adaptive-forms-custom-function-rule-editor)

>[!NOTE]
>
> AEM アーキタイププロジェクト経由でカスタム関数を使用してルールエディターからフォームデータモデル（FDM）を呼び出すには：
>
>1. [設定ファイルを作成](https://github.com/adobe/aem-core-forms-components/blob/master/it/config/src/main/content/jcr_root/apps/system/config/com.adobe.aemds.guide.factory.impl.AdaptiveFormFDMConfigurationFactoryImpl~core-components-it.cfg.json)します。
>1. getContentPathPattern および getFormDataModelPathPattern のプロパティを設定します。
>1. プロジェクトをデプロイします。

## 関連記事

{{af-submit-action}}

