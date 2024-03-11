---
title: AEM FormsEdge Delivery Servicesの概要
description: AEM FormsEdge Delivery Servicesは、効率的なデータ収集とユーザーエンゲージメントの将来を想像できるように、ピークパフォーマンスを実現するために構築されています。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 67d9eaaf18725403f6a152b04e022cdca6902de0
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 2%

---

# AEM FormsEdge Delivery Services

AEM FormsEdge Delivery Servicesは、作成者がすばやく更新および公開でき、新しいフォームが迅速に起動される、迅速な開発環境を可能にする、合成可能なサービスのセットです。

AEM FormsEdge Delivery Servicesは、エンゲージメントとコンバージョンを促進する優れたフォームエクスペリエンスを提供し、オーサリングと開発が容易なインパクトの大きいエクスペリエンスを実現します。

これらのサービスを使用すると、次のことができます。

* **任意のツールを使用して、登録エクスペリエンスを作成します。** コンテンツソースを分離してオーサリング効率を向上させます。 標準では、ドキュメントベースのオーサリング (Microsoft SharePointまたはGoogle Drive) とAEMのオーサリング ( アダプティブFormsエディター ) の両方を使用できます。 そのため、同じフォーム上で複数のコンテンツソースを操作し、Microsoft Excel、Googleシート、アダプティブFormsエディターなどの好みのオーサリングツールを使用できます。

* **優れたデジタル登録エクスペリエンスを提供：** すばやく読み込んでレンダリングするデジタル登録エクスペリエンスを配信します。 読み込み時間の短縮と最適化されたユーザーエクスペリエンスにより、フォームの完成率とコンバージョン率が向上します。

* **開発者向けのツールセットを使用：** AEM Formsは、プレーンHTML、最新の CSS、バニラ JavaScript を使用して、例外的なエクスペリエンスを作成し、特定のフレームワークの急激な学習曲線を回避します。 基本的な Web 開発スキルを持つ開発者は、フォームのコンポーネントやエクスペリエンスをカスタマイズし、容易に構築できます。 パイプラインの実行を待つ必要はありません。コードを Github にチェックインするだけで、変更は有効になります。

## AEM FormsEdge Delivery Servicesの概要 {#edge-overview}

次の図は、Microsoft Excel またはGoogleシート（ドキュメントベースの編集）でフォームを編集し、Edge Delivery Servicesに公開する方法を示しています。 また、アダプティブFormsエディターを使用したAEMの公開方法も表示されます。

