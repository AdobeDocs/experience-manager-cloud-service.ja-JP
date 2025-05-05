---
title: アダプティブフォームフィールドの事前入力方法
description: 既存のデータを使用してアダプティブフォームのフィールドに事前入力します。ユーザーは、ソーシャルプロファイルでログインすることで、フォーム内の基本情報を事前に入力できます。
topic-tags: develop
feature: Adaptive Forms, Foundation Components
exl-id: e2a87233-a0d5-48f0-b883-915fe56f105f
role: User, Developer
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: ht
source-wordcount: '2007'
ht-degree: 100%

---

# アダプティブフォームフィールドに事前入力{#prefill-adaptive-form-fields}

>[!NOTE]
>
> [新しいアダプティブフォームを作成する](/help/forms/creating-adaptive-form-core-components.md)、または [AEM Sites ページにアダプティブフォームを追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)際には、最新の拡張可能なデータキャプチャである[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する従来の方法について説明します。

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

## はじめに {#introduction}

既存データを使用して、アダプティブフォームのフィールドを事前入力することができます。ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。アダプティブフォームにデータを事前入力するには、アダプティブフォームの事前入力データ構造に合った形式を使用して、事前入力 XML または JSON としてユーザーデータを作成します。

## 事前入力データの構造 {#the-prefill-structure}

アダプティブフォームには、連結されたフィールドと連結されていないフィールドが混在している場合があります。連結されたフィールドは、「コンテンツファインダー」タブからドラッグされたフィールドです。フィールドの編集ダイアログには、空ではない `bindRef` プロパティ値が含まれています。連結されていないフィールドは、サイドキックのコンポーネントブラウザーから直接ドラッグされ、`bindRef` 値が含まれています。

アダプティブフォームの連結されたフィールドと連結されていないフィールドの両方を事前入力できます。事前入力データには afBoundData セクションと afUnBoundData セクションが含まれており、アダプティブフォームの連結されたフィールドと連結されていないフィールドの両方を事前入力できます。`afBoundData` セクションには連結されたフィールドとパネルの事前入力データが含まれています。このデータは関連するフォームモデルスキーマに準拠している必要があります。

- [XFA フォームテンプレート](#xfa-based-af)を使用しているアダプティブフォームの場合は、XFA テンプレートのデータスキーマに準拠している事前入力 XML を使用します。
- [XML スキーマ](#xml-schema-af)を使用しているアダプティブフォームの場合は、XML スキーマ構造に準拠している事前入力 XML を使用します。
- [JSON スキーマ](#json-schema-based-adaptive-forms)を使用しているアダプティブフォームの場合は、JSON スキーマに準拠している事前入力 JSON を使用します。
- FDM スキーマを使用しているアダプティブフォームの場合は、FDM スキーマに準拠している事前入力 JSON を使用します。
- [フォームモデルのない](#adaptive-form-with-no-form-model)アダプティブフォームの場合、連結されたデータはありません。すべてのフィールドは、連結されていないフィールドであり、連結されていない XML を使用して事前入力されています。

### 事前入力 XML 構造のサンプル {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         .
         .
    </data>
  </afUnboundData>
</afData>
```

### 事前入力 JSON 構造のサンプル {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

同じ bindref を持つ連結されているフィールド、または同じ名前を持つ連結されていないフィールドの場合、XML タグまたは JSON オブジェクトで指定したデータがすべてのフィールドに入力されます。例えば、フォーム内の 2 つのフィールドは、事前入力データの名前 `textbox` にマップされます。ランタイム時、最初のテキストボックスに「A」が含まれる場合、この「A」が 2 番目のテキストボックスに自動的に挿入されます。このリンクは、アダプティブフォームフィールドのライブリンクと呼ばれます。

### XFA フォームテンプレートを使用したアダプティブフォーム {#xfa-based-af}

XFA ベースのアダプティブフォームの事前入力 XML と送信済み XML の構造は次のとおりです。

- **事前入力 XML 構造**：XFA ベースのアダプティブフォームのための事前入力 XML は、XFA フォームテンプレートのデータスキーマに準拠している必要があります。連結されていないフィールドを事前入力するには、事前入力 XML 構造を `/afData/afBoundData` タグにラップします。

- **送信済み XML 構造**：事前入力 XML が使用されていない場合、送信済み XML の `afData` ラッパータグには、連結されたフィールドと連結されていないフィールドの両方のデータが含まれます。事前入力 XML が使用された場合、送信済み XML は、事前入力 XML と同じ構造をしています。事前入力 XML が `afData` のルートタグで開始する場合、出力 XML もまた同じフォーマットとなります。事前入力 XML に `afData/afBoundData` のラッパーが無く、直接 `employeeData` のようなスキーマルートタグから開始する場合は、送信済み XML もまた `employeeData` タグから開始します。

Prefill-Submit-Data-ContentPackage.zip

[ファイルを取得](assets/prefill-submit-data-contentpackage.zip)
事前入力データと送信済みデータが含まれているサンプル

### XML スキーマベースのアダプティブフォーム  {#xml-schema-af}

XML スキーマをベースとするアダプティブフォームの事前入力 XML と送信済み XML の構造は次のとおりです。

- **事前入力 XML 構造**：事前入力 XML は、関連する XML スキーマに準拠していなければなりません。連結されていないフィールドを事前入力するには、事前入力 XML 構造を /afData/afBoundData タグにラップします。
- **送信済み XML 構造**：事前入力 XML が使用されていない場合、送信済み XML は、`afData` のラッパータグに連結されたフィールドと連結されていないフィールド両方のデータを含みます。事前入力 XML が使用された場合、送信済み XML は、事前入力 XML と同じ構造をしています。事前入力 XML が `afData` のルートタグで開始する場合、出力 XML は同じフォーマットとなります。事前入力 XML に `afData/afBoundData` のラッパーが無く、直接 `employeeData` のようなスキーマルートタグから開始する場合は、送信済み XML もまた `employeeData` タグから開始します。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">

    <xs:element name="sample" type="SampleType"/>

    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

XML スキーマをモデルとするフィールドの場合、以下の XML のサンプルに示すように、`afBoundData` タグのデータは事前入力されます。これは、1 つ以上の連結されていないテキストフィールドでアダプティブフォームを事前入力する場合に使用できます。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>連結されているパネル（サイドキックまたは「データソース」タブからコンポーネントをドラッグして作成された、空ではない `bindRef` が含まれているパネル）では、連結されていないフィールドを使用しないことをお勧めします。これらの連結していないフィールドのデータの損失を招くことがあります。また、フィールド名は、特に連結していないフィールドについては、フォーム間で一意のフィールド名を設定することをお勧めします。

#### afData および afBoundData ラッパーがない場合の例 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### JSON スキーマベースのアダプティブフォーム {#json-schema-based-adaptive-forms}

JSON スキーマをベースとするアダプティブフォームの場合、事前入力 JSON と送信済み JSON の構造は次のようになります。詳しくは、[JSON スキーマを使ったアダプティブフォームの作成](adaptive-form-json-schema-form-model.md)を参照してください。

- **事前入力 JSON スキーマ**：事前入力 JSON は、関連する JSON スキーマに準拠している必要があります。連結していないフィールドの事前入力も行う場合は、オプションで、/afData/afBoundData オブジェクトにまとめることが可能です。
- **送信済み JSON 構造**：事前入力 JSON が使用されていない場合、送信済み JSON は、afData のラッパータグに連結されたフィールドと連結されていないフィールド両方のデータを含みます。事前入力 JSON が使用された場合、送信済み JSON は、事前入力 JSON と同じ構造をしています。事前入力 JSON が afData のルートオブジェクトで開始する場合、出力 JSON もまた同じフォーマットとなります。事前入力 JSON に afData/afBoundData のラッパーが無く、直接ユーザーのようなスキーマルートオブジェクトから開始する場合は、送信済み JSON もま user オブジェクトから開始します。

```json
{
  "id": "https://some.site.somewhere/entry-schema#",
  "$schema": "https://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "address": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string"
        },
        "age": {
          "type": "integer"
        }
      }
    }
  }
}
```

JSON スキーマモデルを使用するフィールドの場合、以下の JSON のサンプルに示すように、afBoundData オブジェクトのデータは事前入力されます。これは、1 つ以上の連結されていないテキストフィールドでアダプティブフォームを事前入力する場合に使用できます。以下は `afData/afBoundData` ラッパーが含まれるデータの一例です。

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

以下は `afData/afBoundData` ラッパーが含まれない場合の一例です。

```json
{
  "user": {
    "address": {
      "city": "Noida",
      "country": "India"
    }
  }
}
```

>[!NOTE]
>
> 連結されているパネル（サイドキックまたは「データソース」タブからコンポーネントをドラッグして作成された、空ではない bindRef が含まれているパネル）では、連結されていないフィールドを使用することは&#x200B;**お勧めしません**。連結されていないフィールドで、データ損失が発生する可能性があるためです。特に連結していないフィールドについては、フォーム間で一意のフィールド名を設定することをお勧めします。
>

### フォームモデルのないアダプティブフォーム {#adaptive-form-with-no-form-model}

フォームモデルが含まれていないアダプティブフォームの場合、すべてのフィールドのデータは、`<afUnboundData> tag` の `<data>` タグの下にあります。

また、次のことに留意してください：

各種フィールドに送信されたユーザーデータのための XML タグは、フィールド名を使用して生成されます。したがって、一意のフィールド名を設定する必要があります。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## 事前入力サービスの設定 {#configuring-prefill-service-using-configuration-manager}

**デフォルトの事前入力サービス設定**&#x200B;の `alloweddataFileLocations` プロパティを使用すると、データファイルの場所またはデータファイルの場所を表す正規表現（regex）を設定できます。

以下の JSON ファイルにサンプルが表示されています。

```JSON
  {
  "alloweddataFileLocations": "`file:///C:/Users/public/Document/Prefill/.*`"
  }
```

設定の値をセットするには、[AEM SDK を使用して OSGi 設定を生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=ja#generating-osgi-configurations-using-the-aem-sdk-quickstart)し、Cloud Service インスタンスに[設定をデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja#deployment-process)します。

>[!NOTE]
>
> - デフォルトでは、事前入力はすべての種類のアダプティブフォーム（XSD、XDP、JSON、FDM、フォームモデルベースなし）で crx ファイルを通じて許可されます。事前入力は JSON ファイルおよび XML ファイルでのみ許可されます。
> - crx プロトコルは、事前入力済みデータのセキュリティを管理するので、デフォルトで許可されています。汎用的な正規表現を使用して他のプロトコル経由で事前入力すると、脆弱性が発生する可能性があります。データを保護するため、設定では安全性の高い URL を指定してください。

## 繰り返し可能なパネルの例外的なケース {#the-curious-case-of-repeatable-panels}

連結された（フォームスキーマ）フィールドや連結されていないフィールドは通常、同じアダプティブフォームに作成されます。ただし、連結が繰り返し可能な場合は、次のような例外があります。

- XFA フォームテンプレート、または XSD、JSON、FDM の各スキーマを使用したアダプティブフォームでは、連結されていない繰り返し可能なパネルはサポートされません。
- 連結された繰り返し可能なパネル内で、連結されていないフィールドを使用しないでください。

>[!NOTE]
>
> 経験則として、連結されていないフィールドでユーザーが入力したデータ上で、連結されているフィールドと連結されていないフィールドが重複する場合は、これらのフィールドを混在させないようにします。可能な場合は、スキーマまたは XFA フォームテンプレートを変更し、連結されていないフィールドのエントリを追加します。これにより、フィールドが連結されて、そのデータを送信済みデータの他のフィールドのデータと同様に使用できます。

## ユーザーデータの事前入力でサポートされるプロトコル {#supported-protocols-for-prefilling-user-data}

アダプティブフォームは、有効な正規表現で設定されている場合、次のプロトコルを介して事前入力データ形式のユーザーデータを事前入力できます。

### crx:// プロトコル {#the-crx-protocol}

```javascript
http
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

特定のノードには、`jcr:data` と呼ばれるプロパティがあり、データを保持していなければなりません。

### The file:// protocol  {#the-file-protocol-nbsp}

```javascript
https://`servername`/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

参照元ファイルは、同じサーバー上になければなりません。

### The https:// protocol {#the-http-protocol}

```javascript
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://servername/somesamplexmlfile.xml
```

### service:// プロトコル {#the-service-protocol}

```javascript
https://`servername`/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

- SERVICE_NAME とは OSGI 事前入力サービスの名前を指します。[事前入力サービスの作成と実行](prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)を参照してください。
- 識別情報とは、OSGI 事前入力サービスが事前入力データを取得するために必要なメタデータを指します。ログイン済みユーザーの識別子は、使用できるメタデータの一例です。

>[!NOTE]
>
> 認証パラメーターの引き渡しはサポートされていません。

### slingRequest でのデータ属性の設定 {#setting-data-attribute-in-slingrequest}

以下のサンプルコードが示すように、`data` 属性が XML または JSON を含む文字列である、`slingRequest` の `data` 属性を設定することもできます（以下は XML が含まれている場合の例です）。

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

すべてのデータが含まれている単純な XML または JSON 文字列を記述して、slingRequest に設定できます。これは、slingRequest data 属性を設定するページに含むすべてのコンポーネントのレンダラー JSP で、簡単にできます。

例えば、特定のタイプのヘッダーを使用して、特定のデザインのページを作成するとします。これを達成するには、頁コンポーネントに含んで、`header.jsp` 属性を設定することができる独自の `data` を作成します。

例えば、Facebook、Twitter、LinkedIn などのソーシャルアカウントを使用して、ログイン時にデータを事前入力するとします。この場合、`header.jsp`ユーザーアカウントからデータを取得し、データパラメーターを設定するに単純な JSP を含めることができます。

prefill-page component.zip

[ファイルを取得](assets/prefill-page-component.zip)
ページコンポーネントのサンプル prefill.jsp

## [!DNL AEM Forms] カスタム事前入力サービス {#aem-forms-custom-prefill-service}

事前定義されたソースからデータを頻繁に読み取る必要がある場合は、カスタム事前入力サービスを使用できます。事前入力サービスでは、定義済みデータソースからデータを読み取り、事前入力データファイルの内容を、アダプティブフォームのフィールドに事前入力します。事前入力データをアダプティブフォームと永続的に関連付ける場合にも役立ちます。

### 事前入力サービスの作成と実行 {#create-and-run-a-prefill-service}

事前入力サービスは OSGi サービスで、OSGi バンドルを使用してパッケージ化します。OSGi バンドルを作成し、アップロードし、[!DNL AEM Forms] バンドルにインストールします。バンドルの作成を開始する前に、以下を行います。

- [ [!DNL AEM Forms]  Client SDK をダウンロードします](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)
- ボイラープレートパッケージをダウンロードします

- データ（事前入力データ）ファイルを crx-repository に配置します。ファイルは crx-repository の \contents フォルダー内の任意の場所に配置できます。

[ファイルを入手](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 事前入力サービスの作成 {#create-a-prefill-service}

ボイラープレートパッケージ（サンプルの事前入力サービスパッケージ）には、[!DNL AEM Forms] 事前入力サービスのサンプル実装が含まれています。ボイラープレートパッケージをコードエディターで開きます。例えば、ボイラープレートプロジェクトを Eclipse で開いて編集します。ボイラープレートパッケージをコードエディターで開いたら、以下の手順でサービスを作成します。

1. src\main\java\com\adobe\test\Prefill.java ファイルを開いて編集します。
1. コードで、以下の値を設定します。

   - `nodePath:` crx-repository の場所を指すノードパス変数には、データ（事前入力）ファイルのパスが含まれています。例：/content/prefilldata.xml
   - `label:` label パラメーターは、サービスの表示名を指定します。例：Default Prefill Service

1. `Prefill.java` ファイルを保存して閉じます。
1. `AEM Forms Client SDK` パッケージをボイラープレートプロジェクトのビルドパスに追加します。
1. プロジェクトをコンパイルし、バンドルの .jar を作成します。

#### 事前入力サービスを起動し、使用します {#start-and-use-the-prefill-service}

事前入力サービスを起動するには、JAR ファイルを [!DNL AEM Forms] web コンソールにアップロードし、サービスをアクティブ化します。サービスはアダプティブフォームエディターに表示されるようになります。事前入力サービスをアダプティブフォームに関連付けるには：

1. アダプティブフォームをフォームエディターで開き、フォームコンテナのプロパティパネルを開きます。
1. プロパティコンソールで、[!DNL AEM Forms] コンテナ／基本／事前入力サービスに移動します。
1. Default Prefill Service を選択し、「**[!UICONTROL 保存]**」をクリックします。サービスはフォームに関連付けられます。

<!-- ## Prepopulate data at client {#prefill-at-client}

When you prefill an Adaptive Form, the [!DNL AEM Forms] server merges data with an Adaptive Form and delivers the filled form to you. By default, the data merge action takes place at the server.

You can configure the [!DNL AEM Forms] server to perform the data merge action at the client instead of the server. It significantly reduces the time required to prefill and render Adaptive Forms. By default, the feature is disabled. You can enable it from the Configuration Manager or command line.

* To enable or disable from configuration manager:
  1. Open AEM Configuration Manager.
  1. Locate and open the Adaptive Form and Interactive Communication Web Channel Configuration
  1. Enable the Configuration.af.clientside.datamerge.enabled.name option
* To enable or disable from the command line:
  * To enable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  * To disable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   To take full advantage of the prepopulate data at client option, update your prefill service to return [FileAttachmentMap](https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) and [CustomContext](https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) -->