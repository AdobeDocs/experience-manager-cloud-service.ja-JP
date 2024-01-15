---
title: アダプティブフォームのフォームデータモデルを作成する方法
description: フォームデータモデル（FDM）に基づいたアダプティブフォームおよびフラグメントの作成方法を説明します。FDM でデータモデルオブジェクトのサンプルデータを生成し、編集します。
feature: Adaptive Forms, Form Data Model
role: Admin, User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 94%

---

# フォームデータモデルの使用 {#use-form-data-model}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/using-form-data-model.html?lang=ja) |
| AEM as a Cloud Service | この記事 |


![data-integration](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] のデータ統合機能により、各種のバックエンドデータソースを使用してフォームデータモデルを作成できます。作成したデータフォームは、様々なアダプティブフォームの<!--and interactive communications-->ワークフローで、スキーマとして使用できます。そのためには、データソースの設定を行い、そのデータソース内の有効なデータモデルオブジェクトとデータモデルサービスに基づいて、フォームデータモデルを作成する必要があります。詳しくは、以下のトピックを参照してください。

* [[!DNL Experience Manager Forms] データ統合](data-integration.md)
* [データソースの設定](configure-data-sources.md)
* [フォームデータモデルの作成](create-form-data-models.md)
* [フォームデータモデルの操作](work-with-form-data-model.md)

JSON スキーマの拡張機能であるフォームデータモデルを使用して、以下の処理を行うことができます。

