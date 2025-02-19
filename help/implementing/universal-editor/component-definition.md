---
title: コンポーネント定義
description: コンポーネント定義とユニバーサルエディター間の JSON 契約について詳しく説明します。
feature: Developing
role: Admin, Architect, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: afb59345b48b39376b62a13cce8910bc9bc42c38
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# コンポーネント定義 {#component-definition}

コンポーネント定義とユニバーサルエディター間の JSON 契約について詳しく説明します。

## 概要 {#overview}

`component-definition.json` ファイルは、コンテンツ作成者がプロジェクトで使用できるコンポーネントを定義します。 このドキュメントでは、このファイルの目的と、ユニバーサルエディターでファイルを使用して作成者にページオーサリングコンポーネントを表示する方法について詳しく説明します。

>[!TIP]
>
>コンテンツモデリングプロセスの概要については、[Edge Delivery Services プロジェクトでのWYSIWYG オーサリング向けコンテンツモデリング ](/help/edge/wysiwyg-authoring/content-modeling.md) を参照してください。

>[!TIP]
>
>最初から独自の `component-definition.json` ファイルを作成する必要はありません。 [ プロジェクトをブートストラップ ](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) するために使用するプロジェクトのボイラープレートには [ 完全に機能する `component-definition.json` ファイル ](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) が含まれており、必要に応じて調整できます。

## コンポーネント定義例 {#example}

以下は完全ですが、簡単な `component-definition.json` を例として示しています。

```json
{
  "groups":[
    {
      "title":"General Components",
      "id":"general",
      "components":[
        {
          "title":"Text",
          "id":"text",
          "model": "text",
          "filter": "texts",
          "plugins":{
            "aem":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            },
            "aem65":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```

## `groups` {#groups}

作成者 `groups`、エディターのプロパティパネルにある **追加** アイコンをクリックして [ 新しいコンポーネントをページに追加 ](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components) したときにユニバーサルエディターに表示されるコンポーネントのグループを定義します。 グループは、コンポーネントの整理に役立ちます。 共通グループには、**一般コンポーネント** や **詳細コンポーネント** があります。

* `title` は、エディター UI に表示されるグループの説明をテキストで定義します。
* グループ `id` 一意に識別します。

## `components` {#components}

`components` は、グループに属するコンポーネントを定義します。

* `title` は、UI に表示されるコンポーネントの説明をテキストで定義します。
* コンポ `id` ネントを一意に識別します。
   * 同 `id` の [ コンポーネントモデル ](/help/implementing/universal-editor/field-types.md#model-structure) は、コンポーネントのフィールドを定義します。
   * 一意なので、例えば [ フィルター定義 ](/help/implementing/universal-editor/filtering.md) で使用して、コンテナに追加できるコンポーネントを決定できます。
* コンポ `model` ネントで使用する [ モデル ](/help/implementing/universal-editor/field-types.md#model-structure) を定義します。
   * これにより、モデルはコンポーネント定義内で一元的に管理され、実装を指定する必要は [ りません ](/help/implementing/universal-editor/field-types.md#instrumentation)。
   * これにより、コンテナ間でコンポーネントを移動できます。
* コンポ `filter` ネントで使用する [ フィルター ](/help/implementing/universal-editor/filtering.md) を定義します。

## `plugins` {#plugins}

`plugins` は、コンポーネントの永続化を担当するプラグインを定義します。 一般的なプラグインは次のとおりです。

* AEM as a Cloud Serviceの `aem`。
* AEM 6.5 の `aem5`。
* AEM as a Cloud Service WYSIWYG オーサリングの `xwalk` ール。

## `page` または `cf` {#page-cf}

`plugin` を定義したら、それがページ関連かフラグメント関連かを示す必要があります。

* `page` は、コンポーネントが現在のページのコンテンツであることを示します。
* `cf` は、コンポーネントが [ コンテンツフラグメント ](/help/assets/content-fragments/content-fragments.md) 内のコンテンツに関連付けられていることを示します。

### `page` {#page}

コンポーネントがページ上のコンテンツの場合は、次の情報を指定できます。

* コンポ `resourceType` ネントのレンダリングに使用する [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType` を定義します。
* `template` は、新しく作成されたコンポーネントに自動的に書き込まれるオプションのキーや値を定義し、コンポーネントに適用するフィルターやモデルを定義します。
   * 説明用、サンプル用、プレースホルダーテキストに便利です。

#### `template` {#template}

オプションのキーと値のペアを指定 `template` ると、これらを新しいコンポーネントに自動的に書き込むことができます。 さらに、次のオプション値も指定できます。

### `cf` {#cf}

コンポーネントがコンテンツフラグメント内のコンテンツに関連する場合は、次の情報を指定できます。

* 新 `name` く作成されたコンポーネントの JCR に保存されるオプション名を定義します。
   * 情報のみであり、通常、`title` のように UI に表示されません。
* 新 `cfModel` く作成されたコンポーネントの [ コンテンツフラグメント ](/help/assets/content-fragments/content-fragments-models.md) モデルを定義します。
* `cfFolder` は、コンテンツフラグメントを作成するフォルダーを定義します。
* 新 `title` いコンテンツフラグメントのタイトルを定義します。
* 新 `description` いコンテンツフラグメントの説明を定義します。
* 新 `template` く作成されたコンテンツフラグメントに自動的に書き込まれるオプションのキーと値を定義します。
   * 説明用、サンプル用、プレースホルダーテキストに便利です。

### `cf` が暗示される {#cf-implied}

参照フィールドを指すようにページが [ 計測 ](/help/implementing/universal-editor/getting-started.md#instrument-page) されている場合、`cf` が想定されます。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

この場合、`data-aue-prop` は参照フィールドを指しているので、`cf` が想定されます。 `data-aue-prop` がない場合、コンポーネントは参照フィールドを介してリンクされないので、ユニバーサルエディターは `page` を想定します。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

コンポーネントは、単にリソースの下のサブノードです。
