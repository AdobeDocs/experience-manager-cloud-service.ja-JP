---
title: Forms as a Cloud Service の通信の概要
description: データを XDP および PDF テンプレートと自動的に結合するか、出力を PCL、ZPL および PostScript 形式で生成します
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: d136062ed0851b89f954e5485c2cfac64afeda2d
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 85%

---

# AEM Forms as a Cloud Service Communications を使用 {#frequently-asked-questions}

**AEM Formsas a Cloud Service通信機能はベータ版です。**

通信機能は、ビジネス文書、ステートメント、請求処理レター、特典通知、毎月の請求書、ウェルカムキットなど、ブランド志向でパーソナライズされた標準的なドキュメントを作成するのに役立ちます。


オンデマンドでドキュメントを生成することも、バッチジョブを作成して、定義された間隔で複数のドキュメントを生成することもできます。通信 API は以下を提供します。

* 合理化されたオンデマンドおよびバッチドキュメント生成機能

* 既存のシステムと簡単に統合するための HTTP API。 オンデマンド（低遅延）およびバッチ操作（高スループット操作）用の個別の API が含まれます。 これにより、ドキュメントの生成が効率的になります。

* データへのセキュリティで保護されたアクセス。通信 API は、顧客が指定したデータリポジトリにのみ接続してデータにアクセスしますが、データのローカルコピーを作成しないため、通信の安全性が高くなります。

![クレジットカード明細書の例](assets/statement.png)
クレジットカード明細は、通信 API を使用して作成できます。 このサンプル文は同じテンプレートを使用していますが、クレジットカードの使用状況に応じて、顧客ごとに別々のデータを使用します。

## 仕組み?

