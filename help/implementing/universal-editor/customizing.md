---
title: ユニバーサルエディターのカスタマイズ
description: コンテンツ作成者のニーズに合わせてユニバーサルエディターをカスタマイズする様々なオプションについて説明します。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 98879fe30482e042da05a390e75d11c0adf7dba9
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 88%

---


# ユニバーサルエディターのカスタマイズ {#customizing}

コンテンツ作成者のニーズに合わせてユニバーサルエディターをカスタマイズする様々なオプションについて説明します。

>[!TIP]
>
>ユニバーサルエディターには多くの[拡張ポイント](/help/implementing/universal-editor/extending.md)も用意されており、プロジェクトのニーズに合わせて機能を拡張できます。

## 公開の無効化 {#disable-publish}

特定のオーサリングワークフローでは、コンテンツを公開する前に確認する必要があります。 このような場合、どの作成者も公開オプションを使用できません。

次のメタデータを追加することで、「**公開**」ボタンを完全にアプリ内で抑制できます。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## プレビューへの公開の無効化 {#publish-preview}

オーサリングワークフローによっては、[ プレビューサービス ](/help/sites-cloud/authoring/sites-console/previewing-content.md) （使用可能な場合）への公開が妨げられることがあります。

したがって、次のメタデータを追加することで、アプリ内で公開ウィンドウの「**プレビュー**」オプション全体を抑制できます。

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## コンポーネントのフィルタリング {#filtering-components}

コンポーネントフィルターを使用して、ユニバーサルエディターでコンテナごとに使用できるコンポーネントを制限できます。 詳しくは、[コンポーネントのフィルタリング](/help/implementing/universal-editor/filtering.md)のドキュメントを参照してください。

## プロパティパネルでのコンポーネントを条件付きで表示および非表示にする {#conditionally-hide}

1 つまたは複数のコンポーネントを一般的に作成者が利用できる場合がありますが、意味をなさない状況が発生する場合もあります。 このような場合、`condition` 属性を[コンポーネントモデルのフィールド](/help/implementing/universal-editor/field-types.md#fields)に追加することによって、プロパティパネルでコンポーネントを非表示にすることができます。

条件は、[JsonLogic スキーマ](https://jsonlogic.com/)を使用して定義できます。条件が true の場合、フィールドが表示されます。条件が false の場合、フィールドは非表示になります。

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

## カスタムプレビュー URL {#custom-preview-urls}

カスタムプレビュー URL は、`urn:adobe:aue:config:preview` メタ設定を使用して指定できます。この URL は、[エディターの右上のツールバー](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)にある「**ページを開く**」ボタンをクリックすると開きます。

これは、[WYSIWYG オーサリングを備えた Edge Delivery Services を使用](/help/edge/wysiwyg-authoring/authoring.md)するアプリケーションなど、特定のプレビュー要件を持つアプリケーションに特に役立ちます。

これを行うには、次の例のように、実装されたアプリのメタタグに目的のプレビュー URL を含めるのみです。

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
