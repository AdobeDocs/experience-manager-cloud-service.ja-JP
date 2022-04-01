---
title: Forms as a Cloud Service の通信の概要
description: データを XDP および PDF テンプレートと自動的に結合するか、出力を PCL、ZPL および PostScript 形式で生成します
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: fdbb927dbd7f6d640100d444431f931d95414ebc
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 44%

---

# AEM Forms as a Cloud Service の通信の使用 {#frequently-asked-questions}

コミュニケーション機能により、ブランド承認、パーソナライズ、標準化されたドキュメント（ビジネス通信、明細書、請求処理レター、特典通知、月々の請求、ウェルカムキットなど）を作成できます。

この機能は、ドキュメントを生成および操作するための API を提供します。 ドキュメントをオンデマンドで生成または操作したり、バッチジョブを作成して、定義した間隔で複数のドキュメントを生成することができます。 通信 API は次のものを提供します。

* 合理化されたオンデマンドおよびバッチドキュメント生成機能.

* PDFドキュメントをオンデマンドで組み合わせ、並べ替え、検証する機能。

* 外部システムとの統合を容易にする HTTP API。 オンデマンド操作（低遅延）用とバッチ操作（高スループット操作）用に別々の API が含まれています。

* データへのセキュリティで保護されたアクセス。通信 API は、顧客が指定したデータリポジトリーからのみデータに接続し、データにアクセスするので、通信の安全性が高まります。

![クレジットカード明細書のサンプル](assets/statement.png)
クレジットカード明細書は、通信 API を使用して作成できます。このサンプル文は同じテンプレートを使用しますが、クレジットカードの使用状況に応じて顧客ごとに別々のデータを使用します。

## ドキュメントの生成

