---
title: アダプティブフォームのコアコンポーネントで繰り返し可能なパネルを作成する方法
description: アダプティブフォームで繰り返し可能なセクションまたはフィールドを作成する方法を説明します。
role: Architect, Developer, Admin, User
exl-id: 02521bf3-83c1-40a0-8fe6-23af240727e9
source-git-commit: defeee2fee42c6274c71438d6f9fde6e49a05081
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 45%

---

# 繰り返し可能なセクション（コアコンポーネント）を含むフォームの作成 {#repeat-panel}


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-forms-repeatable-sections.html?lang=en) |
| AEM as a Cloud Service | この記事 |

繰り返し可能なセクションとは、同じデータの複数のインスタンスに関する情報を収集するために、複製または繰り返し実行できるフォームの一部を指します。

例えば、ある人物の職場体験に関する情報を収集するために使用するフォームについて考えてみましょう。 前の各ジョブの詳細をキャプチャするための繰り返し可能なセクションを用意することができます。 繰り返し可能なセクションには、通常、会社名、役職、雇用日、職責などのフィールドが含まれます。 繰り返し可能なセクションの複数のインスタンスを追加して、保持している各ジョブに関する情報を入力できます。

![再現性](/help/forms/assets/repeatable-adaptive-form-example.gif)

この記事を最後まで読むと、次の内容を習得できます。

* アダプティブフォーム内に繰り返し可能なセクションを作成する
* アダプティブフォームコンポーネントの繰り返し回数の最小数または最大数を設定する
* 繰り返し可能なセクションに対して追加または削除のアクションを設定するには、ルールエディターを使用します

