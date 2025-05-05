---
title: トランザクションレポート請求可能 API
description: トランザクションとして計上されるすべての API のリスト
feature: Adaptive Forms, Foundation Components
exl-id: 6dfcac3e-5654-4b4f-9134-0cd8be24332e
role: Admin, Developer, User
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: ht
source-wordcount: '1438'
ht-degree: 100%

---


# トランザクションレポート請求可能 API {#transaction-reports-billable-apis}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/transaction-reports/transaction-reports-billable-apis) |
| AEM as a Cloud Service | この記事 |


AEM Forms には、フォームの送信、ドキュメントの処理、ドキュメントのレンダリングをおこなうための API がいくつか用意されています。一部の API はトランザクションとして計上され、それ以外は自由に使用できます。このドキュメントでは、トランザクションレポートでトランザクションとして計上されるすべての API のリストを示します。課金対象の API が使用される一般的なシナリオを次に示します。

* アダプティブフォームの送信
* ある形式から別の形式へのドキュメントの変換
* ダイナミック PDF ドキュメントの統合
* レコードのドキュメントの生成（Forms サービスまたは Output サービスを使用）
* インタラクティブ PDF ドキュメントと別の PDF ドキュメントの結合
* AEM ワークフローのタスク割り当て手順と Communication API 手順の使用

請求 API は、ページ数、ドキュメントまたはフォームの長さ、レンダリング済みドキュメントの最終的な形式を考慮しません。トランザクションレポートでは、トランザクションが送信済みフォームとレンダリング済みドキュメントの 2 つのカテゴリに分類されます。

* **送信済みフォーム：** AEM Forms で作成された任意のタイプのフォームからデータが送信され、そのデータが任意のデータストレージリポジトリーまたはデータベースに送信された場合、そのデータはフォーム送信と見なされます。例えば、アダプティブフォームまたはフォームセットを送信すると、送信済みフォームと見なされます。フォームセットに 5 つのフォームが含まれている場合、フォームセットを送信すると、トランザクションレポートサービスでは 5 件の送信としてカウントされます。

* **レンダリング済みドキュメント：**&#x200B;テンプレートとデータを組み合わせたドキュメントの生成、ドキュメントの電子署名または認証、ドキュメントサービスの課金可能なドキュメントサービス API の使用、ある形式から別の形式へのドキュメントの変換は、レンダリング済みドキュメントとして見なされます。

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_submission_graph_en"
>title="フォーム送信トラッカー"
>abstract="このグラフは、特定の期間におけるアダプティブフォームの送信件数を表します。 送信件数の増加は、フォームの人気が高まっているか、ユーザーからより多くのデータを収集する必要性があることを示す可能性があります。 **メモ：**&#x200B;グラフには現在のインスタンスに固有のデータが表示されるので、トレンドを迅速に分析し、情報に基づいた意思決定を行うことができます。 他のインスタンスの送信データについては、各インスタンスのダッシュボードにアクセスするだけ確認できます。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_conversions_graph_en"
>title="ドキュメントレンディショントラッカー"
>abstract="このグラフは、特定の期間におけるドキュメントレンディションの数を表します。 **メモ：**&#x200B;グラフには現在のインスタンスに固有のデータが表示されるので、トレンドを迅速に分析し、情報に基づいた意思決定を行うことができます。 他のインスタンスの送信データについては、各インスタンスのダッシュボードにアクセスするだけ確認できます。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_newForms_graph_en"
>title="新しい Forms トラッカー"
>abstract="グラフには、特定の期間に新しく作成されたフォームの数に関する情報が表示されます。 **メモ：**&#x200B;グラフには、現在の AEM Forms オーサーインスタンスに固有のデータが表示されます。 他のインスタンスのデータを表示するには、各インスタンスのダッシュボードにアクセスします。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_publishedForms_graph_en"
>title="公開済み Forms トラッカー"
>abstract="グラフには、特定の期間に正常に公開されたフォームの数に関する情報が表示されます。 **メモ：**&#x200B;グラフには、現在の AEM Forms パブリッシュインスタンスに固有のデータが表示されます。 他のインスタンスのコンバージョンデータを表示するには、各インスタンスのダッシュボードにアクセスします。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formCreationAvgDuration_graph_en"
>title="フォーム生成の平均期間"
>abstract="グラフは、フォームの作成に要した平均時間を示します。 グラフの各棒は特定のフォームを表し、棒の高さはその時間枠内でフォームの作成に要した平均時間を示します。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formPublishAvgDuration_en"
>title="フォーム作成の平均期間"
>abstract="グラフには、フォームが編集用に開かれた最初の日から測定された、フォームの作成と公開にかかった平均時間が表示されます。 **メモ：**&#x200B;グラフには、現在の AEM Forms オーサーインスタンスに固有のデータが表示されます。 他のインスタンスのデータを表示するには、各インスタンスのダッシュボードにアクセスします。"


