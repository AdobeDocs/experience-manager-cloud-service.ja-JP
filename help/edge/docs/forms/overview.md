---
title: AEM Forms Edge Delivery Services の概要
description: AEM Forms Edge Delivery Services は、ピーク時のパフォーマンスを実現するように作成されており、効率化されたデータ収集とユーザーエンゲージメントの今後を思い描くことができます。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: b32e04dec83992ebfcea7874932a5ab77a1eaa70
workflow-type: ht
source-wordcount: '1017'
ht-degree: 100%

---

# AEM Forms Edge Delivery Services

AEM Forms Edge Delivery Services は、作成者が新しいフォームを迅速に更新、公開、起動できる迅速な開発環境を可能にする、構成可能なサービスセットです。これらのサービスは、エンゲージメントとコンバージョンを促進する、優れた効果の高いフォームエクスペリエンスを提供します。これらのフォームエクスペリエンスは、簡単に作成および開発できます。

これらのサービスにより、次のことが可能になります。

* **選択したツールを使用して登録エクスペリエンスを作成：**&#x200B;コンテンツソースを分離することでオーサリングの効率を高めます。標準では、ドキュメントベースのオーサリング（Microsoft SharePoint または Google Drive）と AEM オーサリング（アダプティブフォームエディター）の両方を使用できます。同じフォームサイト上で複数のコンテンツソースを操作し、Microsoft Excel、Google Sheets、アダプティブフォームエディターなどの推奨オーサリングツールを使用できます。

* **優れたデジタル登録エクスペリエンスを提供：**&#x200B;迅速な読み込みとレンダリングを行うデジタル登録エクスペリエンスを提供し、リアルユーザーモニタリング（RUM）を通じてフォームのパフォーマンスを継続的に監視します。読み込み時間の短縮とユーザーエクスペリエンスの最適化により、フォームの完成率とコンバージョン率が向上します。

* **開発者にわかりやすいツールセットを使用：** AEM Forms Edge Delivery Services は、プレーン HTML、最新の CSS、Vanilla JavaScript を使用して優れたエクスペリエンスを作成し、特定のフレームワークの急な学習曲線を回避します。基本的な web 開発スキルを持つ開発者は、フォームコンポーネントとエクスペリエンスをカスタマイズして簡単に作成できます。パイプラインの実行を待機する必要はありません。コードを GitHub にチェックインするだけで、変更が公開されます。

## AEM Forms Edge Delivery Services の概要 {#edge-overview}

AEM Forms Edge Delivery Services を使用すると、web サイト上でフォームを作成する際の柔軟性を高めることができます。[AEM オーサリング](/help/forms/creating-adaptive-form-core-components.md)と[ドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md)を使用すると、コンテンツとフォームを作成できます。AEM Forms Edge Delivery Services は、[アダプティブフォームブロック](/help/edge/docs/forms/create-forms.md)と呼ばれるフォームブロックを提供し、Edge Delivery Services サイトにフォームを追加します。

例えば、Microsoft Excel または Google Sheets で直接フォームを作成すると、これらのスプレッドシートが web サイト用のフォームに変換されます。新しいフォームやフォームコンテンツ（新しいフォームフィールドなど）は、再作成プロセスを必要とせずに web サイト上で即座に使用できます。

Microsoft Excel または Google Sheets（ドキュメントベースのオーサリング）でフォームを編集し、Edge Delivery Services に公開する方法を次の図に示します。また、アダプティブフォームエディター（AEM オーサリング）を使用した AEM パブリッシング方法も示します。

