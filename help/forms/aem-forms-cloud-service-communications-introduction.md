---
title: Forms as a Cloud Service 通信 API とは
description: 通信 API を使用して、ドキュメントの署名、認証、保護、PDF 生成プロセスの自動化、PDFドキュメントの別の形式への変換を行います。
Keywords: How to generate document?, Generate PDF document, Manipulation PDF documents, Assembling PDF documents, Validating PDF document, APIs used in encrypting or decrypting PDFs
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 100%

---

# AEM Forms as a Cloud Service 通信の概要 {#frequently-asked-questions}


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html) |
| AEM as a Cloud Service | この記事 |

通信機能は、ビジネス文書、ステートメント、請求処理レター、特典通知、毎月の請求書、ウェルカムキットなど、ブランド承認済みのパーソナライズされた標準的なドキュメントを作成するのに役立ちます。

この機能には、ドキュメントを生成および操作するための API が用意されています。オンデマンドでドキュメントを生成または操作することも、バッチジョブを作成して、定義された間隔で複数のドキュメントを生成することもできます。通信 API は以下を提供します。

* 効率化されたオンデマンドおよびバッチドキュメント生成機能。

* PDF ドキュメントをオンデマンドで結合、並べ替えおよび検証する機能。

* 外部システムとの統合を容易にする HTTP API。オンデマンド操作（低遅延）用とバッチ操作（高スループット操作）用に別々の API が含まれています。

* データへのセキュリティで保護されたアクセス。通信 API は、顧客が指定したデータリポジトリにのみ接続してデータにアクセスするので、通信の安全性が高くなります。

![クレジットカード明細書のサンプル](assets/statement.png)
クレジットカード明細書は、通信 API を使用して作成できます。このサンプル文は同じテンプレートですが、クレジットカードの使用状況に応じて、顧客ごとに別々のデータを使用しています。

## ドキュメントの生成

