---
title: ユニバーサルエディターのカスタマイズと拡張
description: コンテンツ作成者のニーズに合わせてユニバーサルエディターの UI をカスタマイズできる、様々な拡張ポイントやその他の機能について説明します。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 73%

---


# ユニバーサルエディターのカスタマイズと拡張 {#customizing-extending}

コンテンツ作成者のニーズに合わせてユニバーサルエディターのオーサリングエクスペリエンスをカスタマイズできる様々な拡張ポイントとその他の機能について説明します。

## 概要 {#overview}

ユニバーサルエディターでは、プロジェクトのニーズに合わせて 2 つのタイプの適応が可能です。

* [ユニバーサルエディターのカスタマイズ](#customizing) - ユニバーサルエディターの標準機能は、複数のカスタマイズ設定を通じて適応させることができます。
* [ユニバーサルエディター UI の拡張](#extending) - ユニバーサルエディターの UI は、プロジェクトのニーズに合わせて、App Builder を使用して拡張することもできます。

次の節では、両方のタイプについて説明します。

## ユニバーサルエディターのカスタマイズ {#customizing}

ユニバーサルエディターには、機能をカスタマイズするためのビルトインオプションがいくつか用意されています。

### 公開の無効化 {#disable-publish}

特定のオーサリングワークフローでは、コンテンツを公開する前に確認する必要があります。 このような場合、どの作成者も公開オプションを使用できません。

次のメタデータを追加することで、「**公開**」ボタンを完全にアプリ内で抑制できます。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### コンポーネントのフィルタリング {#filtering-components}

コンポーネントフィルターを使用して、ユニバーサルエディターでコンテナごとに使用できるコンポーネントを制限できます。 詳しくは、[コンポーネントのフィルタリング](/help/implementing/universal-editor/filtering.md)のドキュメントを参照してください。

### プロパティパネルでのコンポーネントを条件付きで表示および非表示にする {#conditionally-hide}

1 つまたは複数のコンポーネントを一般的に作成者が利用できる場合がありますが、意味をなさない状況が発生する場合もあります。 その場合、`condition` 属性を [ コンポーネントモデルのフィールド ](/help/implementing/universal-editor/field-types.md#fields) に追加することで、プロパティパネルでコンポーネントを非表示にできます。

条件は、[JsonLogic スキーマ ](https://jsonlogic.com/) を使用して定義できます。 条件が true の場合、フィールドが表示されます。 条件が false の場合、フィールドは非表示になります。

>[!BEGINTABS]

>[!TAB サンプルモデル]

```json
 {
    "id": "conditionally-revealed-component",
    "fields": [
      {
        "component": "boolean",
        "label": "Shall the text field be revealed?",
        "name": "reveal",
        "valueType": "boolean"
      },
      {
        "component": "text-input",
        "label": "Hidden text field",
        "name": "hidden-text",
        "valueType": "string",
        "condition": { "===": [{"var" : "reveal"}, true] }
      }
    ]
 }
```

>[!TAB 条件 False]

![非表示のテキストフィールド](assets/hidden.png)

>[!TAB 条件 True]

![表示されたテキストフィールド](assets/shown.png)

>[!ENDTABS]

### カスタムプレビュー URL {#custom-preview-urls}

カスタムプレビュー URL は、`urn:adobe:aue:config:preview` のメタ設定を使用して指定できます。この設定は、**エディターの右上のツールバー ](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar) にある「[ ページを開く** ボタンをクリックすると開きます。

これは、[WYSIWYG オーサリングでEdge Delivery Servicesを使用する ](/help/edge/wysiwyg-authoring/authoring.md) など、特定のプレビュー要件を持つアプリケーションで特に役立ちます。

これを行うには、次の例のように、実装されたアプリのメタタグに目的のプレビュー URL を含めるのみです。

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

## ユニバーサルエディター UI の拡張 {#extending}

Adobe Experience Cloud サービスとして、ユニバーサルエディターの UI は、App Builder とExperience Manager を使用して拡張できます。

UI 拡張機能は、Adobe App Builder で作成された JavaScript アプリケーションで、ユニバーサルエディターなどの Adobe Experience Cloud 統合シェルで実行される UI アプリケーションに埋め込むことができます。 ヘッダーメニューとプロパティパネルに独自のボタンとアクションを追加したり、ユニバーサルエディター用に独自のイベントを作成したりできます。

これらの可能性を調べるには、次のリソースを参照してください。

1. [UI 拡張機能](https://developer.adobe.com/uix/docs/) - UI 拡張機能の開発者向けドキュメント。
1. [UI 拡張機能ガイド](https://developer.adobe.com/uix/docs/guides/) - 独自の拡張機能を開発する方法に関する手順説明
1. [ユニバーサルエディターの拡張ポイント](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - ユニバーサルエディター固有の拡張ポイントについてのドキュメント

>[!TIP]
>
>例を挙げて学びたい場合は、[AEM UI 拡張機能のチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) を参照してください。 コンテンツフラグメントコンソールの拡張に重点を置いていますが、ユニバーサルエディターで UI 拡張機能を実装する場合の概念は同じです。

[AEM SitesのExtension Managerを使用 ](https://developer.adobe.com/uix/docs/extension-manager/) すると、インスタンスごとに拡張機能を有効または無効にしたり、ユニバーサルエディターを含むAdobeのファーストパーティ拡張機能にアクセスしたりできます。
