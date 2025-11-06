---
title: ページプロパティのビューのカスタマイズ
description: 作成者がページのプロパティを表示および編集する方法について説明します。
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 100%

---

# ページプロパティのビューのカスタマイズ{#customizing-views-of-page-properties}

どのページにも、ユーザーが表示および編集できる一連の[プロパティ](/help/sites-cloud/authoring/sites-console/page-properties.md)があります。ページ作成時に使用されるプロパティもあれば（作成ビュー）、後の段階で表示および編集できるプロパティもあります（編集ビュー）。これらのページプロパティは、適切なページコンポーネントのダイアログ（`cq:dialog`）で定義し、使用できるようにします。

各ページプロパティのデフォルトステートは次のとおりです。

* 作成ビューでは非表示（例：**ページを作成**&#x200B;ウィザード）

* 編集ビューでは表示（例：**プロパティを表示**）

変更が必要な場合は、フィールドを明確に設定する必要があります。それには適切なノードプロパティを使用します。

* 作成ビューで利用できるページプロパティ（例：**ページを作成**&#x200B;ウィザード）

   * 名前：`cq:showOnCreate`
   * 型：`Boolean`

* 編集ビューで利用できるページプロパティ（例：**表示**／**編集**／**プロパティ**&#x200B;オプション）：

   * 名前：`cq:hideOnEdit`
   * 型：`Boolean`

>[!TIP]
>
>ページプロパティのカスタマイズ方法については、[ページプロパティの拡張チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=ja)を参照してください。

## ページプロパティの設定 {#configuring-your-page-properties}

ページコンポーネントのダイアログを設定し、適切なノードプロパティを適用することによって、使用可能なフィールドを設定することもできます。

例えば、デフォルトでは、[**ページを作成**&#x200B;ウィザード](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page)には「**その他のタイトルと説明**」の下にグループ化されたフィールドが表示されます。これらのフィールドを非表示にするには、次のように設定します。

1. `/apps` の下にページコンポーネントを作成します。
1. ページコンポーネントの`basic`セクションにオーバーライドを作成します（[Sling リソースマネージャー](/help/implementing/developing/introduction/sling-resource-merger.md) が提供する *ダイアログの差分* を使用）。例を以下に示します。

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. `basic` の `path` プロパティに、基本タブのオーバーライドを指すように設定します（次の手順も参照してください）。次に例を示します。

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 対応するパスに「`basic` - `moretitles` 」セクションのオーバーライドを作成します。例：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 適切なノードプロパティを適用します。

   * **名前**：`cq:showOnCreate`
   * **型**：`Boolean`
   * **値**：`false`

   **ページを作成**&#x200B;ウィザードに「**その他のタイトルと説明**」セクションが表示されなくなります。

>[!NOTE]
>
>ライブコピーで使用するページプロパティを設定する場合、詳しくは[マルチサイトマネージャーの拡張](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties)を参照してください。

## ページプロパティの設定例 {#sample-configuration-of-page-properties}

この例では、[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) のダイアログ差分比較の手法を示しており、[`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties) が使用されています。`cq:showOnCreate` と `cq:hideOnEdit` の両方を使用する方法も説明されています。

このページのコードは [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog) にあります。
