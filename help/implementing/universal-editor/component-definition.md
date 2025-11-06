---
title: コンポーネント定義
description: コンポーネント定義とユニバーサルエディター間の JSON 契約について詳しく説明します。
feature: Developing
role: Admin, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 100%

---

# コンポーネント定義 {#component-definition}

コンポーネント定義とユニバーサルエディター間の JSON 契約について詳しく説明します。

## 概要 {#overview}

`component-definition.json` ファイルは、プロジェクトのコンテンツ作成者が使用できるコンポーネントを定義します。このドキュメントでは、このファイルの目的と、ユニバーサルエディターでこのファイルを使用して作成者にページオーサリングコンポーネントを表示する方法について詳しく説明します。

>[!TIP]
>
>コンテンツモデリングプロセスの概要について詳しくは、[Edge Delivery Services プロジェクトを使用した WYSIWYG オーサリングのコンテンツモデリング](https://www.aem.live/developer/component-model-definitions)ドキュメントを参照してください。

>[!TIP]
>
>独自の `component-definition.json` ファイルをゼロから作成する必要はありません。[プロジェクトのブートストラップ](https://www.aem.live/developer/ue-tutorial)に使用するプロジェクトボイラープレートには、ニーズに合わせて調整できる、[完全に機能する `component-definition.json` ファイル](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json)が含まれています。

## コンポーネント定義の例 {#example}

以下は、例として、完全ですがシンプルな `component-definition.json` です。

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

`groups` は、エディターのプロパティパネルで **追加** アイコンをクリックして[ページに新しいコンポーネントを追加](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components)した際に、作成者がユニバーサルエディターで見るコンポーネントのグループを定義します。グループは、コンポーネントの整理に役立ちます。共通グループには、**一般コンポーネント**&#x200B;と&#x200B;**詳細コンポーネント**&#x200B;があります。

* `title` は、エディター UI に表示されるグループのテキストによる説明を定義します。
* `id` は、グループを一意に識別します。

## `components` {#components}

`components` は、グループに属するコンポーネントを定義します。

* `title` は、エディター UI に表示されるコンポーネントのテキストによる説明を定義します。
* `id` は、コンポーネントを一意に識別します。
   * 同じ `id` の[コンポーネントモデル](/help/implementing/universal-editor/field-types.md#model-structure)は、コンポーネントのフィールドを定義します。
   * これは一意なので、例えば、[フィルター定義](/help/implementing/universal-editor/filtering.md)で使用して、コンテナに追加できるコンポーネントを決定できます。
* `model` は、コンポーネントで使用される[モデル](/help/implementing/universal-editor/field-types.md#model-structure)を定義します。
   * その結果、モデルはコンポーネント定義内で集中管理され、[実装を指定](/help/implementing/universal-editor/field-types.md#instrumentation)する必要はありません。
   * これにより、コンテナ間でコンポーネントを移動できます。
* `filter` は、コンポーネントで使用される[フィルター](/help/implementing/universal-editor/filtering.md)を定義します。

## `plugins` {#plugins}

`plugins` は、コンポーネントの永続化を担当するプラグインを定義します。一般的なプラグインを次に示します。

* [AEM as a Cloud Service](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service) の 。`aem`
* [AEM 6.5](https://experienceleague.adobe.com/ja/docs/experience-manager-65) および [AEM 6.5 LTS](https://experienceleague.adobe.com/ja/docs/experience-manager-65-lts) の `aem65`
* [Edge Delivery Services 向け AEM Sites を使用したオーサリング](https://www.aem.live/developer/ue-tutorial)の `xwalk`。

## `page` または `cf` {#page-cf}

`plugin` を定義したら、それがページ関連かフラグメント関連かを示す必要があります。

* `page` は、コンポーネントが現在のページのコンテンツであることを示します。
* `cf` は、コンポーネントが[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)内のコンテンツに関連していることを示します。

### `page` {#page}

コンポーネントがページ上のコンテンツである場合は、次の情報を指定できます。

* `resourceType` は、コンポーネントのレンダリングに使用される [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType` を定義します。
* `template` は、新しく作成されたコンポーネントに自動的に書き込まれるオプションのキーや値を定義し、コンポーネントに適用するフィルターやモデルを定義します。
   * 説明、サンプル、プレースホルダーテキストに役立ちます。

#### `template` {#template}

オプションのキーと値のペアを指定することで、`template` はこれらを新しいコンポーネントに自動的に書き込むことができます。さらに、次のオプション値も指定できます。

### `cf` {#cf}

コンポーネントがコンテンツフラグメント内のコンテンツに関連している場合は、次の情報を指定できます。

* `name` は、新しく作成されたコンポーネントの JCR に保存されるオプションの名前を定義します。
   * 情報提供のみを目的としており、通常は `title` のように UI には表示されません。
* `cfModel` は、新しく作成されたコンポーネントの[コンテンツフラグメント](/help/assets/content-fragments/content-fragments-models.md)モデルを定義します。
* `cfFolder` は、コンテンツフラグメントが作成されるフォルダーを定義します。
* `title` は、新しいコンテンツフラグメントのタイトルを定義します。
* `description` は、新しいコンテンツフラグメントの説明を定義します。
* `template` は、新しく作成されたコンテンツフラグメントに自動的に書き込まれるオプションのキーや値を定義します。
   * 説明、サンプル、プレースホルダーテキストに役立ちます。

### `cf` は暗黙的に指定可能 {#cf-implied}

ページが参照フィールドを指すように[実装](/help/implementing/universal-editor/getting-started.md#instrument-page)されている場合は、`cf` が想定されます。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

このような場合、`data-aue-prop` が参照フィールドを指しているので、`cf` が想定されます。`data-aue-prop` がない場合、コンポーネントが参照フィールドを通じてリンクされていないので、ユニバーサルエディターでは `page` が想定されます。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

コンポーネントは、単にリソースの下にあるサブノードです。
