---
title: Edge Delivery Servicesを使用したAEM Formsの送信アクションの設定
description: Edge Delivery Servicesを使用してAEM Formsで送信アクションを設定する方法を説明します。 Forms送信サービスとAEM公開送信アクションのどちらかを選択して、フォームデータを安全かつ効率的に処理します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: bca160763fdd1e96f1350ac74eb76ff7c26ac00b
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 1%

---


# フォーム送信の設定：データはどこに送信されますか？

ユーザーがフォーム上で **送信** をクリックした後、そのデータに対して何を行うかをEdge Delivery Servicesに指示する必要があります。 次の 2 つの主なオプションがあります。

## 方法 1:AEM Forms Submission サービスの使用（簡略化）

このサービスは、スプレッドシートやメールへのデータの送信など、一般的でわかりやすいアクションに最適です。

**機能とメリット**

[Forms送信サービス ](/help/forms/forms-submission-service.md) は、Adobeがホストするエンドポイントです。 フォームからデータが送信されると、このサービスが引き継がれ、事前設定済みのアクションを実行します。 設定が簡単になるよう設計されています。 以下を設定できます。スプレッドシートまたはメールへの送信

* **スプレッドシートに送信：** 送信されたフォームデータを新しい行としてGoogle シートまたはMicrosoft Excel ファイル（OneDrive またはSharePointに保存）に自動的に追加します。
* **メールを送信：** フォームデータを含むメールを、指定した 1 つ以上のメールアドレスに送信します。

#### 重要：設定要件

* **Spreadsheet Access:** Google Sheet または OneDrive/SharePoint上の Excel ファイルにデータを送るには、通常、Adobe サービスアカウント （多くの場合 `forms@adobe.com`）は、その特定のスプレッドシートで **編集権限** が必要です。
* **アーリーアクセスプログラム：** このサービスの一部の機能（特にスプレッドシートの機能）は、アーリーアクセスプログラムの一部である可能性があります。 電子メールで送信するか、特定のAdobe フォームにプロジェクトの詳細 `aem-forms-ea@adobe.com` 入力して、アクセスをリクエストする必要がある場合があります。 最新のAdobe ドキュメントを常に確認してください。

**Forms送信サービスのフローチャート**
<!--
```mermaid
    graph TD
    UserForm[User Submits Form on Your EDS Site] >|Data Sent| FormSubmissionService[AEM Forms Submission Service]
    FormSubmissionService -- "If configured for Google Sheets" > GoogleSheet[Data written to Google Sheet]
    FormSubmissionService -- "If configured for Excel (OneDrive or SharePoint)" > ExcelSheet[Data written to Excel]
    FormSubmissionService -- "If configured for Email" > Email[Email with data is sent]

    style UserForm fill:#ccf,stroke:#333
    style FormSubmissionService fill:#fca,stroke:#333
    style GoogleSheet fill:#90ee90,stroke:#333
    style ExcelSheet fill:#90ee90,stroke:#333
    style Email fill:#add8e6,stroke:#333
```-->
![Formsの送信 ](/help/forms/assets/eds-fss.png)

このフローチャートは、Forms送信サービスが送信されたデータを取得して、設定済みのスプレッドシートまたはメールに送信する方法を示しています。

## 方法 2:AEM パブリッシュインスタンスへの送信（詳細）

より複雑なニーズに対しては、[ フォーム（特にユニバーサルエディターで作成されたフォーム）からAEM as a Cloud Service パブリッシュインスタンスに直接データを送信できます ](/help/forms/configure-submit-actions-core-components.md)。 これにより、AEMの完全なバックエンド機能が解放されます。

**AEM Publish に送信する必要があるのはいつですか？**

