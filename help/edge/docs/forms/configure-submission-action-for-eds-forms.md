---
title: Edge Delivery Services を使用したAEM Forms の送信アクションの設定
description: Edge Delivery Servicesを使用して AEM Forms で送信アクションを設定する方法について学習します。 Forms Submission Service とAEM Publish Submit Action のいずれかを選択して、フォームデータを安全かつ効率的に処理します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 75d8ea4f0913e690e3374d62c6e7dcc44ea74205
workflow-type: ht
source-wordcount: '2166'
ht-degree: 100%

---

# フォーム送信の設定：データはどこに送信されますか？

ユーザーがフォーム上で&#x200B;**送信** をクリックした後、そのデータに対して何を行うかをEdge Delivery Servicesに指示する必要があります。 主な 2 つのオプションは次のとおりです。

## 方法 1：AEM Forms Submission Service を使用（簡略）

このサービスは、スプレッドシートやメールへのデータの送信など、一般的なわかりやすいアクションに最適です。

**概要と機能**

[Forms Submission Service](/help/forms/forms-submission-service.md) は、Adobeがホストするエンドポイントです。 フォームからデータが送信されると、このサービスが引き継がれ、事前設定済みのアクションを実行します。 設定が簡単になるよう設計されています。 以下を設定できます。スプレッドシートまたはメールへの送信

* **スプレッドシートへの送信：** 送信されたフォームデータを新しい行として Google スプレッドシートまたは Microsoft Excel ファイル (OneDrive または SharePoint に保存) に自動的に追加します。
* **メールの送信：** フォームデータを含むメールを、指定した 1 つ以上のメールアドレスに送信します。

#### 重要：設定要件

* **Spreadsheet Access:** Google スプレッドシートまたは OneDrive/SharePoint 上の Excel ファイルにデータを送信するには、通常は Adobe サービスアカウント (多くの場合に `forms@adobe.com`) に、その特定のスプレッドシートの **編集権限** が必要です。
* **アーリーアクセスプログラム：** このサービスの一部の機能 (特にスプレッドシートの機能) は、アーリーアクセスプログラムの一部である可能性があります。 メールで送信するか `aem-forms-ea@adobe.com` 、特定のAdobe フォームにプロジェクトの詳細を入力して、アクセスをリクエストする必要がある場合があります。 最新のAdobe ドキュメントを常に確認してください。

**Forms Submission Service のフローチャート**
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
![Forms Submission](/help/forms/assets/eds-fss.png)

このフローチャートは、Forms Submission Service が送信されたデータを取得して、設定済みのスプレッドシートまたはメールに送信する方法を示しています。

## 方法 2：AEM Publish インスタンスへの送信 (高度)

より複雑なニーズについては、[ フォーム (特にユニバーサルエディターで作成されたフォーム) から AEM as a Cloud Service の Publish インスタンスに直接データを送信できます ](/help/forms/configure-submit-actions-core-components.md)。 これにより、AEM の完全なバックエンド機能を活用できます。

**AEM Publish に送信する必要があるのはいつですか？**

* 送信後にカスタム AEM ワークフローをトリガーするには：
* AEM フォームデータモデル (FDM) を使用してデータベースまたは他のエンタープライズシステムと統合する場合。
* Marketo、Microsoft Power Automate、Adobe Workfront Fusion などのサードパーティサービスに接続する場合。
* Azure Blob Storage や SharePoint リスト/ドキュメントライブラリ (単純なスプレッドシートだけでない) などの特定の場所にデータを保存する場合。
* AEM 内に複雑なサーバーサイド検証やデータ処理のロジックがある場合。

**使用可能な送信アクション (AEM Publish Submissions)**

