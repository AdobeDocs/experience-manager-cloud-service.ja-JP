---
title: ユニバーサルエディターイベント
description: リモートアプリのコンテンツや UI の変更に反応するために使用できる、ユニバーサルエディターが送信する様々なイベントについて説明します。
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 3%

---

# ユニバーサルエディターイベント {#events}

リモートアプリのコンテンツや UI の変更に反応するために使用できる、ユニバーサルエディターが送信する様々なイベントについて説明します。

## はじめに {#introduction}

アプリケーションには、ページまたはコンポーネントのアップデートに関する様々な要件があります。 そのため、ユニバーサルエディターは、定義済みのイベントをリモートアプリケーションに送信します。 リモートアプリケーションに送信されたイベントのカスタムイベントリスナーがない場合は、`universal-editor-cors` パッケージから提供される [ フォールバックイベントリスナー ](#fallback-listeners) が実行されます。

すべてのイベントは、リモートページの影響を受ける DOM 要素で呼び出されます。 イベントは、`universal-editor-cors` パッケージによって提供されるデフォルトのイベントリスナーが登録されている `BODY` 要素までバブルアップします。 コンテンツ用のイベントと UI 用のイベントがあります。

すべてのイベントは命名規則に従います。

* `aue:<content-or-ui>-<event-name>`

例：`aue:content-update` および `aue:ui-select`

イベントには、リクエストのと応答のペイロードが含まれ、対応する呼び出しが成功するとトリガーされます。 呼び出しとそのペイロードの例について詳しくは、ドキュメント [ ユニバーサルエディターの呼び出し ](/help/implementing/universal-editor/calls.md) を参照してください。

## コンテンツ更新イベント {#content-events}

### aue:content-add {#content-add}

`aue:content-add` イベントは、新しいコンポーネントがコンテナに追加されるとトリガーされます。

ペイロードは、ユニバーサルエディターサービスのコンテンツと、コンポーネント定義のフォールバックコンテンツです。

```json
{
    details: {
        request: request payload;   // what is sent to the service
        response: {                 // what is returned by the service
            resource: string;       // newly created content resource
            updates: [{
                resource: string;   // resource to update
                type: string;       // type of instrumentation
                content?: string;   // content to replace
            }]
        }
    }
}
```

### aue:content-details {#content-details}

プロパティパネルにコンポーネントが読み込まれると、`aue:content-details` イベントがトリガーされます。

ペイロードは、コンポーネントのコンテンツであり、オプションでスキーマでもあります。

```json
{
    details: {
        content: object             // content object
        model: [object]             // model object
        request: request payload;   // what is sent to the service
        response: response payload; // what is returned by the service
    }
}
```

### aue:content-move {#content-move}

コンポーネントが移動されると、`aue:content-move` イベントがトリガーされます。

ペイロードは、コンポーネント、ソースコンテナ、ターゲットコンテナです。

```json
{
    details: {
        from: string;                   // container we move the component from
        component: string;              // component we move
        to: string;                     // container we move the component to
        before: string;                    // before which component shall we place the component
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-patch {#content-patch}

`aue:content-patch` イベントは、コンポーネントのデータがプロパティパネルで更新されたときにトリガーされます。

ペイロードは、更新されたプロパティの JSON パッチです。

```json
{
    details: {
        patch: {
            name: string;               // attribute which is updated
            value: string;              // new value which is stored to the attribute
        },
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-remove {#content-remove}

`aue:content-remove` イベントは、コンポーネントがコンテナから削除されたときにトリガーされます。

ペイロードは、削除されたコンポーネントの項目 ID です。

```json
{
    details: {
        resource: string;               // the resource which got removed
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-update {#content-update}

コンポーネントのプロパティがコンテキスト内で更新されると、`aue:content-update` イベントがトリガーされます。

ペイロードは更新された値です。

```json
{
    details: {
        value: string;                  // updated value
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service 
    }
}
```

### ペイロードの受け渡し {#passing-payloads}

すべてのコンテンツ更新イベントについて、リクエストされたペイロードと応答ペイロードがイベントに渡されます。 例：更新呼び出しの場合：

リクエストペイロード :

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-p7452-e12433.adobeaemcloud.com"
    }
  ],
  "target": {
    "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "type": "text",
    "prop": "title"
  },
  "value": "Alhoa Spirit Northern Norway!"
}
```

応答ペイロード

```json
{
    "updates": [
        {
            "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
            "prop": "title",
            "type": "text"
        }
    ]
}
```

## UI イベント {#ui-events}

### aue:ui-publish {#ui-publish}

`aue:ui-publish` イベントは、コンテンツが公開されると（`BODY` レベルでの呼び出しを伴って）トリガーされます。

ペイロードは、項目 ID とその公開ステータスのリストです。

### aue:ui-select {#ui-select}

コンポーネントが選択されると、`aue:ui-select` イベントがトリガーされます。

ペイロードは、選択したコンポーネントの項目 ID、項目プロパティおよび項目タイプです。

```json
{
    details: {
        resource: string;       // resource of the selected
        prop: string;           // prop of the selected
        type: string;           // type of the selected
        selected: boolean;      // was selected or unselected
    }
}
```

### aue:ui-preview {#ui-preview}

`aue:ui-preview` イベントは、ページの編集モードが **プレビュー** に変更されたときにトリガーされます。

このイベントのペイロードが空です。

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

`aue:ui-edit` イベントは、ページの編集モードが **編集** に変更されたときにトリガーされます。

このイベントのペイロードが空です。

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

ビューポートのサイズが変更されると、`aue:ui-viewport-change` イベントがトリガーされます。

ペイロードはビューポートのサイズです。

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue:initialized {#initialized}

`aue:initialized` イベントがトリガーされ、ユニバーサルエディターに正常に読み込まれたことがリモートページに通知されます。

このイベントのペイロードが空です。

```json
{
    details: {}
}
```

## フォールバックイベントリスナー {#fallback-listeners}

### コンテンツの更新 {#content-update-fallbacks}

| イベント | 動作 |
|---|---|
| `aue:content-add` | ページの再読み込み |
| `aue:content-details` | 何もしない |
| `aue:content-move` | コンポーネントのコンテンツ/構造をターゲット領域に移動します |
| `aue:content-patch` | ページの再読み込み |
| `aue:content-remove` | DOM 要素を削除します |
| `aue:content-update` | ペイロードを使用して `innerHTML` を更新 |

### UI イベント {#ui-event-fallbacks}

| イベント | 動作 |
|---|---|
| `aue:ui-publish` | 何もしない |
| `aue:ui-select` | 選択した要素までスクロールします |
| `aue:ui-preview` | HTMLタグに `class="adobe-ue-preview"` を追加 |
| `aue:ui-edit` | HTMLタグに `class=adobe-ue-edit"` を追加 |
| `aue:ui-viewport-change` | 何もしない |
| `aue:initialized` | 何もしない |

## その他のリソース {#additional-resources}

* [ユニバーサルエディターの呼び出し](/help/implementing/universal-editor/calls.md)