コミュニケーションドキュメント生成 API は、テンプレート (XFA またはPDF) と顧客データ ([XML データ](#form-data)) を使用して、PS、PCL、DPL、IPL、ZPL 形式などのPDFおよび印刷形式のドキュメントを生成します。 これらの API は [PDFと XFA テンプレート](#supported-document-types) と [XML データ](communications-known-issues-limitations.md#form-data) バッチ・ジョブを使用して、1 つのドキュメントをオンデマンドで生成するか、複数のドキュメントを生成します。

通常、[Designer](use-forms-designer.md) を使用してテンプレートを作成し、通信 API を使用してテンプレートにデータを結合します。アプリケーションは、出力ドキュメントをネットワークプリンター、ローカルプリンター、またはアーカイブ用のストレージシステムに送信できます。標準ワークフローとカスタムワークフローの例を次に示します。

![通信ドキュメント生成ワークフロー](assets/communicaions-workflow.png)

ユースケースによっては、これらのドキュメントを Web サイトまたはストレージサーバーからダウンロードできるようにすることもできます。

ドキュメント生成 API の例を以下に示します。

### PDF ドキュメントの作成 {#create-pdf-documents}

ドキュメント生成 API を使用して、フォームデザインと XML フォームデータに基づくPDFドキュメントを作成できます。 結果として出力されるのは非インタラクティブ PDF ドキュメントです。つまり、ユーザーはフォームデータを入力または変更できません。 基本ワークフローは、XML フォームデータをフォームデザインと結合して PDF ドキュメントを作成することです。次の図は、フォームデザインと XML フォームデータをマージしてPDFドキュメントを生成する方法を示しています。

![PDF文書の作成](assets/outPutPDF_popup.png)
図：ワークフロードキュメントを作成するための一般的なPDF

### PostScript（PS）、Printer Command Language（PCL）、Zebra Printing Language（ZPL）ドキュメントの作成 {#create-PS-PCL-ZPL-documents}

ドキュメント生成 API を使用して、XDP フォームデザインまたはPDFドキュメントに基づく PostScript(PS)、Printer Command Language(PCL) および Zebra Printing Language(ZPL) ドキュメントを作成できます。 これらの API は、フォームデザインとフォームデータを結合してドキュメントを生成するのに役立ちます。 ドキュメントをファイルに保存し、カスタムプロセスを開発してファイルをプリンターに送信することができます。

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### バッチデータの処理による複数のドキュメントの作成 {#processing-batch-data-to-create-multiple-documents}

ドキュメント生成 API を使用して、XML バッチデータソース内のレコードごとに個別のドキュメントを作成できます。 ドキュメントは一括モードと非同期モードで生成できます。コンバージョンの様々なパラメーターを設定し、バッチ処理を開始できます。

![PDF ドキュメントの作成](assets/ou_OutputBatchMany_popup.png)

<!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. 

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use document generation APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document’s fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form. -->

## ドキュメントの操作

通信ドキュメント操作 API は、通信ドキュメントの組み合わせ、並べ替え、検証に役立ちますPDF。 通常、DDX を作成し、ドキュメント操作 API に送信して、ドキュメントを組み立てたり、並べ替えたりします。 DDX ドキュメントには、ソースドキュメントを使用して一連の必須ドキュメントを作成する方法に関する手順が記載されています。 DDX リファレンスドキュメントでは、サポートされるすべての操作に関する詳細情報を提供します。 ドキュメント操作の例を以下に示します。

### PDF ドキュメントのアセンブリ

ドキュメント製造 API を使用して、2 つ以上のPDFまたは XDP ドキュメントを 1 つのPDFドキュメントまたはPDFPortfolioにアセンブリできます。 PDF ドキュメントをアセンブリする方法には、次のようなものがあります。

* 単一 PDF ドキュメントのアセンブリ
* PDF ポートフォリオの作成
* 暗号化ドキュメントのアセンブリ
* ベイツナンバリングを使用したドキュメントのアセンブリ
* ドキュメントの統合およびアセンブリ

![複数のPDFドキュメントからの簡単なPDFドキュメントのアセンブリ](assets/as_document_assembly.png)
図：複数のPDFドキュメントからの簡単なPDFドキュメントのアセンブリ

### PDF ドキュメントのディスアセンブリ

ドキュメントの製造 API を使用して、ディスアセンブリドキュメントをPDFできます。 この API では、ソースドキュメントからページを抽出したり、しおりに基づいてソースドキュメントを分割したりできます。 このタスクは、一般的に、PDF ドキュメントが最初に多数の個別ドキュメント（明細書一式など）から作成された場合に役立ちます。

* ソースドキュメントからのページの抽出
* しおりに基づいたソースドキュメントの分割

![しおりに基づくソースドキュメントを複数のドキュメントに分割する](assets/as_intro_pdfsfrombookmarks.png)
図：しおりに基づくソースドキュメントを複数のドキュメントに分割する

### PDF/A 準拠ドキュメントに変換して検証

ドキュメント作成 API を使用して、PDFドキュメントをPDF/A 準拠のドキュメントに変換し、PDFドキュメントがPDF/A に準拠しているかどうかを判断できます。 PDF/A は、ドキュメントのコンテンツを長期間保存するためのアーカイブ形式です。フォントはドキュメント内に埋め込まれ、ファイルは圧縮されません。その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/A ドキュメントには、オーディオおよびビデオコンテンツは含まれません。

## 通信 API のタイプ

通信は、オンデマンドおよびバッチでのドキュメント生成用に HTTP API を提供します。

* **[同期 API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)** は、オンデマンド、低遅延、単一レコードのドキュメント生成シナリオに適しています。これらの API は、ユーザーアクションに基づいたユースケースにより適しています。例えば、ユーザーがフォームへの入力を完了した後にドキュメントを生成するような場合です。

* **[バッチ API（非同期 API）](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)**&#x200B;は、スケジュール化された、高スループットの、複数のドキュメント生成シナリオに適しています。これらの API は、バッチでドキュメントを生成します。例えば、毎月生成される電話料金、クレジットカード明細、給付計算書などです。

## オンボーディング 

通信機能は、Formsas a Cloud Serviceユーザー向けのスタンドアロンおよびアドオンモジュールとして使用できます。 アクセス権限を要求する場合は、アドビのセールスチームまたはアドビ担当者に問い合わせてください。お客様の組織で変換サービスを使用できるように設定し、組織の管理者に対して必要な権限を設定します。管理者は、組織のFormsas a Cloud Serviceの開発者（ユーザー）に API を使用するアクセス権を付与できます。

オンボーディング後に、Formsas a Cloud Service環境で通信機能を有効にするには、次の手順を実行します。

1. Cloud Manager にログインし、AEM Forms as a Cloud Serviceインスタンスを開きます。

1. 「プログラムを編集」オプションを開き、「ソリューションとアドオン」タブに移動して、「**[!UICONTROL Forms - 通信]**」オプションを選択します。

   ![通信](assets/communications.png)

   既に **[!UICONTROL Forms — デジタル登録]** オプションを選択し、 **[!UICONTROL Forms - Communications Add-On]** オプション。

   ![アドオン](assets/add-on.png)

1. 「**[!UICONTROL 更新]**」をクリックします。

1. ビルドパイプラインを実行します。ビルドパイプラインが成功すると、お使いの環境で通信 API が有効になります。

>[!NOTE]
>
> ドキュメント操作 API を有効にして設定するには、次のルールを [Dispatcher の設定](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service allows you to generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

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

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on a XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document’s fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->
