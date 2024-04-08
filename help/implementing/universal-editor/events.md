---
title: ユニバーサルエディターイベント
description: リモートアプリ内のコンテンツや UI の変更に応じて使用できる、ユニバーサルエディターが送信する様々なイベントについて説明します。
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
source-git-commit: 11a244b7dd4810fbfec92b3effc362102e7322dc
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# ユニバーサルエディターイベント {#events}

リモートアプリ内のコンテンツや UI の変更に応じて使用できる、ユニバーサルエディターが送信する様々なイベントについて説明します。

## はじめに {#introduction}

アプリケーションは、ページやコンポーネントの更新に対して異なる要件を持つ場合があります。 したがって、ユニバーサルエディターは定義されたイベントをリモートアプリケーションに送信します。 リモートアプリケーションに送信されたイベントのカスタムイベントリスナーがない場合、 [フォールバックイベントリスナー](#fallback-listeners) 提供元： `universal-editor-cors` パッケージが実行されます。

すべてのイベントは、リモートページの影響を受ける DOM 要素で呼び出されます。 イベントが `BODY` デフォルトのイベントリスナーが `universal-editor-cors` パッケージが登録されています。 UI にはコンテンツ用のイベントとイベントがあります。

すべてのイベントは、命名規則に従います。

* `aue:<content-or-ui>-<event-name>`

例： `aue:content-update` および `aue:ui-select`

イベントには、リクエストのペイロードと応答のペイロードが含まれ、対応する呼び出しが成功するとトリガーされます。 呼び出しとそのペイロードの例について詳しくは、ドキュメントを参照してください。 [ユニバーサルエディターの呼び出し。](/help/implementing/universal-editor/calls.md)

## コンテンツ更新イベント {#content-events}

### aue:content-add {#content-add}

The `aue:content-add` イベントは、新しいコンポーネントがコンテナに追加されたときにトリガーされます。

ペイロードは、コンポーネント定義からのフォールバックコンテンツと共に、Universal Editor サービスからのコンテンツです。

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

### ause:content-details {#content-details}

The `aue:content-details` イベントは、コンポーネントがプロパティパネルに読み込まれるとトリガーされます。

ペイロードは、コンポーネントのコンテンツで、オプションでそのスキーマです。

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

The `aue:content-move` イベントは、コンポーネントの移動時にトリガーされます。

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

The `aue:content-patch` イベントは、コンポーネントのデータがプロパティパネルで更新されるとトリガーされます。

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

The `aue:content-remove` イベントは、コンポーネントがコンテナから削除されたときにトリガーされます。

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

The `aue:content-update` イベントは、コンポーネントのプロパティがコンテキスト内で更新されたときにトリガーされます。

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

### ペイロードを渡す {#passing-payloads}

すべてのコンテンツ更新イベントについて、リクエストされたペイロードと応答ペイロードがイベントに渡されます。 例：更新呼び出しの場合：

リクエストペイロード：

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

### aute:ui-publish {#ui-publish}

The `aue:ui-publish` イベントは、コンテンツが公開されたときに ( 呼び出し時に `BODY` レベル ) で使用できます。

ペイロードは、項目 ID とその公開ステータスのリストです。

### aue:ui-select {#ui-select}

The `aue:ui-select` イベントが発生した場合は、コンポーネントが選択されたときにトリガーされます。

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

The `aue:ui-preview` イベントは、ページの編集モードが **プレビュー**.

このイベントのペイロードは空です。

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

The `aue:ui-edit` イベントは、ページの編集モードが **編集**.

このイベントのペイロードは空です。

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

The `aue:ui-viewport-change` イベントは、ビューポートのサイズが変更されたときにトリガーされます。

ペイロードは、ビューポートの寸法です。

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aute:initialized {#initialized}

The `aue:initialized` イベントがトリガーされ、リモートページがユニバーサルエディターに正常に読み込まれたことが通知されます。

このイベントのペイロードは空です。

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
| `aue:content-move` | コンポーネントのコンテンツ/構造をターゲット領域に移動する |
| `aue:content-patch` | ページの再読み込み |
| `aue:content-remove` | DOM 要素を削除する |
| `aue:content-update` | を更新します。 `innerHTML` ペイロードを使用 |

### UI イベント {#ui-event-fallbacks}

| イベント | 動作 |
|---|---|
| `aue:ui-publish` | 何もしない |
| `aue:ui-select` | 選択した要素までスクロールします。 |
| `aue:ui-preview` | 追加 `class="adobe-ue-preview"` HTMLタグ |
| `aue:ui-edit` | 追加 `class=adobe-ue-edit"` HTMLタグ |
| `aue:ui-viewport-change` | 何もしない |
| `aue:initialized` | 何もしない |

## その他のリソース {#additional-resources}

* [ユニバーサルエディターの呼び出し](/help/implementing/universal-editor/calls.md)

