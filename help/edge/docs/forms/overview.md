---
title: AEM Forms の Edge Delivery Services の概要
description: AEM FormsのEdge Delivery Servicesは、最高のパフォーマンスを実現するために構築されており、合理化されたデータ収集とユーザーエンゲージメントの将来を思い描くことができます。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 67fe933807f8a1bca681a6bcee7164f7c117bcac
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 7%

---


# AEM Edge Delivery ServicesのFormsの概要

<span class="preview">これはプレリリース機能で、[プレリリースチャネル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features)を通してアクセスできます。</span>

このガイドは、Adobe Experience Manager（AEM）Edge Delivery Services（EDS）を使用してフォームを理解し、実装するのに役立ちます。 単純な連絡先フォームを作成する場合でも、複雑なデータ収集ツールを作成する場合でも、このページではオプションを順を追って説明します。

## Edge Delivery ServicesのFormsについて

Edge Delivery Servicesは、優れたパフォーマンスと俊敏性を備え、フォームを含む web コンテンツを配信するためのAdobeの最新のソリューションです。 フォームにEdge Delivery Servicesを使用すると、次のことができます。

* **より高速なエクスペリエンスの提供：** Formsは、ユーザーに近いエッジサーバー（CDN）のグローバルネットワークから提供されるので、読み込みが非常に高速になります。 これにより、ユーザーの満足度が向上し、フォームの完了率が向上します。
* **Formsをより簡単に更新：** Edge Delivery Servicesのアプローチにより、多くの場合、開発サイクルとコンテンツ更新を高速化し、フォームを迅速に適応させることができます。
* **最新のレスポンシブなFormsを構築：** あらゆるデバイスで、見た目が美しくシームレスに動作するフォームを作成します。
* **スケーラビリティと信頼性のメリット：** フォームは、基盤となるエッジインフラストラクチャと同じくらい堅牢で拡張性があります。

このガイドでは、次の内容を説明します。

* Edge Delivery Sites 用のフォームを作成する方法を説明します。
* ユーザーがフォームを送信した後の動作（送信アクション）を設定する方法を示します。
* 特定のニーズやチームスキルに最適な方法を選択するのに役立ちます。
* アーキテクチャ図とベストプラクティスを説明します。

## 知っておくべき重要な用語

* **Edge Delivery Services（EDS）:CDN を介してAdobe コンテンツを配信するための、AEMのパフォーマンスファーストのアーキテクチャを** します。 プロジェクトフランクリンとも呼ばれます。
* **AEM Forms:** フォームの作成、管理、処理を行うためのAdobeのソリューションです。
* **ユニバーサルエディター（UE）:** フォームを含むAEM コンテンツ用の視覚的なWYSIWYG エディター。
* **ドキュメントベースのオーサリング：** Microsoft Word またはGoogle Docs/Sheets を使用してフォームを作成します。
* **ドキュメントオーサリング（DA）:** Adobeのコンテンツ（フォームをホストできるページを含む）をオーサリングするための、Edge Delivery Servicesでホストされたサービス。
* **Forms送信サービス （FSS）:** フォームデータをスプレッドシートやメールに簡単に送信できるAdobe サービスです。
* **AEM パブリッシュインスタンス：** 複雑なフォーム送信を処理できるライブ AEM環境です。
* **CORS （クロスオリジンリソース共有）:** 異なるドメインからフォームを埋め込む際に設定が必要なブラウザーセキュリティ機能。
* **CDN （コンテンツ配信ネットワーク）:** 地理的な場所に基づいてユーザーに web コンテンツをすばやく配信するサーバーのネットワーク。


**Edge Delivery Services フォームインタラクションの概念図**

