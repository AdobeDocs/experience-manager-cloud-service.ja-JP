---
title: AEM FormsEdge Delivery Servicesの概要
description: AEM FormsEdge Delivery Servicesは、効率的なデータ収集とユーザーエンゲージメントの将来を想像できるように、ピークパフォーマンスを実現するために構築されています。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 6d4b194d17cc27a6a8596825401dc723bebe7b27
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# AEM FormsEdge Delivery Services

AEM FormsEdge Delivery Servicesは、作成者が新しいフォームをすばやく更新、公開、および起動できる、迅速な開発環境を可能にする、合成可能な一連のサービスです。 これらのサービスは、エンゲージメントとコンバージョンを促進する優れた効果の高いフォームエクスペリエンスを提供します。 これらのフォームエクスペリエンスは、作成と開発が容易です。

これらのサービスを使用すると、次のことができます。

* **任意のツールを使用して、登録エクスペリエンスを作成します。** コンテンツソースを分離してオーサリング効率を向上させます。 標準では、ドキュメントベースのオーサリング (Microsoft SharePointまたはGoogle Drive) とAEMオーサリング ( アダプティブFormsエディター ) の両方を使用できます。 同じフォームサイト上で複数のコンテンツソースを操作し、Microsoft Excel、Googleシート、アダプティブFormsエディターなどの好みのオーサリングツールを使用できます。

* **優れたデジタル登録エクスペリエンスを提供：** すばやく読み込んでレンダリングするデジタル登録エクスペリエンスを配信します。 読み込み時間の短縮と最適化されたユーザーエクスペリエンスにより、フォームの完成率とコンバージョン率が向上します。

* **開発者向けのツールセットを使用：** AEM FormsEdge Delivery Servicesは、プレーンHTML、最新の CSS、バニラ JavaScript を使用して、例外的なエクスペリエンスを作成し、特定のフレームワークの急激な学習曲線を避けます。 基本的な Web 開発スキルを持つ開発者は、フォームのコンポーネントやエクスペリエンスをカスタマイズし、容易に構築できます。 パイプラインの実行を待つ必要はありません。コードを GitHub にチェックインするだけで、変更が反映されます。

## AEM FormsEdge Delivery Servicesの概要 {#edge-overview}

AEM Forms Edge Delivery Services を使用すると、Web サイト上でフォームを作成する際の柔軟性を高めることができます。 コンテンツとフォームは、 [AEM Authoring](/help/forms/creating-adaptive-form-core-components.md) 同様に [ドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md). AEM FormsEdge Delivery Servicesは、 [アダプティブFormsブロック](/help/edge/docs/forms/create-forms.md) をクリックして、フォームをEdge Delivery Servicesサイトに追加します。

例えば、Microsoft Excel やGoogleシートで直接フォームを作成し、これらのスプレッドシートを Web サイト用のフォームに変換したとします。 新しいフォームやフォームコンテンツ（新しいフォームフィールドなど）は、再構築プロセスを必要とせずに、Web サイト上で即座に使用できます。

次の図は、Microsoft Excel またはGoogleシート（ドキュメントベースのオーサリング）でフォームを編集し、Edge Delivery Servicesに公開する方法を示しています。 また、アダプティブFormsエディター (AEMオーサリング ) を使用したAEMの公開方法も表示されます。

![Edge Delivery のアーキテクチャ](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

AEM FormsEdge Delivery Servicesでは GitHub を使用するので、ユーザーは GitHub リポジトリから直接コードを管理およびデプロイできます。 例えば、次のいずれかの方法でフォームを書き込むことができます。 [Google Sheets](/help/edge/docs/forms/create-forms.md) または [Microsoft Excel](/help/edge/docs/forms/create-forms.md) また、フォームのコンポーネントは、GitHub リポジトリで CSS と JavaScript を使用して開発できます。

フォームの準備が整ったら、 [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content):chrome ブラウザー拡張機能。コンテンツの更新をプレビューおよび公開します。

![インストールAEM Sidekick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

次の中から選択： [ドキュメントベースのオーサリング](#document-based-authoring-features) および [AEM Authoring](#aem-authoring-features) は、具体的な要件に応じて異なります。

* いくつかのフィールドを持つ基本情報を収集するだけのシンプルなフォーム（お問い合わせください。フォーム、リード生成フォーム、またはサービスリクエストフォーム）と、スプレッドシートを使用した迅速なデータ接続が必要な場合、 [ドキュメントベースのオーサリング](#document-based-authoring-features) いいフィットです。 これらのフォームは、Google Sheet やMicrosoft Excel でドキュメントを作成する場合と同様に作成できます。

* 複数のパネルを必要とするフォーム、複雑なルールとビジネスロジック、データ操作、外部システムとの統合、AEM機能を使用した合理化されたワークフローなど、複雑なフォームの場合は、 [AEM Authoring](#aem-authoring-features) はより良い選択肢です。


### ドキュメントベースのオーサリングとAEMオーサリングの主な機能

ドキュメントベースオーサリングには、基本的な機能セットが用意されています。AEMオーサリングでは、ドキュメントベースオーサリング以外の追加機能をロック解除し、より複雑でインタラクティブなフォームを作成できます。 ドキュメントベースのオーサリングとAEMオーサリングの両方の主な機能は次のとおりです。

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

AEMオーサリングには、フォームを作成するための WYSIWYG インターフェイス ( アダプティブFormsエディター ) が用意されており、ドキュメントベースオーサリングのすべての機能に加えて、様々な機能を提供しています。

* 複雑なロジックを作成するための高度なルールエディター。
* カスタム機能用のサーバー側の拡張機能。
* WYSIWYG で編集操作を実行して、フォームの作成と視覚化を容易にします。
* 送信されたデータの改ざん防止アーカイブを作成するレコードのドキュメント機能。
* 電子署名用のAdobe Signとの統合。
* フォーム送信時にAdobe Workfront Fusion シナリオをトリガーするAdobe Workfront Fusion との統合。
* フォームの事前入力やデータの送信を行うための様々なデータソースとの統合。
* データ構造と様々なデータソースとのやり取りを定義するフォームデータモデル。
* Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics など、様々なデータソースへのデータの送信を含め、複数の送信アクションから選択してフォーム送信を処理できます。

要するに [AEM Authoring](/help/forms/creating-adaptive-form-core-components.md) ～の基盤を基に構築される [ドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md)は、複雑なフォームを作成および管理するためのより高度なツールキットを提供します。

>[!NOTE]
>
>
> AEMオーサリング機能は、アーリーアダプタープログラムで使用できます。 ご興味がある場合は、aem-forms-ea@adobe.com宛に、ご自身の仕事用アドレスからクイックメールを送信して、機能へのアクセスをリクエストしてください。

### AEM FormsEdge Delivery Services:Formsのオーサリング、公開、送信

次の図は、ドキュメントベースのオーサリングとAEMオーサリングを使用してフォームを作成、公開、送信するプロセスを示しています。

![ドキュメントベースのオーサリング ](/help/edge/assets/document-based-authoring-workflow.png)

![AEM Authoring](/help/edge/assets/aem-authoring-workflow.png)




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