以下を使用すると、 [パネル](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html), [アコーディオン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [水平タブ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)または [ウィザード](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html) アダプティブフォームのセクションを繰り返し可能にするコンポーネント パネル、アコーディオン、水平タブ、またはウィザードコンポーネントに子コンポーネントを追加して、フォーム内に繰り返し可能なセクションを作成できます。


このドキュメントの例は、 [パネル](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html) コンポーネント。 同じ手順を実行して、 [アコーディオン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [水平方向のタブ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)、および [ウィザード](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html) コンポーネントは繰り返し可能です。

## フォーム内の繰り返し可能なセクションの追加または削除 {#add-or-delete-repeatable-section-in-panel-container}

フォーム内でパネルを繰り返したり、繰り返し可能なパネルを削除したりする場合、フォーム作成者はボタンコンポーネントを使用してパネルのインスタンスを追加または削除します。 フォームに繰り返し可能なセクション（パネル）を追加または削除するには、次の手順を実行します。

* [パネルコンテナを繰り返し可能にする](#make-panel-container-repeatable)
* [繰り返し可能なセクションを追加](#add-repeatable-section-using-instance-manager-via-scripts)
* [繰り返し可能なセクションの削除](#delete-repeatable-section-using-instance-manager-via-scripts)

### パネルコンテナを繰り返し可能にする {#make-panel-container-repeatable}

![「アクセシビリティ」タブ](/help/forms/assets/repeat-panel.png)

パネルを繰り返し可能にするには、次の手順に従います。
1. パネルコンテナを選択し、 ![cmppr](/help/forms/assets/cmppr.png).
1. 次をクリック： **繰り返しパネル** 切り替えボタンをオンにして、 **パネルを繰り返し可能にする**.
1. 設定 **最小繰り返し** 繰り返し可能な最小セクションに必要に応じて、 **最小繰り返し** を 0 に設定すると、繰り返し使用されるパネルが削除され、パネルが非レプリケーションの場合は削除されます。 デフォルトでは、最小繰り返しの値は 0 です。
1. 設定 **最大繰り返し** 必要な回数だけパネルを繰り返す場合は、デフォルトでは値は無限です。

   >[!NOTE]
   >
   > 
   > * 最小繰り返し回数を —ve 値にすることはできません。
   > * 繰り返し不可能なパネルを作成するには、最大フィールドと最小フィールドの値を 1 に設定します。

### インスタンスマネージャーを使用した繰り返し可能なセクションの追加（スクリプトを使用） {#add-repeatable-section-using-instance-manager-via-scripts}

繰り返しを許可するパネルの親には、パネルの繰り返しインスタンスを管理する追加ボタンが含まれている必要があります。 親要素にボタンを挿入し、ボタン上のスクリプトを有効にするには、以下の手順を実行します。

1. を追加します。 **ボタンコンポーネント** をパネルの親に追加します。 次のビデオの例では、ラベル名がのボタンコンポーネントが 1 つあります **追加** およびフィールド名 **AddPanel**、が使用されます。 コンポーネントを選択して、「![編集ルール](/help/forms/assets/edit-rules.png)」をタップします。ボタンコンポーネントのルールがルールエディターで開きます。
1. ルールエディターウィンドウで、「**作成**」をクリックします。

   フォームオブジェクトと関数の行で、「**ビジュアルエディター**」を選択します。

   1. ルール領域の WHEN で、 **クリックされた** ステートを選択します。
   1. 「THEN」で、「 **インスタンスを追加**&#x200B;をクリックし、 ![toggle-side-panel](/help/forms/assets/toggle-side-panel.png) を使用するか、 **オブジェクトをドロップするか、ここから選択します。**

   フォームオブジェクトと関数の行で、「**コードエディター**」を選択します。「**ルールを編集**」をクリックして、コード領域で以下の操作を行います。

   * 「パネルを追加ボタン」を作成するには、`this.panel.instanceManager.addInstance()` を指定します。

   「**完了**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)


### インスタンスマネージャー（スクリプト経由）を使用した繰り返し可能なセクションの削除 {#delete-repeatable-section-using-instance-manager-via-scripts}

繰り返し可能なパネルのインスタンスを削除するには、パネルの親に削除ボタンを含める必要があります。 親にボタンを挿入し、ボタン上のスクリプトを有効にして繰り返し可能なパネルを削除するには、次の手順を実行します。

1. を追加します。 **ボタンコンポーネント** をパネルの親に追加します。下のビデオでは、ラベル名が付いたボタンコンポーネントを **削除** およびフィールド名 **DeletePanel** が使用されます。 コンポーネントを選択して、「![編集ルール](/help/forms/assets/edit-rules.png)」をタップします。ボタンコンポーネントのルールがルールエディターで開きます。
1. ルールエディターウィンドウで、「**作成**」をクリックします。

   フォームオブジェクトと関数の行で、「**ビジュアルエディター**」を選択します。

   1. ルール領域で、WHEN **DeletePanel**、状態を選択 **クリック済み**.
   1. 「THEN」で、「 **インスタンスを削除**&#x200B;をクリックし、 ![toggle-side-panel](/help/forms/assets/toggle-side-panel.png) を使用するか、 **オブジェクトをドロップするか、ここから選択します。**

   フォームオブジェクトと関数の行で、「**コードエディター**」を選択します。「**ルールを編集**」をクリックして、コード領域で以下の操作を行います。

   * 「パネルを削除」ボタンを作成するには、`this.panel.instanceManager.removeInstance(this.panel.instanceIndex)` を指定します。

   「**完了**」をクリックします。
>[!VIDEO](https://video.tv.adobe.com/v/3421620/adaptive-forms-repeatable-sections)

>[!NOTE]
>
>フィールドが繰り返し可能なパネルに属する場合、スクリプトで名前を指定して直接アクセスすることはできません。フィールドにアクセスするには、`InstanceManager` の `instances` API を使用してフィールドが属している繰り返し可能インスタンスを指定します。`InstanceManager` の `instances` API を使用するための構文を以下に示します。
>
>
>`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
>
>
>例えば、繰り返し可能なパネルにテキストボックスが付いたアダプティブフォームを作成したとします。 このフォームに 3 つの繰り返し可能テキストボックスを事前入力するには、以下の xml が必要です。
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

<!-- 
>For more information, see: Class: InstanceManager#instances in [AEM Forms Java API reference](https://adobe.com/go/learn_aemforms_documentation_63).      
-->

>[!NOTE]
>
> パネルのすべてのインスタンスがアダプティブフォームから削除されているとき、削除されたパネルのインスタンスを 1 つ追加するには、_panelName 構文を使用してパネルのインスタンスマネージャをキャプチャし、インスタンスマネージャの addInstance API を使用して、削除されたインスタンスを追加します。例えば、_panelName.addInstance() です。削除されたパネルのインスタンスを 1 つ追加します。

<!--
![panel-repeatability-video](/help/adaptive-forms/assets/panel-repeatability-video.mp4)
-->

<!--

## Using the accordion layout for the parent panel &nbsp; {#using-the-accordion-layout-for-the-parent-panel-nbsp}

A panel has various layouts options. The Layout for accordian design option has out of the box support for repeatable panels. Perform the following steps to repeatable panel with Layout for accordian design option:

1. On the parent of panel to be repeated, tap ![cmppr](assets/cmppr.png). You can see the properties in the sidebar. In the **Layout** drop-down, select **Accordion**.
1. On a panel, which is to be repeated, tap ![cmppr](assets/cmppr.png). You can see the panel properties in the sidebar. Enable the **Make Panel Repeatable** tab, and specify value for the **Maximum** and **Minimum** fields.

   Now, you can use the plus (+) and delete ( ![delete-panel](assets/delete-panel.png)) buttons to add and remove the panels.

-->

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
1. 次に、フォームテンプレートをアダプティブフォームにリンクします。 詳細な手順については、 [テンプレートに基づくアダプティブフォームの作成](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=en#create-an-adaptive-form-based-on-an-xfa-form-template).
1. 手順 9 で作成したボタンを使用して、サブフォームを追加および削除します。

添付の .zip ファイルには、繰り返し可能なサブフォーラムのサンプルが含まれています。

[ファイルを入手](/help/forms/assets/samplerepeatablesubform.zip)

## XML スキーマ（XSD）の繰り返し設定の使用  {#using-repeat-settings-of-an-xml-schema-xsd-br}

XML スキーマ、または任意の複合タイプエレメントの minOccurs および maxOccurs プロパティから、繰り返し可能なパネルを作成できます。XML スキーマについて詳しくは、 [XML スキーマをフォームモデルとして使用してアダプティブフォームを作成する](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-xml-schema-form-model.html).

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


## 関連記事

* [アダプティブフォームの作成](creating-adaptive-form-core-components.md)
* [フォームのスタイルまたはテーマを作成する](using-themes-in-core-components.md)
* [ルールエディターを使用してフォームに動的な動作を追加する](rule-editor.md)
* [画面サイズやデバイスタイプに応じてフォームのレイアウトを設定する](/help/sites-cloud/authoring/features/responsive-layout.md)