>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formFragments_graph_en"
>title="フォームフラグメントトラッカー"
>abstract="このグラフを使用すると、ユーザーがフォームで使用しているフォームフラグメントの数を確認できます。 **メモ：**&#x200B;グラフには、現在の AEM Forms パブリッシュインスタンスに固有のデータが表示されます。 他のインスタンスのコンバージョンデータを表示するには、各インスタンスのダッシュボードにアクセスします。"

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_avgFormPerFragments_graph_en"
>title="フォームフラグメントの平均時間トラッカー"
>abstract="グラフには、フォームフラグメントが編集用に開かれた最初の日から測定された、フォームフラグメントの作成にかかった平均時間が表示されます。 **メモ：**&#x200B;グラフには、現在の AEM Forms パブリッシュインスタンスに固有のデータが表示されます。 他のインスタンスのコンバージョンデータを表示するには、各インスタンスのダッシュボードにアクセスします。"


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
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
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
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
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
   <td>テンプレートから PDF ドキュメントを生成し、そのドキュメントにデータを結合します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePrintedOutput/post" target="_blank">exportPDF</a></td>
   <td>XDP ファイルまたは PDF ドキュメントをサポートされているファイルタイプに変換します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
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
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutputOptions" target="_blank">generatePDFOutput（PDFOutputOptions）</a></td>
   <td>データとテンプレートを結合して、PDF ドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePDFOutputBatch</a></td>
   <td>データとテンプレートを結合して、一連の PDF ドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutput" target="_blank">generatePrintedOutput</a></td>
   <td>XDP および PDF ドキュメントを PostScript（PS）、Printer Command Language（PCL）および ZPL ファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions" target="_blank">generatePrintedOutput（PrintedOutputOptions）</a></td>
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

### レコードのドキュメント（DOR）サービス {#document-of-record-dor-forms-service-and-output-service}

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
   <td>Forms サービスを使用して処理されたドキュメント</td>
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
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
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
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converts a PDF document to a list of image documents. Supported image formats are JPEG, JPEG2K, PNG, and TIFF.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
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
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
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
   <td>指定した入力ドキュメントに対して DDX を実行し、結果のドキュメントを含むオブジェクトを返します</td>
   <td>処理済みドキュメント</td>
   <td>次の操作はトランザクションとして計上されません。
    <ul>
     <li>パッケージまたはポートフォリオの作成</li>
     <li>複数の XDP のステッチ </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX" target="_blank">呼び出し</a></td>
   <td>指定した入力ドキュメントに対して DDX を実行し、結果のドキュメントを含むオブジェクトを返します</td>
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

次の操作を 1 つ以上実行すると、呼び出し API の使用がトランザクションとしてカウントされます。

1. PDF 以外の形式から PDF 形式への変換。<!--For instance, the conversion from XDP format to PDF format, catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
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
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. In order for a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## 課金対象のデータキャプチャ API {#billable-data-capture-apis}

アダプティブフォームのすべての送信イベントは、トランザクションとして計上されます。デフォルトでは、トランザクションフォームの PDF はトランザクションとして計上されません。提供した[トランザクションレコーダー API](record-transaction-custom-implementation.md) を使用して、PDF フォームの送信をトランザクションとして記録します。

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

## 課金対象のフォーム中心の AEM ワークフロー {#billable--form-centric-aem-workflows}

フォーム中心の AEM ワークフローのタスクおよびドキュメントサービスの割り当て手順は、トランザクションとして計上されます。ワークフローステップがトランザクションとして考慮され、ワークフローの完了に失敗した場合、トランザクション数は元に戻されません。

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
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->

### フォーム中心の AEM ワークフロー {#form-centric-aem-workflows}

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