<!--  
```mermaid
graph LR
    User[User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
    EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
    CDN >|Serves Content| User
    EdgeForm >|Submits Data| Backend[Backend Processing - e.g. Forms Submission Service / AEM Publish]
    style User fill:#f9f,stroke:#333,stroke-width:2px
    style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
    style CDN fill:#9cf,stroke:#333,stroke-width:2px
    style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![ フォームの統合 ](/help/forms/assets/eds-form-interaction.png)
次の図は、CDN 経由で迅速に配信されたフォームをユーザーがやり取りする様子を示しています。 その後、送信されたデータはバックエンドシステムで処理されます。

## FormsのEdgeでの動作

EDS を使用すると、AEM as a Cloud Service、SharePoint、Google Drive、Document Authoring （DA）サービスなど、様々なソースから、web サイトコンテンツ（フォームの構造を含む）を作成できます。 その後、このコンテンツはグローバル CDN に公開されます。 ユーザーがサイトを訪問すると、コンテンツは最も近い CDN エッジサーバーから直接提供され、最高速度が確保されます。

<!--*   **Where AEM Forms Fit In**
    Forms in an EDS architecture are designed to be:
    *   **Fast Loading:** Form structures are often simple HTML rendered client-side.
    *   **Decoupled:** The visual part of the form (frontend) is separate from where the data goes after submission (backend).
    *   **Flexible to Create:** You have different tools to build your forms.
    *   **Configurable for Submission:** You can send data to simple services or powerful AEM backends.-->

**FormsによるEdge Delivery Services アーキテクチャのシンプル化**

<!--
```mermaid
    graph TD
        UserStart[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
        EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
        CDN >|Serves Content| UserEnd[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device]
        EdgeForm >|Submits Data| Backend[Backend Processing - Form Submission Service / AEM Publish]

        style UserStart fill:#f9f,stroke:#333,stroke-width:2px
        style UserEnd fill:#f9f,stroke:#333,stroke-width:2px
        style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
        style CDN fill:#9cf,stroke:#333,stroke-width:2px
        style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![ アーキテクチャ ](/help/forms/assets/eds-simplified-architecture.png)
次の図に、ジャーニーを示します。フォームはオーサリングシステムで定義され、エッジに公開され、ユーザーに提供され、送信されたデータがバックエンドで処理されます。

## フォームのオーサリング方法の選択

Edge Delivery Services サイト用のフォームを作成する主な方法は 3 つあります。 選択する内容は、チームのスキル、フォームの複雑さ、プロジェクトのニーズによって異なります。

### 最適なオーサリングアプローチはどれですか？

このデシジョンツリーを使用して、次の項目を選択します。

**フォームオーサリングのデシジョンツリー**
<!--    
```mermaid
    graph TD
        A{Start: I need to create a form for an Edge Delivery Services site} > B{What are my team's primary content creation tools & skills?}
        B -- "We mainly use Word / Google Docs / Sheets" > C{How complex is the form and where does the data need to go?}
        B -- "We use AEM and prefer visual tools (Marketers or Designers)" > D[Use Universal Editor - WYSIWYG]
        B -- "Our site content is managed in Document Authoring (DA)" > E[Use Document Authoring - Embed Forms]
        C -- "Simple to moderate form, data to a spreadsheet or email" > F[Use Document-Based Authoring]
        C -- "More complex logic or needs AEM backend integration" > D
        E > G[Create form using Document-Based Authoring or Universal Editor, then embed in your DA page]

        style A fill:#f9f,stroke:#333,stroke-width:2px
        style F fill:#ccf,stroke:#333,stroke-width:2px
        style D fill:#ccf,stroke:#333,stroke-width:2px
        style G fill:#ccf,stroke:#333,stroke-width:2px
``` -->

![ 適切なプラットフォームの選択 ](/help/forms/assets/eds-authoring-selection.png)

このデシジョンツリーでは、チームおよびフォームのニーズに基づいてオーサリング方法を選択できます。

### ドキュメントを使用したFormsの作成（Word/Google Docs）

この方法は、[ チームがMicrosoft Word やGoogle Docs/シートに慣れている場合は、フォームをすばやく作成する ](/help/edge/docs/forms/create-forms.md) のに最適です。

**仕組み：ドキュメントから Web フォームへ**

フォームのフィールド、ラベル、および種類は、特殊な表形式または「フォームブロック」を使用して、Word 文書またはGoogle シートで直接定義します。 このドキュメントを公開すると、Edge Delivery Servicesによって、ユーザーがサイト上でやり取りできる web 対応のHTML フォームに自動的に変換されます。

**機能と特徴**

* 使い慣れたツール（Word、Google Docs、Google Sheets）でオーサリングします。
* フィールドの定義：テキスト入力、メール、ドロップダウン、チェックボックス、ラジオボタン、テキスト領域。
* ラベル、プレースホルダーおよびヘルプメッセージを追加します。
* 基本的な検証ルール（必須フィールド、メールフォーマット）を設定します。
* スパム対策として reCAPTCHA を統合します。
* ファイルのアップロードを許可します。
* 即座に公開：ドキュメント内の変更は、ライブサイトに素早く反映されます。
* カスタムコードを使用した拡張：上級ユーザーは、GitHub を使用してカスタムフォームコンポーネントとスタイルを追加できます。

**検討事項**

* チームはコンテンツに Word またはGoogle Docs/シートを定期的に使用している。
* シンプルなフォームから適度に複雑なフォームをすばやく作成する必要があります。
* 最小限の設定で、フォームデータをスプレッドシートまたはメールアドレスに直接送信する場合。

**送信の仕組み（主にForms送信サービス）**

Formsは、通常、この方法で作成されました [ データをAEM Forms送信サービスに送信します ](/help/forms/forms-submission-service.md)。 これは（多くの場合、ソースドキュメント自体で）Google シート、OneDrive/SharePoint上の Excel ファイル、またはメールにデータを送信するように設定します。

**ドキュメントベースのオーサリングの概念**
<!--    
```mermaid
    graph LR
        subgraph Authoring["You define your form in a Google Sheet or Word Document"]
        Sheet[Spreadsheet or Document with field definitions:\nField Name - Type - Label\nemail - email - Email Address\nmessage - textarea - Your Message]
    end

        Sheet >|Edge Delivery Services automatically converts it| JSON[Internal Form Definition as JSON]
    JSON >|A 'Form Block' on your page renders it as| HTMLForm[Live HTML Form on Your Website]

        style Sheet fill:#e6ffe6,stroke:#333
        style JSON fill:#e6e6ff,stroke:#333
        style HTMLForm fill:#ffe6e6,stroke:#333
```-->

![ ドキュメントベース ](/help/forms/assets/eds-doc-based.png)
次の図は、ドキュメント内で定義されたフォームが、ライブ web フォームになる仕組みを示しています。

### ユニバーサルエディターを使用したFormsのビジュアル化

[ ユニバーサルエディター ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) は、Web ブラウザーで直接フォームを作成するための、最新のドラッグ&amp;ドロップインターフェイスを提供します。

**仕組み：フォーム作成をドラッグ&amp;ドロップする**

ビジュアルインターフェイスを使用して、入力フィールド、ボタン、ドロップダウンなどのフォームコンポーネントをページにドラッグできます。 プロパティパネルを使用して各コンポーネントのプロパティ（ラベル、検証など）を設定できます。 ユニバーサルエディターは、フォームのリアルタイムプレビューを表示します。

**機能と特徴**

* 事前定義済みコンポーネントのライブラリを使用したビジュアルフォームの作成。
* リアルタイム検証とビジネスロジックを設定します（例：選択に基づいてフィールドを表示/非表示）。
* 様々なデバイス（デスクトップ、モバイル）のライブプレビューを参照してください。
* と、コンテンツフラグメント、AEM ワークフロー、ユーザー権限などのAEM機能を統合します。
* 「Experience Builder」を使用して、プロンプトを使用したフォームの作成または編集に関する AI の支援を受けることができます。

**検討事項**

* 条件付きロジック、複数手順のパネルまたはパーソナライゼーションを使用して複雑なフォームを作成する必要があります。
* 担当のチーム（マーケター、ビジネスユーザーなど）がビジュアルツールを好んでいる。
* ガバナンス、ワークフロー、またはフォームでAEM as a Cloud Service アセットを使用するには、AEMとの強力な統合が必要です。

**送信の仕組み（Forms送信サービスまたはAEM公開）**

ユニバーサルエディターで構築されたFormsは、次のことが可能です。

* シンプルな [Forms送信サービス ](/help/forms/forms-submission-service.md) （スプレッドシートまたはメールへのデータ送信用）を使用します。
* より高度な処理（AEM ワークフローの開始、フォームデータモデルの使用、他のエンタープライズシステムとの統合など）を行うために、AEM パブリッシュインスタンスにデータを送信します。

**ユニバーサルエディターの概念**

<!--    
```mermaid
    graph TD
    subgraph UE_Interface["Universal Editor Interface in your Browser"]
        Toolbar[Editor Toolbar and Asset Finder]
        Canvas[Your Page with the Form Being Built]
        ComponentPalette[Available Form Components:\nInput / Dropdown / Button\nDrag and drop]
        PropertiesPanel[Configure Selected Component:\nLabel / Validation / Rules]
    end
    ComponentPalette >|Drag & Drop onto| Canvas
    Canvas >|Select a component to edit its| PropertiesPanel
    UE_Interface >|Creates| RenderedForm[Live Form on Your Website]

    style UE_Interface fill:#f0f8ff,stroke:#333
    style RenderedForm fill:#ffe6e6,stroke:#333
```-->

![ユニバーサルエディター](/help/forms/assets/eds-ue-based.png)

次の図は、フォームの作成に使用されるユニバーサルエディターの主要な部分を示しています。

### ドキュメントオーサリング（DA）でのFormsの使用

[ ドキュメントオーサリング（DA） ](https://www.aem.live/developer/da-tutorial) は、Adobeをホストするサービスで、Edge Delivery Servicesを介して配信される主な web サイトコンテンツ（ページ、記事）を作成および管理します。 Edge Delivery Services ソースコンテンツにSharePointまたはGoogle Drive を使用する代わりに使用できます。

**Edge Delivery Services コンテンツのドキュメントオーサリング（DA）について**

ドキュメントオーサリングは、Adobeのデザインシステム（Spectrum）とAEMのドキュメントモデル（ブロック、セクション）を使用した、エンタープライズクラスのオーサリング環境を提供します。 EDS 向けの構造化されたコンテンツ管理向けに設計されています。

**DA によるFormsの処理方法（ダイレクトオーサリングではなく埋め込み）**

DA 自体は **フォームをゼロから作成するためのツールではありません**。 代わりに、DA を使用して web ページを作成し、（ドキュメントベースのオーサリングまたはユニバーサルエディターを使用して作成された *フォームを* 埋め込み」します。

**DA ページにFormsを埋め込む手順**

1. **フォームを作成する：** 次のいずれかを使用してフォームを作成します。
   * ドキュメントベースのオーサリング（Word/Google Docs）
   * ユニバーサルエディター

1. **フォームを公開：** このフォームが公開され、独自のEdge Delivery URL （例：`https://your-eds-project.hlx.page/forms/contact-us`）を使用してアクセスできることを確認します。
1. **DA でページを作成する：** フォームを表示するドキュメントのオーサリングでページを作成または編集します。
1. **フォームを埋め込む：** DA ページ内の特定の「ブロック」またはコンポーネントを使用して、その URL からフォームを参照および埋め込みます。 DA ページは、この外部で作成されたフォームを取得して表示します。

**埋め込みフォームを使用したドキュメントオーサリング**
<!--
```mermaid
    graph TD
    subgraph FormCreation["1. Create Form using other methods"]
        UE_Form[Universal Editor Form] >|Published to| FormLocation[Form lives at its own Edge Delivery Services URL:\nfor example: /forms/my-contact-form]
        DocBased_Form[Document-Based Form] >|Published to| FormLocation
    end

    subgraph DA_Content["2. Author Page in Document Authoring"]
        DAPage[Your Web Page Authored in DA\nExample: /main-site/landing-page]
        EmbedBlock[On DA Page, add 'Embed Form' Block\nPoints to /forms/my-contact-form]
    end

    DAPage > EmbedBlock
    User[User visits your DA Page] > DAPage
    EmbedBlock >|DA Page fetches and displays| FormLocation[The Form appears on your DA Page]

    style FormCreation fill:#e6ffe6,stroke:#333
    style DA_Content fill:#ffe6cc,stroke:#333
    style FormLocation fill:#ccf,stroke:#333
```-->

![ ドキュメントのオーサリング ](/help/forms/assets/eds-da-based.png)

次の図は、最初に UE またはドキュメントを使用してフォームを作成し、次にドキュメントオーサリングで作成するページに埋め込むことを示しています。


### オーサリングオプションの比較

| 条件 | ドキュメントベースのオーサリング | ユニバーサルエディター（WYSIWYG） | ドキュメントオーサリング （DA）におけるForms |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **プライマリ オーサリング ツール** | Word/Google Docs/Sheets | ブラウザー（AEM Universal Editor） | 該当なし（Formsは *埋め込み*） |
| **チームスキルレベル** | ドキュメントエディターに精通している | ビジュアル Web ツールの操作に慣れている | ページコンテンツに DA を使用 |
| **一般的なフォームの複雑さ** | シンプルから中程度 | 中規模から複雑、エンタープライズ・クラス | 埋め込まれたフォームに依存 |
| **送信オプション 1 （シンプル）** | Forms送信サービス （シート/メールへ） | Forms送信サービス （シート/メールへ） | 埋め込みフォームの設定に従う |
| **送信オプション 2 （詳細）** | 該当なし | AEMの公開（ワークフロー、FDM など） | 埋め込みフォームの設定に従う |
| **AEMのバックエンドの統合** | 最小 | 高（AEM パブリッシュ送信付き） | 間接的（埋め込みユニバーサルエディターフォーム経由） |
| **次の場合に最適…** | コンテンツチームによるシンプルなフォームの迅速な作成、迅速なデータキャプチャ。 | 視覚的な制御、複雑なフォーム、AEMの深い統合を必要とするマーケターやビジネスユーザー。 | プライマリコンテンツが DA で管理され、他のソースからのフォームが必要なサイト。 |

**強化されたデシジョンツリー**
<!--
```mermaid
    graph TD
    A{Start Here: I need a form on my Edge Delivery Services Site} > B{What's my team's main authoring tool & skill for form content?};
    B -- "Word/Google Docs" > C{How complex is the form & data destination?};
    C -- "Simple form, data to Sheet/Email" > Sol1[CHOOSE: Document-Based Authoring + Forms Submission Service];
    C -- "Needs more logic OR AEM backend\nlike Workflow or FDM" > Sol2[CONSIDER: Can Universal Editor meet this need better?];

    B -- "AEM User / Visual Editor needed\nMarketer or Designer" > D{Where does the form data need to go?};
    D -- "Simple - to Sheet/Email" > Sol3[CHOOSE: Universal Editor + Forms Submission Service];
    D -- "Advanced - AEM Workflow, FDM,\n3rd Party via AEM" > Sol4[CHOOSE: Universal Editor + AEM Publish Submissions\nRequires additional setup];

    B -- "Our main site content is in Document Authoring (DA)" > Sol5[STRATEGY: Author form using Sol1, Sol2, Sol3 or Sol4 first\nTHEN embed that form into your DA page];

    A > F{Will this form be embedded or fetched from another site or domain?};
    F -- "Yes" > G[IMPORTANT: Configure CORS on the site hosting the form.\nEnsure any form JavaScript blocks are available where the form is displayed];

    style Sol1 fill:#90ee90,stroke:#333
    style Sol2 fill:#fffacd,stroke:#333
    style Sol3 fill:#90ee90,stroke:#333
    style Sol4 fill:#90ee90,stroke:#333
    style Sol5 fill:#add8e6,stroke:#333
    style G fill:#ffb6c1,stroke:#333
```-->

![ デシジョンツリー ](/help/forms/assets/eds-enhanced-decision.png)

## オーサリングメソッドの機能比較

次の表は、様々な AEM フォームオーサリング方法の主な機能の詳細な比較を示し、要件に最も適したアプローチを選択するのに役立ちます。

| **機能** | **ユニバーサルエディター（WYSIWYG）** | **ドキュメントベースのオーサリング** | **ドキュメントオーサリング（DA）** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Sites との統合構成** | ✅ |                              | ✅ （埋め込みフォームを使用） |
| **埋め込みフォームのサポート** | ✅ | ✅ | ✅ （ユニバーサルエディターまたはドキュメントから埋め込み） |
| **ルール（動的動作）** | カスタム関数を備えた高度なルールエディター | 限定的：表示／非表示、値を計算、カスタム関数 | 埋め込みフォームに依存 |
| **添付ファイルのサポート** | ✅ | ℹ️（早期アクセス） | 埋め込みフォームに依存 |
| **CAPTCHA サポート** | reCAPTCHA Enterprise | reCAPTCHA Enterprise | 埋め込みフォームに依存 |
| **送信機能** | REST, メール，FDM, ワークフロー，SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion （EA） | スプレッドシートのみ | 埋め込みフォームの設定に従う |
| **データスキーマ** | FDM、カスタム | カスタム | 埋め込みフォームに基づく |
| **事前入力** | 💡 （ウィザード経由） | ✅ | 埋め込みフォームに依存 |
| **フラグメント** | ✅ | ✅ | 埋め込みフォームに依存 |
| **ビジュアルルールエディター** | ✅ |                              |                              |
| **ローカライゼーション** | 💡 （Sites 経由） | ℹ️（Excel/Sheets マニュアル） | 埋め込みフォームに依存 |
| **データスキーマ（データツリー）** | 💡 （UI 拡張機能を使用） |                              |                              |
| **テンプレートのサポート** | 初期コンテンツのみ |                              |                              |
| **ポータル** |                               |                              |                              |
| **テーマ** | ℹ️（プロジェクトレベルで） | ℹ️（プロジェクトレベルで） | ℹ️（ホスティングサイトをベース） |
| **カスタムコンポーネント** | ✅ | ✅ | ✅ （埋め込みコンポーネントがサポートしている場合） |
| **OOTB およびカスタム関数** | ✅ | ✅ | ✅ （埋め込み形式） |
| **フラグメント参照** |                               |                              |                              |
| **Sign との統合** |                               |                              |                              |
| **実験** | ✅ | ✅ | 埋め込みコンテキストに依存 |
| **Workfront 経由でのタスク管理** | ✅ |                              |                              |
| **パーソナライゼーション拡張機能** | 💡 |                              |                              |
| **エディターのカスタマイズ** | ✅ （UI 拡張機能を使用） |                              |                              |
| **送信アクション** | ✅ | スプレッドシートのみ | 埋め込みフォームに基づく |

<!--

## Best Practices for Creating Forms

Building great forms goes beyond just the technology. Here's how to ensure your forms are user-friendly and achieve their goals:

* **Designing User-Friendly and Accessible Forms**

  *   **Use Clear, Visible Labels:** Every form field needs a `<label>`. Don't rely only on placeholder text (text inside the input field), as it disappears when users type and is bad for accessibility.
        *   *Good:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
        *   *Bad:* `<input type="email" placeholder="Email Address">`
  *   **Keep it Simple:** Use standard HTML input types (`<input type="date">`, `<input type="tel">`) where possible. They often have better mobile support and accessibility than complex custom widgets.
  *   **Logical Order and Grouping:** Arrange fields in a way that makes sense to the user. Group related fields together using `<fieldset>` and `<legend>`.
  *   **Provide Clear Instructions:** For any fields that might be confusing, offer concise help text or tooltips.
  *   **Keyboard Navigation:** Ensure users can navigate through your entire form using only the keyboard (Tab, Shift+Tab, Enter, Spacebar).
  *   **Error Handling:** Make errors obvious and easy to correct. Display error messages next to the relevant field and explain what needs to be fixed.

* **Ensuring Your Forms Load Quickly and Are Visible**

  *   **Place Forms Prominently:** If a form is important, make sure users can see it easily without too much scrolling ("above the fold" if possible). Adobe's research shows many forms get low interaction because they are hidden.
  *   **Optimize Assets:** Keep any custom JavaScript or CSS for your forms as small as possible to ensure fast load times. Edge Delivery Services helps with the base page load, but heavy form scripts can still slow things down.

* **Handling User Data Responsibly**
  *   **Ask Only What You Need:** The less Personal Identifiable Information (PII) you ask for, the better. Every field is a potential reason for a user to abandon the form.
  *   **Be Transparent:** Clearly explain *why* you need certain information and *how it will be used*. Link to your privacy policy. This builds trust.

* **Improving User Experience: Captcha Alternatives**

  * **Rethink Visible Captchas:** Those "type the wavy text" or "click all the traffic lights" tests can be very frustrating for users, especially those with disabilities, and often lead to high drop-off rates.

*   **Consider Alternatives:**
    *   **Honeypot Fields:** Add a hidden field that only bots would fill out. If it has data, the submission is likely spam.
    *   **Time-Based Checks:** Measure how quickly a form is submitted. Submissions that are too fast are often bots.
    *   **Invisible reCAPTCHA (v3):** This Google service analyzes user behavior in the background and only presents a challenge if the user seems suspicious. This is often a much better user experience.

**Form Design Do's and Don'ts**

```mermaid
    graph LR
subgraph GoodFormUX [Do ✅ - For Better Forms]
    direction LR
    ClearLabels[Use Visible <label> Tags for All Fields]
    SimpleInputs[Prefer Standard HTML Input Types]
    KeyboardNav[Ensure Full Keyboard Navigation]
    ClearErrors[Show Clear, Actionable Error Messages]
    MinimalPII[Ask Only for Necessary Information]
    TransparentUse[Explain How Data is Used - Privacy Info]
    InvisibleCaptcha[Use Invisible or Behavioral CAPTCHA]
    ProminentPlacement[Make Form Easy to Find on Page]
end

subgraph BadFormUX [Don't ❌ - Avoid These]
    direction LR
    PlaceholderOnly[Only Use Placeholder Text for Labels]
    ComplexWidgets[Use Overly Complex Custom Widgets]
    PoorErrors[Vague or Missing Error Messages]
    ExcessivePII[Request Excessive Personal Data]
    VisibleHardCaptcha[Use Hard-to-Solve Visible CAPTCHAs]
    HiddenForm[Hide the Form Deep in the Page]
end

style GoodFormUX fill:#e6ffe6,stroke:#333
style BadFormUX fill:#ffe6e6,stroke:#333
```

## Quick Decision Guide: Choosing the Right Form Strategy

Let's bring it all together to help you decide on the best approach for your forms.

*   **Matching Form Features to Your Project Goals**
    *   **For speed and simplicity with basic data capture (to spreadsheets/email):** Document-Based Authoring with the Forms Submission Service is often your fastest route.
    *   **For visually rich forms with potential for AEM backend integration:** Universal Editor is your tool. You can start with the Forms Submission Service for simple needs and scale to full AEM Publish submissions for complex workflows.
    *   **If your site content is managed in Document Authoring (DA):** You'll create forms using one of the above methods and then embed them into your DA pages. The submission logic will be tied to how the original embedded form was configured.-->

学習した内容を踏まえて、進め方を次に示します。

[ 送信方法を選択 ](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) プロジェクトにForms送信サービスのシンプルさ（スプレッドシートやメールの出力に最適）が必要か、AEM公開送信アクションの柔軟なバックエンド統合が必要かを判断します。

効果的でアクセスしやすく、使いやすいフォームを設計する方法については、[Formsを作成するためのベストプラクティス ](/help/edge/docs/forms/universal-editor/best-pratices-eds-forms.md) の記事を参照してください。

## 次の手順

このガイドでは、AEM Edge Delivery Servicesでのフォームの使用の概要について説明しました。 具体的な設定の詳細な手順については、次のAdobe Experience Managerの公式ドキュメントを参照してください。

* [Edge Delivery Services Formsによるドキュメントベースのオーサリング](/help/edge/docs/forms/tutorial.md)
* [Edge Delivery Services Formsを使用したユニバーサルエディター](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [ ドキュメントオーサリング（DA）とコンテンツの埋め込み ](https://www.aem.live/developer/da-tutorial)
* [AEM Forms送信サービス](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)


<!-- 
# Edge Delivery Services for AEM Forms
 

Edge Delivery Services for AEM Forms is a composable set of services that enables a rapid development environment where authors can update, publish, and launch new forms rapidly. These services deliver exceptional and high impact forms experiences that drive engagement and conversions. These forms experiences are easy to author and develop.

These services enable you to:

* **Create enrolment experiences with tools of your choice:** Increase authoring efficiency by decoupling content sources. Out of the box you can use Document-based Authoring (Microsoft SharePoint or Google Drive), WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor). You can work with multiple content sources on the same forms site and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, Universal Editor, or Adaptive Forms Editor.

* **Deliver exceptional Digital Enrolment experiences:** Deliver Digital Enrolment experiences that load and render quickly and continuously monitor your forms performance through Operational Telemetry. Faster loading times and optimized user experience contribute to higher form completion and conversion rates. 

* **Use developer friendly toolset:** Edge Delivery Services for AEM Forms
 uses plain HTML, modern CSS, and vanilla JavaScript to create exceptional experiences, avoiding the steep learning curve of a specific framework. A developer with basic web development skills can customize and easily build form components and experiences. There is no need to wait for a pipeline to run, just check-in your code into GitHub and your changes are live.

## Edge Delivery Services for AEM Forms Overview {#edge-overview}

Edge Delivery Services for AEM Forms allows for a high degree of flexibility in how you author forms on your website. You can author content and forms with [WYSIWYG Authoring](/help/forms/creating-adaptive-form-core-components.md) as well as [Document-based Authoring](/help/edge/docs/forms/create-forms.md). Edge Delivery Services for AEM Forms
 provide a forms block, known as [Adaptive Forms Block](/help/edge/docs/forms/create-forms.md) to add a form to your Edge Delivery Services site.

For example, you author forms directly in Microsoft Excel or Google Sheets and these spreadsheets are transformed into forms for your website. Any new form or form content, such as a new form field, is instantly available on your website without requiring a rebuild process.

The following diagram illustrates how you can edit forms in Microsoft Excel or Google Sheets (Document-based Authoring) and publish to Edge Delivery Services. It also shows the AEM publishing method using the WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor).

![Publish to Edge Delivery Services and AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services for AEM Forms uses GitHub so customers can manage and deploy code directly from their GitHub repository. For example, you can write forms in either [Google Sheets](/help/edge/docs/forms/create-forms.md) or [Microsoft Excel](/help/edge/docs/forms/create-forms.md) and the components of your forms can be developed by using CSS and JavaScript in a GitHub repository.

When your forms are ready, you can use the [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), a chrome browser extension, to preview and publish content updates.

![Install AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

The choice between the [Document-based Authoring ](#document-based-authoring-features) and [WYSIWYG Authoring](#wysiwyg-authoring-features) depends on your specific requirements:

* For simple forms that just collect basic information with a few fields (think contact us forms, lead generation forms, or service request forms), and where you need quick data connectivity using a spreadsheet, the [Document-based Authoring](#document-based-authoring-features) is a good fit. You can build these forms like you would build a document in Google Sheets or Microsoft Excel. 

* For complex forms, like forms requiring multiple panels, complex rules and business logic, data manipulation, integration with external systems, or streamlined workflows using AEM features, then [WYSIWYG Authoring](#wysiwyg-authoring-features) is a better option. 


### Key Features of Document-based Authoring and WYSIWYG Authoring

Document-based Authoring offers a basic set of features and WYSIWYG Authoring unlocks additional capabilities beyond the Document-based Authoring, empowering you to build more complex and interactive forms. The key features of both Document-based Authoring and WYSIWYG Authoring are:

#### Document-based Authoring features

Document-based Authoring  allows you to create forms using familiar tools like Microsoft Excel or Google Sheets. These forms offer the following functionalities:

* Accessible components for a user-friendly experience.
* Standardized HTML structure for consistent rendering.
* Rules and validations to ensure data accuracy.
* File attachment options for collecting additional information.
* Google reCAPTCHA integration for spam protection.
* Ability to create custom form components for specific needs.
* Submit form data directly to Microsoft Excel or Google Sheets or email addresses.
* Monitor your forms performance through Operational Telemetry

#### WYSIWYG Authoring features

WYSIWYG Authoring provides WYSIWYG interfaces (Universal Editor and Adaptive Forms Editor) for building forms and offers all the capabilities of Document-based Authoring, plus a wide range of additional features:

* Advanced rules editor for creating complex logic.
* Server-side extensibility for custom functionalities.
* WYSIWYG editing experience for easy form creation and visualization.
* Document of record functionality to create tamper-proof archives of submitted data.
* Integration with Adobe Sign for electronic signatures.
* Integration with Adobe Workfront Fusion to triggering Adobe Workfront Fusion scenarios upon form submission.
* Integration with various data sources for pre-populating forms and submitting data.
* Form Data Model (FDM) for defining data structure and interactions with various data sources.
* Ability to choose from multiple submit actions for handling form submissions, including submitting data to Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics, many more data sources.

The all above features are also available via Adaptive Forms Editor. 

In essence, WYSIWYG Authoring (Universal Editor and [Adaptive Forms Editor](/help/forms/creating-adaptive-form-core-components.md)) builds upon the foundation of [Document-based Authoring](/help/edge/docs/forms/create-forms.md), providing a more advanced toolkit for creating and managing complex forms. 

>[!NOTE]
>
>
> The WYSIWYG Authoring capability is available under the early-adopter program. If you are interested, send a quick email from your work address to aem-forms-ea@adobe.com to request access to the capability.

### Edge Delivery Services for AEM Forms

: Authoring, Publishing, and Submission of Forms  

The following diagrams illustrate the process of creating, publishing, and submitting forms using Document-based Authoring and WYSIWYG Authoring.

![Document-based Authoring](/help/edge/assets/document-based-authoring-workflow.png)

![WYSIWYG Authoring](/help/edge/assets/wysiwyg-authoring-workflow.png)

## Start creating forms

* [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
* [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
* [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
* [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
* [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
* [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
* [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using Edge Delivery Services forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an Edge Delivery Services form" style="border-radius: 5px;"> </b>
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
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
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
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->
