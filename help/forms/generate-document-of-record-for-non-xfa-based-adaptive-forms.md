---
title: AEM Forms用の送信PDF（旧レコードのドキュメント）の生成
description: アダプティブFormsのフォーム送信から送信PDFを生成する方法について説明します。 アーカイブまたは参照用に、送信されたフォームのPDFを作成します。
feature: Adaptive Forms, Foundation Components
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 16d07932-3308-4b62-8fa4-88c4e42ca7b6
role: User, Developer
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '4208'
ht-degree: 56%

---

# アダプティブForms用の送信PDF（旧レコードのドキュメント）の生成

>[!NOTE]
>
> [新しいアダプティブフォームを作成する](/help/forms/creating-adaptive-form-core-components.md)、または [AEM Sites ページにアダプティブフォームを追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)際には、最新の拡張可能なデータキャプチャである[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する従来の方法について説明します。


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

## 概要 {#overview}

フォームの入力時または送信時には、そのフォームを印刷物またはドキュメント形式で記録しておくことができます。このレコードは、Submission PDF（旧称レコードのドキュメント、DoR）と呼ばれます。 送信されたフォームの印刷用PDFです。 後日お客様が入力した情報については、提出PDFを参照するか、提出PDFを使用してフォームやコンテンツをPDF形式でアーカイブすることもできます。

![提出PDF （旧記録文書） ](assets/document-of-record.png)

送信PDFを作成するには、XFA ベースまたはAcroform ベースのテンプレートを、アダプティブフォームを介して収集されたデータと結合します。 送信PDFは、自動またはオンデマンドで生成できます。
オンデマンドオプションを使用すると、カスタム XFAまたはAcroform ベースのテンプレートを指定して、Submission PDFにカスタム外観を提供できます。

以下の操作を実行できます。

* [XFA ベースの送信PDFの生成](#generate-an-XFA-based-document-of-record)
* [Acroform ベースの（Acrobat Form PDF）送信PDFの生成](#generate-an-Acroform-based-document-of-record)
* [送信PDFの自動生成](#auto-generate-a-document-of-record)

## 開始する前に {#components-to-automatically-generate-a-document-of-record}

Submission PDFに必要なアセットについて学習し、準備を整える前に、次の手順を実行します。

**基本テンプレート：** Forms Designer または Acrobat フォーム（AcroForm）で作成された XFA テンプレート（XDP ファイル）。[基本テンプレート ](#base-template-of-a-document-of-record)は、送信PDFのスタイル設定とブランディング情報を指定するために使用されます。 XFA テンプレート（XDP ファイル）を AEM Forms インスタンスに先にアップロードします。

**アダプティブフォーム：**&#x200B;送信PDFを生成するアダプティブフォーム。

## XFA ベースの送信PDFの生成 {#generate-an-XFA-based-document-of-record}

XFA テンプレート（XDP ファイル）を AEM Forms インスタンスにアップロードします。次の手順を実行して、送信PDFのテンプレートとしてXFA テンプレート（XDP ファイル）を使用するようにアダプティブフォームを設定します。

1. Experience Manager オーサーインスタンスで、**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;をクリックします。
1. フォームを選択し、「**[!UICONTROL プロパティ]**」をクリックします。
1. プロパティウィンドウで、「**[!UICONTROL フォームモデル]**」を選択します。
1. 「**[!UICONTROL フォームモデル]**」タブの「**[!UICONTROL モデルを選択]**」ドロップダウンで、「**[!UICONTROL スキーマ]**」または「**[!UICONTROL なし]**」を選択します。フォームモデルの選択は、フォームの作成時にも行うことができます。
1. 「フォームモデル」タブの「レコードのドキュメントテンプレート設定」セクションで、「**フォームテンプレートをレコードのドキュメントテンプレートとして関連付ける**」を選択します。このオプションを選択すると、マシン上で使用可能なすべての XFA テンプレート（XDP ファイル）が表示されます。適切なファイルを選択します。また、アダプティブフォームと選択した XFA テンプレート（XDP ファイル）で、必ず同じスキーマ（データスキーマ）が使用されるようにします。
1. 「**[!UICONTROL 完了]**」をクリックします。

これで、アダプティブフォームは、送信PDFのテンプレートとしてXDP ファイルを使用するように設定されました。 次の手順では、[アダプティブフォームコンポーネントを対応するテンプレートフィールドにバインド](#bind-adaptive-form-components-with-template-fields)します。

## Acroform ベースの送信PDFの生成 {#generate-an-Acroform-based-document-of-record}

Adobe Acrobat PDF（AcroForm）を AEM Forms インスタンスにアップロードします。Adobe Acrobat PDF（Acroform）を送信PDFのテンプレートとして使用するようにアダプティブフォームを設定するには、次の手順を実行します。

1. Experience Manager オーサーインスタンスで、**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;をクリックします。
1. フォームを選択し、「**[!UICONTROL プロパティ]**」をクリックします。
1. プロパティウィンドウで、「**[!UICONTROL フォームモデル]**」を選択します。
1. 「**[!UICONTROL フォームモデル]**」タブの「**[!UICONTROL モデルを選択]**」ドロップダウンで、「**[!UICONTROL スキーマ]**」または「**[!UICONTROL なし]**」を選択します。フォームモデルの選択は、フォームの作成時にも行うことができます。
1. 「フォームモデル」タブの「レコードのドキュメントテンプレート設定」セクションで、「**フォームテンプレートをレコードのドキュメントテンプレートとして関連付ける**」を選択します。このオプションを選択すると、マシン上で使用可能なすべての Acrobat PDF（AcroForm）が表示されます。適切なファイルを選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

これで、アダプティブフォームは、送信PDFのテンプレートとしてAcroformを使用するように設定されました。 次の手順では、[アダプティブフォームコンポーネントを対応するテンプレートフィールドにバインド](#bind-adaptive-form-components-with-template-fields)します。

## 送信PDFの自動生成 {#auto-generate-a-document-of-record}

アダプティブフォームが送信PDFを自動生成するように設定されている場合、フォームが変更されるたびに、送信PDFが即座に更新されます。 例えば、既存のアダプティブフォームからフィールドが削除された場合、対応するフィールドも削除され、送信PDFには表示されません。 送信PDFを自動生成する他にも多くの利点があります。

* フォーム開発者は、データバインディングを手動で管理する必要はありません。自動生成された送信PDFは、データバインディング関連の更新を処理します。
* フォーム開発者は、送信PDFから除外とマークされたフィールドを手動で非表示にする必要はありません。 自動生成された送信PDFは、そのようなフィールドを除外するように事前設定されています。
* 自動生成された送信PDF オプションにより、送信PDF用のフォームテンプレートの作成に必要な時間を節約できます。
* 自動生成された「送信」PDF オプションを使用すると、様々なベーステンプレートを使用して、様々なスタイルとアピアランスを使用できます。 これは、組織に最適なスタイルと外観を選択するのに役立ちます。提出PDF. スタイル設定を指定しない場合、システムスタイルがデフォルトとして設定されます。
* 自動生成された送信PDFにより、フォームの変更が送信PDFにすぐに反映されます。

送信PDFを自動生成するようにアダプティブフォームを設定するには、次の手順を実行します。

1. Experience Manager オーサーインスタンスで、**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;をクリックします。
1. フォームを選択し、「**[!UICONTROL プロパティ]**」をクリックします。
1. プロパティウィンドウで、「**[!UICONTROL フォームモデル]**」を選択します。
1. 「**[!UICONTROL フォームモデル]**」タブの「**[!UICONTROL モデルを選択]**」ドロップダウンで、「**[!UICONTROL スキーマ]**」または「**[!UICONTROL なし]**」を選択します。フォームモデルの選択は、フォームの作成時にも行うことができます。
1. 「フォームモデル」タブの「レコードのドキュメントテンプレート設定」セクションで、「**レコードのドキュメントを生成**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

## アダプティブフォームコンポーネントとテンプレートフィールドのバインド {#bind-adaptive-form-components-with-template-fields}

アダプティブフォームフィールドをテンプレートフィールドとバインドして、対応する送信PDF フィールドに取り込まれたフォームデータを表示します。 アダプティブフォームコンポーネントを対応する送信PDF テンプレートフィールドにバインドするには：

1. カスタムフォームテンプレートを使用するように設定されたアダプティブフォームを編集用に開きます。

1. アダプティブフォームコンポーネントを選択し、設定アイコン（![設定](assets/Smock_Wrench_18_N.svg)）をクリックします。プロパティブラウザーが開きます。

1. プロパティブラウザーで、フィールドを参照して選択します。

   * （AcroForm テンプレートの場合）**[!UICONTROL レコードのドキュメントバインド参照フィールド]**&#x200B;プロパティ。
   * （XFA テンプレートの場合）**[!UICONTROL データモデルバインド参照]**&#x200B;プロパティ。

1. 「**[!UICONTROL 保存]**」をクリックします。

<!-- 
In the following video, Adaptive Form components are bound with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

メール送信、Experience Manager ワークフロー送信アクションを[ レコードのドキュメントのステップ、およびその他の送信アクション ](configuring-submit-actions.md)と組み合わせて使用すると、送信PDFを受け取ることができます。

## Submission PDF テンプレートの増分更新 {#document-of-record-template-incremental-updates}

アダプティブフォームと対応する送信PDF テンプレートは、時間の経過とともに変化する可能性があります。 アダプティブフォームまたは送信PDF テンプレートにフィールドを追加、削除、または変更することができます。

送信PDF テンプレートを変更し、変更されたテンプレートをAEM Formsにアップロードすると、アダプティブForms エディターは変更されたバインディングを自動的に検出し、新しいバインディングが必要なアダプティブフォームコンポーネントについて通知します。 これにより、送信PDF テンプレートを段階的に更新できます。

例えば、組織&#x200B;*We.Retail*&#x200B;には、AcroForm ベースの送信PDF テンプレート *we-retail-invoice.pdf*&#x200B;があります。 テンプレートは次のようになります。

![オリジナルのテンプレート](assets/we-retail-invoice.png)

このテンプレートをしばらく使用した後、組織は `invoice-number` フィールドの名前を `bill-number` フィールドに変更し、購入者のメールアドレスを取り込むことにします。開発者は `invoice-number` フィールドの名前を更新し、テンプレートに「メール」フィールドを追加します。また、 *we-retail-invoice-v2.pdf* という新しいバージョンのテンプレートも作成します。

![更新されたテンプレート](assets/we-retail-new-invoice.png)

開発者は、更新されたテンプレートをアダプティブフォームにアップロードし、適用します。アダプティブフォームは、バインディングが変更されたフィールドのリストを自動的に検出して表示します。

![バインディングエラー](assets/we-retail-binding-error.png)

フォーム開発者は、アダプティブ Forms フィールドを対応する送信PDF テンプレートとバインドします。

>[!VIDEO](assets/we-retail-binding.mp4)

これで、アダプティブフォームが送信されると、更新された送信PDFが作成されます。

![更新済み ](assets/we-retail-new-invoice-sent-to-customer.png)

## Submission PDFを使用する際の主な考慮事項 {#key-considerations-when-working-with-document-of-record}

アダプティブForms用のPDFを提出する際は、次の考慮事項と制限事項に注意してください。

* **リッチテキストのサポート**：送信PDFは、リッチテキストフィールドのHTML マークアップタグをサポートしています。 サポートされているタグとアクセシビリティに関する考慮事項について詳しくは、[Submission PDFでサポートされているHTML マークアップタグ ](html-markup-tags-support-in-document-of-record.md)を参照してください。
* アダプティブフォームのドキュメントフラグメントは、送信PDFには表示されません。 ただし、アダプティブフォームフラグメントはサポートされています。
* XML スキーマベースのアダプティブフォーム用に生成されたSubmission PDFのコンテンツバインディングはサポートされていません。
* Submission PDFのローカライズ版は、ユーザーがSubmission PDFのレンダリングをリクエストしたときに、ロケールに応じてオンデマンドで作成されます。 送信PDFのローカライズは、アダプティブフォームのローカライズと共に行われます。<!-- For more information on localization of Document of Record and Adaptive Forms see Using AEM translation workflow to localize Adaptive Forms and Document of Record.-->

<!--
 ## Configure an adaptive form to generate  Document of Record {#adaptive-form-types-and-their-documents-of-record}

While creating an adaptive form, in the Form Model tab of Adaptive Form properties, select one the following option: 

* **None**
  Select the option to create an Adaptive Form without a form model. When the option is selected, the Document of Record is automatically generated for your Adaptive Form.

* **[Associate form template as a Document of Record template](creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)**
  
  Select the option to use an XFA Form as a template for Document of Record. 

* **[Generate Document of Record](creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)**
  Select the option to use an XFA Form as a template. When the option is selected, the Document of Record is automatically generated for your Adaptive Form. When you use an XML schema as a template for an Adaptive Form, ensure that the adaptive form and associated XFA Form use the same XML schema as your Adaptive Form
  

When you select a form model, configure Document of Record using options available under Document of Record Template Configuration. See [Document of Record Template Configuration](#document-of-record-template-configuration).
-->

## アダプティブフォーム要素のマッピング {#mapping-of-adaptive-form-elements}

次の表では、アダプティブフォームコンポーネントと対応するXFA コンポーネントについて説明し、それらが送信PDFに表示される場合について説明します。

### フィールド {#fields}

<table>
 <tbody>
  <tr>
   <th>アダプティブフォームコンポーネント</th>
   <th>対応する XFA コンポーネント</th>
   <th>送信PDF テンプレートにデフォルトで含まれますか？</th>
   <th>メモ</th>
  </tr>
  <tr>
   <td>ボタン</td>
   <td>ボタン</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>チェックボックス</td>
   <td>チェックボックス</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>日付選択</td>
   <td>日付／時間フィールド</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>ドロップダウンリスト</td>
   <td>ドロップダウンリスト</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>手書き署名</td>
   <td>手書き署名</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>数値ボックス</td>
   <td>数値フィールド</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>パスワードボックス</td>
   <td>パスワードフィールド</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>ラジオボタン</td>
   <td>ラジオボタン</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>テキストボックス</td>
   <td>テキストフィールド</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>リセットボタン</td>
   <td>リセットボタン</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>送信ボタン</td>
   <td><p>メール送信ボタン</p> <p>HTTP 送信ボタン</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>利用条件</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>ファイル添付</td>
   <td> </td>
   <td>false</td>
   <td>送信PDF テンプレートでは使用できません。 添付ファイルを通じて送信PDFでのみ使用できます。</td>
  </tr>
 </tbody>
</table>

### コンテナ {#containers}

<table>
 <tbody>
  <tr>
   <th>アダプティブフォームコンポーネント</th>
   <th>対応する XFA コンポーネント</th>
   <th>メモ</th>
  </tr>
  <tr>
   <td>パネル<br /> </td>
   <td>サブフォーム<br /> </td>
   <td>繰り返し可能なパネルは、繰り返し可能なサブフォームにマッピングされます。</td>
  </tr>
 </tbody>
</table>

### 静的コンポーネント {#static-components}

| アダプティブフォームコンポーネント | 対応する XFA コンポーネント | メモ |
|---|---|---|
| 画像 | 画像 | TextDraw コンポーネントと画像コンポーネントは、XSD ベースのアダプティブフォームの送信PDFに必ず表示されます。ただし、送信PDF設定で除外する場合は除きます。 |

### テーブル {#tables}

ヘッダー、フッターおよび列といった、アダプティブフォームのテーブルコンポーネントは、対応する XFA コンポーネントにマッピングされます。繰り返し可能なパネルをSubmission PDFのテーブルにマッピングできます。

## Submission PDFのベーステンプレート {#base-template-of-a-document-of-record}

基本テンプレートは、Submission PDFにスタイルとアピアランスに関する情報を提供します。 自動生成された送信PDFのデフォルトの外観をカスタマイズできます。 例えば、基本テンプレートを使用して、Submission PDFのヘッダーに会社ロゴを、フッターに著作権情報を追加できます。

基本テンプレートのマスターページは、送信PDF テンプレートのマスターページとして使用されます。 マスターページには、Submission PDFに適用できるページヘッダー、ページフッター、ページ番号などの情報を含めることができます。 送信PDFの自動生成用の基本テンプレートを使用して、この情報を送信PDFに適用できます。 基本テンプレートを使用すると、フィールドのデフォルトプロパティを変更することができます。

基本テンプレートを設計する際は、[基本テンプレートの規則](#base-template-conventions)に従ってください。

## 基本テンプレートの規則 {#base-template-conventions}

基本テンプレートは、Submission PDFのヘッダー、フッター、スタイル、外観を定義するために使用されます。 ヘッダーとフッターには、会社のロゴや著作権テキストなどの情報を含めることができます。基本テンプレートの最初のマスターページは、コピーされ、送信PDFのマスターページとして使用されます。このマスターページには、ヘッダー、フッター、ページ番号など、送信PDFのすべてのページに表示されるその他の情報が含まれています。 基本テンプレートの規則に準拠していない基本テンプレートを使用する場合でも、基本テンプレートの最初のマスターページはSubmission PDF テンプレートで引き続き使用されます。 基本テンプレートを規則に従ってデザインし、Submission PDFの自動生成に使用することを強くお勧めします。

**メインページの規則**

* 基本テンプレートでは、ルートサブフォームに `AF_METATEMPLATE`、マスターページに `AF_MASTERPAGE` と名前を付けます。

* ルートサブフォームの `AF_METATEMPLATE` 下に位置する `AF_MASTERPAGE` という名前のマスターページは、ヘッダー、フッターおよびスタイル情報を抽出する場合に優先して使用されます。

* `AF_MASTERPAGE` が存在しない場合は、基本テンプレート中に存在する最初のマスターページが使用されます。

**フィールドのスタイリング規則**

* 送信PDFのフィールドにスタイルを適用するには、基本テンプレートで、`AF_FIELDSSUBFORM` ルートサブフォームの下の`AF_METATEMPLATE` サブフォームにあるフィールドが提供されます。

* これらのフィールドのプロパティは、送信PDFのフィールドに適用されます。 これらのフィールドは、`AF_<name of field in all caps>_XFO` の命名規則に従う必要があります。例えば、チェックボックスのフィールド名は `AF_CHECKBOX_XFO` とする必要があります。

基本テンプレートを作成するには、Forms Designer で次の手順を実行します。

1. **[!UICONTROL ファイル]**／**[!UICONTROL 新規]**&#x200B;をクリックします。
1. 「**[!UICONTROL テンプレートに基づく]**」のオプションを選択します。

1. 「**[!UICONTROL Forms - レコードのドキュメント]**」のカテゴリを選択します。
1. 「**[!UICONTROL DoR 基本テンプレート]**」を選択します。
1. 「**[!UICONTROL 次へ]**」をクリックし、必要な情報を入力します。

1. （オプション）送信PDFのフィールドに適用するフィールドのスタイルと外観を変更します。
1. フォームを保存します。

これで、保存したフォームを送信PDFのベーステンプレートとして使用できるようになりました。 基本テンプレート中に存在するスクリプトについて、いずれも変更したり、削除したりしないでください。

**基本テンプレートの変更**

* 基本テンプレート内のフィールドに対していずれのスタイルも適用しない場合は、基本テンプレートからそれらのフィールドを削除することをお勧めします。これにより、基本テンプレートのアップグレードを自動的に適用することができます。
* 基本テンプレートを変更するときは、スクリプトを削除、追加、変更しないでください。

基本テンプレートを設計するときは、上記の規則と手順に厳密に従ってください。

## Submission PDFでのブランディング情報のカスタマイズ {#customize-the-branding-information-in-document-of-record}

送信PDFを生成する際に、「レコードのドキュメント」タブで送信PDFのブランド情報を変更できます。 「レコードのドキュメント」タブには、ロゴ、外観、レイアウト、ヘッダー、フッター、免責事項などのオプションや、選択されていないチェックボックスやラジオボタンを含めるかどうかのオプションが含まれています。

「レコードのドキュメント」タブに入力されたブランディング情報をローカライズするには、ブラウザーのロケールを正しく設定してください。Submission PDFのブランディング情報をカスタマイズするには、次の手順を実行します。

1. 送信PDFでパネル（ルートパネル）を選択し、![configure](assets/configure.png)を選択します。
1. ![dortab](assets/dortab.png) を選択します。「レコードのドキュメント」タブが表示されます。
1. Submission PDFをレンダリングするデフォルトテンプレートまたはカスタムテンプレートのいずれかを選択します。 デフォルトのテンプレートを選択すると、送信PDFのサムネールプレビューがテンプレートドロップダウンの下に表示されます。
1. デフォルトのテンプレートとカスタムのテンプレートのどちらを選択するかに応じて、以下のプロパティの一部またはすべてのプロパティが「レコードのドキュメント」タブに表示されます。以下のプロパティを指定して、送信PDFの外観を定義します。

   1. **基本のプロパティ**：
      * **テンプレート**：カスタムテンプレートを選択する場合は、[!DNL AEM Forms] サーバーで XDP を参照して選択します。お使いの [!DNL AEM Forms] サーバーにまだないテンプレートを使用する場合は、まず XDP を [!DNL AEM Forms] サーバーにアップロードする必要があります。
      * **Accent Color**：送信PDFでヘッダーテキストと区切り文字がレンダリングされる色。
      * **フォントファミリー**：送信PDF内のテキストのフォントファミリー。

        >[!NOTE]
        >
        > AEM Forms には、PDF ファイルとシームレスに統合できる様々なビルトインのフォントが用意されています。サポートされているフォントのリストを表示するには、[こちらをクリック](/help/forms/supported-out-of-the-box-fonts.md)してください。

      * **データモデルにバインドされていないフォームオブジェクトを含める**: プロパティを設定すると、送信PDFのスキーマベースのアダプティブフォームからバインドされていないフィールドが含まれます。
      * **レコードのドキュメントから非表示フィールドを除外**: プロパティを設定すると、送信PDFから除外する非表示フィールドが特定されます。
      * **パネルの説明を非表示**: プロパティを設定すると、パネル/テーブルの説明は送信PDFから除外されます。 パネルとテーブルに対して適用可能です。

      ![基本のプロパティ](/help/forms/assets/basicpropertiesdor.png)

   2. **フォームフィールドのプロパティ**:
      * **チェックボックスおよびラジオボタンのコンポーネントには、選択した値のみを表示**：このプロパティを設定すると、チェックボックスとラジオボタンの選択された値のみが[!UICONTROL レコードのドキュメント]に表示されます。
      * **複数の値の区切り記号**：複数の値を表示する場合は、カンマや改行などの任意の区切り記号を選択できます。
      * **オプションの位置揃え**：目的の整列（水平、垂直、アダプティブフォームと同じ）を選択して、[!UICONTROL レコードのドキュメント]に表示するチェックボックスやラジオボタンなどのフィールドの整列を設定することができます。デフォルトでは、垂直揃えが[!UICONTROL レコードのドキュメント]のフィールドに設定されています。DoR の[!UICONTROL フォームフィールドのプロパティ]からプロパティを設定すると、アダプティブフォームのフィールドの[!UICONTROL 項目の整列]で設定されたプロパティが上書きされます。例えば「[!UICONTROL アダプティブフォームと同じ]」オプションを使用する場合は、アダプティブフォームのオーサーインスタンスで設定された整列が[!UICONTROL レコードのドキュメント]のフィールドに使用されます。
      * **水平整列のオプション数**:You&#x200B;は、水平整列の送信PDFに表示されるオプション数を設定できます。

      ![フォームフィールドのプロパティ](/help/forms/assets/formfieldpropertiesdor.png)

      **複数選択ドロップダウンのラベルを表示**

      <span class="preview">この機能は、早期アクセスプログラムから利用できます。 アクセスをリクエストするには、公式アドレスから[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)にメールを送信してください。</span>

      送信PDFに、内部保存値ではなく、複数選択ドロップダウンコンポーネントの選択した表示ラベルが表示されるようになりました。 例えば、ユーザーがドロップダウンから「California」と「New York」を選択した場合、Submission PDFには、`CA`や`NY`などの内部値ではなく、選択したラベルが表示されます。

   3. **マスターページのプロパティ**:
      * **ロゴイメージ**：アダプティブフォームのロゴイメージを使用するか、DAM から選択するか、またはコンピューターからアップロードすることができます。
      * **フォームのタイトル**：DoR のタイトル。
      * **ヘッダーテキスト**：送信PDFのヘッダーセクションに表示されるテキスト。
      * **免責事項ラベル**：免責事項のラベル。
      * **免責事項**：送信PDFに関する権利と義務の範囲を指定するテキスト。
      * **免責事項テキスト**：免責事項のテキスト。

      ![マスターページのプロパティ](/help/forms/assets/masterpagepropertiesdor.png)

   <!--
   [!NOTE]
   >
   >If you are using an Adaptive Form template created with a version of Designer prior to 6.3, for Accent Color and Font Family properties to work, ensure that the following is present in your Adaptive Form template under the root subform:

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```
   -->

1. ブランディングの変更内容を保存するには、「**[!UICONTROL 完了]**」を選択します。

>[!NOTE]
> 
> 送信PDFにカスタムフォームタイトルを表示するには、**レコードのドキュメントのプロパティ**/**マスターページプロパティ**&#x200B;の&#x200B;**カスタムフォームタイトル**&#x200B;を編集します。 このカスタムタイトル：
> 
> * 生成されたPDFのヘッダーに表示されます
> * PDFのドキュメントプロパティで、タイトルとして表示されます
> * PDFを開いたときに、最初の表示タイトルとして表示されます

## アダプティブフォームエディターでのレコードのドキュメントのサポート {#dor-support-in-adaptiveform}

[!UICONTROL レコードのドキュメント]テンプレートは、アダプティブフォームエディターまたはアダプティブフォームテンプレートエディターから直接設定することができます。

アダプティブフォームエディターのオーサーインスタンスから、以下の手順を実行します。

1. **[!UICONTROL アダプティブフォームコンテナ（ルート）]**&#x200B;コンポーネントを選択します。
1. 「![アイコンを設定](/help/forms/assets/configure-icon.svg)」アイコンをクリックして、アダプティブフォームコンテナの&#x200B;**[!UICONTROL プロパティ]**&#x200B;開きます。
1. 「**[!UICONTROL レコードのドキュメントのテンプレート]**」タブを開き、次のオプションから選択します。
   * **[!UICONTROL なし]**：このオプションを選択すると、アダプティブフォーム用に[!UICONTROL レコードのドキュメント]のテンプレートは作成されません。
   * **[!UICONTROL フォームテンプレートをレコードのドキュメントのテンプレートとして関連付ける]**:Whenこのオプションを選択すると、XFA フォームが送信PDFのテンプレートとして使用されます。
   * **[!UICONTROL レコードのドキュメントを生成]**：このオプションを選択すると、[!UICONTROL レコードのドキュメント]のテンプレートがアダプティブフォーム用に自動的に生成されます。

1. 「![保存](/help/forms/assets/check-button.png)」を選択して、プロパティを保存します。

![レコードのドキュメントのテンプレートのサポート](/help/forms/assets/dor-templatesupport.png)

>[!NOTE]
>
>アダプティブフォームテンプレートエディターを使用して[!UICONTROL レコードのドキュメント]のテンプレートを作成する場合、「[!UICONTROL レコードのドキュメントのテンプレート]」タブで使用できるオプションは、「[!UICONTROL なし]」と「[!UICONTROL レコードのドキュメントを生成]」の 2 つだけです。

## Submission PDFのパネルの表と列のレイアウト {#table-and-column-layouts-for-panels-in-document-of-record}

いくつかのフォームフィールドを使用すると、アダプティブフォームが長くなる場合があります。送信PDFをアダプティブフォームの正確なコピーとして保存したくない場合があります。 これで、送信PDFで1つ以上のアダプティブフォームパネルを保存するためのテーブルまたは列のレイアウトを選択できるようになりました。

提出PDFを作成する前に、パネルの設定で、そのパネルのレコードのドキュメントのレイアウトを表または列として選択します。 パネルのフィールドは、送信PDFで適切に整理されます。

送信PDFのテーブルレイアウトでレンダリングされたパネルの![ フィールド ](assets/dortablelayout.png)

送信PDFのテーブルレイアウトでレンダリングされたパネルのフィールド

送信PDFの列レイアウトでレンダリングされたパネルの![ フィールド ](assets/dorcolumnlayout.png)

送信PDFの列レイアウトでレンダリングされたパネルのフィールド

## 送信PDFの設定 {#document-of-record-settings}

送信PDFの設定では、送信PDFに含めるオプションを選択できます。 例えば、銀行では、名前、年齢、社会保障番号、電話番号などをフォームから受け取ります。このフォームで、銀行口座番号や支店の詳細が生成されます。Submission PDFでは、名前、社会保障番号、銀行口座、支店の詳細のみを表示できます。

レコードのドキュメントコンポーネントの設定は、そのプロパティで使用できます。コンポーネントのプロパティにアクセスするには、コンポーネントを選択し、オーバーレイ内の ![cmppr](assets/cmppr.png) をクリックします。プロパティはサイドバーにリスト表示され、その中で次の設定を検索できます。

**フィールドレベルの設定**

* **レコードのドキュメントから除外**: プロパティ trueを設定すると、フィールドが送信PDFから除外されます。 これは `excludeFromDoR` という名前のスクリプト可能プロパティです。その動作は、**非表示の場合はレコードのドキュメントからフィールドを除外**&#x200B;フォームレベルプロパティに依存します。

* **パネルをテーブルとして表示：** プロパティを設定すると、パネル内のフィールドが6つより少ない場合、パネルは送信PDFにテーブルとして表示されます。 この設定は、パネルにのみ適用されます。
* **レコードのドキュメントからタイトルを除外：** プロパティを設定すると、パネル/テーブルのタイトルが送信PDFから除外されます。 パネルおよび表に対してのみ適用できます。
* **レコードのドキュメントから説明を除外：** プロパティを設定すると、パネル/テーブルの説明が送信PDFから除外されます。 パネルおよび表に対してのみ適用できます。

**フォームレベルの設定**

* **DoR:**&#x200B;に連結されていないフィールドを含めるプロパティを設定すると、送信PDFのスキーマベースのアダプティブフォームから連結されていないフィールドが含まれます。 デフォルトでは true になっています。
* **非表示の場合はDoRからフィールドを除外：** フォーム送信時に送信PDFから非表示のフィールドを除外するプロパティを設定します。 サーバー[で](/help/forms/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)再検証を有効にすると、サーバーは、送信PDFからこれらのフィールドを除外する前に、非表示フィールドを再計算します。

## カスタム XCI ファイルの使用

XCI ファイルは、ドキュメントの様々なプロパティを設定する場合に役立ちます。Forms as a Cloud Service にはマスター XCI ファイルがあります。カスタム XCI ファイルを使用して、マスター XCI ファイルで指定された 1 つ以上のデフォルトのプロパティを上書きできます。例えば、ドキュメントにフォントを埋め込むか、すべてのドキュメントに対してタグ付きプロパティを有効にするかを選択できます。XCI オプションを次の表に示します。

| XCI オプション | 説明 |
|--- |--- |
| config/present/pdf/creator | ドキュメント情報ディクショナリの Creator エントリを使用して、ドキュメント作成者を識別します。このディクショナリについては、[PDF リファレンスガイド](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/)を参照してください。 |
| config/present/pdf/producer | ドキュメント情報ディクショナリの Producer エントリを使用して、ドキュメントプロデューサーを識別します。このディクショナリについては、[PDF リファレンスガイド](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/)を参照してください。 |
| config/present/layout | 出力を単一ページとするか連続ページとするかを制御します。 |
| config/present/pdf/compression/level | PDF ドキュメントの生成時に使用する圧縮レベルを指定します。 |
| config/present/pdf/fontInfo/embed | 出力ドキュメントに埋め込むフォントを制御します。 |
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
| config/present/script/exclude | 無視するイベントを Forms as a Cloud Service に通知します。 |
| config/present/pdf/linearized | 出力 PDF ドキュメントを線形化するかどうかを制御します。 |
| config/present/script/runScripts | Forms as a Cloud Service が実行するスクリプトのセットを制御します。 |
| config/present/pdf/tagged | 出力 PDF ドキュメントへのタグの組み込みを制御します。タグは、PDF のコンテキストでは、ドキュメントの論理構造を公開するためにドキュメントに組み込まれる追加情報です。タグは、アクセシビリティの支援や書式の再設定に役立ちます。例えば、スクリーンリーダーがテキストの途中でページ番号を読み上げてしまわないように、ページ番号をアーティファクトとしてタグ付けすることができます。タグを使用すると、ドキュメントの有用性が高まる反面、ドキュメントのサイズが大きくなり、作成にかかる処理時間も長くなります。 |
| config/present/pdf/fontInfo/alwaysEmbed | 出力ドキュメントに埋め込むフォントを指定します。 |
| config/present/pdf/fontInfo/neverEmbed | 出力ドキュメントに埋め込まないフォントを指定します。 |
| config/present/pdf/pdfa/part | ドキュメントが準拠する PDF/A 仕様のバージョン番号を指定します。 |
| config/present/pdf/pdfa/amd | PDF/A 仕様の修正レベルを指定します。 |
| config/present/pdf/pdfa/conformance | PDF/A 仕様の適合レベルを指定します。 |
| config/present/pdf/version | 生成する PDF ドキュメントのバージョンを指定します |
| config/present/pdf/version/map | ドキュメントのフォールバックフォントを指定します |

>[!NOTE]
>
> AEM Forms には、PDF ファイルとシームレスに統合できる様々なビルトインのフォントが用意されています。サポートされているフォントのリストを表示するには、[こちらをクリック](/help/forms/supported-out-of-the-box-fonts.md)してください。


### Forms as a Cloud Service 環境でのカスタム XCI ファイルの使用

1. 開発プロジェクトにカスタム XCI ファイルを追加します。
1. 次の [inline プロパティ](/help/implementing/deploying/configuring-osgi.md)を指定します。

   ```JSON
    {
     "xciFilePath": "[path of XCI file]"
    }
   ```

   例：

   ```JSON
    {
     "xciFilePath": "/content/dam/formsanddocuments/customMinionProBoldAndTagged.xci"
    }
   ```

1. Cloud Service 環境にコードをデプロイします。

### ローカルの Forms as a Cloud Service 開発環境でのカスタム XCI ファイルの使用

1. XCI ファイルをアップロード環境にローカル開発します。
1. Cloud Service SDK 設定マネージャーを開きます。デフォルトの URL は <http://localhost:4502/system/console/configMgr> です。
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブなコミュニケーション Web チャネル]**」の設定を検索して開きます。
1. XCI ファイルのパスを指定し、「**[!UICONTROL 保存]**」をクリックします。


## よくある質問 {#faq}

**Q：変更が送信PDFに表示されません。**
**Ans:** アダプティブForms エディターでフォームを開き、微調整（フィールドラベルの調整やフィールドの並べ替えなど）をおこない、フォームを保存します。 これにより、送信PDF テンプレートが再生成され、次に生成されるPDFに変更内容が表示されます。

## 関連トピック {#see-also}

{{see-also}}