通信は、[XML データ](#form-data)を含む [PDF および XFA テンプレート](#supported-document-types)を利用して、オンデマンドで単一のドキュメントを生成したり、定義した間隔で複数のドキュメントをバッチジョブで生成することができます。

通信 API は、テンプレート（XFA または PDF）と顧客データ（[XML データ](#form-data)）を組み合わせて、PDF 形式や PS、PCL、DPL、IPL、ZPL 形式などの印刷形式でドキュメントを生成するのに役立ちます。

通常、テンプレートを作成するには、 [Designer](use-forms-designer.md) コミュニケーション API を使用して、データをテンプレートと結合します。 アプリケーションは、出力ドキュメントをネットワークプリンター、ローカルプリンター、またはアーカイブ用のストレージシステムに送信できます。標準ワークフローとカスタムワークフローの例を次に示します。

![通信ワークフロー](assets/communicaions-workflow.png)

ユースケースによっては、これらのドキュメントを Web サイトまたはストレージサーバーからダウンロードできるようにすることもできます。

## 通信 API

通信は、オンデマンドおよびバッチでのドキュメント生成用に HTTP API を提供します。

* **[同期 API](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/)** は、オンデマンド、低遅延、単一レコードのドキュメント生成シナリオに適しています。これらの API は、ユーザーアクションに基づいたユースケースにより適しています。例えば、ユーザーがフォームへの入力を完了した後にドキュメントを生成するような場合です。

* **[バッチ API（非同期 API）](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/batch/)**&#x200B;は、スケジュール化された、高スループットの、複数のドキュメント生成シナリオに適しています。これらの API は、バッチでドキュメントを生成します。例えば、毎月生成される電話料金、クレジットカード明細、給付計算書などです。

## オンボーディング 

通信は、Forms as a Cloud Service のユーザー向けのスタンドアロンおよびアドオンモジュールとして利用できます。AdobeのセールスチームまたはAdobe担当者に連絡して、アクセス権を要求できます。

お客様の組織で変換サービスを使用できるように設定し、組織の管理者に対して必要な権限を設定します。管理者は、API を使用するためのアクセス権限を、組織内の AEM Forms 開発者（ユーザー）に付与することができます。

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

## 検討事項 {#considerations-for-communications-apis}

通信 API を使用したドキュメントの生成を始める前に、次の考慮事項を確認してください。

### フォームデータ {#form-data}

通信 API は、通常、 [Designer](use-forms-designer.md) および XML フォームデータを入力として。 ドキュメントにデータを入力するには、入力先となるすべてのフォームフィールドの XML フォームデータに XML 要素が存在する必要があります。XML 要素名は、フィールド名と一致する必要があります。XML 要素がフォームフィールドに対応していない場合や、XML 要素名がフィールド名と一致しない場合、XML 要素は無視されます。 XML 要素の表示順序を一致させる必要はありません。対応する値で XML 要素が指定される点が重要です。

次のローン申し込みフォームサンプルについて考えてみましょう。

![ローン申し込みフォーム](assets/loanFormData.png)

データをこのフォームデザインに結合するには、フォーム階層、フィールドの命名およびデータ型に対応する XML データソースを作成します。 次の XML は、住宅ローン申し込みフォームサンプルに対応する XML データソースを表しています。

```XML
* <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
* <xfa:data>
* <data>
    * <Layer>
        <closeDate>1/26/2007</closeDate>
        <lastName>Johnson</lastName>
        <firstName>Jerry</firstName>
        <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
        <city>New York</city>
        <zipCode>00501</zipCode>
        <state>NY</state>
        <dateBirth>26/08/1973</dateBirth>
        <middleInitials>D</middleInitials>
        <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
        <phoneNumber>5555550000</phoneNumber>
    </Layer>
    * <Mortgage>
        <mortgageAmount>295000.00</mortgageAmount>
        <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
        <purchasePrice>300000</purchasePrice>
        <downPayment>5000</downPayment>
        <term>25</term>
        <interestRate>5.00</interestRate>
    </Mortgage>
</data>
</xfa:data>
</xfa:datasets>
```

### サポートされているドキュメントタイプ {#supported-document-types}

通信 API のレンダリング機能に完全にアクセスするには、XDP ファイルを入力として使用することをお勧めします。場合によっては、PDF ファイルを使用できます。ただし、PDF ファイルを入力として使用する場合は、次のような制限があります。

XFA ストリームを含んでいない PDF ドキュメントは、PostScript、PCL または ZPL としてレンダリングできません。通信 API は、XFA ストリーム ( つまり、 [Designer](use-forms-designer.md)) をレーザー形式およびラベル形式に変換する必要があります。 PDF ドキュメントが署名済み、証明済み、（AEM Forms Reader Extensions サービスを使用して適用された）使用権限を含んでいる、のいずれかの場合、これらの印刷形式にはレンダリングできません。

<!-- Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

### Email support {#email-support}

For email functionality, you can create a process in Experience Manager Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

### 印刷可能領域 {#printable-areas}

デフォルトの 0.25 インチ印刷不可の余白は、ラベルプリンターには正確ではなく、プリンターによって異なります。また、ラベルサイズからラベルサイズまで異なりますが、0.25 インチの余白を保持するか、小さくすることをお勧めします。 ただし、印刷不能な余白を増やさないことをお勧めします。そうしないと、印刷可能領域内の情報が正しく印刷されません。

必ず、プリンターに合った XDC ファイルを使用してください。例えば、ドキュメントを 200 dpi のプリンターに送信する場合は 300 dpi のプリンター用の XDC ファイルを選択しないようにします。

### スクリプト XFA フォーム (XDP/PDF) のみ {#scripts}

通信 API で使用されるフォームデザインには、サーバー上で実行されるスクリプトを含めることができます。フォームデザインに、クライアント上で実行されるスクリプトが含まれていないことを確認します。フォームデザインスクリプトの作成について詳しくは、 [Designer ヘルプ](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### フォントマッピング {#font-mapping}

プリンター常駐フォントを使用するフォームをデザインするには、プリンターで使用可能なフォントと一致する書体名を Designer で選択します。PCL または PostScript でサポートされているフォントのリストは、対応するデバイスプロファイル（XDC ファイル）に記載されています。または、フォントマッピングを作成して、プリンター常駐フォント以外のフォントを、別の書体名のプリンター常駐フォントにマッピングすることもできます。例えば、PostScript シナリオでは、Arial® フォントへの参照をプリンター常駐の Helvetica® 書体にマッピングできます。

フォントがクライアントコンピューターにインストールされている場合は、Designer のドロップダウンリストで使用できます。フォントがインストールされていない場合は、フォント名を手動で指定する必要があります。Designer の「見つからないフォントを置換して保存」オプションはオフにできます。それ以外の場合、XDP ファイルを Designer で保存すると、置換フォント名が XDP ファイルに書き込まれます。つまり、プリンター常駐フォントは使用されません。

2 種類の OpenType® フォントが存在します。1 つは、PCL でサポートされている TrueType OpenType® フォントです。もう 1 つは CFF OpenType® です。PDF および PostScript 出力では、埋め込みの Type-1、TrueType および OpenType® フォントがサポートされています。PCL 出力では、埋め込みの TrueType フォントがサポートされています。

Type-1 フォントと OpenType® フォントは、PCL 出力には埋め込まれません。Type-1 および OpenType® フォントで書式設定されたコンテンツは、サイズが大きく生成に時間がかかる可能性があるビットマップ画像としてラスタライズおよび生成されます。

ダウンロードされたフォントや埋め込まれたフォントは、PostScript、PCL または PDF 出力の生成時に自動的に置換されます。つまり、生成された出力には、生成されたドキュメントを適切にレンダリングするために必要なフォントグリフのサブセットのみが含まれます。

### デバイスプロファイルファイルの操作（XDC ファイル） {#working-with-xdc-files}

デバイスプロファイル（XDC ファイル）は、XML 形式のプリンター記述ファイルです。このファイルを使用すると、通信 API がレーザープリンターまたはラベルプリンター形式でドキュメントを出力できます。通信 API で使用する XDC ファイルは次のとおりです。

* hppcl5c.xdc

* hppcl5e.xdc

* ps_plain_level3.xdc

* ps_plain.xdc

* zpl300.xdc

* zpl600.xdc

* zpl300.xdc

* ipl300.xdc

* ipl400.xdc

* tpcl600.xdc

* dpl300.xdc

* dpl406.xdc

* dpl600.xdc

提供されている XDC ファイルを使用して、印刷ドキュメントを生成したり、要件に応じて変更したりできます。

<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

これらのファイルは、特定のプリンターの機能（常駐フォント、用紙トレイ、ステープル機能など）をサポートする参照 XDC ファイルです。これらの参照は、デバイスプロファイルを使用したプリンターの設定方法を理解するために提供されています。また、同じ製品ラインの類似プリンターに対応する出発点でもあります。

### XCI 設定ファイルの操作 {#working-with-xci-files}

通信 API では、XCI 設定ファイルを使用して、出力を単一パネルとするかページ分割するかを制御するといったタスクを実行します。このファイル内の設定は編集できますが、通常、値を変更することはありません。<!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

変更した XCI ファイルを通信 API の使用時に渡すことができます。その際は、デフォルトファイルのコピーを作成し、ビジネス要件に合わせて変更する必要がある値のみを変更し、変更した XCI ファイルを使用します。

通信 API は、まずデフォルトの XCI ファイル（または変更された XCI ファイル）を使用します。次に、通信 API を使用して指定された値が適用されます。これらの値は XCI 設定よりも優先されます。

XCI オプションを次の表に示します。

| XCI オプション | 説明 |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/present/pdf/creator | ドキュメント情報ディクショナリの Creator エントリを使用して、ドキュメント作成者を識別します。このディクショナリについては、PDF リファレンスガイドを参照してください。 |
| config/present/pdf/producer | ドキュメント情報ディクショナリの Producer エントリを使用して、ドキュメントプロデューサーを識別します。このディクショナリについては、PDF リファレンスガイドを参照してください。 |
| config/present/layout | 出力を単一ページとするか連続ページとするかを制御します。 |
| config/present/pdf/compression/level | PDF ドキュメントの生成時に使用する圧縮レベルを指定します。 |
| config/present/pdf/scriptModel | 出力 PDF ドキュメントに XFA 固有の情報を含めるかどうかを制御します。 |
| config/present/common/data/adjustData | 結合後に XFA アプリケーションでデータを調整するかどうかを制御します。 |
| config/present/pdf/renderPolicy | ページコンテンツをサーバー側で生成するか、後でクライアント側で生成するかを制御します。 |
| config/present/common/locale | 出力ドキュメントで使用するデフォルトのロケールを指定します。 |
| config/present/destination | present 要素に含まれている場合は、出力形式を指定します。openAction 要素に含まれている場合は、インタラクティブクライアントでドキュメントを開いたときに実行されるアクションを指定します。 |
| config/present/output/type | ファイルに適用する圧縮の種類または生成する出力の種類を指定します。 |
| config/present/common/temp/uri | フォームの URI を指定します。 |
| config/present/common/template/base | フォームデザインの URI のベースを指定します。この要素がない場合や空の場合は、フォームデザインの場所がベースとして使用されます。 |
| config/present/common/log/to | ログデータまたは出力データの書き込み先を制御します。 |
| config/present/output/to | ログデータまたは出力データの書き込み先を制御します。 |
| config/present/script/currentPage | ドキュメントを開いたときの初期ページを指定します。 |
| config/present/script/exclude | どのイベントを無視するかを AEM Forms サーバーまたは通信 API に指示します。 |
| config/present/pdf/linearized | 出力 PDF ドキュメントを線形化するかどうかを制御します。 |
| config/present/script/runScripts | AEM Forms で実行されるスクリプトのセットを制御します。 |
| config/present/pdf/tagged | 出力 PDF ドキュメントへのタグの組み込みを制御します。タグは、PDF のコンテキストでは、ドキュメントの論理構造を公開するためにドキュメントに組み込まれる追加情報です。タグは、アクセシビリティの支援や書式の再設定に役立ちます。例えば、スクリーンリーダーがテキストの途中でページ番号を読み上げてしまわないように、ページ番号を装飾としてタグ付けすることができます。タグを使用すると、ドキュメントの有用性が高まる反面、ドキュメントのサイズが大きくなり、作成にかかる処理時間も長くなります。 |
| config/present/pdf/version | 生成する PDF ドキュメントのバージョンを指定します。 |
