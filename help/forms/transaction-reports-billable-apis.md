---
title: トランザクションレポート請求可能 API
description: トランザクションとして計上されるすべての API のリスト
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: 7318c5e65fc03bfebbf5fb43e4edc30ffbb53909
workflow-type: tm+mt
source-wordcount: '1598'
ht-degree: 50%

---

# トランザクションレポート請求可能 API {#transaction-reports-billable-apis}

AEM Forms には、フォームの送信、ドキュメントの処理、ドキュメントのレンダリングをおこなうための API がいくつか用意されています。一部の API はトランザクションとして計上され、それ以外は自由に使用できます。このドキュメントでは、トランザクションレポートでトランザクションとして計上されるすべての API のリストを示します。課金対象の API が使用される一般的なシナリオを次に示します。

* アダプティブフォームの送信
* ある形式から別の形式へのドキュメントの変換
* ダイナミック PDF ドキュメントの統合
* レコードのドキュメントの生成 (Forms Service または Output Service を使用 )
* インタラクティブ PDF ドキュメントと別の PDF ドキュメントの結合
* AEM Workflows のタスクの割り当て手順と通信 API 手順の使用

請求 API は、ページ数、ドキュメントまたはフォームの長さ、レンダリング済みドキュメントの最終的な形式を考慮しません。トランザクションレポートでは、トランザクションを「Forms送信済み」と「レンダリングされたドキュメント」の 2 つのカテゴリに分けます。

* **送信済みフォーム：** AEM Forms で作成された任意のタイプのフォームからデータが送信され、そのデータが任意のデータストレージリポジトリーまたはデータベースに送信された場合、そのデータはフォーム送信と見なされます。例えば、アダプティブフォームやフォームセットの送信は、送信されたフォームと見なされます。 フォームセットに 5 つのフォームが含まれ、フォームセットが送信されると、トランザクションレポートサービスはそのフォームセットを 5 回の送信としてカウントします。

* **レンダリング済みドキュメント：** テンプレートとデータを組み合わせたドキュメントの生成、ドキュメントの電子署名または認証、ドキュメントサービスの課金可能なドキュメントサービス API の使用、ある形式から別の形式へのドキュメントの変換は、レンダリング済みドキュメントとして計上されます。

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_submission_graph_en"
>title="フォーム送信トラッカー"
>abstract="アドビの直感的なトラッキングダッシュボードを使用して、AEM Formsパブリッシュインスタンス上のフォーム送信を容易に監視できます。 グラフには、現在のインスタンスに固有のデータが表示され、トレンドを迅速に分析し、十分な情報に基づいた決定を下すことができます。 他のインスタンスの送信データの場合は、各インスタンスのダッシュボードにアクセスするだけです。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_conversions_graph_en"
>title="フォーム変換トラッカー"
>abstract="フォームの変換に関する情報を常に把握し、変換の総数をまとめます。 グラフには、現在のAEM Formsパブリッシュインスタンスに固有のデータが表示され、トレンドを迅速に分析し、十分な情報に基づいた決定をおこなうことができます。 他のインスタンスのコンバージョンデータを表示するには、それぞれのインスタンスのダッシュボードにアクセスします。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formCreationAvgDuration_graph_en"
>title="フォーム生成の平均期間"
>abstract="グラフは、フォームの作成に要した平均時間を示します。 グラフの各棒は特定のフォームを表し、棒の高さはその期間中のフォーム作成に要した平均時間を示します。 このグラフを分析すると、ユーザーは、様々な期間や様々なコンテキストでのフォーム作成の効率と速度を把握でき、潜在的な改善点についてのインサイトが得られます。 グラフは、現在のAEM Formsオーサーインスタンスに固有のデータを提供します。 他のインスタンスのデータを表示するには、各インスタンスのダッシュボードにアクセスします。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formPublishAvgDuration_en"
>title="フォーム作成の平均期間"
>abstract="グラフには、フォームの作成と公開にかかった平均時間が表示されます。この時間は、フォームが編集用に開かれた最初の日から測定されます。 各バーは、フォームの特定の期間に対応します。バーの高さは、フォーム開発の開始から最終的なフォーム作成および公開までの平均時間を示します。 グラフは、現在のAEM Formsオーサーインスタンスに固有のデータを提供します。 他のインスタンスのデータを表示するには、各インスタンスのダッシュボードにアクセスします。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_newForms_graph_en"
>title="新しいFormsトラッカー"
>abstract="グラフには、特定の期間に新しく作成されたフォームの数や頻度に関する情報が表示されます。 グラフの各棒は、日、週、月などの個別の測定単位を表します。 各バーの高さは、その特定の間隔で作成された新しいフォームの数量または頻度を示します。 グラフは、現在のAEM Formsオーサーインスタンスに固有のデータを提供します。 他のインスタンスのデータを表示するには、各インスタンスのダッシュボードにアクセスします。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_publishedForms_graph_en"
>title="公開済みForms Tracker"
>abstract="グラフには、特定の期間に正常に発行されたフォームの数や頻度に関する情報が表示されます。 これにより、フォームの公開の経時的な傾向、パターン、または変化を把握し、生産性の監視、ピーク発行期間の特定、フォームの公開プロセスでの変更の成功の評価に役立ちます。 グラフは、現在のAEM Formsパブリッシュインスタンスに固有のデータを提供します。 他のインスタンスのコンバージョンデータを表示するには、それぞれのインスタンスのダッシュボードにアクセスします。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formFragments_graph_en"
>title="公開済みForms Tracker"
>abstract="このグラフを使用すると、ユーザーがフォームで使用するフォームフラグメントの数を確認できます。 これらの再利用可能なパーツがフォーム構築でどれほど頻繁に使用されているかを把握できます。 グラフは、現在のAEM Formsパブリッシュインスタンスに固有のデータを提供します。 他のインスタンスのコンバージョンデータを表示するには、それぞれのインスタンスのダッシュボードにアクセスします。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_avgFormPerFragments_graph_en"
>title="公開済みForms Tracker"
>abstract="グラフには、フォームフラグメントの作成に要した平均時間が表示されます。この時間は、フォームフラグメントが編集用に開かれた最初の日から測定されます。 各バーは、フォームフラグメントの特定の期間に対応します。バーの高さは、フォームフラグメントの開発の開始から最終化および公開までの平均時間を示します。 グラフは、現在のAEM Formsパブリッシュインスタンスに固有のデータを提供します。 他のインスタンスのコンバージョンデータを表示するには、それぞれのインスタンスのダッシュボードにアクセスします。"

