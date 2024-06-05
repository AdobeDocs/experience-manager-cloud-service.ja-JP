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

アプリケーションには、ページまたはコンポーネントのアップデートに関する様々な要件があります。 そのため、ユニバーサルエディターは、定義済みのイベントをリモートアプリケーションに送信します。 リモートアプリケーションに送信されたイベントのカスタムイベントリスナーがない場合、 [フォールバックイベントリスナー](#fallback-listeners) によって提供 `universal-editor-cors` パッケージが実行されます。

すべてのイベントは、リモートページの影響を受ける DOM 要素で呼び出されます。 イベントはまでバブルアップ `BODY` によって提供されるデフォルトのイベントリスナーが存在する要素 `universal-editor-cors` パッケージが登録されました。 コンテンツ用のイベントと UI 用のイベントがあります。

すべてのイベントは命名規則に従います。

* `aue:<content-or-ui>-<event-name>`

例： `aue:content-update` および `aue:ui-select`

イベントには、リクエストのと応答のペイロードが含まれ、対応する呼び出しが成功するとトリガーされます。 呼び出しとそのペイロードの例について詳しくは、ドキュメントを参照してください [ユニバーサルエディター呼び出し。](/help/implementing/universal-editor/calls.md)

## コンテンツ更新イベント {#content-events}

### aue:content-add {#content-add}

この `aue:content-add` 新しいコンポーネントがコンテナに追加されると、イベントがトリガーされます。

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

この `aue:content-details` プロパティ パネルにコンポーネントが読み込まれると、イベントがトリガーされます。

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

この `aue:content-move` コンポーネントが移動されると、イベントがトリガーされます。

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

この `aue:content-patch` コンポーネントのデータがプロパティパネルで更新されると、イベントがトリガーされます。

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

この `aue:content-remove` コンポーネントがコンテナから削除されると、イベントがトリガーされます。

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

この `aue:content-update` コンポーネントのプロパティがコンテキスト内で更新されると、イベントがトリガーされます。

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

この `aue:ui-publish` コンテンツの公開時にイベントがトリガーされます（での呼び出しを使用） `BODY` レベル）。

ペイロードは、項目 ID とその公開ステータスのリストです。

### aue:ui-select {#ui-select}

この `aue:ui-select` コンポーネントが選択されると、イベントがトリガーされます。

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

この `aue:ui-preview` ページの編集モードがに変更されると、イベントがトリガーされます。 **プレビュー**.

このイベントのペイロードが空です。

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

この `aue:ui-edit` ページの編集モードがに変更されると、イベントがトリガーされます。 **編集**.

このイベントのペイロードが空です。

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

この `aue:ui-viewport-change` ビューポートのサイズが変更されると、イベントがトリガーされます。

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

この `aue:initialized` イベントがトリガーされ、ユニバーサルエディターに正常に読み込まれたことがリモートページに通知されます。

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
| `aue:content-update` | を更新 `innerHTML` （ペイロードを使用） |

### UI イベント {#ui-event-fallbacks}

| イベント | 動作 |
|---|---|
| `aue:ui-publish` | 何もしない |
| `aue:ui-select` | 選択した要素までスクロールします |
| `aue:ui-preview` | 追加 `class="adobe-ue-preview"` HTMLタグへ |
| `aue:ui-edit` | 追加 `class=adobe-ue-edit"` HTMLタグへ |
| `aue:ui-viewport-change` | 何もしない |
| `aue:initialized` | 何もしない |

## その他のリソース {#additional-resources}

* [ユニバーサルエディターの呼び出し](/help/implementing/universal-editor/calls.md)

