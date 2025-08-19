---
title: CIF 製品およびカテゴリピッカーの使用
description: 顧客コマースコンポーネントで CIF 製品およびカテゴリピッカーを使用して、作成者やマーケターがコマース製品やカタログのデータを効率的に操作できるようにサポートする方法を説明します。
sub-product: Commerce
topics: Development
version: Experience Manager as a Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 30f1f263-1b78-46ae-99ed-61861c488b2a
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 98%

---


# AEM Content &amp; Commerce Authoring ピッカー {#cif-pickers}

AEM Content &amp; Commerce Authoring には、AEM の作成者やマーケターがコマース製品のデータやカタログを効率的に操作するのに役立つ一連のオーサリングツールが用意されています。製品ピッカーとカテゴリピッカーは CIF アドオンの一部で、CIF コアコンポーネントで使用されます。プロジェクトでは、任意のコンポーネントダイアログでこれらのピッカーを使用して、製品やカテゴリを選択できます。

## 製品ピッカー {#product-picker}

プロジェクトコンポーネントで製品ピッカーを使用するには、開発者がコンポーネントダイアログに `commerce/gui/components/common/cifproductfield` を追加する必要があります。例えば、`cq:dialog` には以下を使用します。

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

製品フィールドを使用すると、ユーザーが選択したい製品に、様々なビューを通じて移動できます。デフォルトでは、製品フィールドは製品の ID を返しますが、`selectionId` 属性を使用して設定できます。

製品ピッカーフィールドでは、次のオプションプロパティをサポートしています。

- selectionId（id、uid、sku、slug、combinedSlug、combinedSku）- ピッカーが返す製品属性を選択できます（デフォルトは id）。SKU を使用すると、選択した製品の SKU が返されます。combinedSku を使用すると、基本製品と選択したバリアントの SKU を含む、base#variant のような文字列が返されます。基本製品が選択されている場合は、単一の SKU が返されます。
- filter（folderOrProduct、folderOrProductOrVariant）- 製品ツリー内を移動する際にピッカーでレンダリングするコンテンツをフィルタリングします。folderOrProduct - フォルダーと製品をレンダリングします。folderOrProductOrVariant - フォルダー、製品および製品バリアントをレンダリングします。製品または製品バリアントがレンダリングされる場合は、ピッカーでも選択できるようになります（デフォルトは folderOrProduct）。
- multiple（true、false）- 1 つまたは複数の製品の選択を有効にします（デフォルトは false）。
- emptyText - ピッカーフィールドの空のテキスト値を設定します。

また、標準のダイアログボックスフィールドプロパティ（`name`、`fieldLabel` または `fieldDescription`）がサポートされています。

>[!CAUTION]
>
>`cifproductfield` コンポーネントには クライアントライブラリが必要です。`cif.shell.picker`ダイアログにクライアントライブラリを追加するには、extraClientlibs プロパティを使用します。

>[!CAUTION]
>
>CIF コアコンポーネントのバージョン 2.0.0 以降、`id` のサポートは削除され、`uid` に置き換わりました。アドビでは、製品識別子として `sku` または `slug` を使用することをお勧めします。アドビでは、CIF コアコンポーネントのバージョン 1.x を使用しているプロジェクトに対してのみ、`id` を引き続きサポートします。

完全に動作する `cifproductfield` の例は、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml)プロジェクトにあります。AEM コアコンポーネントドキュメントの[ダイアログのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=ja#customizing-dialogs)も参照してください。

## カテゴリピッカー {#category-picker}

カテゴリピッカーは、製品ピッカーと同様の方法で、コンポーネントダイアログでも使用できます。

次のスニペットを cq:dialog 設定で使用できます。

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

カテゴリピッカーフィールドでは、次のオプションプロパティをサポートしています。

- selectionId（id、uid、slug、urlPath、idAndUrlPath _（廃止予定）_、uidAndUrlPath _（廃止予定）_）- ピッカーが返すカテゴリ属性を選択できます（デフォルトは id）。
- multiple（true、false）- 1 つまたは複数のカテゴリの選択を有効にします（デフォルトは false）。

また、標準のダイアログボックスフィールドプロパティ（`name`、`fieldLabel` または `fieldDescription`）もサポートされています。

>[!CAUTION]
>
>`cifproductfield` コンポーネントと同様に、`cifcategoryfield` コンポーネントにも クライアントライブラリが必要です。`cif.shell.picker`ダイアログにクライアントライブラリを追加するには、`extraClientlibs` プロパティを使用します。AEM コアコンポーネントドキュメントの[ダイアログのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=ja#customizing-dialogs)を参照してください。

>[!CAUTION]
>
>CIF コアコンポーネントのバージョン 2.0.0 以降、`id` のサポートは削除され、`uid` に置き換わりました。アドビでは、カテゴリ識別子として `uid` または `urlPath` を使用することをお勧めします。アドビでは、CIF コアコンポーネントのバージョン 1.x を使用しているプロジェクトに対してのみ、`id` と `idAndUrlPath` を引き続きサポートします。

完全に動作する `cifcategoryfield` の例は、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)プロジェクトにあります。
