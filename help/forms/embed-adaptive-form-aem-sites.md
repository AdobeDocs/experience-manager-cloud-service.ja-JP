---
title: アダプティブフォームを AEM Sites ページに追加する方法？
description: AEM の外側にホストされた Web ページか AEM Sites ページに、アダプティブフォームをシームレスに埋め込むことができます。
feature: Adaptive Forms
role: Admin, User, Developer
Keywords: Forms AEM Sites, Embed Form to a Sites page, Adaptive Forms AEM Sites, Embed Adaptive Forms to AEM Page, Embed Forms in an AEM Sites page
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: 958c166585ac7eeb667d73744403558b2dc5ce94
workflow-type: tm+mt
source-wordcount: '3323'
ht-degree: 96%

---

# AEM Sites ページへのアダプティブフォームの埋め込み {#embed-an-adaptive-form-to-aem-sites-page}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html?lang=ja) |
| AEM as a Cloud Service | この記事 |


## 概要 {#overview}

AEM Forms を使用すると、フォーム開発者は AEM サイトページまたは AEM の外側にホストされた web ページにアダプティブフォームをシームレスに埋め込むことができます。埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームに記入およびフォームを送信できます。これにより、ユーザーは web ページのその他の要素との整合性を保つことができ、同時にフォームとの相互作用も保つことができます。これにより、訪問者は、ページを離れることなく、フォームに簡単に入力して送信できます。この統合により、顧客が作成済みのアダプティブフォームを再利用する便利な方法が提供されます。

AEM ページエディターを使用すると、複数のフォームをすばやく作成して AEM Sites ページに追加できます。AEM ページエディターを使用すると、コンテンツ作成者は、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームのコンポーネントを活用して、Sites ページ内にシームレスなデータキャプチャのエクスペリエンスを作成できます。また、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sites ページの様々な機能を使用できます。

AEM Forms にはア&#x200B;**[!UICONTROL ダプティブフォームコンテナおよびアダプティブフォーム**&#x200B;[!UICONTROL （埋め込みコンポーネント）]&#x200B;**が用意されています。]**&#x200B;以下を使用できます。 **[!UICONTROL アダプティブForms — 埋め込み (v2)]** 既存のアダプティブフォームを追加するコンポーネント、またはアダプティブFormsエディターを使用してフォームを作成するコンポーネント **[!UICONTROL アダプティブフォームコンテナ]** をクリックして、エクスペリエンスフラグメントページまたはAEM Sitesページ内に新しいフォームを作成します。

![AEM Sites ページでのアダプティブフォームの例](/help/forms/assets/adaptive-form-in-sites-page.png)

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). 

## Why embed an Adaptive Form in AEM Sites page or AEM Experience Fragment? 

Using **[!UICONTROL Adaptive Forms – Embed(v2)]** in AEM Page Editor lets you create seamless data capture experiences within a Sites page using the power of Adaptive Forms components including dynamic behavior, validations, data integration, generate document of record and business process automation. It also lets you use various features of AEM Sites pages like, versioning, targeting, translation, and multi-site manager, enhancing the overall form creation and management experience. Let's explore some of these features:

* **Versioning:** AEM Sites pages offer [robust versioning capabilities](/help/sites-cloud/authoring/sites-console/page-versions.md), allowing you to track and manage different versions of your forms. This enables you to make changes and enhancements to forms while maintaining the ability to roll back to previous versions if needed. Versioning ensures a controlled and organized approach to form development and evolution.
* **Targeting (Integration with Adobe Target):** With AEM Sites pages targeting capabilities, you can also [personalize the form experience for different audiences](/help/sites-cloud/integrating/integrating-adobe-target.md). By using user segments and targeting criteria, you can tailor the form's content, design, or behavior to specific groups of users. This enables you to provide a personalized and relevant form experience, increasing engagement and conversion rates.
* **Translation:** AEM Sites [seamless integration with translation services](/help/sites-cloud/administering/translation/overview.md), allowing you to translate forms into multiple languages easily. This feature simplifies the localization process, ensuring that your forms are accessible to a global audience. You can manage translations efficiently within AEM translation projects, reducing time and effort required for multilingual form support. See considerations section for more information on translation.  
* **Multi-site Management and Live Copy:** AEM Sites provide robust [Multi-site Management and Live Copy capabilities](/help/sites-cloud/administering/msm/overview.md), enabling you to create and manage multiple websites within a single environment. This feature now lets you reuse forms across different sites, ensuring consistency and reducing duplication efforts. With centralized control and management, you can efficiently maintain and update forms across multiple websites.
* **Themes:** AEM Sites pages provide a framework for designing and maintaining consistent visual styles across multiple web pages. These define colors, fonts, style sheets, and other visual elements that contribute to the overall look and feel of the website. [You can use the themes designed for an AEM Sites page for an Adaptive Form, saving time and effort](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes). 
* **Tagging:** AEM Sites pages allow you to [assign tags or labels to a page, an asset, or other content](/help/implementing/developing/introduction/tagging-framework.md). Tags are keywords or metadata labels that provide a way to categorize and organize content based on specific criteria. You can assign one or more tags to pages, assets, or any other content items within AEM to improve search and categorize the assets. 
* **Locking and Unlocking content:** AEM Sites allow users to [control access and modifications to pages](/help/sites-cloud/authoring/page-editor/edit-content.md) within the AEM Sites environment. When a page is locked, it means that it is protected from unauthorized changes or edits by other users. Only the user who has locked the content or a designated administrator can unlock it to allow modifications. 

