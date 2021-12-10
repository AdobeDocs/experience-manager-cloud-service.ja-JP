---
title: 繰り返し可能なセクションを使用したフォームの作成
seo-title: Creating forms with repeatable sections
description: 繰り返し可能なセクションとは、フォームに動的に追加または削除できるパネルのことです。
seo-description: Repeatable sections are panels that can be dynamically added or removed to a form.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 100%

---


# 繰り返し可能なセクションを使用したフォームの作成 {#creating-forms-with-repeatable-sections}

繰り返し可能なセクションとは、フォームに動的に追加または削除できるパネルのことです。

例えば、就職活動の場合、求職者は前職の詳細を提供するにあたって、会社名、役職、担当していたプロジェクト、その他備考などに情報を区分けします。すべての雇用者の情報は当然異なっていますが、セクションの構成は似通っています。そのような場合には、求人応募フォームに雇用者セクションを 1 つ設けておいて、さらに必要に応じてそのようなセクションを動的に追加できるようにしておきます。動的に追加できるこれらのセクションを、繰り返し可能なセクションといいます。

以下に挙げる方法のいずれかによって、繰り返し可能なパネルを作成できます。

## スクリプトを介したインスタンスマネージャーの使用 {#using-instance-manager-via-scripts-nbsp}

1. 編集モードで、パネルを選択し、![cmppr](assets/cmppr.png) をタップします。サイドバーのプロパティで「**[!UICONTROL パネルを繰り返し可能にする]**」を有効にします。「**[!UICONTROL 最大値]**」および「**[!UICONTROL 最小値]**」フィールドの値を指定します。

   「最大値」フィールドでは、パネルがそのページに表示される最大の回数を指定します。パネルの表示回数を制限しないように設定するには、「最大値」フィールドに「-1」を指定します。

   「最小値」フィールドでは、パネルがそのフォームに表示される最小の回数を指定します。「最小値」フィールドを「0」に設定すると、後で、レンダリング完了後にスクリプトを使用してすべてのインスタンスを削除できます。

   >[!NOTE]
   >
   >繰り返しを許可しないパネルを作成するには、「最大値」フィールドと「最小値」フィールドの値を 1 に設定します。アコーディオンレイアウトでは、「最大値」フィールドに「-1」を指定することはできません。この場合、任意の高い数値を入力することで、最大値を制限しない設定と同様の動作を実現します。