![Edge Delivery Services と AEM に公開](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

AEM Forms Edge Delivery Services では GitHub を使用するので、お客様は GitHub リポジトリから直接コードを管理およびデプロイできます。例えば、[Google Sheets](/help/edge/docs/forms/create-forms.md) または [Microsoft Excel](/help/edge/docs/forms/create-forms.md) でフォームを作成でき、GitHub リポジトリで CSS と JavaScript を使用してフォームのコンポーネントを開発できます。

フォームの準備が整ったら、Chrome ブラウザー拡張機能である [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content) を使用して、コンテンツの更新をプレビューおよび公開できます。

![AEM Sidekick のインストール](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

[ドキュメントベースのオーサリング](#document-based-authoring-features)と [AEM オーサリング](#aem-authoring-features)のどちらを選択するかは、特定の要件によって異なります。

* いくつかのフィールドで基本的な情報を収集するだけのシンプルなフォーム（お問い合わせフォーム、リードジェネレーションフォーム、サービスリクエストフォームなど）や、スプレッドシートを使用して迅速なデータ接続が必要な場合は、[ドキュメントベースのオーサリング](#document-based-authoring-features)が適しています。これらのフォームは、Google Sheet や Microsoft Excel でドキュメントを作成する場合と同様に作成できます。

* 複数のパネル、複雑なルールとビジネスロジック、データ操作、外部システムとの統合、AEM 機能を使用した効率化されたワークフローを必要とするフォームなど、複雑なフォームの場合は、[AEM オーサリング](#aem-authoring-features)の方が適しています。


### ドキュメントベースのオーサリングと AEM オーサリングの主な機能

ドキュメントベースのオーサリングには、基本的な機能セットが用意されています。AEM オーサリングでは、ドキュメントベースのオーサリングを超える追加機能をロック解除し、より複雑でインタラクティブなフォームを作成できます。ドキュメントベースのオーサリングと AEM オーサリングの両方の主な機能は次のとおりです。

#### ドキュメントベースのオーサリング機能

ドキュメントベースのオーサリングを使用すると、Microsoft Excel やGoogle Sheet などの使い慣れたツールを使用してフォームを作成できます。これらのフォームには、次の機能が用意されています。

* ユーザーにわかりやすいエクスペリエンスを実現するアクセシブルなコンポーネント。
* 一貫性のあるレンダリングを行う標準化された HTML 構造。
* データの正確性を確保するルールと検証。
* 追加情報を収集する添付ファイルのオプション。
* スパム保護を実現する Google reCAPTCHA 統合。
* 特定のニーズに合わせてカスタムフォームコンポーネントを作成する機能。
* フォームデータを Microsoft Excel、Google Sheets、メールアドレスに直接送信します。
* リアルユーザーモニタリング（RUM）を通じたフォームのパフォーマンスの監視

#### AEM オーサリング機能

AEM オーサリングには、フォームを作成する WYSIWYG インターフェイス（アダプティブフォームエディター）が用意されており、ドキュメントベースのオーサリングのすべての機能に加えて、次の幅広い追加機能を提供します。

* 複雑なロジックを作成する高度なルールエディター。
* カスタム機能を実現するサーバーサイド拡張機能。
* 簡単なフォームを作成し視覚化する WYSIWYG 編集エクスペリエンス。
* 送信されたデータの改ざん防止アーカイブを作成するレコードのドキュメント機能。
* 電子署名を行う Adobe Sign との統合。
* フォーム送信時に Adobe Workfront Fusion シナリオをトリガーする Adobe Workfront Fusion との統合。
* フォームの事前入力とデータの送信の様々なデータソースとの統合。
* データ構造と様々なデータソースとのインタラクションを定義するフォームデータモデル。
* Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics、その他多くのデータソースへのデータ送信を含む、フォーム送信を処理する複数の送信アクションから選択する機能。

基本的に、[AEM オーサリング](/help/forms/creating-adaptive-form-core-components.md)は、[ドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md)の基盤の上に作成されており、複雑なフォームの作成および管理を行うより高度なツールキットを提供します。

>[!NOTE]
>
>
> AEM オーサリング機能は、早期導入プログラムで利用できます。詳しくは、作業用アドレスから aem-forms-ea@adobe.com にメールを送信して、機能へのアクセスをリクエストしてください。

### AEM Forms Edge Delivery Services：フォームのオーサリング、公開、送信

ドキュメントベースのオーサリングと AEM オーサリングを使用してフォームを作成、公開、送信するプロセスを次の図に示します。

![ドキュメントベースのオーサリング](/help/edge/assets/document-based-authoring-workflow.png)

![AEM オーサリング](/help/edge/assets/aem-authoring-workflow.png)

## フォームの作成を開始

* [AEM Forms Edge Delivery Services の基本を学ぶ](/help/edge/docs/forms/tutorial.md)
* [Google Sheet または Microsoft Excel を使用したフォームの作成](/help/edge/docs/forms/create-forms.md)
* [データの受け入れを開始するための Google Sheets または Microsoft Excel ファイルの設定](/help/edge/docs/forms/submit-forms.md)
* [フォームを公開してデータの収集を開始](/help/edge/docs/forms/publish-forms.md)
* [フォームの外観のカスタマイズ](/help/edge/docs/forms/style-theme-forms.md)
* [フォームへの繰り返し可能なセクションの追加](/help/edge/docs/forms/repeatable-forms.md)
* [フォーム送信後にカスタムのお礼のメッセージを表示](/help/edge/docs/forms/thank-you-page-form.md)
* [アダプティブフォームブロックのコンポーネントとそのプロパティ](/help/edge/docs/forms/form-components.md)
* [リアルタイムユーザーモニタリング](https://www.aem.live/developer/rum#authentication)

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