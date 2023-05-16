---
title: AEM Sitesページでのアダプティブフォーム（コアコンポーネント）の追加
seo-title: How to add an Adaptive Form (Core Components) to an AEM Sites page?
description: AEM Sitesページでアダプティブフォーム（コアコンポーネント）を使用すると、AEM Sitesページから移動することなく、フォームに入力して送信することができます。
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 1046231f-787c-4e49-9ba0-e7dd59e41bce
source-git-commit: 0d21b4ba2e7ce7592e3f2c57e4d320adc0af1008
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 19%

---

# AEM SitesページへのアダプティブFormsの追加 {#add-an-adaptive-form-to-aem-sites-page}

## 概要 {#overview}

AEM SitesページでアダプティブFormsの作成や埋め込みをシームレスにおこなえるので、ユーザーはサイトページから移動することなくフォームに入力して送信できます。 これにより、ユーザーは Web ページの他の要素のコンテキストにとどまり、同時にフォームを操作できます。

アダプティブフォームをAEM Sitesページに作成または埋め込むには、次のいずれかの方法を選択できます。

* **フォームコンポーネントをアダプティブFormsコンテナコンポーネントにドラッグ&amp;ドロップしてアダプティブフォームを作成する**:以下を使用： [アダプティブFormsコンテナ](#af-container-component) コンポーネントを使用して、アダプティブフォームをホストするスペースを web ページ内に作成します。 このスペースにアダプティブフォームコンポーネントをドラッグ&amp;ドロップしてフォームを作成できます。 例えば、以下のビデオを参照して、アダプティブフォームの作成方法を確認してください。 [!UICONTROL アダプティブFormsコンテナ] コンポーネント：

この [アダプティブフォームコンテナ](#af-container-component) コンポーネントを使用すると、AEM Sitesエディター内で直接アダプティブFormsコンポーネントを利用して、デジタル登録エクスペリエンスを構築できます。 この統合により、AEM Sitesの作成者はAEM Sitesページ内でフォームを作成し管理する際に、シームレスな操作をおこなうことができます。

* **既存のアダプティブフォームを埋め込む**:この [アダプティブForms — 埋め込み (V2)](#embed-existing-af) コンポーネントを使用すると、既存のアダプティブフォームをAEM Sites内のページに簡単に組み込むことができます。 例えば、 [!UICONTROL アダプティブForms — 埋め込み] コンポーネントをサイトのページに追加します（次のビデオを参照）。

この機能により、アダプティブFormsの適応性と再利用性が向上します。 この統合により、作成済みのアダプティブFormsを再利用する便利な方法が提供されます。

* **アダプティブFormsウィザードを使用したフォームの作成**:

   以下を使用： [アダプティブForms — 埋め込み (v2)](#embed-new-af) フォーム作成ウィザードを使用してAEM Sitesエディター内でアダプティブフォームを作成するためのコンポーネントです。 フォームは外部エンティティとして保存されます。 このフォームは、他の Sites ページやスタンドアロンフォームでも再利用できます。
例えば、以下のビデオを参照して、新しく作成したアダプティブフォームを作成し、 [!UICONTROL アダプティブForms — 埋め込み] コンポーネントをサイトのページに追加します。

### 検討 {#considerations}

ルールエディターを使用して、アダプティブフォームコンポーネントの動的動作を追加または制御できます。 例えば、コンポーネントの表示/非表示を切り替えます。 ルールエディターは、アダプティブフォーム以外のコンポーネントでは使用できません。 そのため、AEM Formsコンテナコンポーネントでアダプティブフォーム以外のコンポーネントを使用する場合は、これを参考にしてください。

## アダプティブフォームの作成 ( アダプティブFormsコンテナコンポーネントを使用 ) {#af-container-component}

この [!UICONTROL アダプティブフォームコンテナ] コンポーネントを使用すると、AEM SitesエディターのアダプティブFormsコンポーネントを使用して、デジタル登録エクスペリエンスを構築できます。 アダプティブフォームを作成するには、フォームコンポーネントをドラッグ&amp;ドロップします。

### 前提条件 {#prerequisites-af-container}

+++ 有効にする **[!UICONTROL アダプティブFormsコンテナ]** 関連付けられたテンプレートのポリシー内のコンポーネント。

有効にするには [!UICONTROL アダプティブFormsコンテナ] テンプレートのポリシーのコンポーネントで、次の手順を実行します。

1. 次に移動： [!UICONTROL ページ情報] > [!UICONTROL テンプレートを編集]
1. 次をクリック： [!UICONTROL ポリシー] をクリックし、 **[!UICONTROL アダプティブFormsコンテナ]**  の下のチェックボックス **[AEM Archetype プロジェクト名]  — アダプティブフォーム**.
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

+++ Site のページに clientlibs を含める

AEM SitesページでアダプティブFormsコンポーネントを使用するには、 AEM Archetype/Git リポジトリとデプロイメントパイプラインを使用して、 Customheaderlibs クライアントライブラリと Customfooterlibs クライアントライブラリをAEM Sitesページに含めます。

1. を開きます。 [AEM Formsアーキタイプまたは複製された Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) プロジェクトをテキストエディターで作成します。 たとえば、Visual Studio Code などです。
1. `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml` に移動します。
1. 次の値をコピー： `sling:resourceSuperType`. 例えば、値は `core/wcm/components/page/v3/page`.

   ![sling リソース](/help/forms/assets/slingresource.png)

1. の場所で類似した構造を作成します。 `ui.apps/src/main/content/jcr_root/apps` 同じ `core/wcm/components/page/v3/page`.

   ![オーバーレイ構造](/help/forms/assets/overlaystructure.png)

1. 追加 `customheaderlibs.html` および `customfooterlibs.html` ファイル。

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

1. [パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) をクリックして変更をデプロイします。

+++

### アダプティブフォームコンテナコンポーネントを使用したアダプティブFormsの作成 {#create-af-using-af-container}


を使用してアダプティブフォームを作成するには [!UICONTROL アダプティブFormsコンテナ] コンポーネント：

1. AEM Sitesページを編集モードで開きます。
1. コンポーネントブラウザーパネルから、 **[!UICONTROL アダプティブFormsコンテナ]** コンポーネントをページ上に配置します。
1. アダプティブフォームを作成するには、アダプティブフォームのFormsコンポーネントを使用します。
1. 設定を保存します。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

フォームの準備が整いました。 AEM Sitesページを公開すると、アダプティブフォームと、関連する参照アセットが自動的に公開されます。

#### アダプティブフォームコンテナのプロパティの設定 {#configure-additional-settings-container}

この [!UICONTROL アダプティブフォームコンテナ] コンポーネント。 例えば、事前入力サービスを設定して、サイトのページに事前入力された値を持つアダプティブフォームを読み込むことができます。 アダプティブフォームをデータモデルに関連付けるように、データモデルを設定します。 アダプティブフォームの送信時に OneDrive またはSharePointにデータを保存する場合は、送信アクションの設定を行います。 また、アダプティブForms用にカスタム送信アクションを追加することもできます。

のプロパティを設定するには **[!UICONTROL アダプティブFormsコンテナ]** コンポーネント、 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) をクリックします。 この **[!UICONTROL アダプティブFormsコンテナの編集]** ダイアログが開きます。

![編集ダイアログ](/help/forms/assets/adaptiveformcontainer-editdialog.png)

内 [!UICONTROL アダプティブFormsコンテナの編集] ダイアログでは、次の項目を指定できます。
* **「基本」タブ**
   * **事前入力サービス**:事前入力サービスを使用すると、既存のデータを使用してアダプティブフォームのフィールドに自動入力することができます。 ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。事前入力サービスについて詳しくは、 [アダプティブフォームフィールドの事前入力](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html#configuring-prefill-service-using-configuration-manager)
   * **クライアントライブラリカテゴリ**:次を指定： [JavaScript 関数](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#custom-functions) 式で使用され、Adaptive Formsでサポートされる
* **データモデル**:データモデルを使用すると、異なるデータソースのエンティティやサービスをアダプティブフォームに統合できます。 選択 **[!UICONTROL フォームデータモデル]** 作成するアダプティブフォームに、複数のデータソースのデータの取得および書き込みが含まれる場合。
   * **フォームデータモデル**:フォームデータモデルを使用すると、アダプティブフォームは異なるデータソースと通信できます。 データソースの設定について詳しくは、 [データソースを設定します。](/help/forms/configure-data-sources.md)
   * **スキーマ**:スキーマは、組織のバックエンドシステムによってデータが生成または使用される構造を表します。 以下が可能です。 [スキーマをアダプティブフォームに関連付ける](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) その要素を使用して、アダプティブフォームに動的コンテンツを追加します。

      >[!NOTE]
      >
      > フォームデータモデルを設定した後は、関連するフォームモデルを変更できません。 ただし、フォームデータモデルに関連付けられたスキーマを変更することはできます。

* **「送信」タブ**

   * **URL にリダイレクト**

      **リダイレクト URL/パス**:送信アクションの後にアダプティブフォームがリダイレクトされる URL またはパスを指定します。

      **送信アクション**:送信アクションは、ユーザーがアダプティブフォームの「送信」ボタンをクリックするとトリガーされます。 以下が可能です。 [アダプティブフォームでの送信アクションの設定](/help/forms/configuring-submit-actions.md). アダプティブフォームには、すぐに使用できる送信アクションがいくつか用意されています。
      * REST エンドポイントへの送信
      * メールを送信
      * フォームデータモデルを使用して送信
      * AEM ワークフローを起動
      * SharePoint に送信
      * OneDrive に送信
      * Azure Blob Storage に送信

   また、 [デフォルトの送信アクションの拡張](custom-submit-action-form.md) 独自のカスタム送信アクションを作成する場合。

* **メッセージを表示**
   * **メッセージコンテンツ**:フォーム送信時に表示するメッセージをリッチテキストエディターで記述します。 このオプションは、「ありがとうございます」メッセージの表示が有効な場合にのみ選択できます。

## アダプティブフォームの埋め込み  {#aem-container-component}

使用 **[!UICONTROL アダプティブForms — 埋め込み (V2)]** コンポーネントを使用する場合は、新しいアダプティブフォームを埋め込むか、既存のアダプティブフォームをサイトのページに埋め込むことができます。 この [!UICONTROL アダプティブForms — 埋め込み] コンポーネントでは次のことが可能です。

* [既存のアダプティブフォームを埋め込む](#embed-new-af)

* [新しいアダプティブフォームの作成と埋め込み](#embed-existing-af)

### 前提条件 {#prerequisites}

+++ を有効にします。 **アダプティブForms — 埋め込み** 関連付けられたテンプレートのポリシー内のコンポーネント。

有効にするには [!UICONTROL アダプティブForms — 埋め込み (v2)] テンプレートのポリシーのコンポーネントで、次の手順を実行します。

1. 次に移動： [!UICONTROL ページ情報] > [!UICONTROL テンプレートを編集]

1. 次をクリック： [!UICONTROL ポリシー] をクリックし、 **[!UICONTROL アダプティブフォーム — 埋め込み (v2)]** の下のチェックボックス **[!UICONTROL [AEM Archetype プロジェクト名] - Forms]** グループ化する。
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

+++ Site のページに clientlibs を含める

次の場合に **[!UICONTROL フォームがページの幅全体に対応している場合]** オプションが **[!UICONTROL フォームコンテナ]** 設定ダイアログボックスと **コアコンポーネントを使用したアダプティブForms** を使用する場合は、対応するサイトのページに clientlibs を含める必要があります。

![GIF をオーバーレイ](/help/forms/assets/overlaycorecomponent.gif)

AEM SitesページでアダプティブFormsコンポーネントを使用するには、 AEM Archetype/Git リポジトリとデプロイメントパイプラインを使用して、 Customheaderlibs クライアントライブラリと Customfooterlibs クライアントライブラリをAEM Sitesページに含めます。

1. を開きます。 [AEM Formsアーキタイプまたは複製された Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) プロジェクトをテキストエディターで作成します。 たとえば、Visual Studio Code などです。
1. `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml` に移動します。
1. 次の値をコピー： `sling:resourceSuperType`. 例えば、値は `core/wcm/components/page/v3/page`.

   ![sling リソース](/help/forms/assets/slingresource.png)

1. の場所で類似した構造を作成します。 `ui.apps/src/main/content/jcr_root/apps` 同じ `core/wcm/components/page/v3/page`.

   ![オーバーレイ構造](/help/forms/assets/overlaystructure.png)

1. 追加 `customheaderlibs.html` および `customfooterlibs.html` ファイル。

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

   customfooterlibs.html は JavaScript で使用され、customheaderlibs.html は CSS で使用されます。

1. [パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) をクリックして変更をデプロイします。

+++

### 新しいアダプティブフォームを埋め込む {#embed-new-af}

1. AEM Sitesページを編集モードで開きます。
1. コンポーネントブラウザーパネルから、 [!UICONTROL アダプティブForms — 埋め込み (v2)] コンポーネントをページ上に配置します。
1. 次をクリック： **プラス** アイコンが表示され、フォーム作成ウィザードにリダイレクトされます。

   ![アダプティブForms — 埋め込みコンポーネント](/help/forms/assets/aemformcontainer.png)

1. 新しいアダプティブフォームを [!UICONTROL フォームの作成] ウィザード。
1. この [!UICONTROL アセットパス] 作成したアダプティブフォームのパスが既に含まれています
1. 設定を保存します。これで、アダプティブフォームがページに埋め込まれました。

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

### 既存のアダプティブフォームを埋め込む {#embed-existing-af}

1. AEM Sitesページを編集モードで開きます。
1. コンポーネントブラウザーパネルから、 [!UICONTROL アダプティブForms — 埋め込み] コンポーネントをページ上に配置します。
1. 次をタップします。 [!UICONTROL アダプティブForms — 埋め込み] サイトページのコンポーネントをタップし、 ![settings_icon](/help/forms/assets/Smock_Wrench_18_N.svg) をクリックします。 この **[!UICONTROL アダプティブFormsを編集 — 埋め込み]** ダイアログが開きます。
1. に埋め込むアダプティブフォームを参照して選択します。 [!UICONTROL アセットパス].
1. 設定を保存します。これで、アダプティブフォームがページに埋め込まれました。

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

#### アダプティブフォームの埋め込みプロパティの設定

この [!UICONTROL アダプティブフォーム — 埋め込み (v2)] コンポーネント。 内 [!UICONTROL アダプティブFormsの編集 — 埋め込み (v2)] ダイアログでは、次の項目を指定できます。

* **アセットパス**： 埋め込むアダプティブフォームを参照して選択します。また、アセットブラウザーからドロップすると、自動的に入力されます。
* **送信後処理**：フォーム送信時にトリガーするアクションを選択します。お礼のメッセージを表示するため、「ありがとうございます」ページを設けることができます。
   * **「ありがとうございます」メッセージを表示**:フォーム送信時に表示するメッセージをリッチテキストエディターで記述します。 このオプションは、「ありがとうございます」メッセージの表示が有効な場合にのみ選択できます。
   * **「ありがとうございます」ページを表示**:フォーム送信時に表示するページを参照して選択します。 このオプションは、ありがとうページの表示が有効な場合にのみ選択できます。
   * **ありがとうページにリダイレクト**：このオプションを有効にすると、アダプティブフォームが埋め込まれたページはありがとうページに置き換わります。 それ以外の場合は、「ありがとうございます」ページが [!UICONTROL アダプティブForms — 埋め込み] コンポーネントを更新せずに、基になるサイトを更新します。 このオプションは、ありがとうページの表示が有効な場合にのみ選択できます。
* **ページ言語を使用**：アダプティブフォームのロケールではなく、AEM Sites ページのロケールを使用します。
* **フォームにフォーカスを設定**：アダプティブ フォームの最初のフィールドにフォーカスを設定する場合に選択します。
* **フォームはフレームの幅全体をカバーします**:オンにすると、iframe はフォームのレンダリングに使用されません。
* **高さ**:コンテナの高さを指定します。 コンテナのサイズを自動的に変更する場合は、空白のままにします。
* **CSS クライアントライブラリ**:CSS クライアントライブラリへのパスを指定します。

### 埋め込まれたアダプティブフォームを発行する {#publishing-embedded-adaptive-form}

ここでは、AEM Sites ページに埋め込まれたアダプティブフォームを公開するための、次のようなシナリオを考えてみます。

* 初めて AEM Sites ページを公開する場合で、かつページにアダプティブフォームが埋め込まれている場合は、Sites ページに加え、埋め込みアセットも公開します。
* 公開済みサイトページに埋め込まれたアダプティブフォームのみを変更した場合は、元のアセットを公開します。変更内容は、公開されたサイトページに反映されます。公開されたサイトページにはアセットへの参照情報が含まれているため、ページを再公開する必要はありません。
* サイトページに加え、埋め込まれたアダプティブフォームを変更した場合は、サイトページと埋め込みアセットを再公開します。

### 埋め込まれたアダプティブフォームを変更する  {#modifying-embedded-adaptive-form}

埋め込まれたアダプティブフォームの設定やプロパティを変更するには、次のいずれかの操作を行います。

* 元のフォームをアダプティブフォーム内の各エディターで開き、変更します。
* 編集モードでサイトページ内からアダプティブフォームをタップし、続けて「**[!UICONTROL 新しいウィンドウで編集]**」をタップします。元のフォームは、修正可能な編集モードで開きます。

>[!NOTE]
>
>元のフォームに加えた変更は、埋め込まれたフォームに自動的に反映されます。ただし、アダプティブフォームまたはサイトのページを再公開して、公開されたページに変更を反映します。

### ベストプラクティス {#best-practices}

* 元のフォームのヘッダーとフッターは、埋め込まれたフォームには含まれません。
* 埋め込みフォームのユーザードラフトと送信はサポートされ、Forms Portal の「ドラフト」タブと「送信済みのForms 」タブに表示されます。

[AEM Sitesページで、レイアウトモード](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/responsive-layout.html?#defining-layouts-layout-mode) AEM Site のページ内に作成または埋め込まれたアダプティブフォームのサイズを変更できます。

![AF-layout-support](/help/forms/assets/afsite-layoutsupport.gif)

AEM sites ページには、アダプティブフォームへの参照が保持されます。 AEM Sitesページを翻訳すると、アダプティブフォームとその関連する参照アセットが、 [翻訳プロジェクト](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/translation/managing-projects.html?lang=en#adding-pages-assets-to-a-translation-job) を他の言語に変換する