![Edge Delivery のアーキテクチャ](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

AEM Forms Edge Delivery Services は、Web サイト上でフォームを作成する際の柔軟性を高める、合成可能な一連のサービスです。 AEMコンテンツ管理を [AEM authoring](/help/forms/creating-adaptive-form-core-components.md) 同様に [ドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md).

例えば、Microsoft Excel やGoogleシートで直接フォームを作成し、これらのスプレッドシートを Web サイト用のフォームに変換したとします。 新しいフォームフィールドなどの新しいフォームコンテンツは、再構築プロセスを必要とせずに、Web サイト上で即座に使用できます。

Edge 配信サービスでは GitHub を利用しているので、ユーザーは自分の GitHub リポジトリから直接コードを管理およびデプロイできます。例えば、次のいずれかの方法でフォームを書き込むことができます。 [Google Sheet またはMicrosoft Excel](/help/edge/docs/forms/create-forms.md) また、フォームのコンポーネントは、GitHub で CSS と JavaScript を使用して開発できます。 準備が整ったら、 [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content) コンテンツの更新をプレビューおよび公開するためのブラウザー拡張機能。

![インストールAEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

AEM FormsEdge Delivery Servicesは、 [アダプティブFormsブロック](/help/edge/docs/forms/create-forms.md) をクリックして、フォームをEdge Delivery Servicesサイトに追加します。

次の中から選択： [ドキュメントベースのオーサリング](#document-based-authoring-features) および [AEM authoring](#aem-authoring-features) は、具体的な要件に応じて異なります。

名前や電子メールなどの基本情報を収集するだけの簡単なフォーム（お問い合わせください。フォーム、リードジェネレーションフォーム、またはサービスリクエストフォーム）の場合、データをスプレッドシートに送るだけでよい場合、 [ドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md) 完璧なフィットです。 これらのフォームは、Google Docs のドキュメントと同様に作成できます。

複数のパネルの必要性、複雑なルールとビジネスロジック、データの操作、外部システムとの統合、AEM機能を使用したワークフローの合理化など、フォームがより複雑になった場合は、 [AEM Authoring](/help/forms/creating-adaptive-form-core-components.md) はより良い選択肢です。


### ドキュメントベースのオーサリングとAEMオーサリングの主な機能

ドキュメントベースのオーサリングには、基本的な機能のセットが用意されています。AEMオーサリングでは、ドキュメントベースのオーサリング以外の追加機能をロック解除し、より複雑でインタラクティブなフォームを作成できます。 ドキュメントベースのオーサリングとAEMオーサリングの両方の主な機能は次のとおりです。

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

#### ドキュメントベースのオーサリング機能

ドキュメントベースのオーサリングを使用すると、Microsoft Excel やGoogle Sheet などの使い慣れたツールを使用してフォームを作成できます。 これらのフォームは、次の機能を提供します。

* 使いやすいエクスペリエンスのためのアクセシブルなコンポーネント。
* 一貫性のあるレンダリングのための標準化されたHTML構造。
* ルールと検証を使用して、データの正確性を確保します。
* 追加情報を収集するためのファイル添付オプション。
* スパム保護のためのGoogle reCAPTCHA 統合。
* 特定のニーズに合わせてカスタムフォームコンポーネントを作成する機能。
* フォームデータをMicrosoft Excel、Googleシート、電子メールアドレスに直接送信する。

#### AEMオーサリング機能

AEMオーサリング ( アダプティブFormsエディターを使用 ) には、フォームを作成するための WYSIWYG インターフェイスが用意されており、ドキュメントベースオーサリングのすべての機能に加えて、様々な機能を提供しています。

* 複雑なロジックを作成するための高度なルールエディター。
* カスタム機能用のサーバー側の拡張機能。
* WYSIWYG で編集操作を実行して、フォームの作成と視覚化を容易にします。
* 送信されたデータの改ざん防止アーカイブを作成するレコードのドキュメント機能。
* 電子署名用のAdobe Signとの統合。
* フォーム送信時にAdobe Workfront Fusion シナリオをトリガーするAdobe Workfront Fusion との統合。
* フォームの事前入力やデータの送信を行うための様々なデータソースとの統合。
* データ構造と様々なデータソースとのやり取りを定義するフォームデータモデル。
* データをMicrosoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics、その他多くのデータソースに送信するなど、フォーム送信を処理するための複数の送信アクションを設定できる機能。

基本的に、AEM Authoring はドキュメントベースのオーサリングの基盤を基に構築され、複雑なフォームを作成および管理するためのより高度なツールキットを提供します。

### オーサリングワークフロー

![ドキュメントベースのオーサリング](/help/edge/assets/document-based-authoring-workflow.png)

![AEM authoring](/help/edge/assets/aem-authoring-workflow.png)


## フォームの作成を開始

* [AEM FormsEdge Delivery Servicesの概要](/help/edge/docs/forms/tutorial.md)
* [Google Sheet またはMicrosoft Excel を使用したフォームの作成](/help/edge/docs/forms/create-forms.md)
* [データの受け入れを開始するためのGoogleシートまたはMicrosoft Excel ファイルのセットア&#x200B;ップ](/help/edge/docs/forms/submit-forms.md)
* [フォームを発行してデータの収集を開始する](/help/edge/docs/forms/publish-forms.md)
* [フォームの外観をカスタマイズす&#x200B;る](/help/edge/docs/forms/style-theme-forms.md)
* [フォームに繰り返し可能なセクションを&#x200B;追加](/help/edge/docs/forms/repeatable-forms.md)
* [フォーム送信後にカスタムの「ありがとうございます」メッセージを&#x200B;表示](/help/edge/docs/forms/thank-you-page-form.md)
* [アダプティブフォームブロックのコンポーネントとそのプロパティ](/help/edge/docs/forms/form-components.md)



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