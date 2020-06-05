---
title: アクセス可能なWebページとサイトを作成するようにRTEを設定します。
description: Adobe Experience Managerでリッチテキストエディターを設定して、アクセシブルなサイトを作成する方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 78ec0ed2a1473797a07905baa346a83376779419
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 8%

---


# Configure RTE to create accessible sites {#configure-rte-accessible-sites}

Adobe Experience Managerは、画像の代替テキストなどの標準的なアクセシビリティ機能や、コンテンツの作成時にアクセスできる追加機能をサポートしています。 コンテンツ作成者は、リッチテキストエディター(RTE)を使用するコンポーネントでこれらの機能を使用します。 これには、見出しや段落要素から代替テキストや構造情報を追加するなどが含まれます。

RTEの一般的な設定の詳細については、RTEの [設定と、特定の機能に対するRTEプラグインの](rich-text-editor.md) 設定を参照してください [](configure-rich-text-editor-plug-ins.md)。

RTEプラグイン設定を使用して、アクセシビリティ関連機能を設定およびカスタマイズします。 例えば、基本要素を超えてサポートされ、デフォルトで提供される見出しレベルの数を拡張するなど、ブロックレベルのセマンティック要素を追加する場合に使用し `paraformat` ま `H1``H2``H3` す。 リッチテキストの編集は、オーサリングユーザーインターフェイスの多くのコンポーネントを使用して可能です。 一般的に使用されるコンポーネントは、テキスト、画像、ダウンロードなどです。

RTE機能は、多くのコンポーネントで使用できます。 主要なコンポーネントは `Text` コンポーネントです。

Experience Managerの `Text` コンポーネントの場合、次のスクリーンショットにリッチテキストエディターが表示され、以下を含む様々なプラグインが有効になってい `paraformat`ます。

![フルスクリーンモードのRTEテキストコンポーネント](assets/rte-toolbar-full-screen-mode.png)

## Configure the plugin features {#configuring-the-plugin-features}

RTEの設定手順については、「リッチテキストエディターの [設定](rich-text-editor.md) 」ページを参照してください。 この記事は次の内容を扱っています。

* [プラグインとその機能](rich-text-editor.md#aboutplugins)
* [設定の場所](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [プラグインをアクティブ化し、featuresプロパティを設定します](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [RTEの他の機能の設定](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

プラグインの一部またはすべての機能をアクティブにするには、CRXDE Liteの適切な `rtePlugins` サブブランチ内にプラグインを設定します。

![CRXDE Lite で rtePlugin の例を表示。](assets/chlimage_1-208.png)

### Example - Specify paragraph formats available in RTE selection field {#example-specifying-paragraph-formats-available-in-rte-selection-field}

意味的ブロックの新しい書式を選択可能にするには、次の手順を実行します。

1. 使用している RTE によって、[設定場所](rich-text-editor.md#understand-the-configuration-paths-and-locations)を特定し、移動します。
1. [プラグインをアク](rich-text-editor.md) ティブ化して、段落選択フィールドを有効にします [](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
1. [段落選択フィールドで、使用可能な書式を指定します](rich-text-editor.md)。
1. 段落書式は、RTEの選択フィールドからコンテンツ作成者が使用できます。

RTEで段落形式のオプションを使用して構造要素を利用できるExperience Managerは、アクセシブルなコンテンツの開発にとって有効な基盤となります。 コンテンツ作成者は、RTEを使用してフォントサイズや色などの関連属性の形式を設定できず、インライン形式を作成できません。 代わりに、見出しなどの適切な構造要素を選択し、[スタイル]オプションから選択したグローバルスタイルを使用する必要があります。 これにより、マークアップがきれいになり、独自のスタイルシートを使用して正しく構造化されたコンテンツを参照するユーザにとって、より多くのオプションが提供されます。

## ソース編集機能の使用 {#use-of-the-source-edit-feature}

In some cases, content authors will find it necessary to examine and adjust the HTML source code created using the RTE. For example, a piece of content created within the RTE may require additional markup to ensure compliance with WCAG 2.0. This can be done with the [source edit](rich-text-editor.md#aboutplugins) option of the RTE. この [`sourceedit` 機能はプラグインで指定でき `misctools` ます](rich-text-editor.md#aboutplugins)。

>[!CAUTION]
>
>Use the `sourceedit` feature carefully. タイピングの誤りやサポート対象外の機能は、問題を大きくする可能性があります。

<!--
TBD ENGREVIEW: Is this only applicable to Classic UI? 

## Adding Support for Additional HTML Elements and Attributes {#adding-support-for-additional-html-elements-and-attributes}

To further extend the accessibility features of Experience Manager, it is possible to extend the existing components based on the RTE (such as the `Text` and `Table` components) with additional elements and attributes.

The following procedure illustrates how to extend the `Table` component with a `Caption` element that provides information about a data table to assistive technology users:

### Example: Add a caption to a table properties dialog {#example-adding-the-caption-to-the-table-properties-dialog}

In the constructor of the `TablePropertiesDialog`, add an additional text input field that is used for editing the caption. Set the `itemId` to `caption` (the DOM attribute’s name) to automatically handle its content.

In a `Table`, set the attribute to the DOM element or or remove it from the DOM element. The dialog in the `config` object passed the value. Set or remove the DOM attributes using the corresponding `CQ.form.rte.Common` methods (`com` is a shortcut for `CQ.form.rte.Common`). Using `CQ.form.rte.Common` methods avoids common pitfalls with browser implementations.

>[!NOTE]
>
>This procedure is only suitable for the classic UI.

### Step-by-step instructions {#step-by-step-instructions}

1. Start CRXDE Lite. For example: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`. Create intermediate folders if those do not exist.

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` file to edit.

1. In the `constructor` method, before the mention of `var dialogRef = this;`, add the following code:

   ```javascript
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` file.

1. Add the following code at the end of the `transferConfigToTable` method:

   ```javascript
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. To save your changes, click **[!UICONTROL Save All]**.

## Best practices and limitations {#best-practices-limitations-tips}

* A plain text field is not the only type of input allowed for the value of the caption element. You can use any ExtJS widget, that provides the caption’s value through its `getValue()` method.
* To add editing capabilities for further additional elements and attributes, ensure that:

  * The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
  * The attribute is set and/or removed on the DOM element explicitly (`Table`).
-->

>[!MORELIKETHIS]
>
>* [WCAG基準のクイックガイド](/help/onboarding/accessibility/quick-guide-wcag.md)
>* [Experience Managerでのアクセシブルなコンテンツの作成](/help/sites-cloud/authoring/fundamentals/accessible-content.md)

