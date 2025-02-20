---
title: Forms の Edge Delivery Services のユニバーサルエディター（EDS Forms ブロック）
description: Forms の Edge Delivery Services のユニバーサルエディター（EDS Forms ブロック）を使用して、アダプティブフォームを作成します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: 7a868ddc3d13eaf3b5352e130b2026db64a02723
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 78%

---

# Forms の Edge Delivery Services のユニバーサルエディター（EDS Forms ブロック）

ユニバーサルエディターは、シンプルで視覚的かつ直感的な WYSIWYG（見たままが得られる）インターフェイスを提供することで、Adobe Edge Delivery Services（EDS）のフォーム作成に革命をもたらします。コンテンツ作成者とフォーム作成者向けに設計されており、従来のフォーム作成プロセスの複雑さを排除し、技術に詳しくないユーザーでもアクセスできます。

ユニバーサルエディターを使用すると、テキストフィールド、チェックボックス、ラジオボタンなどの事前定義済みコンポーネントを使用して、レスポンシブでインタラクティブなフォームをすばやく設計できます。その堅牢な機能セットは、動的なルール、シームレスなデータ統合、高度なパーソナライゼーションをサポートし、すべてのフォームをニーズに合わせて調整します。

軽量のクライアントサイドレンダリングの管理、ブラウザー間の互換性の確保、または厳密なアクセシビリティ標準の準拠のいずれであっても、ユニバーサルエディターはフォームの作成と管理の効率化されたソリューションを提供します。

![ユニバーサルエディター](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center} -->

## EDS Forms のユニバーサルエディターの主な機能



次に、幅が等しいカードのレイアウトを示します（固定幅の列を使用）。