1. パネルの親要素に繰り返しを許可する場合は、繰り返し可能なパネルのインスタンスを管理するために、追加ボタンおよび削除ボタンが親要素に含まれている必要があります。親要素にボタンを挿入し、ボタン上のスクリプトを有効にするには、以下の手順を実行します。

   1. サイドバーから、ボタンコンポーネントをパネルの親要素にドラッグ＆ドロップします。コンポーネントを選択して、「![編集ルール](assets/edit-rules.png)」をタップします。ルールエディターでボタンのルールが開きます。
   1. ルールエディターウィンドウで、「**作成**」をクリックします。

      フォームオブジェクトと関数の行で、「**ビジュアルエディター**」を選択します。

      1. ルール領域の WHEN で、**クリックされた**&#x200B;ステートを選択します。
      1. THEN で、以下の操作を行います。

         * 「パネルを追加」ボタンを作成するには、「**インスタンスを追加**」を選択し、![toggle-side-panel](assets/toggle-side-panel.png) を使用してパネルをドラッグ＆ドロップするか、「**オブジェクトをドロップまたは次から選択**」を使用してパネル選択します。
         * 「パネルを削除」ボタンを作成するには、「**インスタンスを削除**」を選択し、![toggle-side-panel](assets/toggle-side-panel.png) を使用してパネルをドラッグ＆ドロップするか、「**オブジェクトをドロップまたは次から選択**」を使用してパネル選択します。

      フォームオブジェクトと関数の行で、「**コードエディター**」を選択します。「**ルールを編集**」をクリックして、コード領域で以下の操作を行います。

      * 「パネルを追加ボタン」を作成するには、`this.panel.instanceManager.addInstance()` を指定します。
      * 「パネルを削除」ボタンを作成するには、`this.panel.instanceManager.removeInstance(this.panel.instanceIndex)` を指定します。

      「**完了**」をクリックします。

      >[!NOTE]
      >
      >フィールドが繰り返し可能なパネルに属する場合、スクリプトで名前を指定して直接アクセスすることはできません。フィールドにアクセスするには、`InstanceManager` の `instances` API を使用してフィールドが属している繰り返し可能インスタンスを指定します。`InstanceManager` の `instances` API を使用するための構文を以下に示します。
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
      >詳しくは、[AEM Forms Java API リファレンス](https://adobe.com/go/learn_aemforms_documentation_63_jp)の「Class: InstanceManager#instances」を参照してください。

      >[!NOTE]
      >
      >パネルのすべてのインスタンスがアダプティブフォームから削除されている場合、削除されたパネルのインスタンスを 1 つ追加するには、_panelName 構文を使用してパネルのインスタンスマネージャーを取得し、インスタンスマネージャーの addInstance API を使用して、削除されたインスタンスを追加します。例えば、_panelName.addInstance() です。削除されたパネルのインスタンスを 1 つ追加します。



## 親パネルに対するアコーディオンレイアウトの使用  {#using-the-accordion-layout-for-the-parent-panel-nbsp}

パネルには、様々なレイアウトオプションがあります。アコーディオンデザインオプションのレイアウトでは、繰り返し可能なパネルをすぐに使用できます。アコーディオンデザインオプションのレイアウトで繰り返し可能なパネルを使用するには、以下の手順を実行します。

1. 繰り返しを許可するパネルの親で、![cmppr](assets/cmppr.png) をタップします。サイドバーにプロパティが表示されます。**レイアウト**&#x200B;ドロップダウンで、「**アコーディオン**」を選択します。
1. 繰り返しを許可するパネルで、![cmppr](assets/cmppr.png) をタップします。サイドバーにパネルプロパティが表示されます。「**パネルを繰り返し可能にする**」タブを有効にし、「**最大値**」および「**最小値**」フィールドの値を指定します。

   これで、プラス（+）ボタンと削除（![delete-panel](assets/delete-panel.png)）ボタンを使用して、パネルの追加と削除を行うことができるようになりました。

## フォームテンプレート（XDP／XSD）からのサブフォームの繰り返しの使用  {#using-repeating-subforms-from-form-template-xdp-xsd}

繰り返し可能なサブフォームは、アダプティブフォームの繰り返し可能なパネルに似ています。[!DNL AEM Forms] Designer で繰り返しのサブフォームを作成するには、以下の手順を実行します。

1. 階層パレットで、繰り返したいサブフォームの親サブフォームを選択します。
1. オブジェクトパレットの「サブフォーム」タブをクリックし、コンテンツリストで「フローレイアウト」を選択します。
1. 繰り返すサブフォームを選択します。
1. オブジェクトパレットで「サブフォーム」タブをクリックし、コンテンツリストで「配置済み」または「フローレイアウト」を選択します。
1. 「連結」タブをクリックして、「各データアイテムについてサブフォームを繰り返す」を選択します。
1. 繰り返し回数の最小値を指定する場合は、「最小値」を選択して関連するボックスに数値を入力します。このオプションを 0 に設定した場合は、データ結合時にサブフォーム内のオブジェクトにデータが提供されないと、フォームのレンダリング時にサブフォームが配置されません。
1. サブフォームの繰り返し回数の最大値を指定する場合は、「最大値」を選択して、関連するボックスに数値を入力します。「最大値」に値を入力しなければ、サブフォームの繰り返し回数は無制限になります。
1. サブフォームの繰り返し回数をデータ量に関係なく指定する場合は、「初期値」オプションを選択して、関連するボックスに数値を入力します。このオプションを選択した場合は、データが使用できないときやデータ項目が指定された「初期値」の値より少ないときにも、フォーム上に空のサブフォームインスタンスが配置されます。
1. 親サブフォームにボタンを 2 つ追加します。ひとつはインスタンスの追加に、もうひとつは繰り返し可能なサブフォームのインスタンスの削除に使用します。詳しい手順については、「[アクションの作成](https://help.adobe.com/ja_JP/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2)」を参照してください。
1. ここで、アダプティブフォームにフォームテンプレートをリンクします。詳しい手順については、「[テンプレートに基づくアダプティブフォームの作成](creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template)」を参照してください。
1. 手順 9 で作成したボタンを使用して、サブフォームを追加および削除します。

添付の .zip ファイルには、繰り返し可能なサブフォーラムのサンプルが含まれています。

[ファイルを入手](assets/samplerepeatablesubform.zip)

## XML Schema（XSD）の繰り返し設定の使用  {#using-repeat-settings-of-an-xml-schema-xsd-br}

XML スキーマから、および任意の複合タイプ要素の minOccurs および maxOccurs プロパティから、繰り返し可能なパネルを作成できます。XML スキーマについて詳しくは、「[XML スキーマをフォームモデルとして使用するアダプティブフォームの作成](adaptive-form-xml-schema-form-model.md)」を参照してください。

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

>[!NOTE]
>
>アコーディオンデザインではないレイアウトの場合、インスタンスを追加および削除するには、アダプティブフォームのボタンコンポーネントを使用します。
