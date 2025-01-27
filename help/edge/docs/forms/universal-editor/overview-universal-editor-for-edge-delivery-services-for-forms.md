---
title: AEM Forms の Edge Delivery Services の概要
description: AEM Forms の Edge Delivery Services
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 60998217ea7d3d9c426975510b433308b0ddea14
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 16%

---

# Forms用Edge Delivery Servicesのユニバーサルエディター（EDS Forms ブロック）


ユニバーサルエディターは、コンテンツ作成者やフォーム作成者がフォームを簡単に作成、管理、編集できるように設計されています。 Edge Delivery Services（EDS）に焦点を当てたシンプルで視覚的かつ効率的な編集エクスペリエンスを提供します。

ユニバーサルエディターを使用すると、フォーム要素（テキストフィールド、チェックボックス、ラジオボタンなど）を使用して、What You See Is What You Get（WYSIWYG）インターフェイスでフォームを作成できます。 WYSIWYGのアプローチを使用すると、技術的な専門知識がないユーザーでも、フォームを直感的に簡単に作成できます。

ユニバーサルエディターは、特にEdge Delivery Services（EDS）に焦点を当てています。 ユニバーサルエディターの主な強みは、高度なフォーム作成機能、動的なルール編集、様々なデータソースとのシームレスな統合など、堅牢な機能セットにあります。 ユーザーは、事前定義済みのコンポーネント、カスタマイズ可能なテンプレート、およびフォーム要素の広範なライブラリを使用して、レスポンシブフォームをすばやくデザインできます。

![ユニバーサルエディター](/help/edge/docs/forms/universal-editor/assets/universal-editor.png)



ユニバーサルエディターの機能は、軽量なクライアントサイドレンダリング、クロスブラウザー互換性、アクセシビリティ標準への厳密な準拠を維持するように慎重に設計されています。

## EDS Forms用ユニバーサルエディターの主な機能


<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス"> 
    <h3>WYSIWYG インターフェイス</h3>
    <p>ユニバーサルエディターは、事前定義済みのコンポーネントライブラリ、レスポンシブデザイン、テンプレートベースの作成、リアルタイムフィールドの変更を含むフォームデザインのためのWYSIWYG インターフェイスを提供します。
 </p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/rule-editor.svg" alt="WYSIWYG インターフェイス" alt="ルールエディター">
    <h3>ルールエディター</h3>
    <p>デバイス間でシームレスに適応するレスポンシブフォームのデザイン。 レスポンシブモードを使用して、デスクトップ、タブレットおよびモバイルのデザインをプレビューおよびテストします。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス" alt="送信アクション">
    <h3>レスポンシブモード </h3>
    <p>デバイス（デスクトップ、タブレット、モバイル）間でシームレスに適応するフォームを設計します。 レスポンシブモードを使用して、様々な画面サイズのフォームをプレビューします。</p>
  </div>
