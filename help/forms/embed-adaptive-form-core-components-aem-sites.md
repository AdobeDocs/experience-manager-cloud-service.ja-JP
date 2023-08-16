---
title: AEM Sites ページでのアダプティブフォーム（コアコンポーネント）の追加または作成
seo-title: How to add or create an Adaptive Form (Core Components) to an AEM Sites page?
description: AEM Sites ページでアダプティブフォーム（コアコンポーネント）を使用すると、AEM Sites ページを離れずにフォームに入力して送信できます。
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2131'
ht-degree: 95%

---

# AEM サイトエディターを使用したアダプティブフォームの作成または追加 {#add-an-adaptive-form-to-aem-sites-page}

アダプティブフォームを AEM Sites ページでシームレスに作成または埋め込むことで、ユーザーが Sites ページから離れずにフォームに入力して送信できます。これにより、ユーザーは web ページのその他の要素のコンテキストから離れずに、同時にフォームの操作も行うことができます。

アダプティブフォームを作成または AEM Sites ページに追加するには、以下の方法のいずれかを選択します。

* **アダプティブフォームコンテナコンポーネントを使用したアダプティブFormsの作成**: [アダプティブフォームコンテナ](#af-container-component) コンポーネントを使用すると、AEM Sitesエディター内で直接アダプティブFormsコンポーネントを利用して、デジタル登録エクスペリエンスを構築できます。 この統合により、AEM Sites の作成者は AEM Sites ページ内でフォームを作成し管理する際に、シームレスなエクスペリエンスを実現できます。

* **既存のアダプティブフォームを追加する**: [アダプティブForms — 埋め込み (v2)](#embed-existing-af) コンポーネントを使用すると、既存のアダプティブフォームをAEM Sites内のページに簡単に追加できます。 この機能により、アダプティブフォームの適応性と再利用性が向上します。この統合により、顧客が作成済みのアダプティブフォームを再利用する便利な方法が提供されます。

* **アダプティブフォームウィザードを使用したフォームの作成**：[アダプティブフォーム - 埋め込み（v2）](#embed-new-af)コンポーネントを使用して、AEM サイトエディター内からフォーム作成ウィザードを使用してアダプティブフォームを作成します。作成したフォームは外部エンティティとして保存されます。このフォームは、他の Sites ページやスタンドアロンフォームでも再利用できます。

* **AEM Sites ページへの複数のアダプティブフォームの追加**：AEM Sites ページに複数のアダプティブフォームを追加するには、AEM Forms コンテナコンポーネント - [アダプティブフォーム - 埋め込み（v2）](#embed-new-af)および[アダプティブフォームコンテナ](#af-container-component)を使用します。AEM Sites ページ内の div として複数のアダプティブフォームを追加する必要がある場合は、アダプティブフォームコンテナコンポーネントを使用できます。

ルールエディターを使用すると、アダプティブフォームコンポーネントの動的動作を追加または制御できます。例えば、コンポーネントの表示／非表示を切り替えます。ルールエディターは、アダプティブフォーム以外のコンポーネントでは使用できません。したがって、AEM Forms コンテナコンポーネントでアダプティブフォーム以外のコンポーネントを使用する場合は、慎重に行ってください。

## アダプティブフォームコンテナコンポーネントを使用したアダプティフォームの作成 {#af-container-component}

[!UICONTROL アダプティブフォームコンテナ]コンポーネントを使用すると、AEM サイトエディターのアダプティブフォームコンポーネントを使用して、デジタル登録エクスペリエンスを構築できます。アダプティブフォームを作成するには、フォームコンポーネントをドラッグ＆ドロップします。

### 前提条件 {#prerequisites-af-container}

+++ **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントを有効にします。

テンプレートのポリシーで[!UICONTROL アダプティブフォームコンテナ]コンポーネントを有効にするには、次の手順を実行します。

1. [!UICONTROL ページ情報]／[!UICONTROL テンプレートを編集]に移動します。
1. 「[!UICONTROL ポリシー]」をクリックし、**[AEM アーキタイププロジェクト名] - アダプティブフォーム**&#x200B;の下にある&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;チェックボックスを選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ アダプティブフォームクライアントライブラリを AEM Sites ページに含める

AEM Sites ページでアダプティブフォームコンポーネントを使用するには、AEM アーキタイプ／Git リポジトリとデプロイメントパイプラインを使用して、Customheaderlibs クライアントライブラリとCustomfooterlibs クライアントライブラリを AEM Sites ページに含めます。

1. [AEM Forms アーキタイプまたは複製された Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)プロジェクトをテキストエディターで開きます。例えば Visual Studio Code などです。
1. `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml` に移動します。
1. `sling:resourceSuperType` の値をコピーします。例えば、値は `core/wcm/components/page/v3/page` です。

   ![Sling リソース](/help/forms/assets/slingresource.png)

1. `core/wcm/components/page/v3/page` と同じ場所 `ui.apps/src/main/content/jcr_root/apps` に類似した構造を作成します。

   ![オーバーレイ構造](/help/forms/assets/overlaystructure.png)

1. `customheaderlibs.html` ファイルと `customfooterlibs.html` ファイルを追加します。

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly> 
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly> 
   ```

   customfooterlibs.html は JavaScript で使用され、customheaderlibs.html は CSS で使用されます。

1. [パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=ja)して変更をデプロイします。

+++

### アダプティブフォームコンテナコンポーネントを使用したアダプティフォームの作成 {#create-af-using-af-container}


[!UICONTROL アダプティブフォームコンテナ]コンポーネントを使用して、アダプティブフォームを作成するには、次の手順を実行します。

1. AEM Sites ページを編集モードで開きます。
1. コンポーネントブラウザーパネルから、**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントをページ上にドラッグ＆ドロップします。
1. アダプティブフォームのコンポーネントを使用して、アダプティブフォームを作成します。
1. 設定を保存します。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

これでフォームが作成されました。AEM Sites ページを公開すると、アダプティブフォームおよび関連する参照先のアセットが自動的に公開されます。

#### アダプティブフォームコンテナのプロパティの設定 {#configure-additional-settings-container}

[!UICONTROL アダプティブフォームコンテナ]コンポーネントの詳細設定はカスタマイズできます。例：

* 事前入力サービスを設定して、Sites のページにアダプティブフォームを、値が事前入力された状態で読み込むことができます。
* データモデルを設定して、アダプティブフォームをデータソースに関連付けることができます。
* 送信アクションを設定して、フォームの送信時に Microsoft® OneDrive、Microsoft® OneDrive、またはその他のデータソースのデータを送信することができます。また、アダプティブフォーム用のカスタム送信アクションを作成して選択することもできます。

**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントのプロパティを設定するには、アクションバーの ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) をクリックします。**[!UICONTROL アダプティブフォームコンテナを編集]**&#x200B;ダイアログが開きます。

![編集ダイアログ](/help/forms/assets/adaptiveformcontainer-editdialog.png)

[!UICONTROL アダプティブフォームコンテナを編集]ダイアログで、次の設定を行います。
* **「基本」タブ**
   * **事前入力サービス**：事前入力サービスを使用すると、既存のデータを使用してアダプティブフォームのフィールドに自動で入力することができます。ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。事前入力サービスについて詳しくは、[アダプティブフォームフィールドの事前入力](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html?lang=ja#configuring-prefill-service-using-configuration-manager)を参照してください。
   * **クライアントライブラリカテゴリ**：式で使用され、アダプティブフォームでサポートされている [JavaScript 関数](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=ja#custom-functions)を指定します。
* **データモデル**：データモデルを使用すると、異なるデータソースのエンティティやサービスをアダプティブフォームに統合することができます。作成するアダプティブフォームで、複数のデータソースに対するデータの取得と書き込みが必要になる場合は、**[!UICONTROL フォームデータモデル]**&#x200B;を選択します。
   * **フォームデータモデル**：フォームデータモデルを使用すると、アダプティブフォームが異なるデータソースと通信できます。データソースの設定について詳しくは、 [データソースの設定](/help/forms/configure-data-sources.md).
   * **スキーマ**：スキーマは、組織内のバックエンドシステムによってデータが作成または使用される構造を表しています。[アダプティブフォームにスキーマを関連付け](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html?lang=ja)て、そのスキーマの要素を使用することにより、アダプティブフォームに動的コンテンツを追加できます。

     >[!NOTE]
     >
     > フォームデータモデルを設定した後は、関連するフォームモデルを変更できません。 ただし、フォームデータモデルに関連付けられたスキーマは変更できます。

* **「送信」タブ**

   * **URL にリダイレクト**
      * **リダイレクト URL／パス**：送信後にアダプティブフォームがリダイレクトされる URL またはパスを指定します。

      * **送信アクション**：送信アクションは、ユーザーがアダプティブフォームの「送信」ボタンをクリックしたときにトリガーされます。[アダプティブフォームでの送信アクションを設定する](/help/forms/configuring-submit-actions.md)ことができます。アダプティブフォームには、次の送信アクションが標準搭載されています。
         * REST エンドポイントへの送信
         * メールを送信
         * フォームデータモデルを使用して送信
         * AEM ワークフローを起動
         * SharePoint に送信
         * OneDrive に送信
         * Azure Blob Storage に送信

  [デフォルトの送信アクションを拡張](custom-submit-action-form.md)して、独自のカスタム送信アクションを作成することもできます。

* **メッセージを表示**
   * **メッセージコンテンツ**：フォーム送信時に表示するメッセージをリッチテキストエディターで作成できます。このオプションは、ありがとうメッセージの表示が有効な場合にのみ選択できます。

## アダプティブフォームを埋め込み  {#aem-container-component}

**[!UICONTROL アダプティブフォーム - 埋め込み（V2）]**&#x200B;コンポーネントを使用することで、新しいアダプティブフォームを埋め込むか、既存のアダプティブフォームを Sites のページに埋め込むことができます。The [!UICONTROL アダプティブForms — 埋め込み (v2)] コンポーネントでは、次のことが可能です。

* [既存のアダプティブフォームを追加](#embed-new-af)

* [新しいアダプティブフォームを作成して追加](#embed-existing-af)

### 前提条件 {#prerequisites}

+++ **アダプティブフォーム - 埋め込み**&#x200B;コンポーネントを有効にします。

テンプレートのポリシーで[!UICONTROL アダプティブフォーム - 埋め込み（v2）]コンポーネントを有効にするには、次の手順を実行します。

1. [!UICONTROL ページ情報]／[!UICONTROL テンプレートを編集]に移動します。

1. 「[!UICONTROL ポリシー]」をクリックし、**[!UICONTROL [AEM アーキタイププロジェクト名] - Forms]** グループの「**[!UICONTROL アダプティブフォーム - 埋め込み（v2）]**」チェックボックスを選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ アダプティブフォームクライアントライブラリを AEM Sites ページに含める

**[!UICONTROL フォームコンテナ]**&#x200B;設定ダイアログボックスで「**[!UICONTROL フォームがページの幅全体に広がっている場合]**」オプションが選択されており、**コアコンポーネントを使用したアダプティブフォーム**&#x200B;が使用されている場合は、対応する Sites ページに clientlibs を含める必要があります。

![GIF をオーバーレイ](/help/forms/assets/overlaycorecomponent.gif)

AEM Sites ページでアダプティブフォームのコンポーネントを使用するには、AEM アーキタイプ／Git リポジトリとデプロイメントパイプラインを使用して、AEM Sites ページに `Customheaderlibs` および `Customfooterlibs` クライアントライブラリを含めます。

1. [AEM Forms アーキタイプまたは複製された Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)プロジェクトをテキストエディターで開きます。例えば Visual Studio Code などです。
1. `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml` に移動します。
1. `sling:resourceSuperType` の値をコピーします。例えば、値は `core/wcm/components/page/v3/page` です。

   ![Sling リソース](/help/forms/assets/slingresource.png)

1. `core/wcm/components/page/v3/page` と同じ場所 `ui.apps/src/main/content/jcr_root/apps` に類似した構造を作成します。

   ![オーバーレイ構造](/help/forms/assets/overlaystructure.png)

1. `customheaderlibs.html` および `customfooterlibs.html` ファイルを追加します。

   ```
   //Customheaderlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
       data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
       <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
   </sly>
   
   //customfooterlibs.html
   <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
     data-sly-use.form="com.adobe.cq.forms.core.components.models.aemform.AEMForm">
     <sly data-sly-test="${form.formVersion=='2.1' && !wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
   </sly>
   ```

   `customfooterlibs.html` は JavaScript に使用され、`customheaderlibs.html` は CSS に使用されます。

1. [パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=ja)して変更をデプロイします。

+++

### AEM Sites ページへの既存のアダプティブフォームの追加 {#embed-existing-af}

1. AEM Sites ページを編集モードで開きます。
1. コンポーネントブラウザーパネルから、[!UICONTROL アダプティブフォーム - 埋め込み]コンポーネントをページ上にドラッグ＆ドロップします。
1. Sites ページに埋め込まれた[!UICONTROL アダプティブフォーム - 埋め込み]コンポーネントをタップし、アクションバーの ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) をタップします。**[!UICONTROL アダプティブフォームを編集 - 埋め込み]**&#x200B;ダイアログが開きます。
1. [!UICONTROL アセットパス]に埋め込むアダプティブ フォームを参照して選択します。
1. 設定を保存します。これで、アダプティブフォームがページに埋め込まれました。

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)



### AEM Sites ページへの新規アダプティブフォームの作成と追加 {#embed-new-af}

1. AEM Sites ページを編集モードで開きます。
1. コンポーネントブラウザーパネルから、[!UICONTROL アダプティブフォーム - 埋め込み（v2）]コンポーネントをページ上にドラッグ＆ドロップします。
1. 「**プラス**」アイコンをクリックすると、フォーム作成ウィザードにリダイレクトされます。

   ![アダプティブフォーム - 埋め込みコンポーネント](/help/forms/assets/aemformcontainer.png)

1. [!UICONTROL フォーム作成]ウィザードから新しいアダプティブフォームを作成します。
1. [!UICONTROL アセットパス]には、作成されたアダプティブフォームのパスが既に含まれています
1. 設定を保存します。これで、アダプティブフォームがページに埋め込まれました。

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

#### アダプティブフォームの設定 - 埋め込み（v2）プロパティ {#configure-adaptive-form-embed}

[!UICONTROL アダプティブフォーム - 埋め込み（v2）]コンポーネントの詳細設定をカスタマイズできます。 [!UICONTROL アダプティブフォーム - 埋め込み（v2）]ダイアログでは、次の項目を指定できます。

* **アセットパス**： 埋め込むアダプティブフォームを参照して選択します。また、アセットブラウザーからドロップすると、自動的に入力されます。
* **送信後処理**：フォーム送信時にトリガーするアクションを選択します。お礼のメッセージを表示するため、「ありがとうございます」ページを設けることができます。
   * **ありがとうメッセージの表示**：フォーム送信時に表示するメッセージをリッチテキストエディターで書き込みます。このオプションは、ありがとうメッセージの表示が有効な場合にのみ選択できます。
   * **ありがとうページの表示**： フォームの送信時に表示するページを参照して選択します。このオプションは、ありがとうページの表示が有効な場合にのみ選択できます。
   * **ありがとうページにリダイレクト**：このオプションを有効にすると、アダプティブフォームが埋め込まれたページはありがとうページに置き換わります。 このオプションを有効にしない場合は、ありがとうページは、[!UICONTROL アダプティブフォーム - 埋め込み]コンポーネントのアダプティブフォームを置き換え、ベースとなる Sites ページは更新されません。このオプションは、ありがとうページの表示が有効な場合にのみ選択できます。
* **ページ言語を使用**：アダプティブフォームのロケールではなく、AEM Sites ページのロケールを使用します。
* **フォームにフォーカスを設定**：アダプティブ フォームの最初のフィールドにフォーカスを設定する場合に選択します。
* **フォームがフレームの幅全体をカバー**：オンにすると、iframe はフォームのレンダリングには使用されません。
* **高さ**：コンテナの高さを指定します。コンテナのサイズを自動的に変更するには、空白のままにします。
* **CSS クライアントライブラリ**：CSS クライアントライブラリへのパスを指定します。

### アダプティブフォーム - 埋め込み（v2）コンポーネントを使用した、追加されたアダプティブフォームの公開  {#publish-embedded-adaptive-form}

**[!UICONTROL アダプティブフォーム - 埋め込み（v2）]**&#x200B;コンポーネントを使用して、追加されたアダプティブフォームを公開する次のシナリオを検討してください。

* AEM Sites ページを初めて公開すると、Sites ページに追加されたフォームは自動的に公開されます。
* 既に公開されている Sites ページに追加されたアダプティブフォームを変更する場合は、、対応するアダプティブフォームを手動で公開します。
* Sites ページと対応するアダプティブフォームを変更する場合は、Sites ページと、Sites ページに追加されたすべてのアダプティブフォームを再公開します。

### アダプティブフォーム - 埋め込み（v2）コンポーネントを使用した、追加済みアダプティブフォームの変更  {#modifying-embedded-adaptive-form}

アダプティブフォームの設定やプロパティを変更するには、次のいずれかの操作を行います。

* それぞれのエディターのアダプティブフォームで元のフォームを開いて、変更します。
* 編集モードでサイトページ内からアダプティブフォームをタップし、続けて「**[!UICONTROL 新しいウィンドウで編集]**」をタップします。元のフォームは、修正可能な編集モードで開きます。

## AEM Sites ページに追加アダプティブフォームのレイアウトの変更 {#change-layout-af-aem-sites-page}

AEM Sites ページで[レイアウトモード](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?lang=ja#defining-layouts-layout-mode)を使用すると、作成されたまたは AEM Sites ページに追加されているアダプティブフォームのサイズを変更できます。

![AF-layout-support](/help/forms/assets/afsite-layoutsupport.gif)

AEM Sites ページには、アダプティブフォームへの参照情報が保存されます。AEM Sites ページを翻訳すると、アダプティブフォームと関連する参照先のアセットが、[翻訳プロジェクト](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=ja#adding-pages-assets-to-a-translation-job)を使用して他の言語に自動で翻訳されます。

## ベストプラクティス {#best-practices}

* 元のフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ユーザードラフトと埋め込みフォームの送信はサポートされており、フォームポータル上の「下書き」タブや「送信済みフォーム」タブに表示されます。