| ![WYSIWYG インターフェイス ](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![ルールエディター](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![ 送信アクション ](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**WYSIWYG インターフェイス**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**ルールエディター**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**送信アクション**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| ユニバーサルエディターでは、事前定義済みのコンポーネントライブラリ、レスポンシブデザイン、テンプレートベースの作成、リアルタイムのフィールド変更を備えたフォームデザイン用の WYSIWYG インターフェイスを提供します。 | ルールエディターを使用すると、ユーザーは、イベント駆動型ルール、即時検証、軽量の JavaScript と JSON によるエラー処理を使用して、動的なフォームインタラクションを作成できます。 | 送信アクションは、バックエンド統合、条件付き送信ロジック、安全なエンドポイント、プリプロセッサーをサポートし、送信ワークフローを効率化します。 |

| ![ 公開/非公開 ](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![ レスポンシブモード ](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![ カスタムコンポーネント ](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|

| [**公開/非公開**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**レスポンシブモード**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**カスタムコンポーネント**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
|フォームの表示を簡単に制御 – 数回クリックするだけで、エディターから直接フォームを公開または非公開にできます。 | デバイス（デスクトップ、タブレット、モバイル）間でシームレスに適応するフォームをデザインします。 レスポンシブモードを使用して、様々な画面サイズのフォームをプレビューおよびテストします。 | カスタムコンポーネントを使用すると、デベロッパーは特定の組織のユースケースに合わせて独自の要素を作成することで、フォーム機能を拡張できます。 |

| ![スタイル設定](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![ 事前入力サービス ](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![A/B テスト ](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**スタイル設定**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **事前入力サービス** （近日公開） | [**A/B テスト**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| CSS を使用したスタイル設定により、開発者はフォーム要素の外観をカスタマイズし、web サイトの美学に合わせて、視覚的に魅力的なデザインを作成できます。 | 事前入力サービスでは、様々なソースから関連するユーザーデータを自動的にフォームフィールドに入力し、手動入力を減らしてユーザーエクスペリエンスを向上させることができます。 | A/B テストを使用すると、組織は様々なフォームデザイン、レイアウト、機能を試して、最もパフォーマンスの高いバリアントを特定できます。 |

| ![ 分析とトラッキング ](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![ タスクの管理 ](/help/edge/docs/forms/universal-editor/assets/adobe-workfront.svg) | ![ データ バインディング ](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**分析とトラッキング**](https://www.aem.live/developer/martech-integration) | **タスクの管理** | **データ バインディング** |
| 組み込みの分析とトラッキングを使用して、ユーザーの行動、フォームのインタラクション、送信率に関するインサイトを取得し、データ駆動型のフォーム最適化を実現します。 | Adobe Workfront との統合により、チームはフォームの作成とメンテナンスのタスクを管理し、ワークフローを効率化できます。 | データバインディングにより、フォームフィールドとバックエンドデータソース間の直接接続が可能になり、リアルタイムの更新と高度なデータマッピングがサポートされます。 |

| ![CAPTCHA](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![Formsの埋め込み ](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![Thank You 設定 ](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|

| **エディターのカスタマイズ** | **Formsの埋め込み** | [**ありがとう設定**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
|開発者は、UI 拡張を通じてエディターの機能を拡張し、特定の組織ニーズに合わせてカスタマイズされたソリューションを実現できます。 | ユニバーサルエディターに組み込まれた埋め込みコンポーネントを使用して、フォームをEdge Delivery Services Sites ページに直接埋め込みます。 |フォームの送信が成功した後に、ユーザーに表示される確認メッセージまたはページを簡単にカスタマイズできます。 |


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
      <th></th> 
      <th>フォームコンポーネント</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="フォームコンポーネント" style="width: 100%;"></td> 
      <td><b>アコーディオン</b></td>
      <td>コンテンツを整理する折りたたみ可能なパネル構造。</td>
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
      <td>ユーザーがグループから複数のオプションを選択できます。</td>
    </tr>
    <tr>
      <td><b>日付選択</b></td>
      <td>ユーザーがカレンダーインターフェイスを使用して日付を選択できます。</td>
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
      <td>アラート、追加情報、または確認に使用されることが多いポップアップダイアログボックスを表示します。</td>
    </tr>
    <tr>
      <td><b>数値フィールド</b></td>
      <td>数値入力をキャプチャし、数値または範囲の検証を可能にします。</td>
    </tr>
    <tr>
      <td><b>パネル</b></td>
      <td>展開／折りたたみ可能なパネルを使用して、フォームのセクションを整理します。</td>
    </tr>
    <tr>
      <td><b>ラジオボタン</b></td>
      <td>オプションのグループからの単一選択を有効にします。</td>
    </tr>
    <tr>
      <td><b>レーティング</b></td>
      <td>ユーザーが星形ベースの評価を提供できます。</td>
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
      <td>国に基づく形式を使用して、電話番号をキャプチャします。</td>
    </tr>
    <tr>
      <td><b>テキスト</b></td>
      <td>法的条件を表示し、チェックボックスを通じてユーザーの同意を収集するための専用セクションを提供します。</td>
    </tr>
    <tr>
      <td><b>テキストフィールド</b></td>
      <td>名前やメールアドレスなど、単一行の入力をキャプチャします。</td>
    </tr>
    <tr>
      <td><b>ウィザード</b></td>
      <td>複数のパートで構成されるフォームプロセスを段階的にユーザーに説明します。</td>
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

ユニバーサルエディターおよび高度な機能（ルールエディターなど）を有効にするには、公式メール ID から aem-forms-ea@adobe.com までご連絡ください。フォーム作成エクスペリエンスを変えられるよう、アドビチームが支援します。

## よくある質問（FAQ）

**Q. ユニバーサルエディターは、どのようなユーザーが使用できますか？**
ユニバーサルエディターは、次のような幅広いオーディエンス向けに設計されています。

* 視覚に訴えるフォームを作成するコンテンツ制作者。
* 高度なカスタマイズおよび統合機能を必要とする開発者。
* スケーラブルで安全、かつ規制に準拠したフォームソリューションを探している組織。

**Q：ユニバーサルエディターで作成したフォームを既存のシステムに統合できますか？**
もちろんです。ユニバーサルエディターは、バックエンドシステムとのシームレスなデータバインディングをサポートし、リアルタイムの更新と高度なデータマッピングを可能にします。また、タスク管理用の Adobe Workfront などのツールと統合し、データ送信ワークフローの安全なエンドポイントをサポートします。

**Q：フォームコンポーネントをカスタマイズできますか？**
はい、ユニバーサルエディターを使用すると、開発者は特定の組織のニーズに合わせて調整されたカスタムコンポーネントを作成できます。さらに、UI 拡張機能とカスタムワークフローを通じてエディターの機能を拡張できます。

**Q：ユニバーサルエディターはアクセシビリティにどのように対応しますか？**
ユニバーサルエディターは、WCAG（Web コンテンツアクセシビリティガイドライン）を含むアクセシビリティ標準に厳密に準拠して設計されています。これにより、障がい者でもフォームを使用できるので、包括的なエクスペリエンスを提供できます。

**Q：フォームからどのような分析を取得できますか？**
ユニバーサルエディターには、ユーザーのインタラクション、フォーム送信率およびコンバージョン指標を監視する組み込みの分析およびトラッキングツールが含まれています。これらのインサイトは、フォームを最適化してパフォーマンスを向上させるのに役立ちます。


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