</div>
<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス alt=" WYSIWYG Interface"> 
    <h3>パーソナライズ機能</h3>
    <p>Personalizationはユーザーデータを使用して、ユーザーの環境設定に基づいてカスタマイズされたフォームエクスペリエンスを提供し、コンテンツ、レイアウト、オプションを動的に調整します。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg" alt="WYSIWYG インターフェイス" alt="ルールエディター">
    <h3>A/B テスト</h3>
    <p>A/B テスト（実験）を使用すると、組織は様々なフォームデザイン、レイアウト、機能を試して、最もパフォーマンスの高いバリアントを特定できます。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/task-management.svg" alt="WYSIWYG インターフェイス" alt="送信アクション">
    <h3> タスク管理 </h3>
    <p>とAdobe Workfrontを統合すると、チームはフォームの作成と管理のタスクを管理でき、シームレスな共同作業と効率化されたワークフローが実現します。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス" alt="事前入力サービス">
    <h3>事前入力サービス</h3>
    <p>事前入力サービスは、様々なソースからの関連するユーザーデータをフォームフィールドに自動的に入力するので、手動での入力を減らし、ユーザーエクスペリエンスを向上させることができます。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス" alt="データ連結">
    <h3>データ連結</h3>
    <p>データバインディングにより、フォームフィールドとバックエンドデータソース間の直接接続が可能になり、リアルタイムの更新と高度なデータマッピングがサポートされます。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/localization.svg" alt="WYSIWYG インターフェイス" alt="国際化/ローカリゼーション">
    <h3>公開/非公開</h3>
    <p>フォームの表示を簡単に制御します。数回のクリックでフォームを公開または非公開にし、可用性、ユーザーアクセス、コンテンツ更新を動的に管理します。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg" alt="WYSIWYG インターフェイス" alt="分析とトラッキング">
    <h3>分析とトラッキング</h3>
    <p>組み込みの分析とトラッキングを使用して、ユーザーの行動、フォームのインタラクション、送信率に関するインサイトを取得し、データ駆動型のフォーム最適化を可能にします。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス" alt="実験（A/B テスト）">
    <h3>送信アクション</h3>
    <p>送信アクションは、バックエンド統合、条件付き送信ロジック、安全なエンドポイント、プリプロセッサーをサポートし、送信ワークフローを合理化します。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス" alt="タスク管理">
    <h3>カスタムコンポーネント</h3>
    <p>カスタムコンポーネントを使用すると、デベロッパーは特定の組織のユースケースに合わせて独自の要素を作成することで、フォーム機能を拡張できます。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス" alt="エディターのカスタマイズ">
    <h3>エディターのカスタマイズ</h3>
    <p>開発者は、UI 拡張機能を通じてユニバーサルエディターの機能を拡張し、特定の組織ニーズに合わせてカスタマイズされたソリューションを実現できます。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス" alt="Formsの埋め込み">
    <h3>Formsの埋め込み</h3>
    <p>ユニバーサルエディターの組み込み埋め込みコンポーネントを使用してEdge Delivery Services Sites ページにフォームを直接埋め込み、シームレスなユーザーエクスペリエンスを実現します。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG インターフェイス" alt="カスタムコンポーネント">
    <h3>「ありがとうございます」設定</h3>
    <p>フォームの送信が成功した後に、ユーザーに表示される確認メッセージまたはページを簡単にカスタマイズできます。
    </p>
  </div>
</div>
</div>


<!-- ![Universal Editor](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg)  **WYSIWYG interface for Form creation**: Universal Editor provides a WYSIWYG interface for form design. It provides pre-built component library, responsive design support, and template-based form creation. You can instantly add or remove form fields and modify field properties (like label, data binding, validation). You can also plugin custom form components to Universal Editor.


* **Rule editor**: The rule editor stands out as a powerful mechanism for creating sophisticated form interactions. It supports event-driven rules, instant validation, and error handling through lightweight JavaScript and JSON-based definitions. This allows developers to implement complex form logic, such as conditional field visibility, automatic calculations, and dynamic form behaviour without extensive coding.

* **Submit actions**: Submit Actions enable form submission workflows. These actions provide comprehensive backend integration options, supporting protocols like REST API. The system allows you configure data pre-processors for automatic data transformation, conditional submission logic based on form field values, and secure endpoint connections. Organizations can define complex submission rules that validate data, and manage form responses with granular control.

* **Pre-fill services:** Pre-fill Services enhance user experience by intelligently populating form fields with relevant data. These services connect to various data sources, including user profiles, browser local storage, and external databases. The mechanism supports dynamic data population, enabling automatic completion of form fields based on contextual information. Users benefit from reduced manual data entry, while administrators gain flexibility in configuring pre-fill rules across different form types and scenarios. The pre-fill functionality adapts to different authentication methods, including session-based approaches and token-based systems, ensuring both convenience and security.

* **Data binding capabilities**: Data binding in the Universal Editor enables direct, dynamic connections between form fields and backend data sources. This feature allows real-time synchronization of form data, supporting complex data mapping scenarios. The system supports transforming form inputs into structured database records with minimal configuration. Advanced mapping supports nested data structures, allowing complex form designs to interact seamlessly with intricate data models.

* **Internationalization/localization capabilities**: Internationalization support ensures global accessibility, with multi-language rendering, right-to-left language compatibility, and locale-specific formatting.

