---
title: ユニバーサルエディターのカスタマイズ
description: コンテンツ作成者のニーズに合わせてユニバーサルエディターをカスタマイズする様々なオプションについて説明します。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 68%

---


# ユニバーサルエディターのカスタマイズ {#customizing}

コンテンツ作成者のニーズに合わせてユニバーサルエディターをカスタマイズする様々なオプションについて説明します。

>[!TIP]
>
>ユニバーサルエディターには多くの[拡張ポイント](/help/implementing/universal-editor/extending.md)も用意されており、プロジェクトのニーズに合わせて機能を拡張できます。

## Meta設定タグの使用 {#meta-tags}

オーサリングワークフローによっては、ユニバーサルエディターの機能の一部を使用する必要があり、他の機能を使用する必要がない場合があります。 このような様々なケースをサポートするために、エディターの特定の機能やボタンを設定または無効にするメタタグを使用できます。

ページの「`<head>`」セクションでこのタグを使用して、1 つ以上の機能を無効にします。

```html
<meta name="urn:adobe:aue:config:disable" content="..." />
```

複数の機能を無効にする場合は、値のコンマ区切りリストを指定します。

メタタグで無効にできる機能など、`content` でサポートされている値を以下に示します。

| コンテンツの値 | 説明 |
|---|---|
| `publish` | すべての [ 公開 ](/help/sites-cloud/authoring/universal-editor/publishing.md) 機能（[ 公開ボタン ](/help/sites-cloud/authoring/universal-editor/navigation.md#publish) および [ 非公開ボタン）を無効にする ](/help/sites-cloud/authoring/universal-editor/navigation.md#ellipsis) |
| `publish-live` | ライブ [ 公開 ](/help/sites-cloud/authoring/universal-editor/publishing.md) を無効にする |
| `publish-preview` | プレビュー公開を無効にする（「プレビューサービス [ が使用可能 ](/help/sites-cloud/authoring/sites-console/previewing-content.md) 場合） |
| `unpublish` | [ 非公開 ](/help/sites-cloud/authoring/universal-editor/publishing.md#unpublishing-content) ボタンを無効にします |
| `copy` | [ コピーボタンと貼り付けボタン ](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) を無効にします |
| `duplicate` | [ 複製 ](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) ボタンを無効にします |
| `header-open-page` | [ ページを開く ](/help/sites-cloud/authoring/universal-editor/navigation.md#open-page) ボタンを無効にします |

## エンドポイントの変更 {#custom-endpoint}

アドビがホストするユニバーサルエディターサービスではなく、独自にホストするバージョンを使用する場合は、メタタグでこれを設定できます。詳しくは、[AEM のユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md##configuration-settings)ドキュメントを参照してください。

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

これを行うには、次の例のように、実装されたアプリのメタタグに目的のプレビュー URL を含めます。

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
