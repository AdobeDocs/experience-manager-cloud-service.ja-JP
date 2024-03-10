---
title: AEM FormsEdge Delivery Servicesの概要
description: AEM FormsEdge Delivery Servicesは、効率的なデータ収集とユーザーエンゲージメントの将来を想像できるように、ピークパフォーマンスを実現するために構築されています。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 17%

---

# AEM FormsEdge Delivery Services

AdobeのAEM FormsEdge Delivery Servicesを使用して、フォームの作成を合理化し、完了率を高めます。 これらの強力で合成可能なサービスにより、優れたパフォーマンスと視覚的な魅力を備えたエンタープライズクラスのフォームを構築できます。 AEMは、ユーザーエクスペリエンスとビジネス目標の両方を優先し、超高速読み込み時間とフォームのコンバージョンの向上を保証します。

サービスを使用して以下のことが行えます。

* **優れた登録エクスペリエンスの構築**：低速なインターネット接続でも、すばやく読み込んでレンダリングする登録エクスペリエンスを構築します。 読み込み時間の短縮と最適化されたユーザーエクスペリエンスは、フォームの完了率の向上とコンバージョン率の向上に貢献します。

* **任意のツールを使用して登録エクスペリエンスを作成**：コンテンツソースを分離することで、オーサリングの効率を向上させます。 標準では、 **ドキュメントベースのオーサリング** (Microsoft SharePointまたはGoogle Drive) および **AEM authoring** ( アダプティブFormsエディター )。 そのため、同じフォーム上で複数のコンテンツソースを操作し、Microsoft Excel、Googleシート、アダプティブFormsエディターなどの好みのオーサリングツールを使用できます。

* **開発者向けのツールセットを使用：** AEM Formsは、プレーンHTML、最新の CSS、Vanilla JavaScript を使用して、通常のオーバーヘッドなしで例外的なエクスペリエンスを作成します。 HTML、CSS および JS の基本的な知識を持つ開発者は、独自のコンポーネントを構築でき、特定の言語やフレームワークを学ぶ必要はありません。 パイプラインや待機は不要です。コードを GitHub にチェックインすると、変更は有効になります。 さらに、パイプラインや待機は必要ありません。コードを GitHub にチェックインすると、変更が反映されます。


## AEM FormsEdge Delivery Servicesの概要 {#edge-overview}

次の図は、Microsoft Excel またはGoogleシート（ドキュメントベースの編集）でコンテンツを編集し、Edge Delivery Servicesに公開する方法を示しています。 また、アダプティブFormsエディターを使用したAEMの公開方法も表示されます。

