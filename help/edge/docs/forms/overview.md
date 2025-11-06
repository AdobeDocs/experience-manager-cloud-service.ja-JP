---
title: AEM Forms の Edge Delivery Services の概要
description: ユニバーサルエディターのオーサリングアプローチに重点を置いて、Adobe Experience Manager Edge Delivery Services でパフォーマンスの高いフォームを作成および配信します。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 100%

---


# AEM Forms の Edge Delivery Services


AEM Forms の Edge Delivery Services は、作成者が新しいフォームを迅速に更新、公開、起動できる高速開発環境を可能にする、構成可能な一連のサービスです。これらのサービスは、エンゲージメントとコンバージョンを促進する、優れた効果の高いフォームエクスペリエンスを提供します。これらのフォームエクスペリエンスは、簡単に作成および開発できます。

これらのサービスにより、次のことが可能になります。

- **選択したツールを使用して登録エクスペリエンスを作成：**&#x200B;コンテンツソースを分離することでオーサリングの効率を高めます。標準では、ドキュメントベースのオーサリング（Microsoft SharePoint または Google Drive）と WYSIWYG オーサリング（ユニバーサルエディターまたはアダプティブフォームエディター）を使用できます。同じフォームサイト上で複数のコンテンツソースを操作し、Microsoft Excel、Google Sheets、ユニバーサルエディター、アダプティブフォームエディターなどの推奨オーサリングツールを使用できます。

- **優れたデジタル登録エクスペリエンスを提供：**&#x200B;迅速な読み込みとレンダリングを行うデジタル登録エクスペリエンスを提供し、運用テレメトリによってフォームのパフォーマンスを継続的に監視します。読み込み時間の短縮とユーザーエクスペリエンスの最適化により、フォームの完成率とコンバージョン率が向上します。

- **開発者にわかりやすいツールセットを使用：**AEM Forms の Edge Delivery Services は、
プレーン HTML、最新の CSS、Vanilla JavaScript を使用して優れたエクスペリエンスを作成し、特定のフレームワークの急な学習曲線を回避します。基本的な web 開発スキルを持つ開発者は、フォームコンポーネントとエクスペリエンスをカスタマイズして簡単に作成できます。パイプラインの実行を待機する必要はありません。コードを GitHub にチェックインするだけで、変更が公開されます。

## オーサリング方法の選択


Adobe Experience Manager（AEM）Edge Delivery Services（EDS）を使用すると、非常に高速で拡張性の高い web エクスペリエンスをエッジから提供できます。このガイドでは、明確なレコメンデーション階層を持つ&#x200B;**これらのエクスペリエンス向けのフォームを作成および公開する方法**&#x200B;について説明します。

- **ユニバーサルエディター（UE）- ほとんどのチームに最適な選択肢**
- **ドキュメントベースのオーサリング（ドキュメント／スプレッドシート） - 迅速でシンプルなフォームに最適**
- **ドキュメントオーサリング（DA） - DA で作成したページにフォームを埋め込むために使用**

最終的には、適切なオーサリング方法を選択し、送信オプションを理解して、実稼動対応のフォームに向けた次の手順に従うことができるようになります。


| チームと要件 | 推奨される方法 | 理由 |
|--------------------|--------------------|-----|
| マーケター／デザイナーには、ビジュアルコントロール、条件付きロジックまたは AEM 統合が必要です | **ユニバーサルエディター** | ドラッグ＆ドロップ、高度なルール、FSS または AEM パブリッシュへの送信 |
| コンテンツ作成者は、既に Word／Google Docs／Sheets で作業し、スプレッドシート／メールへのシンプルなデータキャプチャが可能です | **ドキュメントベースのオーサリング** | 使い慣れたツール、基本フォームへの最速パス |
| **ドキュメントオーサリング（DA）**&#x200B;で作成された web サイトページ | UE またはドキュメントベースのフォームを DA ページに&#x200B;**埋め込む** | DA ではフォーム自体を作成しません |


## オーサリング方法の詳細

### ユニバーサルエディター

<!--
<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features">pre-release channel</a>. </span>
-->

