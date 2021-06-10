---
title: CIF製品およびカテゴリピッカーの使用
description: 顧客コマースコンポーネントでCIF製品およびカテゴリピッカーを使用して、作成者やマーケターがコマース製品およびカタログデータを効率的に操作できるようにする方法を説明します。
sub-product: コマース
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: コマース統合フレームワーク
exl-id: 30f1f263-1b78-46ae-99ed-61861c488b2a
source-git-commit: 764d70db8026bad1683fffdb44092f1d2a8e8d28
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 1%

---

# AEM Content &amp; Commerce Authoring Pickers {#cif-pickers}

AEM Content &amp; Commerce Authoringは、AEMの作成者やマーケターがコマース製品のデータやカタログを効率的に操作するのに役立つ、一連のオーサリングツールを提供します。 製品ピッカーとカテゴリピッカーは、CIFアドオンの一部で、CIFコアコンポーネントで使用されます。 プロジェクトでは、任意のコンポーネントダイアログでこれらのピッカーを使用して、製品やカテゴリを選択できます。

## 製品ピッカー {#product-picker}

プロジェクトコンポーネントで製品ピッカーを使用するには、開発者がコンポーネントダイアログに`commerce/gui/components/common/cifproductfield`を追加する必要があります。 例えば、cq:dialogに対して次を使用します。

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

製品フィールドを使用すると、ユーザーが選択したい製品に別の表示で移動できます。 デフォルトでは、製品フィールドは製品のIDを返しますが、`selectionId`属性を使用して設定できます。

製品ピッカーフィールドでは、次のオプションのプロパティをサポートしています。

- selectionId(id、uid、sku、slug、combinedSlug、combinedSku) — ピッカーが返す製品属性を選択できます（デフォルト= id）。 skuを使用すると、選択した製品のskuが返され、 combinedSkuを使用すると、base#variantのような文字列と、基本製品および選択したバリアントのskuが返されます。基本製品が選択されている場合は、単一のskuが返されます。
- filter (folderOrProduct, folderOrProductOrVariant) — 製品ツリー内を移動する際に、ピッカーでレンダリングするコンテンツをフィルタリングします。 folderOrProduct — フォルダーと製品をレンダリングします。 folderOrProductOrVariant — フォルダー、製品および製品バリアントをレンダリングします。 製品または製品バリアントがレンダリングされると、ピッカーで選択できるようになります。 （デフォルト= folderOrProduct）
- multiple (true、false) - 1つまたは複数の製品の選択を有効にします（デフォルト= false）
- emptyText — ピッカーフィールドの空のテキスト値を設定します

また、`name`、`fieldLabel`、`fieldDescription`などの標準のダイアグログフィールドプロパティもサポートされています。

>[!CAUTION]
>
>`cifproductfield`コンポーネントには`cif.shell.picker` clientlibが必要です。 clientlibをダイアログに追加するには、 extraClientlibsプロパティを使用します。

`cifproductfield`の完全な動作例は、[CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml)プロジェクトにあります。 AEMコアコンポーネントのドキュメントの[ダイアログ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs)のカスタマイズも参照してください。

## カテゴリピッカー{#category-picker}

カテゴリピッカーは、製品ピッカーと同様の方法で、コンポーネントダイアログでも使用できます。

次のスニペットをcq:dialog設定で使用できます。

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

カテゴリピッカーフィールドでは、次のオプションのプロパティをサポートしています。

- selectionId(id, uid, slug, idAndUrlPath, uidAndUrlPath) — ピッカーが返すカテゴリ属性を選択できます（デフォルト= id）。 idAndUrlPathとuidAndUrlPathは、 |文字の例：1|men/tops
- multiple (true、false) - 1つまたは複数のカテゴリの選択を有効にします（デフォルト= false）

また、`name`、`fieldLabel`、`fieldDescription`などの標準のダイアグログフィールドプロパティもサポートされています。

>[!CAUTION]
>
>`cifproductfield`コンポーネントと同じ`cifcategoryfield`コンポーネントにも`cif.shell.picker` clientlibが必要です。 clientlibをダイアログに追加するには、`extraClientlibs`プロパティを使用します。 AEMコアコンポーネントのドキュメントの[ダイアログ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs)のカスタマイズを参照してください。

`cifcategoryfield`の完全な動作例は、[CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)プロジェクトにあります。