* **Analytics and tracking mechanisms**: The built-in analytics and tracking mechanisms provide comprehensive insights into form interactions, submission rates, and user behavior, enabling continuous optimization of form design and performance. 

* **Experimentation (A/B Testing)**: The Universal Editor supports experimentation by allowing organizations to run A/B tests on form designs to identify the best-performing layouts or features.

* **Task Management via Adobe Workfront**: Integration with Adobe Workfront allows teams to manage tasks related to form creation and maintenance, ensuring streamlined collaboration and efficient workflows.

* **Editor Customization via UI Extension**: Developers can extend the functionality of the Universal Editor through UI extensions, enabling tailored solutions that fit specific organizational needs. -->

## 事前定義済みフォームコンポーネント

ユニバーサルエディターには、次のフォームコンポーネントが標準搭載されています。

<table>
  <thead>
    <tr>
      <th>美しい</th> 
      <th>フォームコンポーネント</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="フォームコンポーネント" style="width: 100%;"></td> 
      <td><b>アコーディオン</b></td>
      <td>コンテンツを整理するための折りたたみ可能なパネル構造。</td>
    </tr>
    <tr>
      <td><b>ボタン</b></td>
      <td>ナビゲーションやカスタムロジックなどのアクション用にインタラクティブ要素を追加します。</td>
    </tr>
    <tr>
      <td><b>Captcha</b></td>
      <td>Google reCaptcha または HCaptcha を使用して人間が行う検証タスクを完了するようにユーザーに求めることで、スパムを防止します。</td>
    </tr>
    <tr>
      <td><b>チェックボックス</b></td>
      <td>ユーザーがチェックボックスを設定できます。</td>
    </tr>
    <tr>
      <td><b>チェックボックスグループ</b></td>
      <td>ユーザーがグループから複数のオプションを選択できるようにします。</td>
    </tr>
    <tr>
      <td><b>日付選択</b></td>
      <td>ユーザーがカレンダーインターフェイスを使用して日付を選択できるようにします。</td>
    </tr>
    <tr>
      <td><b>ドロップダウンリスト</b></td>
      <td>定義済みのリストから 1 つまたは複数のオプションを選択できます。</td>
    </tr>
    <tr>
      <td><b>メール</b></td>
      <td>基本的な形式の検証でメールアドレスをキャプチャします。</td>
    </tr>
    <tr>
      <td><b>ファイル添付</b></td>
      <td>ドキュメント、画像、またはその他のファイルタイプのアップロードを有効にします。</td>
    </tr>
    <tr>
      <td><b>フォームフラグメント</b></td>
      <td>住所フィールドや連絡先詳細などのセクションに再利用可能なフォームコンポーネント。</td>
    </tr>
    <tr>
      <td><b>画像</b></td>
      <td>フォーム内での画像のアップロードと表示をサポートします。</td>
    </tr>
    <tr>
      <td><b>モーダル</b></td>
      <td>アラート、追加情報、または確認に使用されることが多いポップアップ ダイアログ ボックスを表示します。</td>
    </tr>
    <tr>
      <td><b>数値フィールド</b></td>
      <td>数値入力をキャプチャし、数値または範囲の検証を可能にします。</td>
    </tr>
    <tr>
      <td><b>パネル</b></td>
      <td>展開/折りたたみ可能なパネルを使用してフォームのセクションを整理します。</td>
    </tr>
    <tr>
      <td><b>ラジオボタン</b></td>
      <td>オプションのグループから単一選択を有効にします。</td>
    </tr>
    <tr>
      <td><b>レーティング</b></td>
      <td>ユーザーが星ベースの評価を提供できるようにします。</td>
    </tr>
    <tr>
      <td><b>リセットボタン</b></td>
      <td>フォームフィールドをデフォルトの状態にリセットします。</td>
    </tr>
    <tr>
      <td><b>送信ボタン</b></td>
      <td>フォームの送信をトリガーし、定義されたワークフローを開始します。</td>
    </tr>
    <tr>
      <td><b>電話番号フィールド</b></td>
      <td>国に基づくフォーマットを使用して電話番号をキャプチャします。</td>
    </tr>
    <tr>
      <td><b>テキスト</b></td>
      <td>法律条項を表示したり、チェックボックスを通じてユーザー契約書を収集したりする専用のセクションを提供します。</td>
    </tr>
    <tr>
      <td><b>テキストフィールド</b></td>
      <td>名前やメールアドレスなど、単一行の入力をキャプチャします。</td>
    </tr>
    <tr>
      <td><b>ウィザード</b></td>
      <td>ユーザーが複数のパートから成るフォームプロセスを段階的にガイドします。</td>
    </tr>
  </tbody>
