---
title: ページプロパティのビューのカスタマイズ
description: 作成者がページのプロパティを表示および編集する方法について説明します。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 47%

---


# ページプロパティのビューのカスタマイズ{#customizing-views-of-page-properties}

各ページには [プロパティ](/help/sites-cloud/authoring/fundamentals/page-properties.md) ユーザーが表示および編集できるページの作成（ビューの作成）時に必要なものと、後のステージで表示および編集（ビューの編集）できるものがあります。 これらのページプロパティは、適切なページコンポーネントのダイアログ（`cq:dialog`）で定義し、使用できるようにします。

各ページプロパティのデフォルト状態は次のとおりです。

* 作成ビューで非表示 ( 例： **ページを作成** ウィザード )

* 編集ビューで使用できます ( 例： **プロパティを表示**)

変更が必要な場合は、フィールドを具体的に設定する必要があります。 これは、次の適切なノードプロパティを使用しておこないます。

* 作成ビューで使用できるページプロパティ ( 例： **ページを作成** ウィザード ):

   * 名前：`cq:showOnCreate`
   * 型：`Boolean`

* 編集ビューで使用できるページプロパティ ( **表示**/**編集**  **プロパティ** オプション：

   * 名前：`cq:hideOnEdit`
   * 型：`Boolean`

>[!TIP]
>
>ページプロパティのカスタマイズ方法については、「[ページプロパティの拡張チュートリアルl](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=ja) 」を参照してください。

## ページプロパティの設定 {#configuring-your-page-properties}

また、ページコンポーネントのダイアログを設定し、適切なノードプロパティを適用することで、使用可能なフィールドを設定できます。

例えば、デフォルトでは、[**ページを作成**&#x200B;ウィザード](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)には「**その他のタイトルと説明**」の下にグループ化されたフィールドが表示されます。これらのフィールドを非表示にするには、次のように設定します。

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
>ライブコピーで使用するページプロパティを設定する場合は、ドキュメントを参照してください [マルチサイトマネージャの拡張](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) を参照してください。

## ページプロパティの設定例 {#sample-configuration-of-page-properties}

このサンプルは、 [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) 使用を含む [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). `cq:showOnCreate` と `cq:hideOnEdit` の両方を使用することも説明されています。

このページのコードは、 [GitHub です。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
