---
title: CIF 製品およびカテゴリピッカーの使用
description: 顧客コマースコンポーネントで CIF 製品およびカテゴリピッカーを使用して、作成者やマーケターがコマース製品やカタログのデータを効率的に操作できるようにサポートする方法を説明します。
sub-product: コマース
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: コマース統合フレームワーク
exl-id: 30f1f263-1b78-46ae-99ed-61861c488b2a
source-git-commit: 2e0a2b543fe0b6302a5dd62055f89a8f30427e6b
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 83%

---

# AEM Content &amp; Commerce Authoring ピッカー {#cif-pickers}

AEM Content &amp; Commerce Authoring には、AEM の作成者やマーケターがコマース製品のデータやカタログを効率的に操作するのに役立つ一連のオーサリングツールが用意されています。製品ピッカーとカテゴリピッカーは CIF アドオンの一部で、CIF コアコンポーネントで使用されます。プロジェクトでは、任意のコンポーネントダイアログでこれらのピッカーを使用して、製品やカテゴリを選択できます。

## 製品ピッカー {#product-picker}

プロジェクトコンポーネントで製品ピッカーを使用するには、開発者がコンポーネントダイアログに `commerce/gui/components/common/cifproductfield` を追加する必要があります。例えば、cq:dialog:に対して次のように使用します。

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

製品フィールドを使用すると、ユーザーが選択したい製品に様々なビューを使用して移動できます。デフォルトでは、製品フィールドは製品の ID を返しますが、`selectionId` 属性を使用して設定できます。

製品ピッカーフィールドでは、次のオプションプロパティをサポートしています。

- selectionId（id、uid、sku、slug、combinedSlug、combinedSku）- ピッカーが返す製品属性を選択できます（デフォルトは id）。sku を使用する場合は、選択した製品の sku が返され、combinedSku を使用する場合は、base#variant のような文字列と、基本製品および選択したバリアントの sku が返されます。基本製品が選択されている場合は、単一の sku が返されます。
- filter（folderOrProduct、folderOrProductOrVariant）- 製品ツリー内を移動する際にピッカーでレンダリングするコンテンツをフィルタリングします。folderOrProduct - フォルダーと製品をレンダリングします。folderOrProductOrVariant - フォルダー、製品および製品バリアントをレンダリングします。製品または製品バリアントがレンダリングされる場合は、ピッカーでも選択できるようになります（デフォルトは folderOrProduct）。
- multiple（true、false）- 1 つまたは複数の製品の選択を有効にします（デフォルトは false）。
- emptyText - ピッカーフィールドの空のテキスト値を設定します。

また、`name`、`fieldLabel`、`fieldDescription` などの標準のダイアグログフィールドプロパティもサポートされています。

>[!CAUTION]
>
>`cifproductfield` コンポーネントには クライアントライブラリが必要です。`cif.shell.picker`ダイアログにクライアントライブラリを追加するには、extraClientlibs プロパティを使用します。
>[!CAUTION]
>
>CIFコアコンポーネントバージョン2.0.0以降、`id`のサポートは削除され、`uid`に置き換えられました。 製品IDとして`sku`または`slug`を使用することを強くお勧めします。 アドビでは、CIFコアコンポーネントバージョン1.xを使用するプロジェクトに対してのみ`id`を引き続きサポートします。

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

- selectionId(id, uid, slug, urlPath, idAndUrlPath _（非推奨）_, uidAndUrlPath _（非推奨）_) — ピッカーから返されるカテゴリ属性を選択できます（デフォルト= id）。
- multiple（true、false）- 1 つまたは複数のカテゴリの選択を有効にします（デフォルトは false）。

また、`name`、`fieldLabel`、`fieldDescription` などの標準のダイアグログフィールドプロパティもサポートされています。

>[!CAUTION]
>
>`cifproductfield` コンポーネントと同様に、`cifcategoryfield` コンポーネントにも クライアントライブラリが必要です。`cif.shell.picker`ダイアログにクライアントライブラリを追加するには、`extraClientlibs` プロパティを使用します。AEM コアコンポーネントドキュメントの[ダイアログのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs)を参照してください。
>[!CAUTION]
>
>CIFコアコンポーネントバージョン2.0.0以降、`id`のサポートは削除され、`uid`に置き換えられました。 カテゴリ識別子として`uid`または`urlPath`を使用することを強くお勧めします。 CIFコアコンポーネントバージョン1.xを使用するプロジェクトでのみ、引き続き`id`と`idAndUrlPath`をサポートします。

完全に動作する `cifcategoryfield` の例は、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)プロジェクトにあります。
