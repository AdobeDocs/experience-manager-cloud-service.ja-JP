---
title: アダプティブフォームのコアコンポーネントで繰り返し可能なパネルを作成する方法
description: アダプティブフォームで繰り返し可能なセクションまたはフィールドを作成する方法を説明します。
role: Architect, Developer, Admin, User
feature: Adaptive Forms, Core Components
exl-id: 02521bf3-83c1-40a0-8fe6-23af240727e9
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '1258'
ht-degree: 100%

---

# 繰り返し可能なセクション（コアコンポーネント）を使ったフォームの作成 {#repeat-panel}


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-forms-repeatable-sections.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

繰り返し可能なセクションとは、同じデータの複数のインスタンスに関する情報を収集するために、複製または繰り返し実行できるフォームの一部を指します。

例えば、ある人物の職歴に関する情報を収集するために使用するフォームについて考えてみましょう。前の各職務の詳細を取得するための繰り返し可能なセクションがある場合があります。繰り返し可能なセクションには、通常、会社名、役職、雇用日、職務責任などのフィールドが含まれます。繰り返し可能なセクションの複数のインスタンスを追加して、保持している各ジョブに関する情報を入力できます。

![繰り返し可能性](/help/forms/assets/repeatable-adaptive-form-example.gif)

この記事を最後まで読むと、以下の操作を実行できるようになります。

* アダプティブフォーム内に繰り返し可能なセクションを作成する
* アダプティブフォームコンポーネントの繰り返し回数の最小数または最大数を設定する
* 繰り返し可能なセクションに対して追加または削除のアクションを設定するために、ルールエディターを使用する

[パネル](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)、[アコーディオン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=ja)、[水平タブ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=ja)、[垂直タブ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)または[ウィザード](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=ja)コンポーネントを使用して、アダプティブフォームのセクションを繰り返し可能にすることができます。これらのコンポーネントに子コンポーネントを追加して、フォーム内に繰り返し可能なセクションを作成できます。


このドキュメントの例は、[パネル](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)コンポーネントに基づいています。同じ手順を実行して、[パネル](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)、[アコーディオン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=ja)、[水平タブ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=ja)、[垂直タブ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)または[ウィザード](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=ja)コンポーネントを繰り返し可能にすることができます。

## フォーム内の繰り返し可能なセクションの追加または削除 {#add-or-delete-repeatable-section-in-panel-container}

フォーム内でパネルを繰り返したり、繰り返し可能なパネルを削除したりする場合、フォーム作成者はボタンコンポーネントを使用してパネルのインスタンスを追加または削除します。フォームに繰り返し可能なセクション（パネル）を追加または削除するには、次の手順を実行します。