In addition, Adaptive Forms in AEM Page Editor use [Adaptive Forms Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja#features). These Core Components provide a standard and easier methods to style and customize the components, identical to [AEM Sites WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja).

-->

## AEM Sites ページまたは AEM エクスペリエンスフラグメントでアダプティブフォームを作成または追加する方法？ {#various-options-to-create-or-embed-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

次のオプションを使用すると、この機能を最大限に活用できます。

* **[承認済みのテンプレートを使用してアダプティブフォームを作成し、AEM Sites ページに埋め込む](#embed-form-using-adaptive-form-wizzard-aem-sites)：**&#x200B;事前に承認されたテンプレートを使用して、組織のブランディングガイドラインやデザイン標準に合ったアダプティブフォームをすばやく作成し、埋め込むことができます。

* **[既存のフォームを AEM Sites ページに追加：](#embed-an-adaptive-form-in-sites-editor)**&#x200B;作成済みのフォームを web サイトに簡単に統合し、訪問者が直接操作できるようにします。

* **[アダプティブフォームをエクスペリエンスフラグメントに変換](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)：** AEM Sites ページに追加されたアダプティブフォームをエクスペリエンスフラグメントに変換して、複数の AEM Sites ページでフォームを再利用します。

* **[カスタムアダプティブフォームを作成し、AEM Sites ページに追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor-or-experience-fragment)：**&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントを使用すると、要件やデザインの環境設定に合わせてカスタマイズし、新規フォームをゼロから作成します。

* **[カスタムアダプティブフォームを作成し、エクスペリエンスフラグメントに追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor)：** AEM エクスペリエンスフラグメントにフォームを追加して、フォームのリーチを拡張し、複数のページやサイトでシームレスに再利用できます。

* **複数のフォームを AEM Sites ページまたはエクスペリエンスフラグメントに追加：**&#x200B;複数のアダプティブフォームを作成し、AEM Sites ページに追加して、ユーザーの環境設定や要件に基づいて複数の選択肢をユーザーに提供します。AEM ページエディターを使用すると、複数のフォームをすばやく作成して AEM Sites ページに追加できます。以下を使用すると、 **[!UICONTROL アダプティブフォームコンテナ]** コンポーネントを複数回追加して、AEM SitesページにアダプティブFormsを追加します。 以下を使用すると、 **[!UICONTROL アダプティブForms — 埋め込み]** AEM Sitesページでコンポーネントを複数回作成する ( **[!UICONTROL フォームはフレームの幅全体をカバーします]** 」オプションが選択されている。 例えば、 **[!UICONTROL フォームはフレームの幅全体をカバーします]** 「 」オプションがオフの場合、AEM Sitesページでは、iframe なしで存在するアダプティブフォームが 1 つだけサポートされます。 を使用してアダプティブFormsをさらに追加するには **[!UICONTROL アダプティブForms — 埋め込み]** コンポーネント、選択 **[!UICONTROL フォームはフレームの幅全体をカバーします]** オプション。

## AEM Sites ページまたは AEM エクスペリエンスフラグメントでアダプティブフォームを作成する際の考慮事項 {#consideration}

* **[!UICONTROL アダプティブフォーム - 埋め込み]**&#x200B;コンポーネントを使用してフォームを作成または追加する場合、そのフォームは AEM Forms の翻訳フローを使用して翻訳およびローカライゼーションが実行されます。 この場合、単一のフォームが維持され、Sites ページのすべての言語コピーで参照されます。**[!UICONTROL アダプティブフォーム - 埋め込み]**&#x200B;コンポーネントでは、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sites ページの様々な機能にアクセスできません。

* **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を使用してフォームを作成または追加する場合、フォームは AEM Sites 翻訳フローを通じて翻訳およびローカライゼーションが実行されます。言語ごとに、Sites ページと対応するフォームの個別のコピー（言語コピー）が生成され、コンテンツ作成者が親ページのフォームのルールを変更する場合は、全言語のフォームのコピーで同じ変更を行う必要があります。**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;では、AEM Sites ページの様々な機能（バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど）を使用できます。


## AEM Sites ページまたは AEM エクスペリエンスフラグメントでアダプティブフォームを作成する際の考慮事項 {#before-you-start-embedding-an-adaptive-form}

新しいアダプティブフォームまたは既存のアダプティブフォームを埋め込む前に、 **[!UICONTROL アダプティブForms — 埋め込み (v2)]**，有効 **アダプティブFormsコアコンポーネント** とを追加します。 **アダプティブFormsクライアントライブラリ** をAEM Sitesページに追加します。

### AEM Cloud Service 環境でのアダプティブフォームコアコンポーネントの有効化

お使いの AEM Cloud Service 環境でアダプティブフォームコアコンポーネントを有効にするには、最新版をインストールします。

### AEM Sites ページまたはエクスペリエンスフラグメントに、アダプティブフォームクライアントライブラリを追加

**[!UICONTROL フォームコンテナ]**&#x200B;設定ダイアログボックスで「**[!UICONTROL フォームがページの幅全体に広がっている場合]**」オプションが選択されており、コアコンポーネントを使用したアダプティブフォームが使用されている場合は、対応する Sites ページに clientlibs を含める必要があります。

![フォームがページオプションの幅全体を覆っている場合、コアコンポーネントを含むアダプティブフォームが使用されます](/help/forms/assets/overlaycorecomponent.gif)

**ケース 1：個別の Sites ページコンポーネントの使用**

次を追加： **Customheaderlibs** および **Customfooterlibs** クライアントライブラリをAEM Sitesページに追加します。 ライブラリを追加するには、次の手順を実行します。

1. [AEM Cloud Service Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html?lang=ja)にアクセスしてクローンを作成します。
2. プランテキストエディターで AEM Cloud Service Git リポジトリフォルダーを開きます。例えば Microsoft Visual Code などです。
3. `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

4. `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

5. `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

6. `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

7. [デプロイメントパイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=ja)して、クライアントライブラリを AEM as a Cloud Service 環境にデプロイします。

>[!NOTE]
>
> カスタム関数のクライアントライブラリは、すべてのフォームで必要な場合にのみハードコードします。 フォームタイプによって異なるライブラリの場合は、次の節で説明するように、テンプレートページポリシーを使用して追加します。

**ケース 2：同じ Sites ページコンポーネントの使用**

フォームを使用してページを作成するために使用するテンプレートのページポリシーに、ランタイムクライアントライブラリまたはカスタム関数ライブラリを含めます。

1. AEM Sites ページまたはエクスペリエンスフラグメントを編集用に開きます。ページを編集用に開くには、ページを選択して「**[!UICONTROL 編集]**」をクリックします。
2. Sites ページまたはエクスペリエンスフラグメントページのテンプレートを開きます。テンプレートを開くには、**[!UICONTROL ページ情報]**&#x200B;に移動し、![ページ情報](/help/forms/assets/Smock_Properties_18_N.svg)／**[!UICONTROL テンプレートを編集]**&#x200B;を選択します。対応するテンプレートがテンプレートエディターで開きます。
3. テンプレートの「**[!UICONTROL ページ情報]**![&#x200B; ページ情報 &#x200B;](/help/forms/assets/Smock_Properties_18_N.svg)」セクションに移動し、「**[!UICONTROL ページポリシー]**」オプションを選択します。 これにより、AEM Sites テンプレートのプロパティが開き、カスタム関数またはランタイムクライアントライブラリを定義できます。
4. 「**[!UICONTROL プロパティ]**」タブの「**[!UICONTROL 追加]**」ボタンをクリックして、新しいカスタム関数ライブラリまたはランタイムライブラリを追加します。
5. 「**[完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3476178?quality=12&learn=on)

### AEM Sites ページまたはエクスペリエンスフラグメントのアダプティブフォーム – 埋め込み（v2）の有効化

テンプレートのポリシーで&#x200B;**[!UICONTROL アダプティブフォーム - 埋め込み（v2）]**&#x200B;コンポーネントを有効にするには、次の手順を実行します。

1. AEM Sites ページまたはエクスペリエンスフラグメントを編集用に開きます。ページを編集用に開くには、ページを選択して「**[!UICONTROL 編集]**」をクリックします。
1. Sites ページまたはエクスペリエンスフラグメントページのテンプレートを開きます。テンプレートを開くには、**[!UICONTROL ページ情報]**&#x200B;に移動し、![ページ情報](/help/forms/assets/Smock_Properties_18_N.svg)／**[!UICONTROL テンプレートを編集]**&#x200B;を選択します。対応するテンプレートがテンプレートエディターで開きます。
1. 構造ビューで、メニューバーから「**[!UICONTROL ポリシー]**」![ポリシー](/help/forms/assets/Smock_FeedManagement_18_N.svg)アイコンをクリックします。**[!UICONTROL 許可されたコンポーネント]**&#x200B;リストで、**[!UICONTROL AEM アーキタイププロジェクト名]** - アダプティブフォーム&#x200B;**[の下にある]アダプティブフォームコンテナ**&#x200B;チェックボックスを選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

## アダプティブフォーム - 埋め込みコンポーネントを使用してアダプティブフォームを埋め込むには： {#embed-an-adaptive-form-in-sites-editor-or-experience-fragment}

以下を使用します。 **[!UICONTROL アダプティブForms — 埋め込み (v2)]** フォーム作成ウィザードを使用して、AEM Sitesエディター内で直接アダプティブフォームを作成するためのコンポーネントです。 結果のフォームは外部エンティティとして保存され、他の Sites ページやスタンドアロンフォームで再利用できます。 要件やデザインの環境設定に合わせて、AEM Sites ページまたはエクスペリエンスフラグメント内で直接新しいフォームを最初から作成できます。単一用途のフォームの場合は、AEM Sites ページへの直接オーサリングをお勧めします。一方、エクスペリエンスフラグメントは、web サイトの複数のページで再利用する必要があるフォームに最適です。

新しいフォームを簡単に埋め込むには、 **[!UICONTROL アダプティブForms — 埋め込み (v2)]**.  例えば、新しい連絡先フォームをAEM SitesページやAEM Experience Fragment に組み込むとします。 AEM Sitesページまたはエクスペリエンスフラグメント内の連絡先フォームに対する更新や変更は、デプロイ先のすべてのページに自動的に適用されます。 これにより、Web サイトのフォームの管理が簡素化され、プロセス全体を合理化しながら、シームレスなユーザーエクスペリエンスを実現します。

使用 **[!UICONTROL アダプティブForms — 埋め込み (v2)]**&#x200B;を使用すると、次のことができます。

* [AEM SitesページのアダプティブFormsウィザードを使用して新しいフォームを埋め込む](#embed-form-using-adaptive-form-wizzard-aem-sites)
* [アダプティブフォームウィザードを使用して、エクスペリエンスフラグメントに新しいフォームをFormsに埋め込む](#embed-form-using-adaptive-form-wizzard-experience-fragment)
* [AEM Sites ページへのアダプティブフォームの埋め込み](#embed-an-adaptive-form-in-sites-editor)
* [エクスペリエンスフラグメントに既存のフォームを埋め込む](#embed-an-adaptive-form-in-experience-fragment)
* [AEM Sites ページ内のアダプティブフォームをエクスペリエンスフラグメントに変換](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### AEM SitesページのアダプティブFormsウィザードを使用して新しいフォームを埋め込む {#embed-form-using-adaptive-form-wizzard-aem-sites}

新しいフォームをAEM Sitesページに埋め込む手順は次のとおりです。

1. AEM Sites ページを編集モードで開きます。
1. コンポーネントブラウザーパネルから、**[!UICONTROL アダプティブフォーム - 埋め込み（v2）]**&#x200B;コンポーネントをページ上にドラッグ＆ドロップします。
1. 「**プラス**」アイコンをクリックすると、フォーム作成ウィザードにリダイレクトされます。

   ![アダプティブフォーム - 埋め込みコンポーネント](/help/forms/assets/aemformcontainer.png)

1. **[!UICONTROL フォーム作成]**&#x200B;ウィザードから新しいアダプティブフォームを作成します。
**[!UICONTROL アセットパス]**&#x200B;には、作成されたアダプティブフォームのパスが既に含まれています
1. 設定を保存します。これで、アダプティブフォームがページに埋め込まれました。

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

次に、次の操作を行います。 [送信アクションの設定](/help/forms/configuring-submit-actions.md) 埋め込まれたアダプティブフォームの詳細プロパティを作成するには、フォーム作成ウィザードを使用します。


### アダプティブフォームウィザードを使用して、エクスペリエンスフラグメントに新しいフォームをFormsに埋め込む {#embed-form-using-adaptive-form-wizzard-experience-fragment}

エクスペリエンスフラグメントに新しいフォームを埋め込む手順は、次のとおりです。

1. エクスペリエンスフラグメントを編集モードで開きます。
1. コンポーネントブラウザーパネルから、**[!UICONTROL アダプティブフォーム - 埋め込み（v2）]**&#x200B;コンポーネントをページ上にドラッグ＆ドロップします。
1. 「**プラス**」アイコンをクリックすると、フォーム作成ウィザードにリダイレクトされます。

   ![アダプティブフォーム - 埋め込みコンポーネント](/help/forms/assets/aemformcontainer.png)

1. **[!UICONTROL フォーム作成]**&#x200B;ウィザードから新しいアダプティブフォームを作成します。
**[!UICONTROL アセットパス]**&#x200B;には、作成されたアダプティブフォームのパスが既に含まれています
1. 設定を保存します。これで、アダプティブフォームがページに埋め込まれました。

次に、次の操作を行います。 [送信アクションの設定](/help/forms/configuring-submit-actions.md) 埋め込まれたアダプティブフォームの詳細プロパティを作成するには、フォーム作成ウィザードを使用します。

### AEM Sites ページへのアダプティブフォームの埋め込み {#embed-an-adaptive-form-in-sites-editor}

を使用 **[!UICONTROL アダプティブForms — 埋め込み (v2)]** コンポーネントを使用すると、既存のアダプティブフォームをAEM Sites内のページに容易に統合できます。 この機能は、アダプティブFormsの適応性と再利用性を大幅に向上させ、作成済みのフォームを再利用する便利な方法を提供します。 例えば、AEM Sitesページに連絡先フォームを組み込むと、フォームを複数回再作成しなくても済むとします。

Sites ページでアダプティブフォームを作成するには、次の手順を実行します。

1. AEM Sites ページを編集モードで開きます。
1. **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントをコンポーネントブラウザーから Sites ページにラッグ＆ドロップします。
1. Sites ページに埋め込まれた&#x200B;**[!UICONTROL アダプティブフォーム - 埋め込み]**&#x200B;コンポーネントを選択し、アクションバーの ![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) を選択します。**[!UICONTROL アダプティブフォーム - 埋め込みを編集]**&#x200B;ダイアログが開きます。
1. **[!UICONTROL アセットパス]**&#x200B;に埋め込むアダプティブ フォームを参照して選択します。
1. 設定を保存します。これで、アダプティブフォームがページに埋め込まれました。

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

次に、次の操作を行います。 [送信アクションの設定](/help/forms/configuring-submit-actions.md) 埋め込まれたアダプティブフォームの詳細プロパティを作成するには、フォーム作成ウィザードを使用します。

### エクスペリエンスフラグメント内に既存のアダプティブフォームを埋め込む {#embed-an-adaptive-form-in-experience-fragment}

また、フォームをAEM Experience Fragment に埋め込むことで、フォームのアクセシビリティを拡張することもできます。 エクスペリエンスフラグメント内にアダプティブフォームを作成するには、次の手順を実行します。

1. エクスペリエンスフラグメントを編集モードで開きます。
1. **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントを、コンポーネントブラウザーからエクスペリエンスフラグメントにドラッグ＆ドロップします。
1. エクスペリエンスフラグメントに埋め込まれた&#x200B;**[!UICONTROL アダプティブフォーム - 埋め込み]**&#x200B;コンポーネントを選択し、アクションバーの ![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) を選択します。**[!UICONTROL アダプティブフォーム - 埋め込みを編集]**&#x200B;ダイアログが開きます。
1. **[!UICONTROL アセットパス]**&#x200B;に埋め込むアダプティブ フォームを参照して選択します。
1. 設定を保存します。アダプティブフォームがエクスペリエンスフラグメントに埋め込まれました。

次に、次の操作を行います。 [送信アクションの設定](/help/forms/configuring-submit-actions.md) 埋め込まれたアダプティブフォームの詳細プロパティを作成するには、フォーム作成ウィザードを使用します。

### AEM Sites ページ内のフォームをエクスペリエンスフラグメントに変換 {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Sites ページエディター内にある既存のアダプティブフォームをエクスペリエンスフラグメントに変換すると、複数のページやサイトでフォームを再利用できます。

AEM Sites ページ内のアダプティブフォームをエクスペリエンスフラグメントに変換するには、次の手順を実行します。

1. アダプティブフォームを含む AEM Sites ページ（アダプティブフォームコンテナコンポーネント内）を編集モードで開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. メニューバーで、![「エクスペリエンスフラグメントバリエーションに変換」アイコン](/help/forms/assets/Smock_FilingCabinet_18_N.svg)を選択します。「エクスペリエンスフラグメントバリエーションに変換」アイコン。

   ![ファイルキャビネットのロゴをクリックして、AEM Sites ページのアダプティブフォームをエクスペリエンスフラグメントに変換](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   アダプティブフォームコンテナを新しいエクスペリエンスフラグメントに変換するか、既存のエクスペリエンスフラグメントに追加するためのダイアログボックスが表示されます。

1. **[!UICONTROL エクスペリエンスフラグメントバリエーションに変換]**&#x200B;ダイアログボックスで、次のオプションの値を設定します。

   * **アクション：**&#x200B;新しいエクスペリエンスフラグメントを作成するか、既存のエクスペリエンスフラグメントに追加するかを選択します。
   * **親パス：**&#x200B;エクスペリエンスフラグメントをホストするフォルダーのパスを指定します。このオプションは、新しいエクスペリエンスフラグメントを作成する場合にのみ使用できます。
   * **テンプレート：**&#x200B;エクスペリエンスフラグメントテンプレートのパスを指定します。エクスペリエンスフラグメントテンプレートがない場合は、[作成します](/help/implementing/developing/extending/experience-fragments.md)。このオプションは、アダプティブフォームを既存のエクスペリエンスフラグメントに追加する場合にのみ使用できます。
   * **フラグメントのタイトル：**&#x200B;エクスペリエンスフラグメントのタイトルを指定します。タイトルは、エクスペリエンスフラグメントを一意に識別します。
   * **フラグメントのタイトル：**&#x200B;エクスペリエンスフラグメントのタイトルを指定します。このタグは、エクスペリエンスフラグメントのカテゴリを一意に識別します。

## アダプティブフォーム埋め込み (v2) プロパティの設定

**[!UICONTROL アダプティブフォーム - 埋め込み（v2）]**&#x200B;コンポーネントの詳細設定をカスタマイズできます。**[!UICONTROL アダプティブフォーム - 埋め込み（）]**&#x200B;ダイアログでは、次の項目を指定できます。

* **アセットパス**：埋め込むアダプティブフォームを閲覧して選択します。また、アセットブラウザーからドロップすると、自動的に入力されます。
* **送信後処理**：フォーム送信時にトリガーするアクションを選択します。お礼のメッセージを表示するため、「ありがとうございます」ページを設けることができます。
   * **ありがとうメッセージの表示**：フォーム送信時に表示するメッセージをリッチテキストエディターで書き込みます。このオプションは、ありがとうメッセージの表示が有効な場合にのみ選択できます。
   * **ありがとうページの表示**： フォームの送信時に表示するページを参照して選択します。このオプションは、ありがとうページの表示が有効な場合にのみ選択できます。
   * **ありがとうページにリダイレクト**：このオプションを有効にすると、アダプティブフォームが埋め込まれたページはありがとうページに置き換わります。 このオプションを有効にしない場合は、**[!UICONTROL アダプティブフォーム - 埋め込み]**&#x200B;コンポーネント内のアダプティブフォームがありがとうページに置き換わり、ベースとなる Sites ページは更新されません。このオプションは、ありがとうページの表示が有効な場合にのみ選択できます。
   * **感謝状メッセージ**：フォームが正常に送信された後に画面に表示される簡単な確認または確認。
   * **感謝のページ**：フォームが正常に送信された後に表示するページを参照および選択します。

* **ページ言語を使用**：アダプティブフォームのロケールではなく、AEM Sites ページのロケールを使用します。このオプションは、アダプティブフォーム (Foundation) にのみ適用されます。
* **フォームにフォーカスを設定**：アダプティブフォームの最初のフィールドにフォーカスを設定する場合に選択します。このオプションは、アダプティブフォーム (Foundation) にのみ適用されます。
* **テーマ**： アダプティブフォームのコンポーネントのスタイルを定義するテーマを選択します。スタイル設定には、フォントスタイル、背景色、サイズ、配置など、外観のプロパティが含まれます。このオプションは、アダプティブフォーム (Foundation) にのみ適用されます。

  >[!NOTE]
  >
  > 以下を使用すると、 **ページ言語を使用**, **フォームにフォーカスを設定** および **テーマ** のオプションは、アダプティブフォーム (Foundation) に対してのみ使用できます。

* **フォームはフレームの幅全体をカバーします**：インラインフレーム (iframe) は、アダプティブフォームをAEM Sitesページに読み込むHTML要素です。

   * 次の場合、 **[!UICONTROL フォームはフレームの幅全体をカバーします]** チェックボックスがオンの場合、アダプティブフォームは配置されるコンテナの全幅を占有します。 この場合、iframe はフォームのレンダリングには使用されません。 アダプティブフォームのレイアウトとデザインは、コンテナの幅全体に適応し、レスポンシブで、様々な画面サイズに調整できます。 このオプションを使用すると、AEM Sites ページ内に複数のアダプティブフォームを埋め込むことができます。

     >[!NOTE]
     >
     > 複数のフォームをAEM Sitesページに埋め込むには、 **[!UICONTROL フォームはフレームの幅全体をカバーします]** チェックボックス。

   * 次の場合、 **[!UICONTROL フォームはフレームの幅全体をカバーします]** チェックボックスがオフの場合、アダプティブフォームはコンテナの幅全体をカバーしません。 代わりに、iframe を使用してフォームをレンダリングします。このフォームは、特定の幅を超えて拡張することはできません。 この方法は、アダプティブフォームに明確な境界があり、コンテナ内でアダプティブフォームの隣にある他の AEM コンポーネントと共存する必要がある場合に役立ちます。このオプションを選択しない場合、AEM Sitesページで iframe を使用せずに埋め込むアダプティブFormsは 1 つだけになります。

     >[!NOTE]
     >
     > AEM Sitesページでは、iframe なしで存在するアダプティブフォームは 1 つだけサポートされています。 を使用してアダプティブFormsをさらに追加するには **[!UICONTROL アダプティブForms — 埋め込み]** コンポーネント、選択 **[!UICONTROL フォームはフレームの幅全体をカバーします]** オプション。

* **高さ**：コンテナの高さを指定します。コンテナのサイズを自動的に変更するには、空白のままにします。
* **CSS クライアントライブラリ**：CSS クライアントライブラリへのパスを指定します。

<!--
In AEM Sites page, you can add an Adaptive Form using:

* **Adaptive Forms - Embed component**
   Adaptive Forms - Embed component enables AEM Sites authors to include an existing Adaptive Form within an AEM Sites page, thereby enhancing the reusability of adaptive forms. Existing Adaptive Forms can be used standalone or embedded in the site page. This integration provides a convenient way for customers to reuse Adaptive Forms they have already created.

* **Asset browser**
  All the forms are available under Assets. You can drag-drop the form as an asset on your page.

## Prerequisites {#prerequisites}

 To embed an Adaptive Form in an AEM Sites page that uses an editable template, ensure that the AEM Form component is configured as an allowed component in the associated template. 

In case **Adaptive Forms - Embed component** is not visible in the **Component browser panel** of AEM sites page, perform the following steps as illustrated in the video.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

In case Sites page is using a static template, you need to configure it in the paragraph system of the site page. 

## Embedding an Adaptive Form {#af-component}

To embed an Adaptive Form using the **[!UICONTROL Adaptive Forms - Embed]** component:

1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the [!UICONTROL Adaptive Forms - Embed] component on the page. Alternatively, you can search for an Adaptive Form in the Assets browser and drag-drop it onto the Sites page. You can add a new Adaptive Form or embed an existing Adaptive Form. 

   >[!NOTE]
   >
   >Multiple Adaptive Forms - Embed components on a page are not supported.

1. To create and embed a new form, on the component toolbar, select the **Create Form** icon. A window to create the form opens. 

1. Select the embedded Adaptive Forms - Embed component in the sites page, and then select ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit Adaptive Forms - Embed]** dialog opens.
1. In the Edit Adaptive Forms - Embed dialog, specify the following.

    **Asset Type:** Select the type of asset to embed. 
    * **Asset Path**: Browse and select the Adaptive Form to embed. It is auto-populated if you dropped it from the Assets browser.
    * **Post Submission** : Select the action to trigger on form submission. You can choose to show a thank you message or a thank you page.
        * Show

        * **Thank You Message**: Write a message using the rich text editor to show on form submission. This option is available only when you choose to show a thank you message.
        * **Thank You Page**: Browse and select the page to display on form submission. This option is available only when you choose to show a thank you page.
           * **Redirect to thank you page**: Enable the option to replace the page containing the embedded Adaptive Form with thank you page. Otherwise, the thank you page replaces the Adaptive Form in the [!UICONTROL Adaptive Forms - Embed] component, without refreshing underlying sites the page. This option is available only when you choose to show a thank you page.
    * **Use Page Language**: Use local of the AEM Sites page instead locale of Adaptive Form.
    * **Set Focus on Form**: Select to set the focus on the first field of the Adaptive Form.
    * **Theme**: Select a theme that defines styling for components of your Adaptive Form. Styling includes appearance properties such as font style, background color, dimensions, and alignment.
    * **Form covers entire width of the frame**: If checked, iframe is not used to render the form. 
    * **Height**: Specify the height of the container. Leave it blank to automatically resize the container.
    * **CSS Client library**: Specify path to a CSS client library.

1. Save the settings. The Adaptive Form  is now embedded in the page.


AEM site also lets you create an Adaptive Form on the fly using the Adaptive Forms - Embed component. Follow the steps to create an Adaptive Form using the **Adaptive Forms - Embed component** on AEM sites page:
1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the Adaptive Forms - Embed component on the page.
1. Click the **Plus** icon and you are redirected to the form creation wizard.

    ![Adaptive Forms - Embed Component](/help/forms/assets/aemformcontainer.png)

1. You can now embed an Adaptive Form on AEM site pages using the [!UICONTROL AEM Forms Container Component].
-->

## 埋め込まれたアダプティブフォームの公開 {#publishing-embedded-adaptive-form}

ここでは、AEM Sites ページに埋め込まれたアダプティブフォームを公開するための、次のようなシナリオを考えてみます。

* 初めて AEM Sites ページを公開する場合で、かつページにアダプティブフォームが埋め込まれている場合は、Sites ページに加え、埋め込みアセットも公開します。
* 公開済みサイトページに埋め込まれたアダプティブフォームのみを変更した場合は、元のアセットを公開します。変更内容は、公開されたサイトページに反映されます。公開されたサイトページにはアセットへの参照情報が含まれているため、ページを再公開する必要はありません。
* サイトページに加え、埋め込まれたアダプティブフォームを変更した場合は、サイトページと埋め込みアセットを再公開します。

## 埋め込まれたアダプティブフォームの公開  {#modifying-embedded-adaptive-form}

埋め込まれたアダプティブフォームの設定やプロパティを変更するには、次のいずれかの操作を行います。

* それぞれのエディターのアダプティブフォームで元のフォームを開いて、変更します。
* 編集モードで開いた Site ページ内からアダプティブフォームを選択し、「**[!UICONTROL 新しいウィンドウで編集]**」をクリックします。元のフォームは、修正可能な編集モードで開きます。

>[!NOTE]
>
>元のフォームに加えた変更は、埋め込まれたフォームに自動的に反映されます。ただし、公開済みページに変更内容を反映するために、アダプティブフォームまたはサイトページを再公開する必要があります。

## ベストプラクティス {#best-practices}

AEM Sites ページにアダプティブフォームを埋め込む際は、以下の点に留意してください。

* 元のフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ユーザードラフトと埋め込みフォームの送信はサポートされており、フォームポータル上の「下書き」タブや「送信済みフォーム」タブに表示されます。
* 元のフォームに設定された送信アクションは、埋め込まれたフォームでも保持されます。
* 元のフォームに Adobe Analytics が設定されている場合、埋め込まれたフォームの分析データは Adobe Analytics でキャプチャされます。ただし、フォームの分析レポートでは使用できません。

## 関連トピック {#see-also}

* [コアコンポーネントベースのスタンドアロンのアダプティブフォームを作成する](/help/forms/creating-adaptive-form-core-components.md)
* [コアコンポーネントベースのアダプティブフォームを AEM Sites ページで直接作成する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
