---
title: CIF商品とカテゴリの選択の使用
description: 作成者やマーケターがコマース商品やカタログデータを効率的に操作できるように、顧客コマースコンポーネントでCIF商品やカテゴリ選択を使用する方法を説明します。
sub-product: Commerce
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: Commerce Integration Framework
translation-type: tm+mt
source-git-commit: 0f2747190523613d2fa1f4710dee1c28d4a5148f
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# AEM Content &amp; Commerce Authoring Pickers {#cif-pickers}

AEM Content &amp; Commerce Authoringには、AEMの作成者やマーケティング担当者が商取引製品のデータやカタログを効率的に扱うのに役立つオーサリングツールが用意されています。 製品選択とカテゴリ選択はCIFアドオンの一部で、CIFコアコンポーネントで使用されます。 プロジェクトでは、任意のコンポーネントダイアログでこれらのピッカーを使用して、製品やカテゴリを選択できます。

## 製品ピッカー {#product-picker}

プロジェクトコンポーネントで製品選択を使用するには、開発者がコンポーネントダイアログに`commerce/gui/components/common/cifproductfield`を追加する必要があります。 例えば、cq:dialogには次を使用します。

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

製品フィールドでは、様々な表示を介して、選択したい製品にナビゲーションできます。 デフォルトでは、製品フィールドは製品のIDを返しますが、`selectionId`属性を使用して設定できます。

製品選択フィールドでは、次のオプションのプロパティを使用できます。

- selectionId (id、uid、sku、combinedSlug、combinedSku) — ピッカーから返す製品属性を選択できます（デフォルト= id）。 skuを使用すると、選択した製品のskuが返されます。combinedSkuを使用すると、base#variantのような文字列と、基本製品および選択したバリアントのskuが返されます。また、基本製品が選択されている場合は単一のskuが返されます。
- filter (folderOrProduct, folderOrProductOrVariant) — 製品ツリー内を移動する際にピッカーでレンダリングされるコンテンツをフィルターします。 folderOrProduct — フォルダーと製品をレンダリングします。 folderOrProductOrVariant — フォルダ、製品および製品のバリアントをレンダリングします。 製品または製品バリアントがレンダリングされると、ピッカーで選択できるようになります。 （デフォルト= folderOrProduct）
- multiple (true, false) - 1つまたは複数の製品を選択できるようにします（デフォルト= false）
- emptyText — ピッカーフィールドの空のテキスト値を設定します。

また、`name`、`fieldLabel`、`fieldDescription`などの標準的なダイアログフィールドプロパティもサポートされています。

`cifproductfield`コンポーネントにはcif.shell.picker clientlibが必要です。 clientlibをダイアログに追加するには、extraClientlibsプロパティを使用します。

`cifproductfield`の完全な実例は、[CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml)プロジェクトにあります。 AEMコアコンポーネントドキュメントの[ダイアログのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs)も参照してください。

## カテゴリ選択{#category-picker}

カテゴリ選択は、製品選択と同様の方法で、コンポーネントダイアログでも使用できます。

cq:dialogの設定では、次のスニペットを使用できます。

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

カテゴリ選択フィールドでは、次のオプションのプロパティがサポートされます。

- selectionId(id, uid, slug, idAndUrlPath, uidAndUrlPath) — ピッカーから返すカテゴリ属性を選択できます（デフォルト= id）。 idAndUrlPathとuidAndUrlPathは、カテゴリid/uidとurl_pathを 例1|men/topsのような|文字。
- multiple (true, false) - 1つまたは複数のカテゴリを選択できるようにします（デフォルト= false）

また、`name`、`fieldLabel`、`fieldDescription`などの標準的なダイアログフィールドプロパティもサポートされています。

`cifproductfield`コンポーネントと同様に、`cifcategoryfield`コンポーネントにもcif.shell.picker clientlibが必要です。 clientlibをダイアログに追加するには、`extraClientlibs`プロパティを使用します。 AEMコアコンポーネントのドキュメントの[ダイアログのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs)を参照してください。

`cifcategoryfield`の完全な実例は、[CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)プロジェクトにあります。
