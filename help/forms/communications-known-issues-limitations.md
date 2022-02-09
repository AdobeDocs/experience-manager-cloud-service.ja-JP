---
title: '既知の問題 '
description: コミュニケーションのベストプラクティス、既知の問題、制限事項
source-git-commit: bf7ce5850700141a8a6d1eeb90ea0fd21ff811e7
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 91%

---


# 考慮事項の既知の問題とベストプラクティス {#best-practices-known-issues-and-limitations}

通信 API の使用を開始する前に、次の考慮事項、既知の問題、よくある質問を確認してください。

## 検討事項  {#considerations-for-communications-apis}

### フォームデータ {#form-data}

通信 API は、通常 Designer で作成されるフォームデザインと、XML フォームデータの両方を入力として受け付けます。ドキュメントにデータを入力するには、入力先となるすべてのフォームフィールドの XML フォームデータに XML 要素が存在する必要があります。XML 要素名は、フィールド名と一致する必要があります。XML 要素がフォームフィールドに対応していない場合や、XML 要素名がフィールド名と一致しない場合、XML 要素は無視されます。XML 要素の表示順序を一致させる必要はありません。対応する値で XML 要素が指定される点が重要です。

次のローン申し込みフォームサンプルについて考えてみましょう。

![ローン申し込みフォーム](assets/loanFormData.png)

このフォームデザインにデータを結合するには、フォームに対応する XML データソースを作成します。次の XML は、住宅ローン申し込みフォームサンプルに対応する XML データソースを表しています。

```XML
<?xml version="1.0" encoding="UTF-8" ?>
- <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
- <xfa:data>
- <data>
    - <Layer>
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
    - <Mortgage>
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

通信 API のレンダリング機能に完全にアクセスするには、XDP ファイルを入力として使用することをお勧めします。場合によっては、PDF ファイルを使用できます。ただし、PDF ファイルを入力として使用する場合は、制限があります。

XFA ストリームを含んでいない PDF ドキュメントは、PostScript、PCL または ZPL としてレンダリングできません。通信 API は、XFA ストリーム（Designer で作成されたフォーム）を使用して PDF ドキュメントをレーザー形式およびラベル形式にレンダリングできます。PDF ドキュメントが署名済み、証明済み、（AEM Forms Reader Extensions サービスを使用して適用された）使用権限を含んでいる、のいずれかの場合、これらの印刷形式にはレンダリングできません。


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


## 既知の問題

* 特定のレンダリングタイプ (PDF、印刷 ) は、印刷オプションリストで 1 回だけ使用できます。 例えば、PCL レンダリングタイプを指定する PRINT オプションを 2 つ設定することはできません。

* バッチ設定の場合、OutputType（PDF、PRINT）と RenderType（PostScript、PCL、IPL、ZPL など）の値の組み合わせのインスタンスは 1 つだけ許可されています。

* 非同期 API（バッチ処理）の場合、デフォルトのレコードレベルは 2 に設定されます。 カスタム XCI を使用して、レコードレベルを 1 に変更できます。

* デフォルトの XCI が設定されている場合は、元のレンディションまでのパスが含まれます。 例：`/content/dam/formsanddocuments/default.xci/jcr:content/renditions/original`



## ベストプラクティス

* AEM Cloud Service が使用するクラウド領域で、データファイルの blob コンテナストアをホストすることをお勧めします。

## よくある質問  {#faq}

**監視フォルダーやその他のストレージメカニズムを使用して、入出力を保存することはできますか？**

現時点では、Microsoft Azure ストレージを使用して、入力データと生成されたドキュメントを保存できます。Microsoft Azure ストレージは、[データ移動操作の自動化](https://docs.microsoft.com/ja-jp/azure/storage/common/storage-use-azcopy-v10)に対する様々なオプションを提供しています。

**Microsoft Azure ストレージアカウントは Experience Manager Forms Cloud Service ライセンスに含まれていますか？**

Microsoft Azure ストレージアカウントは、Experience Manager Forms Cloud Service ライセンスとは独立したものです。

**通信 API はデータを Experience Manager Forms Cloud Service サーバーに保存しますか？**

入力および出力データは、Microsoft Azure ストレージにのみ保存されます。

**通信 API は Experience Manager Forms Cloud Service でのみ使用できますか？オンプレミス環境でも同様の機能を利用できますか？**

AEM Forms Output サービスを使用すると、テンプレート（XFA または PDF）と顧客データを組み合わせて、PDF、PS、PCL、ZPL 形式のドキュメントを生成できます。

オンプレミス環境と比較すると、Cloud Service は、自動スケーリングとコスト効率のメリットがさらに大きくなります。

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**複数のバッチ操作を同時に実行できますか？**
はい、複数のバッチ操作を同時に実行できます。競合を避けるために、操作ごとに異なるソースフォルダーと出力先フォルダーを常に使用するようにします。