<!-- 

>[!NOTE]
>
>Transaction Reports UI displays three categories: Forms Submitted, Documents Rendered, and Documents Processed. Both Documents Rendered and Documents Processed are accounted as Documents Rendered.
-->


<!--

## Billable Document Services APIs {#billable-document-services-apis}

### Generate PDF Service {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## 課金対象のドキュメントサービス API {#billable-document-services-apis}

### PDF 生成サービス {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#section/Before-you-start" target="_blank">createPDF</a></td>
   <td>テンプレートから PDF ドキュメントを生成し、そのドキュメントにデータを結合する。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePrintedOutput/post" target="_blank">exportPDF</a></td>
   <td>XDP ファイルまたはPDFドキュメントをサポートされるファイルタイプに変換します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

### Output サービス {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutput" target="_blank">generatePDFOutput</a></td>
   <td>データとテンプレートを結合して、PDF ドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutputOptions" target="_blank">generatePDFOutput (PDFOutputOptions)</a></td>
   <td>データとテンプレートを結合して、PDF ドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePDFOutputBatch</a></td>
   <td>データとテンプレートを結合して、一連の PDF ドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutput" target="_blank">generatePrintedOutput</a></td>
   <td>XDP および PDF ドキュメントを PostScript（PS）、Printer Command Language（PCL）および ZPL ファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions" target="_blank">generatePrintedOutput (PrintedOutputOptions)</a></td>
   <td>XDP および PDF ドキュメントを PostScript（PS）、Printer Command Language（PCL）および ZPL ファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePrintedOutputBatch</a></td>
   <td>XDP および PDF ドキュメントのセットを、PostScript（PS）、Printer Command Language（PCL）および ZPL の各ファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
 </tbody>
</table>

### DocAssurance サービス {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/docassurance/#tag/DocAssurance" target="_blank">secureDocument</a><br /> </td>
   <td>この API を使用すると、ドキュメントを保護できます。API を使用して、PDF ドキュメントの署名、認証、Reader 用の拡張、暗号化を行うことができます。</td>
   <td>処理済みドキュメント</td>
   <td>secureDocument の署名および認証操作のみが請求されます。</td>
  </tr>
 </tbody>
</table>

### レコードのドキュメント (DOR) サービス {#document-of-record-dor-forms-service-and-output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://opensource.adobe.com/aem-forms-af-runtime/api/#tag/Generate-DoR/operation/generateDoR" target="_blank">render</a></td>
   <td>指定されたレンダリングメソッドを呼び出して、設定されたパラメーターを使用してレコードのドキュメントを生成します。</td>
   <td>Forms Service を使用して処理されたドキュメント</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed using Output Service</td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

<!--

### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Convert PDF Service {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converts a PDF document to a list of image documents. Supported image formats are JPEG, JPEG2K, PNG, and TIFF.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Converts a Flat PDF file to PostScript format using the options specified in the option spec.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Barcoded Forms Service {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Decodes all the barcodes in a Document object and returns an org.w3c.dom.Document object that contains data that was retrieved from the barcode.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