* [パネルコンテナを繰り返し可能にする](#make-panel-container-repeatable)
* [繰り返し可能なセクションを追加する](#add-repeatable-section-using-instance-manager-via-scripts)
* [繰り返し可能なセクションを削除する](#delete-repeatable-section-using-instance-manager-via-scripts)

### パネルコンテナを繰り返し可能にする {#make-panel-container-repeatable}

![「アクセシビリティ」タブ](/help/forms/assets/repeat-panel.png)

パネルを繰り返し可能にするには、次の手順を実行します。

1. パネルコンテナを選択して、![cmppr](/help/forms/assets/cmppr.png) をクリックします。
1. **繰り返しパネル**&#x200B;をクリックし、**パネルを繰り返し可能にする**&#x200B;のスイッチをオンに切り替えます。
1. 最小繰り返し可能セクションの必要に応じて&#x200B;**最小繰り返し回数**&#x200B;を設定します。パネルを繰り返しない場合、または繰り返しパネルを削除するには、**最小繰り返し回数**&#x200B;を 0 に設定できます。デフォルトでは、最小繰り返し回数の値は 0 です。
1. **最大繰り返し回数**&#x200B;を設定して、必要な回数パネルを繰り返します。デフォルトの値は無限です。

   >[!NOTE]
   >
   > 
   > * 最小繰り返し回数を -ve 値にすることはできません。
   > * 繰り返しを許可しないパネルを作成するには、最大値フィールドと最小値フィールドの値を 1 に設定します。

### インスタンスマネージャーを使用した繰り返し可能なセクションの追加（スクリプトを使用） {#add-repeatable-section-using-instance-manager-via-scripts}

パネルの親要素に繰り返しを許可する場合は、パネルの繰り返しインスタンスを管理するために追加ボタンが含まれている必要があります。親要素にボタンを挿入し、ボタン上のスクリプトを有効にするには、以下の手順を実行します。

1. **ボタンコンポーネント**&#x200B;をパネルの親要素に追加します。以下のビデオの例では、ラベル名 **Add** とフィールド名 **AddPanel** のボタンコンポーネントが使用されています。コンポーネントを選択して、「![編集ルール](/help/forms/assets/edit-rules.png)」をクリックします。ルールエディターでボタンコンポーネントのルールが開きます。
1. ルールエディターウィンドウで、「**作成**」をクリックします。

   フォームオブジェクトと関数の行で、「**ビジュアルエディター**」を選択します。

   1. ルール領域の WHEN で、 **クリックされた** ステートを選択します。
   1. THEN で、「**インスタンスを追加**」を選択し、![toggle-side-panel](/help/forms/assets/toggle-side-panel.png) を使用してパネルをドラッグ＆ドロップするか、「**オブジェクトをドロップまたは次から選択**」を使用して選択します。

   フォームオブジェクトと関数の行で、「**コードエディター**」を選択します。「**ルールを編集**」をクリックして、コード領域で以下の操作を行います。

   * 「パネルを追加ボタン」を作成するには、`this.panel.instanceManager.addInstance()` を指定します。

   「**完了**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)


### インスタンスマネージャー（スクリプト経由）を使用した繰り返し可能なセクションの削除 {#delete-repeatable-section-using-instance-manager-via-scripts}

パネルの親要素には、繰り返し可能なパネルのインスタンスを削除するために削除ボタンが含まれている必要があります。親要素にボタンを挿入し、ボタン上のスクリプトを有効にして反復可能なパネルを削除するには、以下の手順を実行します。

1. **ボタンコンポーネント**&#x200B;をパネルの親要素に追加します。下のビデオでは、ラベル名 **DELETE** が付いたボタンコンポーネントおよびフィールド名 **DeletePanel** が使用されます。コンポーネントを選択して、「![編集ルール](/help/forms/assets/edit-rules.png)」をクリックします。ルールエディターでボタンコンポーネントのルールが開きます。
1. ルールエディターウィンドウで、「**作成**」をクリックします。

   フォームオブジェクトと関数の行で、「**ビジュアルエディター**」を選択します。

   1. ルール領域の WHEN **DeletePanel** で、**クリックされた**&#x200B;ステートを選択します。
   1. THEN で、「**インスタンスを削除**」を選択し、![toggle-side-panel](/help/forms/assets/toggle-side-panel.png) を使用してパネルをドラッグ＆ドロップするか、「**オブジェクトをドロップまたは次から選択**」を使用して選択します。

   フォームオブジェクトと関数の行で、「**コードエディター**」を選択します。「**ルールを編集**」をクリックして、コード領域で以下の操作を行います。

   * 「パネルを削除」ボタンを作成するには、`this.panel.instanceManager.removeInstance(this.panel.instanceIndex)` を指定します。

   「**完了**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3421620/adaptive-forms-repeatable-sections)

>[!NOTE]
>
>フィールドが繰り返し可能なパネルに属する場合、スクリプトで名前を指定して直接アクセスすることはできません。フィールドにアクセスするには、`instances` の `InstanceManager` API を使用してフィールドが属している繰り返し可能インスタンスを指定します。`instances` の API `InstanceManager`を使用するための構文を以下に示します。
>
>
>`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
>
>
>例えば、テキストボックスを持つ繰り返し可能なパネルを含むアダプティブフォームを作成するとします。このフォームに 3 つの繰り返し可能テキストボックスを事前入力するには、以下の xml が必要です。
>
>
>`<panel1><textbox1>AA1</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA2</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA3</panel1></textbox1>`
>
>
>AA1 データを読み込むには、以下のように指定します。
>
>
>`Panel1.instanceManager.instances[0].textbox.value`
>
>
>AA2 データを読み込むには、以下のように指定します。
>
>
>`Panel1.instanceManager.instances[1].textbox.value`
>
>
>

>[!NOTE]
>
> パネルのすべてのインスタンスがアダプティブフォームから削除されている場合、削除されたパネルのインスタンスを追加するには、_panelName 構文を使用してパネルのインスタンスマネージャをキャプチャし、インスタンスマネージャーの addInstance API を使用して削除されたインスタンスを追加します。例えば、「_panelName.addInstance()」です。削除されたパネルのインスタンスを 1 つ追加します。

## フォームテンプレート（XDP／XSD）からのサブフォームの繰り返しの使用  {#using-repeating-subforms-from-form-template-xdp-xsd}

繰り返し可能なサブフォームは、アダプティブフォームの繰り返し可能なパネルに似ています。AEM Forms Designer で繰り返しのサブフォームを作成するには、以下の手順を実行します。

1. 階層パレットで、繰り返したいサブフォームの親サブフォームを選択します。
1. オブジェクトパレットの「サブフォーム」タブをクリックし、コンテンツリストで「フローレイアウト」を選択します。
1. 繰り返すサブフォームを選択します。
1. オブジェクトパレットで「サブフォーム」タブをクリックし、コンテンツリストで「配置済み」または「フローレイアウト」を選択します。
1. 「連結」タブをクリックして、「各データアイテムについてサブフォームを繰り返す」を選択します。
1. 繰り返し回数の最小値を指定する場合は、「最小値」を選択して関連するボックスに数値を入力します。このオプションを 0 に設定した場合は、データ結合時にサブフォーム内のオブジェクトにデータが提供されないと、フォームのレンダリング時にサブフォームが配置されません。
1. サブフォームの繰り返し回数の最大値を指定する場合は、「最大値」を選択して、関連するボックスに数値を入力します。「最大値」に値を入力しなければ、サブフォームの繰り返し回数は無制限になります。
1. サブフォームの繰り返し回数をデータ量に関係なく指定する場合は、「初期値」オプションを選択して、関連するボックスに数値を入力します。このオプションを選択した場合は、データが使用できないときやデータ項目が指定された「初期値」の値より少ないときにも、フォーム上に空のサブフォームインスタンスが配置されます。
1. 親サブフォームにボタンを 2 つ追加します。ひとつはインスタンスの追加に、もうひとつは繰り返し可能なサブフォームのインスタンスの削除に使用します。詳しい手順については、「[アクションの作成](https://help.adobe.com/ja_JP/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2)」を参照してください。
1. ここで、アダプティブフォームにフォームテンプレートをリンクします。手順について詳しくは、[テンプレートに基づいてアダプティブフォームを作成](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=ja#create-an-adaptive-form-based-on-an-xfa-form-template)を参照してください。
1. 手順 9 で作成したボタンを使用して、サブフォームを追加および削除します。

添付の .zip ファイルには、繰り返し可能なサブフォーラムのサンプルが含まれています。

[ファイルを入手](/help/forms/assets/samplerepeatablesubform.zip)

## XML スキーマ（XSD）の繰り返し設定の使用  {#using-repeat-settings-of-an-xml-schema-xsd-br}

XML スキーマ、または任意の複合タイプ要素の minOccurs および maxOccurs プロパティから、繰り返し可能なパネルを作成できます。XML スキーマについて詳しくは、[XML スキーマをフォームモデルとして使用してアダプティブフォームを作成](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-xml-schema-form-model.html?lang=ja)を参照してください。

以下のコードでは、`SampleType` パネルで minOccurs および maxOccurs プロパティが使用されています。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```


## 関連トピック {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
>* [Create style or themes for your forms](using-themes-in-core-components.md)
>* [Add dynamic behavior to forms using the rule editor](rule-editor.md)
>* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/console-layout.md)

-->