* [アダプティブフォームとアダプティブフォームフラグメントの作成](#create-af)
  <!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [サンプルデータを使用したプレビュー](#preview-ic)
* [フォームデータモデルサービスの使用](#prefill)
* [送信されたアダプティブフォームデータのデータソースへの書き戻し](#write-af)
* [アダプティブフォームのルールを使用したサービスの呼び出し](#invoke-services)

## アダプティブフォームとアダプティブフォームフラグメントの作成 {#create-af}

フォームデータモデルに基づいて、[アダプティブフォーム](creating-adaptive-form.md)とアダプティブフォームフラグメント<!-- [Adaptive Form Fragments](adaptive-form-fragments.md) -->を作成できます。フォームデータモデルを使用してアダプティブフォームまたはアダプティブフォームフラグメントを作成するには、以下の手順を実行します。

1. プロパティを追加画面の「フォームモデル」タブで、 **[!UICONTROL 次から選択]** ドロップダウンリストから「**[!UICONTROL フォームデータモデル]**」を選択します。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 選択して展開 **[!UICONTROL フォームデータモデルを選択]**. すべての有効なフォームデータモデルが一覧表示されます。

   フォームデータモデルを選択します。

   ![create-af-2-1](assets/create-af-2-1.png)

1. （**アダプティブフォームフラグメントのみ**）フォームデータモデル内の 1 つのデータモデルオブジェクトのみに基づいて、アダプティブフォームフラグメントを作成できます。**[!UICONTROL フォームデータモデル定義]**&#x200B;ドロップダウンを展開します。指定したフォームデータモデル内のすべてのデータモデルオブジェクトがリスト表示されます。リストからデータモデルオブジェクトを選択します。

   ![create-af-3](assets/create-af-3.png)

   フォームデータモデルに基づいてアダプティブフォームまたはアダプティブフォームフラグメントを作成すると、アダプティブフォームエディターのコンテンツブラウザーの「**[!UICONTROL データソース]**」タブにフォームデータモデルオブジェクトが表示されます。

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

フォームデータモデルエディターでは、フォームデータモデル内のデータモデルオブジェクト用のサンプルデータを生成して編集できます。このデータを使用して、<!--interactive communications and-->アダプティブフォームをプレビューおよびテストできます。プレビュー表示を行う前に、「[フォームデータモデルの操作](work-with-form-data-model.md#sample)」の説明に従って、サンプルデータを生成する必要があります。

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and select **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and select **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

サンプルデータを含むアダプティブフォームをプレビューするには、アダプティブフォームをオーサリングモードで開き、「 **[!UICONTROL プレビュー]**.

## フォームデータモデルサービスを使用したデータの事前入力 {#prefill}

[!DNL Experience Manager Forms] には、すぐに使用できるフォームデータモデル事前入力サービスが用意されています。フォームデータモデルに基づいて、このサービスをアダプティブフォーム<!--and interactive communications-->で使用できます。この事前入力サービスは、アダプティブフォーム<!--and interactive communication-->内のデータモデルオブジェクトに対してデータソースのクエリを実行し、フォームまたは通信のレンダリング時にデータを事前入力します。

アダプティブフォームに対してフォームデータモデル事前入力サービスを有効にするには、アダプティブフォームコンテナのプロパティを開き、基本アコーディオンの **[!UICONTROL 事前入力サービス]** ドロップダウンで「**[!UICONTROL フォームデータモデル事前入力サービス]**」を選択します。次に、各プロパティを保存します。

![prefill-service](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## 送信されたアダプティブフォームデータのデータソースへの書き込み {#write-af}

フォームデータモデルに基づくフォームを送信した場合、そのフォームを設定して、特定のデータモデルオブジェクトに対して送信されたデータをそのデータモデルオブジェクトのデータソースに書き込むことができます。この設定を行うために、[!DNL Experience Manager Forms] には、すぐに使用できる[フォームデータモデル送信アクション](configuring-submit-actions.md)が用意されています。これは、フォームデータモデルをベースとするアダプティブフォーム専用のアクションです。このアクションを実行すると、特定のデータモデルオブジェクトに対して送信されたデータが、そのデータモデルオブジェクトのデータソースに書き込まれます。

フォームデータモデル送信アクションを設定するには、アダプティブフォームコンテナのプロパティを開き、送信アコーディオンの送信アクションドロップダウンで「**[!UICONTROL フォームデータモデルを使用して送信]**」を選択します。次に、 **[!UICONTROL 送信するデータモデルオブジェクトの名前]** ドロップダウンで、目的のデータモデルオブジェクトを探して選択します。各プロパティを保存します。

フォームを送信すると、設定されているデータモデルオブジェクトのデータが、各データソースに書き込まれます。

<!--![data-submission](assets/data-submission.png)-->

バイナリデータモデルオブジェクトのプロパティを使用して、フォームの添付ファイルをデータソースに送信することもできます。添付ファイルを JDBC データソースに送信するには、次の手順を実行します。

1. バイナリプロパティを含むデータモデルオブジェクトをフォームデータモデルに追加します。
1. コンポーネントブラウザーの「**[!UICONTROL 添付ファイル]**」コンポーネントを、アダプティブフォームにドラッグ＆ドロップします。
1. 「 」を選択して追加したコンポーネントを選択し、「 」を選択します。 ![settings_icon](assets/configure-icon.svg) をクリックして、コンポーネントのプロパティブラウザーを開きます。
1. 「バインド参照」フィールドで、「 ![foldersearch_18](assets/folder-search-icon.svg) フォームデータモデルに追加したバイナリプロパティに移動して選択します。 必要に応じて、他のプロパティを設定します。

   選択 ![check-button](assets/save_icon.svg) をクリックしてプロパティを保存します。 これで、添付ファイルフィールドがフォームデータモデルのバイナリプロパティに連結されます。

1. アダプティブフォームコンテナプロパティの「送信」セクションで、「**[!UICONTROL フォームの添付ファイルを送信]**」を有効にします。これで、フォーム送信時に、バイナリプロパティフィールド内の添付ファイルがデータソースに送信されます。

## ルールを使用したアダプティブフォーム内のサービスの呼び出し {#invoke-services}

フォームデータモデルに基づくアダプティブフォームの場合、[ルールを作成](rule-editor.md)して、フォームデータモデル内で設定されているサービスを呼び出すことができます。ルール内の「**[!UICONTROL サービスを起動]**」操作を実行すると、フォームデータモデル内のすべての有効なサービスが一覧表示され、サービスの入力フィールドと出力フィールドを選択できます。「**[!UICONTROL 指定値]**」というルールタイプを使用してフォームデータモデルサービスを呼び出し、そのサービスから返された出力に対するフィールドの値を設定することもできます。

例えば以下のルールの場合、従業員 ID を入力として使用する Get サービスが呼び出され、このサービスから返された値が、フォーム内の対応する扶養家族 ID フィールド、姓フィールド、名フィールド、性別フィールドに設定されます。

![invoke-service](assets/invoke-service.png)

また、`guidelib.dataIntegrationUtils.executeOperation` API を使用して、ルールエディターのコードエディターで JavaScript を記述することもできます。<!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->

### カスタム関数を使用したフォームデータモデルの呼び出し {#invoke-form-data-model-using-custom-functions}

[カスタム関数を使用してルールエディターからフォームデータモデルを呼び出す](/help/forms/rule-editor.md#custom-functions-in-rule-editor-custom-functions)ことができます。フォームデータモデルを呼び出すには、許可リストにフォームデータモデルを追加します。許可リストにフォームデータモデルを追加するには、次の手順を実行します。

1. `https://server:host/system/console/configMgr` で Experience Manager web コンソールに移動します。
1. 「**[!UICONTROL サービス呼び出し用のフォームデータモデルのアダプティブフォームレベルの許可リスト登録 - 設定ファクトリ]**」を見つけます。
1. ![プラスアイコン ](/help/forms/assets/Smock_Add_18_N.svg) をクリックして設定を追加します。
1. **[!UICONTROL コンテンツパスパターン]**&#x200B;を追加して、アダプティブフォームの場所を指定します。デフォルトでは、値は `/content/forms/af/(.*)` で、すべてのアダプティブフォームが含まれています。特定のアダプティブフォームのパスを指定することもできます。
1. **[!UICONTROL フォームデータモデルのパスパターン]**&#x200B;を追加して、フォームデータモデルの場所を指定します。デフォルトでは、値は `/content/dams/formsanddocuments-fdm/(.*)` で、すべてのフォームデータモデルが含まれています。特定のフォームデータモデルのパスを指定することもできます。
1. 設定を保存します。

追加した設定は、「**[!UICONTROL サービス呼び出し用のフォームデータモデルのアダプティブフォームレベルの許可リスト登録 - 設定ファクトリ]**」オプションに保存されます。

>[!VIDEO](https://video.tv.adobe.com/v/3423977/adaptive-forms-custom-function-rule-editor)

>[!NOTE]
>
> AEM アーキタイププロジェクト経由でカスタム関数を使用してルールエディターからフォームデータモデルを呼び出すには、次の手順を実行します。
>
>1. [設定ファイルを作成](https://github.com/adobe/aem-core-forms-components/blob/master/it/config/src/main/content/jcr_root/apps/system/config/com.adobe.aemds.guide.factory.impl.AdaptiveFormFDMConfigurationFactoryImpl~core-components-it.cfg.json)します。
>1. getContentPathPattern および getFormDataModelPathPattern のプロパティを設定します。
>1. プロジェクトをデプロイします。