</table>

<!-- * Footer: Adds a footer section for consistent design or additional information.
* Form Container: Wraps all form elements and manages overall form properties.
* Header: Adds a header section for form titles, branding, or instructions.-->
<!-- * 
* Prefillable Fields: Automatically populates form fields with data from predefined sources such as user profiles or APIs. 

* Switches/Toggle Buttons: Provides binary on/off choices for user input.


* Title: Adds a text-based heading or label to improve form clarity and organization.


In-addtion to pre-built form components, the Universal editor also provides support for:

* **Embedding Forms in Another Webpage**: The Universal Editor supports embedding forms directly into Edge Deliver Services Sites pages. This can be done using the embed component provided out of the box.

* **Validation Messages**: Validation messages provide real-time feedback to users when they enter incorrect or incomplete data. Features include:
    * Dynamic Error Display: Instantly alerts users to errors, such as invalid email addresses or missing required fields.
    * Customizable Messages: Allows form authors to define user-friendly error texts.
    * Rule-Based Validation: Supports advanced validation logic, such as checking dependencies between fields or implementing conditional rules.

* **Hidden Fields**: Hidden fields store data invisibly within the form, often for backend processing or prefilled values. Use cases include:
    * Passing contextual information (e.g., user ID or session data) to the backend without displaying it to users.
    * Capturing metadata like timestamps or tracking IDs.
    * Hidden fields are not visible to end-users but can be prefilled, updated dynamically, or used in workflows.

* **Custom Components**: Custom components allow developers to extend the functionality of forms by creating specialized or third-party integrations. Features include:
    * Flexibility: Developers can design unique form elements tailored to specific use cases.
    * Third-Party Integration: Embed widgets or tools like payment gateways, analytics trackers, or AI-driven input fields.
    * Seamless Compatibility: Custom components can integrate with the Universal Editor's drag-and-drop interface and existing features like data binding or validation.

* **Thank you Configuration**: Customize the acknowledgment message or page shown after form submission.
-->


## オンボーディング

ユニバーサルエディターとルールエディターをお使いの環境で有効にする場合や、Forms ポータル、レコードのドキュメント、Adobe Signとの統合、右から左への言語のサポートなどの追加機能をリクエストする場合は、公式アドレスからmailto:aem-forms-ea@adobe.comにお問い合わせください。



## フォームの作成を開始

* [AEM Forms の Edge Delivery Services の基本を学ぶ](/help/edge/docs/forms/tutorial.md)
* [Google Sheet または Microsoft Excel を使用したフォームの作成](/help/edge/docs/forms/create-forms.md)
* [データの受け入れを開始するための Google Sheets または Microsoft Excel ファイルの設定](/help/edge/docs/forms/submit-forms.md)
* [フォームを公開してデータの収集を開始](/help/edge/docs/forms/publish-forms.md)
* [フォームの外観のカスタマイズ](/help/edge/docs/forms/style-theme-forms.md)
* [繰り返し可能なセクションをフォームに追加する](/help/edge/docs/forms/repeatable-forms.md)
* [フォーム送信後にカスタムのお礼のメッセージを表示](/help/edge/docs/forms/thank-you-page-form.md)
* [アダプティブフォームブロックのコンポーネントとそのプロパティ](/help/edge/docs/forms/form-components.md)
* [実際の使用のモニタリング](https://www.aem.live/developer/rum#authentication)

<!-- 

## Start creating forms

<div>

  <style>
    .card-container {
        width: calc(30% - 10px);;
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