![Edge Delivery のアーキテクチャ](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

Edge 配信サービスは、web サイト上のコンテンツの非常に柔軟なオーサリングを可能にする、構成可能なサービスセットです。前述のように、 [AEM content management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=ja) 次を使用 [AEM authoring](/help/implementing/universal-editor/introduction.md) 同様に [ドキュメントベースのオーサリング](https://www.aem.live/docs/authoring)

例えば、Microsoft Excel やGoogleシートから直接コンテンツを使用できます。 つまり、これらのソースのコンテンツを Web サイト上のフォームにすることができます。 新しいコンテンツは、再作成プロセスなしで即座に追加されます。

Edge 配信サービスでは GitHub を利用しているので、ユーザーは自分の GitHub リポジトリから直接コードを管理およびデプロイできます。例えば、GoogleシートまたはMicrosoft Excel でフォームを作成し、GitHub で CSS と JavaScript を使用してフォームのコンポーネントを開発することができます。 準備が整ったら、Sidekick ブラウザー拡張機能を使用して、コンテンツの更新をプレビューおよび公開できます。

AEM FormsEdge Delivery Servicesは、 [アダプティブFormsブロック](/help/edge/docs/forms/create-forms.md) をクリックして、フォームをEdge Delivery Servicesサイトに追加します。

### AEM FormsEdge Delivery Servicesの主な機能

ドキュメントベースのオーサリング基本的な一連の機能とAEMのオーサリングでは、ドキュメントベースのオーサリング以外の追加機能がロック解除され、より複雑でインタラクティブなフォームを構築できます。 次の表は、両方の主な機能を示しています。

<!-- 

>[!BEGINTABS]

>[!TAB Document-based authoring]

Document-based authoring is a versatile option suitable for creating simple forms with essential functionalities. It allows you to integrate various input types like text fields, dropdown menus, and radio buttons, enabling you to collect user data effectively. It offers a basic version of rules to add dynamic behaviour to forms. Key features of Document-based authoring are: 

* **[HTML5-based Form Field components](/help/edge/docs/forms/form-components.md)**: AEM Forms Edge Delivery Services allow you to create user-friendly and interactive forms using form components based on HTML5 [input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, and <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elements. These components cater to different types of data collection and can be easily customized to fit your specific needs.  

* **Accessibility**: The fields in the form block are accessible. Each label is linked with its respective input element, and IDs are auto-generated for linking. Descriptions associated with fields are linked via the aria-describedby attribute. Keyboard navigation using the standard Tab/Shift + Tab keys is supported.

* **[Styling](/help/edge/docs/forms/style-theme-forms.md)**: Each form field has a fixed HTML structure that can be easily decorated using custom CSS or JavaScript files. Selectors for targeting fields in CSS and JS are provided based on type and name. You can easily create new selectors due to the standradized structure and style your form. 

* **Basic Rules**: Easily create logic that adjusts field visibility, validation, and behavior based on user input or predefined conditions. Rules offer a flexible and intuitive way to add intelligence to your forms, ensuring they adapt seamlessly based on user inputs.

* **Validations**: Before submission, the form is validated, and invalid fields are appropriately marked with error messages displayed to the user. Adaptive Forms Block support all the HTML form validation, supported by modern browsers, and provide additional validation mechanism like validation script, file size, file type, overall file size, and more. 

* **File Uploads**: You can add file attachment capabilities to your forms. Whether you need to gather documents, images, or other files from your users, file upload functionality serves you effortlessly. With custom handling options available, you can tailor the file upload process to suit your specific requirements.

* **reCAPTCHA**: Benefit from seamless integration of Google reCAPTCHA into your forms with our out-of-the-box (OOTB) support. Safeguard your forms against fraudulent activities, spam, and abuse, while maintaining a smooth and uninterrupted user experience. Adaptive Forms Block supports reCaptcha V3 and reCaptcha Enterprise. 

* **Send email notification on form submission**: Eliminate the hassle of manual follow-ups and ensure timely communication with our built-in email automation for form submissions. This integrated solution lets you effortlessly notify relevant parties, including sending form data, whenever someone fills out a form on your website. No need for complex configurations or additional tools – it's ready to use out of the box.

>[!TAB AEM Authoring]

AEM Authoring unlocks additional capabilities beyond the document-based authoring, empowering you to build more complex and interactive forms. In additon to the features of Document-based authoring, AEM authoring offers the following additional features:  

* Advanced Rules: Define logic-based actions within your forms. You can use rules to conditionally show or hide form sections, pre-populate fields based on user input, and perform various validations to ensure data integrity.

* Server-side extensibility: Extend the functionalities of your forms by integrating them with server-side logic. This allows you to perform complex calculations, interact with external systems, and automate specific tasks based on user actions within the form.
* Streamline workflows and data management: Leverage the power of AEM to:
    * Design user-friendly forms using AEM editors.
    * Generate a "Document of Record" for secure and tamper-proof archiving of submitted data.
    * Facilitate e-signing with Adobe Sign for a smooth and secure signing experience.
    * Automate business processes through AEM workflows, triggering actions based on form submissions.
    * Effortlessly integrate with various data sources, enabling seamless data flow and exchange.

>[!ENDTABS]



## Start creating forms

-->

|                                           | ドキュメントベースのオーサリング | AEMオーサリング ( アダプティブFormsエディター ) |
| ----------------------------------------- | ------------------------ | ------------------------------------ |
| **フォーム機能** |                          |                                      |
| アクセシブルなコンポーネント | ✓ | ✓ |
| 標準化されたHTML構造 | ✓ | ✓ |
| ルールと検証 | ✓ | ✓ |
| 添付ファイル（ファイルのアップロード） | ✓ | ✓ |
| Google reCAPTCHA | ✓ | ✓ |
| カスタムコンポーネント | ✓ | ✓ |
| 電子メールに送信 | ✓ | ✓ |
| **高度な機能** |                          |                                      |
| ビジュアルルールエディターを使用した高度なルール |                          | ✓ |
| サーバー側の拡張機能 |                          | ✓ |
| 複数の送信アクション |                          | ✓ |
| **フォームデザインと管理** |                          |                                      |
| WYSIWYG 編集用のアダプティブFormsエディター |                          | ✓ |
| **統合** |                          |                                      |
| レコードのドキュメント |                          | ✓ |
| Adobe Sign との統合 |                          | ✓ |
| Adobe Analyticsとの統合 |                          | ✓ |
| Marketoとの統合 |                          | ✓ |
| 複数のデータソースとの統合 |                          | ✓ |
| 複数の送信アクション |                          | ✓ |


## フォームの作成を開始

* [はじめに — 開発者向けチュートリアル](/help/edge/docs/forms/tutorial.md)
* [Google Sheet またはMicrosoft Excel を使用したフォームの作成](/help/edge/docs/forms/create-forms.md)
* [Microsoft Excel またはGoogleシートに直接フォームを送信する](/help/edge/docs/forms/submit-forms.md)
* [フォームの外観を変更する](/help/edge/docs/forms/style-theme-forms.md)


<!-- 

## Start creating forms

<div>

  <style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using eds forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an eds form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Customize a theme</b>
        </a>
        <p>Create a consistent brand image by applying the same theme across forms.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Add validations to form fields" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Apply field validations</b>
        </a>
        <p>Reduce errors and frustration by checking form inputs for proper formatting.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Use rules to add dynamic behaviour to a form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use rules to add dynamic behaviour to a form</b>
        </a>
        <p>Reuse preconfigured fragments across multiple forms.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Add repeatable sections</b>
        </a>
        <p>Effortlessly create and add repeatable sections to a form.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Create custom forms components using standard JavaScript and CSS"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create custom components</b>
        </a>
        <p>Use standard JavaScript and CSS to create components and themes.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->