* 送信後にカスタム AEM ワークフローをトリガーするには：
* AEM フォームデータモデル（FDM）を使用してデータベースまたは他のエンタープライズシステムと統合するには、次の手順を実行します。
* Marketo、Microsoft Power Automate、Adobe Workfront Fusion などのサードパーティサービスに接続する場合。
* Azure Blob Storage やSharePoint リスト/ドキュメントライブラリ（単純なスプレッドシートだけでなく）などの特定の場所にデータを保存する場合。
* AEM内に複雑なサーバーサイド検証やデータ処理ロジックがある場合。

**使用可能な送信アクション（AEM公開送信）**

* [REST エンドポイントへの送信](/help/forms/configure-submit-action-restpoint.md)
* [メールの送信（AEMのメールサービスを使用）](/help/forms/configure-submit-action-send-email.md)
* [フォームデータモデル（FDM）を使用して送信](/help/forms/configure-data-sources.md)
* [AEM ワークフローを起動](/help/forms/aem-forms-workflow-step-reference.md)
* [SharePointへの送信（リスト項目またはドキュメントとして）](/help/forms/configure-submit-action-sharepoint.md)
* [OneDrive に送信（ドキュメントとして）](/help/forms/configure-submit-action-onedrive.md)
* [Azure Blob Storage に送信](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Microsoft Power Automate への送信](/help/forms/forms-microsoft-power-automate-integration.md)
* [Adobe Workfront Fusion への送信](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Adobe Marketo Engageへの送信](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> AEM Publish からGoogle Sheet/Excel をターゲットに設定する場合でも、Formsへの直接送信サービスとは異なる設定手順が必要になります。

**AEM送信公開フローチャート**

<!--```mermaid
    graph TD
    UEForm[User Submits Universal Editor Form on EDS Site] >|Data sent to AEM Publish URL - example: /adobe/forms/af/submit/...| AEMPublish[AEM Publish Instance]
    AEMPublish -- Configured to run AEM Workflow > AEMWorkflow[AEM Workflow is Triggered]
    AEMPublish -- Configured to use Form Data Model > FDM[FDM updates Backend System or Database]
    AEMPublish -- Configured for Marketo > Marketo[Data sent to Marketo Engage]
    AEMPublish -- Other configured actions... > OtherIntegrations[...]

    style UEForm fill:#ccf,stroke:#333
    style AEMPublish fill:#fca,stroke:#333
    style AEMWorkflow fill:#add8e6,stroke:#333
    style FDM fill:#add8e6,stroke:#333
    style Marketo fill:#add8e6,stroke:#333
```-->

![AEM送信公開フローチャート ](/help/forms/assets/eds-aem-publish.png)
このフローチャートは、AEM公開に送信するフォームを示しています。このフォームが、複雑なバックエンドタスクを処理します。

### Forms Submission サービスとAEM Publish の送信の比較

| 機能 | Forms送信サービス | AEM送信内容の公開 |
| :- | :- | :-- |
| **次に最適** | スプレッドシートやメール通知へのシンプルなデータキャプチャ | 複雑なワークフロー、エンタープライズ統合、カスタムロジック |
| **フォームオーサリング** | ドキュメントベースに適しています。シンプルな UE フォームで問題ありません | ユニバーサルエディターで作成されたフォームに最適 |
| **設定作業** | 低（多くの場合、シンプルな設定） | 上位（AEM パブリッシュ、Dispatcher、OSGi、CDN 設定が必要） |
| **バックエンドシステム** | Adobeがホストするサービス | AEM as a Cloud Service パブリッシュインスタンス |
| **柔軟性** | シート / メールに制限 | 非常に柔軟で、AEM Formsの様々なアクション |
| **例** | Google シートへのコンタクトフォームデータ | AEM承認ワークフローをトリガーするローン申請 |

## 様々なサイトやページにFormsを埋め込む方法

作成および管理が 1 か所で行われているフォーム（中央の「フォームサイト」など）を、別の web ページやサイトに表示したい場合があります。

### フォームを埋め込む理由

* ユニバーサルエディターで作成された標準の「お問い合わせ」フォームがあり、ドキュメントベースのオーサリングで作成された複数のランディングページに表示する必要がある場合。
* メインの web サイトのコンテンツはドキュメントオーサリング（DA）内にあり、専用のフォームを含める必要があります。
* 複数の異なる EDS プロジェクトにわたって、適切に管理された 1 つのフォームを再利用したい。

### フォームの埋め込みが技術的にどのように機能するか

フォームを表示するページ（「ホストページ」と呼びましょう）には、いくつかのコード（通常は特別なブロックまたはスクリプト）が含まれます。 ユーザーがホストページにアクセスすると、このコードは、実際のフォームがホストされている URL に対してリクエストを行います（これを「フォームSource」と呼びましょう）。 その後、フォームSourceがHTMLを返し、ホストページが挿入されて表示されます。

**埋め込みフォームアーキテクチャ**

<!--```mermaid
   graph LR
    User[User] >|Visits| HostPage[Host Page - for example: your-site.com/landing-page]
    HostPage >|Contains code to embed form| FetchForm{Host Page Requests Form HTML}
    FetchForm >|HTTP GET request to the form URL| FormSource[Form Source - for example: forms-repo.hlx.page/my-form]
    FormSource >|Returns form HTML| FetchForm
    FetchForm >|Injects form HTML into page| HostPage
    HostPage >|Displays full page with embedded form| User

    subgraph Submission ["Form Submission from Host Page"]
        HostPage_Form[Embedded form on the host page] >|User submits| TargetEndpoint[Submission endpoint - FSS or AEM Publish]
    end

    style HostPage fill:#e6f3ff,stroke:#333
    style FormSource fill:#ffe6e6,stroke:#333
    style FetchForm fill:#fff2cc,stroke:#333
    style Submission fill:#f0fff0,stroke:#333
```-->
![ 埋め込みフォームアーキテクチャ ](/help/forms/assets/eds-embedded-form.png)
次の図は、フォームSourceからフォームHTMLを取得して表示するホストページを示しています。 送信では、元のフォームの設定済みエンドポイントが使用されます。

## 埋め込みForms用 CORS の設定

[CORS （クロスオリジンリソース共有） ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) は、ブラウザーのセキュリティ機能です。 ホストページ（`site-a.com` など）が別のドメイン（`forms-site-b.com` など）からフォームを取得しようとすると、ブラウザーは CORS ヘッダーを使用して明示的に許可しない限り、フォームをブロック `forms-site-b.com` ます。

**Form Source サーバー** で正しい CORS ヘッダーが設定されていない場合、ブラウザーはホストページでフォームを読み込めなくなり、埋め込まれたフォームは表示されません。

### フォームを提供するサイトで CORS を設定する方法

**フォームSource** をホストするサーバーを設定して、応答に特定の HTTP ヘッダーを送信する必要があります。 正確な方法は、EDS の設定によって異なります（例えば、Franklin プロジェクトの場合、多くの場合、CDN 動作やエッジワーカーロジックを制御する GitHub リポジトリ内の `helix-config.yaml` または類似の設定ファイルで行われます）。
フォームSourceの応答に追加するキーヘッダー：

* `Access-Control-Allow-Origin: <URL_of_Host_Page>` （例：`https://your-site.com`）。 テストには `*` を使用できますが、実稼動には正確なドメインを指定します。
* `Access-Control-Allow-Methods: GET, OPTIONS` （フォーム送信自体もクロスオリジンですが、通常は送信が別の（多くの場合、同じオリジンまたは特別に設定された）エンドポイントに送信される場合、`POST` が必要になる場合があります）。
* `Access-Control-Allow-Headers: Content-Type` （およびフォーム取得で使用するその他のカスタムヘッダー）。

**例（設定ファイルの概念）:**

```yaml
        # In the configuration for the site HOSTING THE FORM (Form Source)
        headers:
          # Apply to paths where your forms are served, e.g., /forms/**
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-page-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS
```

## その他の考慮事項：CDN と複数のコードベース（Helix 4）

* **CDN ルール：** CDN がリクエストをプロキシする方法を提供する場合があります。 例えば、`host-page.com/embedded-form` へのリクエストは CDN によって内部でルーティングされ、`form-source.com/actual-form` からコンテンツを取得できるので、ブラウザーには同じオリジンのように見えます。 これは、設定が複雑になる場合があります。
* **複数のコードベース（Helix 4）:** ホストページとフォームSourceが異なる GitHub リポジトリ（Helix 4 の設定で共通）にある場合は、フォームのレンダリングや管理に必要なJavaScriptの「フォームブロック」がホストページのコードベースで利用可能であること、または、フォームSourceから取得したフォームHTMLが必要なすべてのJavaScriptで自己完結型であることを確認します。 元のドキュメントでは、「コードベースの異なる helix4 の場合、両方のコードベースにフォームブロックを追加する必要がある」と記載されています。

### 一般的なアーキテクチャ設定と設定手順

オーサリング方法と送信戦略を組み合わせ、主要な設定ポイントを使用して、フォームを設定する一般的な方法をいくつか示します。

#### スプレッドシート/メール送信付きのドキュメントベースのフォーム

これは最も簡単な設定です。 Word/Google Docsでフォームを作成し、Forms送信サービスを使用してスプレッドシートまたはメールにデータを送信します。

1. 指定したテーブル構造またはフォームブロックを使用して、Word/Google ドキュメント/シート内のフォームを定義します。
1. ドキュメント（または関連する設定）で、Forms Submission Service のターゲットスプレッドシート URL またはメールアドレスを指定します。
1. `forms@adobe.com` （または関連するサービスアカウント）に、ターゲットのスプレッドシートへの編集アクセス権があることを確認します。
1. ドキュメントをEdge Delivery サイトに公開します。

**ドキュメントベース + Forms送信サービスのアーキテクチャ**
<!--
```mermaid
    graph TD
        User[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User] >|Fills Out| EDS_Page_DocBased[EDS Page with Document-Based Form]
        EDS_Page_DocBased >|Submits Data| FSS[AEM Forms Submission Service]
        FSS > Target[<img src='https://img.icons8.com/color/48/000000/google-sheets.png' width='30' /> Data to Spreadsheet / <img src='https://img.icons8.com/color/48/000000/filled-sent.png' width='30' /> Email Notification]

        Authoring[Form defined in Google Doc/Sheet] >|EDS Syncs & Renders| EDS_Page_DocBased

        style EDS_Page_DocBased fill:#ccf,stroke:#333
        style FSS fill:#fca,stroke:#333
        style Target fill:#90ee90,stroke:#333
        style Authoring fill:#e6ffe6,stroke:#333
```-->

![ ドキュメントベース + Forms送信サービスのアーキテクチャ ](/help/forms/assets/eds-doc-fss.png)

#### スプレッドシート/メール送信付きのユニバーサルエディターフォーム

フォームを作成するにはビジュアルユニバーサルエディターを使用しますが、データ取得にはシンプルなForms送信サービスを引き続き使用します。

1. AEMのユニバーサルエディターを使用してフォームを作成します。
1. 「Forms送信サービスに送信」オプションを使用するように、UE でフォームの送信アクションを設定します。
1. ターゲットスプレッドシートの URL またはメールアドレスを指定します。
1. スプレッドシートを使用する場合は、編集アクセス権が `forms@adobe.com` ることを確認します。
1. フォームを含んだページをAEMからEdge Delivery サイトに公開します。

   **ユニバーサルエディター+ Forms送信サービスのアーキテクチャ**

   ![ ユニバーサルエディター+ Forms送信サービスのアーキテクチャ ](/help/forms/assets/eds-ue-fss.png)

   <!--```mermaid
    graph TD
    User[User] >|Fills Out| EDS_Page_UE[EDS Page with Universal Editor Form]
    EDS_Page_UE >|Submits Data| FSS[AEM Forms Submission Service]
    FSS > Target[Data sent to Google Sheet and Email Notification]
    AuthoringUE[Form built in Universal Editor - AEM] >|AEM Publishes to EDS| EDS_Page_UE
    style EDS_Page_UE fill:#ccf,stroke:#333
    style FSS fill:#fca,stroke:#333
    style Target fill:#90ee90,stroke:#333
    style AuthoringUE fill:#e6f3ff,stroke:#333
    ```
    -->

#### AEMのパブリッシュ送信機能を備えたユニバーサルエディターフォーム（詳細）

この設定では、フォームの作成にはユニバーサルエディターを、強力なバックエンド処理（ワークフロー、FDM など）にはAEM パブリッシュインスタンスを使用します。 これには、より多くの設定が必要です。

1. **UE でフォームを作成：** ユニバーサルエディターでフォームを作成します。 AEM Formsのアクション（「AEM ワークフローの呼び出し」、「フォームデータモデルを使用した送信」など）を指すように、送信アクションを設定します。
1. **AEM Dispatcher設定（AEM パブリッシュ層）:**
   * **リダイレクトなし：** Dispatcherのルールで、*のパスに対して行われたリダイレクトリクエストが* 行 `/adobe/forms/af/submit/...` れないようにします。
   * **送信を許可：** Dispatcher フィルター（`filters.any` など）を変更して、Edge Delivery サイトのドメインまたは IP アドレスから `allow` に対する POST リクエストを明示的に `/adobe/forms/af/submit/...` 認します。
1. **AEMの OSGi リファラーフィルター（AEM パブリッシュ層）:**
   * AEM OSGi コンソール（`/system/console/configMgr`）で、「Apache Sling Referrer Filter」を探して設定します。
   * Edge Delivery サイトのドメイン（`https://your-eds-domain.hlx.page`、`https://your-custom-eds-domain.com` など）を「Allow Hosts」または「Allow Hosts RegExp」リストに追加します。 これにより、AEMは EDS サイトからの送信を受け入れるようになります。
1. **CDN リダイレクトルール （Edge Delivery CDN 上）:**
   * Edge Delivery サイト（`your-eds-domain.hlx.page` など）は、AEM パブリッシュインスタンスに送信リクエストを正しくルーティングする必要があります。
   * EDS ページ上のフォームが送信する際、`/adobe/forms/af/submit/...` のような相対パスをターゲットにする可能性があります。 Edge Delivery CDN （またはエッジワーカー）で、「リクエストが `your-eds-domain.hlx.page/adobe/forms/af/submit/...` に届いたら、`your-aem-publish-instance.com/adobe/forms/af/submit/...` に転送（プロキシまたはリダイレクト）する」というルールが必要です。
   * 正確な実装は CDN プロバイダー（Fastly VCL、Akamai Property Manager、Cloudflare Workers など）によって異なります。
1. **（オプション）開発用の `constants.js` （EDS プロジェクトのコードベース内）:**
   * ローカル開発のために、またはクライアントサイドのフォームスクリプトがAEMの完全な公開 URL を知る必要がある場合は、Edge Delivery プロジェクトの GitHub リポジトリ内の `constants.js` または同様の設定ファイルで、これを設定できます。 例：

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **公開：** フォームページをAEMから EDS に公開し、AEM パブリッシュインスタンスですべてのAEM設定がアクティブであることを確認します。

   **ユニバーサルエディター+ AEM パブリッシュアーキテクチャ**

![ ユニバーサルエディター+ AEM パブリッシュアーキテクチャ ](/help/forms/assets/eds-aem-publish.png)

これは、ユーザーが EDS サイトに送信し、CDN がAEM Dispatcherにルーティングされ、次にAEM パブリッシュが処理するというフローを示しています。

#### ドキュメントオーサリング（DA）ページへのフォームの埋め込み

メインの web サイトコンテンツは、ドキュメントオーサリング（DA）で作成されます。 ドキュメントベースのオーサリングまたはユニバーサルエディターのいずれかを個別に使用してフォームを作成し、DA ページに埋め込みます。

1. **フォームを作成して公開：**
   * ドキュメントベースのオーサリングまたはユニバーサルエディターを使用してフォームを作成します。
   * 送信方法を設定します（設定 1、2、3 に従って、Forms送信サービスまたはAEM パブリッシュに対して）。
   * このフォームを公開して、独自のEdge Delivery URL に存在するようにします（例：`.../forms/my-special-form`）。
1. **CORS を設定：** このスタンドアロンフォームをホストするEdge Delivery サイト/プロジェクトで、ドキュメントオーサリングサイトのドメインが取得できるように CORS ヘッダーが設定されていることを確認します。
1. **DA でのページの作成：** ドキュメントオーサリングでページを作成または編集します。
1. **フォームブロックの埋め込み：** 外部 URL を埋め込むには、DA で適切なブロックを使用します。 このブロックは、スタンドアロンで公開されたフォームの URL を指定します。
1. **DA ページを公開：** DA ページを公開します。 これで、フォームが取得され、表示されます。

   **DA アーキテクチャに埋め込まれたForms**

   ![DA アーキテクチャに埋め込まれたForms](/help/forms/assets/eds-forms-embedd-da.png)

   これは、別の EDS の場所からフォームを取り込む DA ページを示しています。 埋め込まれたフォームは、独自の送信を処理します。

## トラブルシューティング

* **フォームの送信が機能しない。**
   * **コンソールエラーの確認：** ブラウザーの開発者コンソール（通常は F12）を開き、送信時に「ネットワーク」タブまたは「コンソール」タブでエラーを探します。
   * **送信 URL の確認：** フォームは正しいエンドポイント（Forms送信サービスの URL またはAEM公開パス）に送信しようとしていますか？
   * **Forms送信サービス：** スプレッドシートに送信する場合、編集アクセス権 `forms@adobe.com` 付与されていますか？ スプレッドシートの URL は正しいですか？
   * **AEM送信内容の公開：**
      * Dispatcherは POST を `/adobe/forms/af/submit/...` 認していますか？
      * AEM Publish の Sling リファラーフィルターは、EDS ドメインを許可するように設定されていますか。
      * `/adobe/forms/af/submit/...` の CDN リダイレクトルールは正しく機能していますか？

* **埋め込みフォームが表示されません。**

   * **CORS!** これが最も一般的な理由です。 ブラウザーコンソールで CORS エラーを確認します。 サイト *ホスティング* のフォームに正しい `Access-Control-Allow-Origin` ヘッダーが含まれていることを確認します。
   * **フォーム URL が正しいですか？** ホストページの埋め込みコードは、フォームの正しいライブ URL を指していますか？
   * **JavaScript ブロック：** フォームがレンダリングに特定のJavaScriptの「フォームブロック」に依存している場合、そのブロックのコードはホストページで使用できますか？

* **AEM パブリッシュに送信すると、「403 Forbidden」または「401 Unauthorized」が表示される。**

   * これは多くの場合、AEM Publish 上の Sling リファラーフィルターが EDS ドメインからのリクエストを許可しないことを指しています。 設定を再度確認します。
   * また、標準のフォーム送信は通常は匿名ですが、AEM送信エンドポイントで必要な場合は、認証/承認の問題になる可能性があります。

## 次の手順

このガイドでは、AEM Edge Delivery Servicesでのフォームの使用の概要について説明しました。 具体的な設定の詳細な手順については、次のAdobe Experience Managerの公式ドキュメントを参照してください。

* [Edge Delivery Services Formsによるドキュメントベースのオーサリング](/help/edge/docs/forms/tutorial.md)
* [Edge Delivery Services Formsを使用したユニバーサルエディター](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [ ドキュメントオーサリング（DA）とコンテンツの埋め込み ](https://www.aem.live/developer/da-tutorial)
* [AEM Forms送信サービス](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)