コミュニケーションドキュメント生成 API は、テンプレート（XFA または PDF）と顧客データ（XML）を組み合わせて、PDF 形式や PS、PCL、DPL、IPL、ZPL 形式などの印刷形式でドキュメントを生成するのに役立ちます。これらの API は、[XML データ](communications-known-issues-limitations.md#form-data)を含んだ PDF および XFA テンプレートを利用して、単一のドキュメントをオンデマンドで生成したり、複数のドキュメントをバッチジョブで生成したりすることができます。

通常、[Designer](use-forms-designer.md) を使用してテンプレートを作成し、通信 API を使用してテンプレートにデータを結合します。アプリケーションは、出力ドキュメントをネットワークプリンター、ローカルプリンター、またはアーカイブ用のストレージシステムに送信できます。標準ワークフローとカスタムワークフローの例を次に示します。

![通信機能のドキュメント生成ワークフロー](assets/communicaions-workflow.png)

ユースケースによっては、これらのドキュメントを Web サイトまたはストレージサーバーからダウンロードできるようにすることもできます。

ドキュメント生成 API の例を以下に示します。

### PDF ドキュメントの作成 {#create-pdf-documents}

ドキュメント生成 API を使用すると、フォームデザインと XML フォームデータに基づく PDF ドキュメントを作成できます。結果として出力されるのは非インタラクティブ PDF ドキュメントです。つまり、ユーザーはフォームデータの入力や変更はできません。基本ワークフローは、XML フォームデータをフォームデザインと結合して PDF ドキュメントを作成することです。次の図は、フォームデザインと XML フォームデータを結合して PDF ドキュメントを生成するところを示しています。

![PDF ドキュメントの作成](assets/outPutPDF_popup.png)
図：PDF ドキュメントを作成するための一般的なワークフロー

### PostScript（PS）、Printer Command Language（PCL）、Zebra Printing Language（ZPL）ドキュメントの作成 {#create-PS-PCL-ZPL-documents}

ドキュメント生成 API を使用して、XDP フォームデザインまたは PDF ドキュメントに基づく PS、PCL および ZPL ドキュメントを作成できます。これらの API は、フォームデザインとフォームデータを結合してドキュメントを生成します。ドキュメントをファイルに保存し、カスタムプロセスを開発してファイルをプリンターに送信することができます。

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### バッチデータの処理による複数のドキュメントの作成 {#processing-batch-data-to-create-multiple-documents}

ドキュメント生成 API を使用して、XML バッチデータソース内のレコードごとに別個のドキュメントを作成できます。ドキュメントは一括モードと非同期モードで生成できます。コンバージョンの様々なパラメーターを設定し、バッチ処理を開始できます。

![PDF ドキュメントの作成](assets/ou_OutputBatchMany_popup.png)

<!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. 

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use document generation APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form. -->

## ドキュメントの操作

通信機能のドキュメント操作 API は、PDF ドキュメントの結合、並べ替えおよび検証に役立ちます。通常は、DDX を作成し、それをドキュメント操作 API に送信して、ドキュメントをアセンブリしたり、並べ替えたりします。[DDX ドキュメント](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf)には、ソースドキュメントを使用して 1 組の必要なドキュメントを生成する方法についての指示が記述されています。DDX リファレンスドキュメントは、サポートされているすべての操作に関する詳細な情報を提供します。ドキュメント操作の例を以下に示します。

### PDF ドキュメントのアセンブリ

ドキュメント操作 API を使用すると、複数の PDF または XDP ドキュメントを 1 つの PDF ドキュメントまたは PDF ポートフォリオに組み合わせることができます。次に、PDF ドキュメントのアセンブリ方法を示します。

* 単純な PDF ドキュメントのアセンブリ
* PDF ポートフォリオの作成
* 暗号化ドキュメントのアセンブリ
* ベイツナンバリングを使用したドキュメントのアセンブリ
* ドキュメントの統合およびアセンブリ

![複数の PDF ドキュメントからの単一 PDF ドキュメントのアセンブリ](assets/as_document_assembly.png)
図：複数の PDF ドキュメントからの単一 PDF ドキュメントのアセンブリ

### PDF ドキュメントのディスアセンブリ

ドキュメント操作 API を使用して PDF ドキュメントを分割できます。また、ソースドキュメントからページを抽出したり、しおりの位置を境にソースドキュメントを分割することもできます。通常、このタスクは PDF ドキュメントが最初に多数の個別ドキュメント（明細書など）から作成された場合に役立ちます。

* ソースドキュメントからのページの抽出
* しおりに基づいたソースドキュメントの分割

![しおりに基づいたソースドキュメントの複数のドキュメントへの分割](assets/as_intro_pdfsfrombookmarks.png)
図：しおりに基づいたソースドキュメントの複数のドキュメントへの分割

### PDF/A 準拠ドキュメントへの変換と PDF/A 準拠ドキュメントの検証

ドキュメント操作 API を使用して、PDF ドキュメントを PDF/A 準拠のドキュメントに変換したり、PDF ドキュメントが PDF/A に準拠しているかどうかを判断したりできます。PDF/A は、ドキュメントのコンテンツを長期保存するためのアーカイブ形式です。フォントはドキュメントに埋め込まれ、ファイルは非圧縮になります。その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。なお、PDF/A ドキュメントには、オーディオおよびビデオのコンテンツは含まれません。

<!-- 

## Document utilities

Document utilities synchronous APIs helps you convert documents between PDF and XDP file formats, and query information about a PDF document. For example, you can determine whether a PDF document contains comments or attachments. 

### Retrieve PDF document properties

You can [query a PDF document](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Extraction/) for the following information:

* Is a PDF Document: Check whether the source document is a PDF document.
* Is a fillable form: Check whether the source PDF document is a fillable form.
* Form Type: Retrieve the form type of the document.
* Check for Attachments: Check whether the source PDF document has any attachments.
* Check for Comments: Check whether the source PDF document has any review comments.
* Is a PDF Package: Check whether the document is a PDF package.
* Get the PDF Version: Retrieve the [version of the PDF document](https://en.wikipedia.org/wiki/History_of_PDF).
* Recommended Acrobat Version: Retrieve the required version of Acrobat (Reader) to open the PDF document.
* Is an XFA Document: Check whether the source PDF document is an XFA-based PDF document.
* Is Shell PDF: Check whether the source PDF document is shell PDF. A shell PDF contains only an XFA stream, font and image resources, and one page that is either blank or contains a warning that the document must be opened using Acrobat or Adobe Reader. The shell PDF is used with PDF transformation to optimize delivery of PDFForm transformations only.
* Get the XFA Version: Retrieve the [XFA Version for an XFA-based PDF document](https://en.wikipedia.org/wiki/XFA#XFA_versions).

### Convert PDF Documents into XDP Documents

The [PDF to XDP API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Conversion) converts a PDF document to an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the dictionary. -->

## ドキュメント保証 {#doc-assurance}

DocAssurance サービスには、以下の Signature API と Encyption API が含まれています。

### Signature API

Signature API を使用すると、組織は配布および受信する Adobe PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。セキュリティ機能がドキュメント自体に適用されるので、ドキュメントは安全で、ライフサイクル全体にわたって制御されます。オフラインでダウンロードされる場合や組織に送り返される場合にファイアウォールを超えても、ドキュメントを安全な状態に維持します。Signature API を使用して、次のタスクを実行できます。

* PDF ドキュメントに署名フィールドを追加します。
* PDF ドキュメント内の指定した署名フィールドに署名します。
* PDF ドキュメントの証明

### 暗号化 API

暗号化 API を使用すると、ドキュメントの暗号化および復号が可能になります。ドキュメントが暗号化されると、その内容が読み取れなくなります。承認済みユーザーは、ドキュメントを復号して内容を確認できます。PDF ドキュメントがパスワードで暗号化されている場合、ユーザーは開くパスワードを指定してから、Adobe Reader または Adobe Acrobat でドキュメントを表示する必要があります。同様に、PDF ドキュメントが証明書で暗号化されている場合は、、PDF ドキュメントの暗号化に使用された証明書 (秘密鍵) に対応する公開鍵で PDF ドキュメントを復号する必要があります。

暗号化 API を使用して、次のタスクを実行できます。

* パスワードで PDF ドキュメントを暗号化します。
* PDF ドキュメントからパスワードベースの暗号化を削除します。
* PDF ドキュメントに適用されるセキュリティのタイプを取得します。

Signature API と Encryption API は両方とも [同期 API](#types-of-communications-apis-types) です。


## 通信 API のタイプ {#types}

通信は、オンデマンドおよびバッチでのドキュメント生成用に HTTP API を提供します。

* **[同期 API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** は、オンデマンド、低遅延、単一レコードのドキュメント生成シナリオに適しています。これらの API は、ユーザーアクションに基づいたユースケースにより適しています。例えば、ユーザーがフォームへの入力を完了した後にドキュメントを生成するような場合です。

* **[バッチ API（非同期 API）](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)**&#x200B;は、スケジュール化された、高スループットの、複数のドキュメント生成シナリオに適しています。これらの API は、バッチでドキュメントを生成します。例えば、毎月生成される電話料金、クレジットカード明細、給付計算書などです。

## オンボーディング

通信機能は、Forms as a Cloud Service ユーザー向けのスタンドアロンおよびアドオンモジュールとして利用できます。アクセス権限を要求する場合は、アドビのセールスチームまたはアドビ担当者に問い合わせてください。お客様の組織で変換サービスを使用できるように設定し、組織の管理者に対して必要な権限を設定します。管理者は、API を使用するためのアクセス権限を、組織内の Forms as a Cloud Service 開発者（ユーザー）に付与することができます。

オンボーディング後、Forms as a Cloud Service 環境で通信機能を有効にするには：

1. Cloud Manager にログインし、AEM Forms as a Cloud Service インスタンスを開きます。

1. 「プログラムを編集」オプションを開き、「ソリューションとアドオン」タブに移動して、「**[!UICONTROL Forms - 通信]**」オプションを選択します。

   ![通信](assets/communications.png)

   「**[!UICONTROL Forms - デジタル登録]**」オプションを既に有効にしてある場合は、「**[!UICONTROL Forms - 通信アドオン]**」オプションを選択します。

   ![アドオン](assets/add-on.png)

1. 「**[!UICONTROL 更新]**」をクリックします。

1. ビルドパイプラインを実行します。ビルドパイプラインが正常に完了すると、お使いの環境で通信 API が有効になります。

>[!NOTE]
>
> ドキュメント操作 API を有効にし設定するには、次のルールを [Dispatcher 設定](setup-local-development-environment.md#forms-specific-rules-to-dispatcher)に追加します。
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service lets you generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

The [API reference documentation](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) provides detailed information about all the parameters, authentication methods, and various services provided by APIs. The API reference documentation is also available in the .yaml format. You can download the .yaml for [Batch APIs](assets/batch-api.yaml) or [non-Batch API.yaml](assets/non-batch-api.yaml) file and upload it to postman to check functionality of APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

Uploading Communication APIs .yaml file to postman to check functionality of APIs.

## Using the Communications APIs {#workflows}

Typically, you create a template using [Designer](use-forms-designer.md) and use communications APIs ( generatePDFOutput and generatePrintedOutput) to:

* Convert these templates to various formats, including PDF, PostScript, ZPL, and PCL.
* Merge XML form data with a form design to generate a document.
* Generate a document without merging XML form data into the document. However, the primary workflow is merging data into the document.

Then, the output document is stored to a file. You can design custom workflows to send the file to a network printer, a local printer, or to a storage system for archival. A typical out of the box and custom workflows look like the following:

![Communications Workflow](assets/communicaions-workflow.png)

### Create PDF documents {#create-pdf-documents}

You can use the _generatePDFOutput_ API to create PDF document that is based on a form design and XML form data. The output is a non-interactive PDF document. That is, users cannot enter or modify form data. A basic workflow is to merge XML form data with a form design to create a PDF document. The following illustration shows the merging of a form design and XML form data to produce a PDF document.

![Create PDF Documents](assets/outPutPDF_popup.png)

### Create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) document {#create-PS-PCL-ZPL-documents}

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on an XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->

## 関連トピック {#see-also}

* [通信処理 - 同期 API](/help/forms/aem-forms-cloud-service-communications.md)
* [通信処理 - バッチ API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [アダプティブフォームおよび通信 API 用の AEM Forms as a Cloud Service アーキテクチャ](/help/forms/aem-forms-cloud-service-architecture.md)