[ユニバーサルエディター](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)は、次の速度とエンタープライズグレードの機能を組み合わせた、マーケターやデザイナー向けの視覚的なドラッグ＆ドロップオーサリングツールです。

- リアルタイムの WYSIWYG 編集とデバイスのプレビュー。
- AEM のアセット、ワークフロー、フォームデータモデル（FDM）との直接統合。
- Vanilla JS／CSS のカスタムコンポーネントの開発者へのシームレスなハンドオフ。
- 複雑なロジックを作成する高度なルールエディター。
- カスタム機能を実現するサーバーサイド拡張機能。
- 簡単なフォームを作成し視覚化する WYSIWYG 編集エクスペリエンス。
- 送信されたデータの改ざん防止アーカイブを作成するレコードのドキュメント機能。
- 電子署名を行う Adobe Sign との統合。
- フォーム送信時に Adobe Workfront Fusion シナリオをトリガーする Adobe Workfront Fusion との統合。
- フォームの事前入力とデータの送信の様々なデータソースとの統合。
- 様々なデータソースとのインタラクションとデータ構造を定義するフォームデータモデル（FDM）。
- Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics、その他多くのデータソースへのデータ送信を含む、フォーム送信を処理する複数の送信アクションから選択する機能。
- Forms 送信サービス（FSS）または AEM パブリッシュの送信アクションを使用した送信

**レコメンデーション**：チームが 100％ドキュメント中心で、フォームが非常に基本的でない限り、すべての新しいフォームプロジェクトはユニバーサルエディターで開始します。


### ドキュメントベースのオーサリング（Microsoft Docs または Google Sheets を使用）

[ドキュメントベースのオーサリング](/help/edge/docs/forms/tutorial.md)は、Microsoft Word、Google Docs、Google Sheets などの使い慣れたツールを使用して、シンプルで複雑さの少ないフォームを作成するのに最適です。この方法は、フォームをすばやく簡単に作成する必要があるコンテンツチームに最適です。

- ユーザーにわかりやすいエクスペリエンスを実現するアクセシブルなコンポーネント。
- 一貫性のあるレンダリングを行う標準化された HTML 構造。
- データの正確性を確保するルールと検証。
- 追加情報を収集する添付ファイルのオプション。
- スパム保護を実現する Google reCAPTCHA 統合。
- 特定のニーズに合わせてカスタムフォームコンポーネントを作成する機能。
- フォームデータを Microsoft Excel、Google Sheets、メールアドレスに直接送信します。
- 運用テレメトリによるフォームのパフォーマンスの監視


### ドキュメントオーサリング（DA）でのフォームの埋め込み

ドキュメントオーサリング（DA）は、構造化されたページコンテンツの作成用に設計されており、ネイティブフォームの作成はサポートしていません。DA で作成したページにフォームを追加するには、**ユニバーサルエディター**（推奨）またはドキュメントベースのオーサリングを使用してフォームを作成し、このフォームをドキュメントのオーサリングページに埋め込みます。

## Edge Delivery Services Forms の公開 {#edge-overview}

Microsoft Excel または Google Sheets（ドキュメントベースのオーサリング）でフォームを編集し、Edge Delivery Services に公開する方法を次の図に示します。また、WYSIWYG オーサリング（ユニバーサルエディター）を使用した AEM パブリッシング方法も示します。

![Edge Delivery Services と AEM に公開](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)


<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |
-->

## 次の手順

- [Forms の Edge Delivery Services のユニバーサルエディターの機能](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [ユニバーサルエディターを使用した最初のフォームの作成](/help/edge/docs/forms/universal-editor/create-forms.md)
- [Google Sheet または Microsoft Excel を使用した最初のフォームの作成](/help/edge/docs/forms/tutorial.md)。
- [ドキュメントオーサリング（DA）でのフォームの埋め込み](https://www.aem.live/developer/da-tutorial)


これで、AEM Edge Delivery Services を使用して最初のパフォーマンスの高いフォームを作成する準備が整いました。

<!--
## Start creating forms

- [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
- [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
- [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
- [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
- [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
- [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
- [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
- [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
- [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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