* [REST エンドポイントに送信](/help/forms/configure-submit-action-restpoint.md)
* [メールの送信 (AEMのメールサービスを使用)](/help/forms/configure-submit-action-send-email.md)
* [フォームデータモデル（FDM）を使用して送信](/help/forms/configure-data-sources.md)
* [AEM ワークフローを起動](/help/forms/aem-forms-workflow-step-reference.md)
* [SharePoint への送信 (リスト項目またはドキュメントとして)](/help/forms/configure-submit-action-sharepoint.md)
* [OneDrive への送信 (ドキュメントとして)](/help/forms/configure-submit-action-onedrive.md)
* [Azure Blob Storage への送信](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Microsoft Power Automate への送信](/help/forms/forms-microsoft-power-automate-integration.md)
* [Adobe Workfront Fusion への送信](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Adobe Marketo Engage への送信](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> AEM Publish からGoogle スプレッドシート/Excel をターゲットにする場合でも、直接の Forms Submission Service とは異なる設定手順が必要になります。

**AEM Publish Submission のフローチャート**

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

![AEM Publish Submission のフローチャート ](/help/forms/assets/eds-aem-publish.png)
このフローチャートは、AEM Publishに送信するフォームを示しています。このフォームは、複雑なバックエンドタスクを処理します。

### Forms Submission Service と AEM Publish Submissions の比較

| 機能 | Forms 送信サービス | AEM パブリッシュ送信 |
| :- | :- | :-- |
| **次に最適** | スプレッドシートやメール通知へのシンプルなデータキャプチャ | 複雑なワークフロー、エンタープライズ統合、カスタムロジック |
| **フォームオーサリング** | ドキュメントベースに適しています。シンプルな UI フォームの場合は問題ありません | ユニバーサルエディターで作成したフォームに最適です |
| **設定の手間** | 低（多くの場合、シンプルな設定） | より高（AEM パブリッシュ、Dispatcher、OSGi、CDN の設定が必要） |
| **バックエンドシステム** | アドビがホストするサービス | AEM as a Cloud Service パブリッシュインスタンス |
| **柔軟性** | シート／メールに制限 | 非常に柔軟で、幅広い AEM Forms アクション |
| **例** | Google Sheet に対するお問い合わせフォームのデータ | ローン申請での AEM 承認ワークフローのトリガー |

## 様々なサイトやページにフォームを埋め込む方法

場合によっては、1 つの場所（例：中央の「フォームサイト」）で作成および管理されているフォームを別の web ページやサイトに表示することがあります。

### フォームを埋め込む理由

* ドキュメントベースのオーサリングで作成した複数のランディングページに表示する必要がある、ユニバーサルエディターで作成した標準の「お問い合わせ」フォームがある。
* メインの web サイトコンテンツがドキュメントオーサリング（DA）で作成され、専用のフォームを含める必要がある。
* 適切に管理された単一のフォームを、複数の異なる EDS プロジェクトをまたいで再利用したいと考えている。

### フォーム埋め込みの技術的な仕組み

フォームを表示するページ（「ホストページ」と呼ぶ）には、何らかのコード（通常は特別なブロックまたはスクリプト）が含まれます。 ユーザーがホストページにアクセスすると、このコードは、実際のフォームがホストされているURL（ここでは「フォームソース」と呼ぶ）にリクエストを行います。 次に、フォームソースは HTML を返し、ホストページが挿入して表示します。

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
![埋め込みフォームアーキテクチャ](/help/forms/assets/eds-embedded-form.png)
この図は、フォームソースからフォーム HTML を取得して表示するホストページを示しています。 送信には、元のフォームの設定済みエンドポイントが使用されます。

## 埋め込みフォームの CORS の設定

[CORS（クロスオリジンリソース共有）](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)は、ブラウザーのセキュリティ機能です。 ホストページ（例：`site-a.com`）が別のドメイン（例：`forms-site-b.com`）からフォームを取得しようとすると、`forms-site-b.com` が CORS ヘッダー経由で明示的に許可しない限り、ブラウザーはブロックします。

**フォームソースサーバー**&#x200B;に正しい CORS ヘッダーが設定されていない場合、ブラウザーではホストページでフォームを読み込めなくなり、埋め込みフォームは表示されません。

### フォームを提供するサイトでの CORS の設定方法

**フォームソース**&#x200B;をホストするサーバーを設定して、応答に特定の HTTP ヘッダーを送信する必要があります。 正確な方法は、EDS の設定により異なります（例えば、Franklin プロジェクトでは、多くの場合、CDN の動作やエッジワーカーのロジックを制御する GitHub リポジトリ内の `helix-config.yaml` または類似の設定ファイルで行われます）。
フォームソースの応答に追加する主なヘッダー：

* `Access-Control-Allow-Origin: <URL_of_Host_Page>`（例：`https://your-site.com`）。 テスト環境では `*` を使用できますが、実稼動環境では正確なドメインを指定します。
* `Access-Control-Allow-Methods: GET, OPTIONS`（フォームの送信自体もクロスオリジンの場合は `POST` が必要になることがありますが、通常、送信は別の、多くの場合、同じオリジンまたは特別に設定されたエンドポイントに送信されます）。
* `Access-Control-Allow-Headers: Content-Type`（およびフォーム取得で使用される可能性がある他のカスタムヘッダー）。

**例（設定ファイルの概念）：**

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

* **CDN ルール：** CDN によっては、リクエストをプロキシする方法が提供されている可能性があります。 例えば、`host-page.com/embedded-form` へのリクエストは、CDN によって内部でルーティングされ、`form-source.com/actual-form` からコンテンツが取得される可能性があるので、ブラウザーには同じオリジンとして表示されます。 これにより、設定は複雑になる場合があります。
* **複数のコードベース (Helix 4)：** ホストページとフォームソースが異なる GitHub リポジトリ (Helix 4 の設定で共通) にある場合は、フォームのレンダリングや管理に必要な JavaScript の「フォームブロック」がホストページのコードベースで利用可能であること、またはフォームソースから取得したフォーム HTML が必要なすべての JavaScript で自己完結型であることを確認します。 元のドキュメントには、「コードベースの異なる helix4 の場合、両方のコードベースにフォームブロックを追加する必要がある」旨が記載されています。

### 一般的なアーキテクチャ設定と設定手順

オーサリング方法と送信戦略を組み合わせて主要な設定ポイントと併用し、フォームを設定する一般的な方法をいくつか示します。

#### スプレッドシート/メール送信付きのドキュメントベースのフォーム

これは最も簡単な設定です。 Word/Google ドキュメントでフォームを作成し、Forms Submission Service を使用してスプレッドシートまたはメールにデータを送信します。

1. 指定したテーブル構造またはフォームブロックを使用して、Word/Google ドキュメント/スプレッドシート内のフォームを定義します。
1. ドキュメント (または関連する設定) で、Forms Submission Service のターゲットとなるスプレッドシート URL またはメールアドレスを指定します。
1. `forms@adobe.com` (または関連するサービスアカウント)に、ターゲットのスプレッドシートへの編集アクセス権があることを確認します。
1. ドキュメントを Edge Delivery サイトに公開します。

**ドキュメントベース + Forms Submissions Service のアーキテクチャ**
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

![ ドキュメントベース + Forms Submissions Service のアーキテクチャ ](/help/forms/assets/eds-doc-fss.png)

#### スプレッドシート/メール送信のユニバーサルエディターフォーム

フォームの作成にはビジュアルユニバーサルエディターを使用しますが、データ取得にはシンプルな Forms Submissions Service を引き続き使用します。

1. AEM のユニバーサルエディターを使用してフォームを作成します。
1. 「Forms Submissions Service に送信」オプションを使用するように、UE でフォームの送信アクションを設定します。
1. ターゲットとにするスプレッドシートの URL またはメールアドレスを指定します。
1. スプレッドシートを使用する場合は、`forms@adobe.com` に編集アクセス権があることを確認します。
1. フォームを含んだページを AEM からEdge Delivery サイトに公開します。

   **ユニバーサルエディター + Forms Submissions Service のアーキテクチャ**

   ![ ユニバーサルエディター + Forms Submissions Service のアーキテクチャ ](/help/forms/assets/eds-ue-fss.png)

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

#### AEM Publish Submissionsを備えたユニバーサルエディターフォーム (高度)

この設定では、フォームの作成にはユニバーサルエディターを、強力なバックエンド処理 (ワークフロー、FDM など) には AEM Publish インスタンスを使用します。 これには、より多くの設定が必要です。

1. **UE でフォームを作成：** ユニバーサルエディターでフォームを作成します。 AEM Forms のアクション (「AEM ワークフローの呼び出し」、「フォームデータモデルを使用した送信」など) を指すように、送信アクションを設定します。
1. **AEM Dispatcher 設定 (AEM Publish層)：**
   * **リダイレクトなし：** Dispatcher のルールによって、`/adobe/forms/af/submit/...` パスに対して行われたリクエストがリダイレクト&#x200B;*されない* ようにします。
   * **送信を許可：** Dispatcher フィルター (`filters.any` 上など) を変更して、Edge Delivery サイトのドメインまたは IP アドレスから `/adobe/forms/af/submit/...` に対して明示的に `allow` POST リクエストします。
1. **AEMの OSGi リファラーフィルター (AEM Publish 層)：**
   * AEM OSGi コンソール (`/system/console/configMgr`) で、「Apache Sling Referrer Filter」を見つけて設定します。
   * Edge Delivery サイトのドメイン (`https://your-eds-domain.hlx.page`、`https://your-custom-eds-domain.com` など) を「Allow Hosts」または「Allow Hosts RegExp」リストに追加します。 これにより、AEM は EDS サイトからの送信を受け入れるようになります。
1. **CDN リダイレクトルール (Edge Delivery CDN 上)：**
   * Edge Delivery サイト (`your-eds-domain.hlx.page` など) は、AEM Publish インスタンスに送信リクエストを正しくルーティングする必要があります。
   * EDS ページ上のフォームが送信する際、`/adobe/forms/af/submit/...` のような相対パスをターゲットにする可能性があります。 Edge Delivery CDN (またはエッジワーカー) で、「リクエストが `your-eds-domain.hlx.page/adobe/forms/af/submit/...` に届いたら、`your-aem-publish-instance.com/adobe/forms/af/submit/...` に転送 (プロキシまたはリダイレクト) する」というルールが必要です。
   * 正確な実装は CDN プロバイダー (Fastly VCL、Akamai Property Manager、Cloudflare Workers など) によって異なります。
1. **(オプション) 開発用の `constants.js` (EDS プロジェクトのコードベース内)：**
   * ローカル開発のために、またはクライアントサイドのフォームスクリプトが完全な AEM Publish URL を知る必要がある場合は、Edge Delivery プロジェクトの GitHub リポジトリ内の `constants.js` または同様の設定ファイルでこれを設定できます。 例：

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **公開：** フォームページを AEM から EDS に公開し、AEM Publish インスタンスですべての AEM 設定がアクティブであることを確認します。

   **ユニバーサルエディター + AEM Publish アーキテクチャ**

![ ユニバーサルエディター + AEM Publish アーキテクチャ ](/help/forms/assets/eds-aem-publish.png)

これは、ユーザーが EDS サイトに送信し、CDN が AEM Dispatcher にルーティングし、次に AEM Publish が処理するというフローを示しています。

#### ドキュメントオーサリング (DA) ページへのフォームの埋め込み

メインの web サイトコンテンツは、ドキュメントオーサリング (DA) で作成されます。 ドキュメントベースのオーサリングまたはユニバーサルエディターのいずれかを個別に使用してフォームを作成し、DA ページに埋め込みます。

1. **フォームを作成して公開：**
   * ドキュメントベースのオーサリングまたはユニバーサルエディターを使用してフォームを作成します。
   * （設定 1、2、3 に従って、Forms Submission Service または AEM Publish に対して）送信方法を設定します。
   * このフォームを公開して、独自の Edge Delivery URL 上でライブにします（例：`.../forms/my-special-form`）。
1. **CORS を設定：**&#x200B;このスタンドアロンフォームをホストする Edge Delivery サイト／プロジェクトで、ドキュメントオーサリングサイトのドメインが取得できるように CORS ヘッダーが設定されていることを確認します。
1. **DA でのページのオーサリング：** ドキュメントオーサリングでページを作成または編集します。
1. **フォームブロックの埋め込み：** 外部 URL を埋め込むには、DA で適切なブロックを使用します。 このブロックを、スタンドアロンで公開されたフォームの URL に指定します。
1. **DA ページを公開：** DA ページを公開します。 これで、フォームが取得され、表示されます。

   **DA アーキテクチャに埋め込まれたForms**

   ![DA アーキテクチャに埋め込まれたForms](/help/forms/assets/eds-forms-embedd-da.png)

   これは、別の EDS の場所からフォームを取り込む DA ページを示しています。 埋め込まれたフォームは、自身で送信処理を行います。

## トラブルシューティング

* **フォームの送信がうまくいきません。**
   * **コンソールエラーの確認：** ブラウザーの Developer Console（通常は F12）を開き、送信時に「ネットワーク」タブまたは「コンソール」タブでエラーを探します。
   * **送信 URL の確認：** フォームは正しいエンドポイント（Forms Submission Service の URL または AEM Publish パス）に送信しようとしていますか？
   * **Forms Submission Service：** スプレッドシートに送信する場合、`forms@adobe.com` に編集アクセス権が付与されていますか？ スプレッドシートの URL は正しいですか？
   * **AEM Publish Submissions：**
      * Dispatcher は`/adobe/forms/af/submit/...` への POST を許可していますか？
      * AEM Publish の Sling Referrer Filter は、EDS ドメインを許可するように設定されていますか？
      * `/adobe/forms/af/submit/...` に対する CDN リダイレクトルールは正しく機能していますか？

* **埋め込みフォームが表示されません。**

   * **CORS!**&#x200B;これが最も一般的な原因です。 ブラウザーコンソールで CORS エラーを確認します。 フォームを&#x200B;*ホスト*&#x200B;しているサイトに、正しい `Access-Control-Allow-Origin` ヘッダーが含まれていることを確認します。
   * **フォームの URL は正しいですか？**&#x200B;ホストページの埋め込みコードは、フォームの正しいライブ URL を指していますか？
   * **JavaScript ブロック：**&#x200B;フォームがレンダリングに特定のJavaScriptの「フォームブロック」に依存している場合、そのブロックのコードはホストページで使用できますか？

* **AEM Publish に送信すると、「403 Forbidden」または「401 Unauthorized」が表示されます。**

   * これは多くの場合、AEM Publish 上の Sling Referrer Filter が EDS ドメインからのリクエストを許可していないことを指しています。 設定を再度確認します。
   * AEM の送信エンドポイントで認証や認可が必要な場合、それが原因の可能性もありますが、通常のフォーム送信は匿名で行われます。

## 次の手順

このガイドでは、AEM Edge Delivery Services でのフォームの使用の概要について説明しました。 具体的な設定の詳細な手順については、次の Adobe Experience Manager の公式ドキュメントを参照してください。

* [Edge Delivery Services Forms でのドキュメントベースのオーサリング](/help/edge/docs/forms/tutorial.md)
* [Edge Delivery Services Forms でのユニバーサルエディター](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [ドキュメントオーサリング（DA）とコンテンツの埋め込み ](https://www.aem.live/developer/da-tutorial)
* [AEM Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