### Assembler サービス {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX">呼び出し</a></td>
   <td>指定された入力ドキュメントに対して DDX を実行し、結果のドキュメントを含むオブジェクトを返します</td>
   <td>処理済みドキュメント</td>
   <td>次の操作はトランザクションとして計上されません。
    <ul>
     <li>パッケージまたはポートフォリオの作成</li>
     <li>複数の XDP のステッチ </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX" target="_blank">呼び出し</a></td>
   <td>指定された入力ドキュメントに対して DDX を実行し、結果のドキュメントを含むオブジェクトを返します</td>
   <td>処理済みドキュメント</td>
   <td>Assembler サービスは、PDF Generator、Forms、Output サービスがサポートするすべての入力ファイル形式を、出力ファイル形式としてサポートします。 </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA">toPDFA</a></td>
   <td>指定したオプションを使用して、指定したドキュメントを PDF/A に変換します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

呼び出し API の使用状況は、次の操作を 1 つ以上実行すると、トランザクションとしてカウントされます。

1. 非PDF形式からPDF形式への変換 <!--For instance, the conversion from XDP format to PDF format, catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. PDF 形式から PDF/A 形式への変換。
1. PDF 形式から非 PDF 形式への変換。例としては、PDF 形式から画像形式への変換、または PDF 形式からテキスト形式への変換があります。


>[!NOTE]
>
>* Assembler サービスの invoke API は、入力に応じて別のサービスの課金対象 API を内部的に呼び出すことができます。したがって、呼び出し API は、０、単一、複数のトランザクションのいずれかとして計上される可能性があります。カウントされるトランザクションの数は、入力と呼び出される内部 API によって異なります。
>* Assembler サービスを使用して生成された単一の PDF ドキュメントは、0、単一、複数のトランザクションのいずれかとして計上される可能性があります。カウントされるトランザクションの数は、指定されたコードによって異なります。
>

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. In order for a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## 課金対象のデータキャプチャ API {#billable-data-capture-apis}

アダプティブフォームのすべての送信イベントは、トランザクションとして扱われます。 デフォルトでは、トランザクションフォームの PDF はトランザクションとして計上されません。提供した[トランザクションレコーダー API](record-transaction-custom-implementation.md) を使用して、PDF フォームの送信をトランザクションとして記録します。

### アダプティブフォーム {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>ユースケース</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td>アダプティブフォームの送信</td>
   <td>アダプティブフォームを設定済みの送信アクションに送信します。 </td>
   <td>送信済みフォーム</td>
   <td>
    <ul>
     <li>送信が成功した場合、1 回または 2 回のトランザクションが発生します。カウントされるトランザクションの数は、送信に使用する送信アクションのタイプによって異なります。例えば、メール送信アクションを使用した PDF の送信は、2 回のトランザクションが発生します。フォーム送信するトランザクション 1 回と、レコードのドキュメント（DOR）サービスを使用して PDF が生成されるトランザクション 1 回です。 </li>
     <li>アダプティブフォーム（アダプティブフォームフォームセット）内でアダプティブフォームを使用すると、1 回のトランザクションのみがカウントされます。アダプティブフォーム内には、任意の数のアダプティブフォームを含めることができます。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

<!--

### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Form set {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting a form set</td>
   <td>Submits form set to the submit URL configured in the form set.</td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
     <li>Every form in an HTML5 Forms form set accounts as a separate transaction. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

## 課金対象のフォーム中心のAEMワークフロー {#billable--form-centric-aem-workflows}

Form 中心のAEM Workflow のタスクの割り当て手順とドキュメントサービスの手順は、トランザクションと見なされます。 ワークフローステップがトランザクションとして考慮され、ワークフローの完了に失敗した場合、トランザクション数は元に戻されません。

<!--
Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.
-->


<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->

### フォーム中心のAEMワークフロー {#form-centric-aem-workflows}

<table>
 <tbody>
  <tr>
   <td><p>ユースケース</p> </td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td>割り当てタスクの送信手順</td>
   <td>送信済みフォーム</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>ワークフローアプリケーションのスタートポイントの送信 </td>
   <td>送信済みフォーム</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## カスタムコードのトランザクションとしての課金対象 API の記録 {#recording-billable-apis-as-transactions-for-custom-code}

PDF フォームの送信、エージェント UI を使用したインタラクティブな通信のプレビュー、非標準のフォーム送信の使用、カスタム実装などのアクションは、トランザクションとして考慮されません。AEM Forms は、トランザクションなどのアクションを記録する API を提供します。カスタム実装から API を呼び出して、[トランザクションを記録](/help/forms/record-transaction-custom-implementation.md)することができます。

## 関連記事 {#related-articles}

* [カスタム実装のトランザクションの記録](/help/forms/record-transaction-custom-implementation.md)
