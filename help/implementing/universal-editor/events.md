---
title: ユニバーサルエディターイベント
description: リモートアプリのコンテンツや UI の変更に対応するのに使用できる、ユニバーサルエディターが送信する様々なイベントについて説明します。
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Developer
source-git-commit: ac361c31b116466cc9a718640c1de4e4ef396fba
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 94%

---

# ユニバーサルエディターイベント {#events}

リモートアプリのコンテンツや UI の変更に対応するのに使用できる、ユニバーサルエディターが送信する様々なイベントについて説明します。

## はじめに {#introduction}

アプリケーションでは、ページまたはコンポーネントの更新に関して様々な要件がある場合があります。したがって、ユニバーサルエディターは、定義済みのイベントをリモートアプリケーションに送信します。リモートアプリケーションに送信されたイベントに対するカスタムイベントリスナーがない場合、`universal-editor-cors` パッケージによって提供される[フォールバックイベントリスナー](#fallback-listeners)が実行されます。

すべてのイベントは、リモートページの影響を受ける DOM 要素で呼び出されます。イベントは、`universal-editor-cors` パッケージによって提供されるデフォルトのイベントリスナーが登録されている `BODY` 要素までバブルアップします。コンテンツ用のイベントと UI 用のイベントがあります。

すべてのイベントは命名規則に従います。

* `aue:<content-or-ui>-<event-name>`

例えば、`aue:content-update` と `aue:ui-select` です。

イベントには、リクエストと応答のペイロードが含まれ、対応する呼び出しが成功するとトリガーされます。呼び出しとそのペイロードの例について詳しくは、[ユニバーサルエディターの呼び出し](/help/implementing/universal-editor/calls.md)ドキュメントを参照してください。

## コンテンツ更新イベント {#content-events}

### オーサリング&amp;amp；コロン；content-add {#content-add}

`aue:content-add` イベントは、コンテナに新しいコンポーネントを追加した際にトリガーされます。

ペイロードは、ユニバーサルエディターサービスからのコンテンツと、コンポーネント定義からのフォールバックコンテンツです。

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

### オーサーマップ（&amp;A）；コロン；content-details {#content-details}

`aue:content-details` イベントは、プロパティパネルにコンポーネントを読み込んだ際にトリガーされます。

ペイロードは、コンポーネントのコンテンツであり、オプションでそのスキーマでもあります。

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

### オーサリング（&colon;content-move） {#content-move}

`aue:content-move` イベントは、コンポーネントを移動した際にトリガーされます。

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

### オーサー&amp;amp；コロン；content-patch {#content-patch}

`aue:content-patch` イベントは、プロパティパネルでコンポーネントのデータを更新した際にトリガーされます。

ペイロードは、更新したプロパティの JSON パッチです。

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

### オーサリング&amp;amp；コロン；コンテンツ削除 {#content-remove}

`aue:content-remove` イベントは、コンポーネントをコンテナから削除した際にトリガーされます。

ペイロードは、削除したコンポーネントの項目 ID です。

```json
{
    details: {
        resource: string;               // the resource which got removed
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### オーサリング&amp;amp；コロン；content-update {#content-update}

`aue:content-update` イベントは、コンポーネントのプロパティをコンテキスト内で更新した際にトリガーされます。

ペイロードは、更新した値です。

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

すべてのコンテンツ更新イベントでは、リクエストしたペイロードと応答ペイロードがイベントに渡されます。例：更新呼び出しの場合：

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

### オーサーマップ（&colon;ui-preview） {#ui-preview}

`aue:ui-preview` イベントは、ページの編集モードを&#x200B;**プレビュー**&#x200B;に変更した際にトリガーされます。

ペイロードは、このイベントの場合は空です。

```json
{
    details: {}
}
```

### オーサリング&amp;amp；コロン；ui-edit {#ui-edit}

`aue:ui-edit` イベントは、ページの編集モードを&#x200B;**編集**&#x200B;に変更した際にトリガーされます。

ペイロードは、このイベントの場合は空です。

```json
{
    details: {}
}
```

### オーサー&colon;ui-viewport-change {#ui-viewport-change}

`aue:ui-viewport-change` イベントは、ビューポートのサイズを変更した際にトリガーされます。

ペイロードは、ビューポートのディメンションです。

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### カスタム&amp;colon；初期化済み {#initialized}

`aue:initialized` イベントは、ユニバーサルエディターに正常に読み込まれたことをリモートページに通知するためにトリガーされます。

ペイロードは、このイベントの場合は空です。

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
| `aue:content-move` | コンポーネントのコンテンツ／構造をターゲット領域に移動 |
| `aue:content-patch` | ページの再読み込み |
| `aue:content-remove` | DOM 要素を削除 |
| `aue:content-update` | ペイロードを使用して `innerHTML` を更新 |

### UI イベント {#ui-event-fallbacks}

| イベント | 動作 |
|---|---|
| `aue:ui-select` | 選択した要素までスクロール |
| `aue:ui-preview` | HTML タグに `class="adobe-ue-preview"` を追加 |
| `aue:ui-edit` | HTML タグに `class=adobe-ue-edit"` を追加 |
| `aue:ui-viewport-change` | 何もしない |
| `aue:initialized` | 何もしない |

## その他のリソース {#additional-resources}

* [ユニバーサルエディターの呼び出し](/help/implementing/universal-editor/calls.md)
