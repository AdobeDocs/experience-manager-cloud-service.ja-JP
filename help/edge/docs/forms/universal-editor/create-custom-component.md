---
title: EDS フォームのカスタムコンポーネントの作成
description: EDS フォームのカスタムコンポーネントの作成
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 95%

---

# WYSIWYG オーサリングでのカスタムコンポーネントの作成

<span class="preview"> この機能は、早期アクセスプログラムを通じて利用できます。 アクセスをリクエストするには、GitHub 組織名とリポジトリ名を記載したメールを公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に送信してください。 例えば、リポジトリ URL がhttps://github.com/adobe/abcの場合、組織名は adobe で、リポジトリ名は abc.</span> です


Edge Delivery Services Forms には、カスタマイズ機能が用意されているので、フロントエンド開発者は調整されたフォームコンポーネントを作成できます。これらのカスタムコンポーネントは WYSIWYG オーサリングエクスペリエンスにシームレスに統合されるので、フォーム作成者はフォームエディター内で簡単に追加、設定、管理できます。カスタムコンポーネントを使用すると、作成者はスムーズで直感的なオーサリングプロセスを確保しながら機能を強化できます。

このドキュメントでは、ネイティブ HTML フォームコンポーネントをスタイル設定してカスタムコンポーネントを作成し、ユーザーエクスペリエンスを向上させ、フォームの視覚的な魅力を高める手順について説明します。

## 前提条件

カスタムコンポーネントの作成を開始する前に、次のことを行う必要があります。

* [ネイティブ HTML コンポーネント](/help/edge/docs/forms/form-components.md)の基本知識を持つ。
* [CSS セレクターを使用してフィールドタイプに基づいてフォームフィールドをスタイル設定](/help/edge/docs/forms/style-theme-forms.md)する方法を理解する

## カスタムコンポーネントの作成

ユニバーサルエディターでカスタムコンポーネントを追加すると、フォーム作成者はフォームを設計する際に新しいコンポーネントを使用できます。これには、コンポーネントの登録、そのプロパティの定義およびコンポーネントを使用できる場所の設定が含まれます。カスタムコンポーネントを作成する手順は次のとおりです。

[1. 新しいカスタムコンポーネントの構造の追加](#1-adding-structure-for-new-custom-component) 
[2.オーサリング用のカスタムコンポーネントのプロパティの定義](#2-defining-the-properties-of-your-custom-component-for-authoring)
[3.WYSIWYGコンポーネントリストでのカスタムコンポーネントの表示](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4.カスタムコンポーネントの登録](#4-registering-your-custom-component)
[5.カスタムコンポーネントの実行時の動作の追加](#5-adding-the-runtime-behaviour-for-your-custom-component)

**範囲**&#x200B;と呼ばれる新しいカスタムコンポーネントを作成する例を見てみましょう。範囲コンポーネントは直線として表示され、最小値、最大値、選択した値などの値が表示されます。

![範囲コンポーネントスタイル](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

この記事を最後まで読むと、カスタムコンポーネントをゼロから作成する方法を理解できるようになります。

### 1. 新しいカスタムコンポーネントの構造の追加

カスタムコンポーネントを使用する前に、ユニバーサルエディターで使用可能なオプションとして認識されるように登録する必要があります。これは、一意の識別子、デフォルトのプロパティおよびコンポーネントの構造を含むコンポーネント定義を通じて実現されます。カスタムコンポーネントをフォームオーサリングに使用できるようにするには、次の手順を実行します。

1. **新しいフォルダーとファイルを追加**
AEM プロジェクトに新しいカスタムコンポーネント用の新しいフォルダーとファイルを追加します。
   1. AEM プロジェクトを開き、`../blocks/form/components/` に移動します。
   1. `../blocks/form/components/<component_name>` でカスタムコンポーネントの新しいフォルダーを追加します。この例では、`range` という名前のフォルダーを作成します。
   1. `../blocks/form/components/<component_name>` に新しく作成したフォルダーに移動します。例えば、`../blocks/form/components/range` に移動して、次のファイルを追加します。
      * `/blocks/form/components/range/_range.json`：カスタムコンポーネントの定義が含まれます。
      * `../blocks/form/components/range/range.css`：カスタムコンポーネントのスタイル設定を定義します。
      * `../blocks/form/components/range/range.js`：実行時にカスタムコンポーネントをカスタマイズします。

        ![オーサリング用のカスタムコンポーネントの追加](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > JSON ファイルのファイル名に、プレフィックスとしてアンダースコア（_）が含まれていることを確認します。

1. `/blocks/form/components/range/_range.json` ファイルに移動し、カスタムコンポーネントのコンポーネント定義を追加します。

1. **コンポーネント定義を追加**

   定義を追加するには、`_range.json` ファイルに次のフィールドを追加する必要があります。

   * **タイトル**：ユニバーサルエディターに表示されるコンポーネントのタイトル。
   * **ID**：コンポーネントの一意の ID。
   * **fieldType**：Forms では、特定のタイプのユーザー入力を取り込む様々な **fieldType** をサポートしています。[サポートされている fieldType は、追加バイトの節](#supported-fieldtypes)で確認できます。
   * **resourceType**：各カスタムコンポーネントには、fieldType に基づいて関連付けられたリソースタイプがあります。[サポートされている resourceType は、追加バイトの節](#supported-resourcetype)で確認できます。
   * **jcr:title**：タイトルに似ていますが、コンポーネントの構造内に保存されます。
   * **fd:viewType**：カスタムコンポーネントの名前を表します。これはコンポーネントの一意の ID です。コンポーネントのカスタマイズされたビューを作成する必要があります。

コンポーネント定義を追加した後の `_range.json` ファイルは次のとおりです。

```javascript
{
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ]
}
```

>[!NOTE]
>
> フォーム関連のすべてのコンポーネントは、ユニバーサルエディターにブロックを追加する際に、Sites と同じアプローチに従います。詳しくは、[ユニバーサルエディターで使用するために実装されたブロックの作成](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block)の記事を参照してください。

### 2. オーサリング用のカスタムコンポーネントのプロパティの定義

カスタムコンポーネントには、フォーム作成者が設定できるプロパティを指定するコンポーネントモデルが含まれます。これらのプロパティは、ユニバーサルエディターの&#x200B;**プロパティ**&#x200B;ダイアログに表示され、作成者はラベル、検証ルール、スタイル、その他の属性などの設定を調整できます。プロパティを定義するには：

1. `/blocks/form/components/range/_range.json` ファイルに移動し、カスタムコンポーネントのコンポーネントモデルを追加します。

1. **コンポーネントモデルを追加**

   カスタムコンポーネントのコンポーネントモデルを定義するには、関連するフィールドを `_range.json` ファイルに追加する必要があります。

   1. **モデルを作成**

      * モデル配列に新しいオブジェクトを追加し、コンポーネントモデルの `id` を、コンポーネント定義で以前に設定した `fd:viewType` プロパティと一致するように設定します。
      * このオブジェクト内にフィールド配列を含めます。

   2. **プロパティダイアログのフィールドを定義**

      * フィールド配列内の各オブジェクトは、コンテナタイプのコンポーネントにする必要があり、**プロパティ**&#x200B;ダイアログにタブとして表示できます。
      * 一部のフィールドでは、`models/form-common` で使用できる再利用可能なプロパティを参照できます。

   3. **既存のコンポーネントモデルを参照として使用**

      * 選択した `fieldType` に対応する既存のコンポーネントモデルのコンテンツをコピーし、必要に応じて変更できます。例えば、`number-input` コンポーネントを拡張して&#x200B;**範囲**&#x200B;コンポーネントを作成すると、`models/form-components/_number-input.json` のモデル配列を参照として使用できます。

   コンポーネントモデルを追加した後の `_range.json` ファイルは次のとおりです。

   ```javascript
   "models": [
   {
     "id": "range",
     "fields": [
       {
         "component": "container",
         "name": "basic",
         "label": "Basic",
         "collapsible": false,
         "...": "../../../../models/form-common/_basic-input-fields.json"
       },
       {
         "...": "../../../../models/form-common/_help-container.json"
       },
       {
         "component": "container",
         "name": "validation",
         "label": "Validation",
         "collapsible": true,
         "...": "../../../../models/form-common/_number-validation-fields.json"
       }
     ]
   }
   ]
   ```

   >[!NOTE]
   >
   > カスタムコンポーネントの&#x200B;**プロパティ**&#x200B;ダイアログに新しいフィールドを追加するには、[定義されたスキーマ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model)に従います。

   また、カスタムコンポーネントに[カスタムプロパティを追加](#adding-custom-properties-for-your-custom-component)して、機能を拡張することもできます。

#### カスタムコンポーネントのカスタムプロパティの追加

カスタムプロパティを使用すると、コンポーネントのプロパティダイアログで設定された値に基づいて特定の動作を定義できます。これは、コンポーネントの機能とカスタマイズオプションを拡張するのに役立ちます。

この例では、範囲コンポーネントにカスタムプロパティとしてステップ値を追加します。

![ステップ値のカスタムプロパティ](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

ステップ値のカスタムプロパティを追加するには、` _<component>.json` ファイルに次のコード行を含むコンポーネントモデルを追加します。

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

JSON スニペットは、**範囲**&#x200B;コンポーネントの&#x200B;**ステップ値**&#x200B;と呼ばれるカスタムプロパティを定義します。各フィールドの分類を以下に示します。

* **コンポーネント**：プロパティダイアログで使用される入力フィールドのタイプを指定します。この場合、`number` は、フィールドが数値を受け入れることを示します。
* **name**: プロパティの識別子。コンポーネントのロジックで参照するために使用されます。 ここで、`stepValue` は範囲のステップ値設定を表します。
* **ラベル**：プロパティダイアログに表示されるプロパティの表示名。
* **valueType**：プロパティに期待されるデータタイプを定義します。`number` では、数値の入力のみが許可されます。

これで、`range.js` の JSON プロパティで `stepValue` をカスタムプロパティとして使用し、実行時にその値に基づいて動的な動作を実装できます。

したがって、コンポーネント定義、コンポーネントモデル、カスタムプロパティを追加した後の最終的な `_range.json` ファイルは次のとおりです。

```javascript
 {
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ],
  "models": [
    {
      "id": "range",
      "fields": [
        {
          "component": "container",
          "name": "basic",
          "label": "Basic",
          "collapsible": false,
          "...": "../../../../models/form-common/_basic-input-fields.json"
         {
           "component": "number",
           "name": "stepValue",
            "label": "Step Value",
             "valueType": "number"
}
        },
        {
          "...": "../../../../models/form-common/_help-container.json"
        },
        {
          "component": "container",
          "name": "validation",
          "label": "Validation",
          "collapsible": true,
          "...": "../../../../models/form-common/_number-validation-fields.json"
        }
      ]
    }
  ]
}
```

![コンポーネントの定義とモデル](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)


### 3. WYSIWYGコンポーネントリストでのカスタムコンポーネントの表示

フィルターは、ユニバーサルエディターでカスタムコンポーネントを使用できるセクションを定義します。これにより、コンポーネントは適切なセクションでのみ使用でき、構造と使いやすさが確保されます。

WYSIWYG でのフォームオーサリング中に、カスタムコンポーネントが使用できるコンポーネントのリストに表示されるようにするには：

1. `/blocks/form/_form.json` ファイルに移動します。
1. `id="form"` を持つオブジェクト内でコンポーネント配列を見つけます。
1. `definitions[]` の `fd:viewType` 値を `id="form"` を持つオブジェクトのコンポーネント配列に追加します。

```javascript
 "filters": [
    {
      "id": "form",
      "components": [
        "captcha",
        "checkbox",
        "checkbox-group",
        "date-input",
        "drop-down",
        "email",
        "file-input",
        "form-accordion",
        "form-button",
        "form-fragment",
        "form-image",
        "form-modal",
        "form-reset-button",
        "form-submit-button",
        "number-input",
        "panel",
        "plain-text",
        "radio-group",
        "rating",
        "telephone-input",
        "text-input",
        "tnc",
        "wizard",
        "range"
      ]
    }
  ]
```

![コンポーネントフィルター](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

### 4. カスタムコンポーネントの登録

フォームブロックがカスタムコンポーネントを認識し、フォーム作成中にコンポーネントモデルで定義されたプロパティを読み込むことができるようにするには、コンポーネント定義の `fd:viewType` 値を `mappings.js` ファイルに追加します。
コンポーネントを登録するには：
1. `/blocks/form/mappings.js` ファイルに移動します。
1. `customComponents[]` 配列を見つけます。
1. `definitions[]` 配列の `fd:viewType` 値を `customComponents[]` 配列に追加します。

```javascript
let customComponents = ["range"];
const OOTBComponentDecorators = ['file-input',
                                 'wizard', 
                                 'modal', 'tnc',
                                'toggleable-link',
                                'rating',
                                'datetime',
                                'list',
                                'location',
                                'accordion'];
```

![コンポーネントのマッピング](/help/edge/docs/forms/universal-editor/assets/custom-component-mapping-file.png)

上記の手順を完了すると、カスタムコンポーネントがユニバーサルエディター内のフォームのコンポーネントリストに表示されます。その後、フォームセクションにドラッグ＆ドロップできます。

![範囲コンポーネント](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

以下のスクリーンショットは、コンポーネントモデルに追加された `range` コンポーネントのプロパティを示しています。このプロパティは、フォーム作成者が設定できるプロパティを指定します。

![範囲コンポーネントのプロパティ](/help/edge/docs/forms/universal-editor/assets/range-properties.png)

これで、スタイル設定と機能を追加して、カスタムコンポーネントの実行時の動作を定義できます。

### 5. カスタムコンポーネントの実行時の動作の追加

[フォームフィールドのスタイル設定](/help/edge/docs/forms/style-theme-forms.md)に従って、事前定義済みのマークアップを使用してカスタムコンポーネントを変更できます。これは、コンポーネントの外観を向上させるカスタム CSS（カスケーディングスタイルシート）とカスタムコードを使用して実現できます。コンポーネントの実行時の動作を追加するには：

1. スタイル設定を追加するには、`/blocks/form/components/range/range.css` ファイルに移動して次のコード行を追加します。

   ```javascript
   /** Styling for range */
   main .form .range-widget-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, #ADD8E6 calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-widget-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-widget-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #00008B; /* Dark Blue */
   border: 3px solid #00008B; /* Dark Blue */
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-widget-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: #00008B; /* Dark Blue */
   }
   
   .range-widget-wrapper.decorated .range-bubble {
   color: #00008B; /* Dark Blue */
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   font-weight: bold;
   }
   
   .range-widget-wrapper.decorated .range-min,
   .range-widget-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-widget-wrapper.decorated .range-max {
   float: right;
   }
   ```
   このコードは、カスタムコンポーネントのスタイル設定と外観を定義するのに役立ちます。

1. 機能を追加するには、`/blocks/form/components/range/range.js` ファイルに移動して次のコード行を追加します。

   ```javascript
   function updateBubble(input, element) {
   const step = input.step || 1;
   const max = input.max || 0;
   const min = input.min || 1;
   const value = input.value || 1;
   const current = Math.ceil((value - min) / step);
   const total = Math.ceil((max - min) / step);
   const bubble = element.querySelector('.range-bubble');
   // during initial render the width is 0. Hence using a default here.
   const bubbleWidth = bubble.getBoundingClientRect().width || 31;
   const left = `${(current / total) * 100}% - ${(current / total) * bubbleWidth}px`;
   bubble.innerText = `${value}`;
   const steps = {
       '--total-steps': Math.ceil((max - min) / step),
       '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   
   export default async function decorate(fieldDiv, fieldJson) {
   console.log('RANGE DIV: ', fieldDiv);
   console.log('RANGE JSON: fieldJson', fieldJson);
    const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 10;
   input.max = input.max || 1000;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper decorated';
   input.after(div);
   const hover = document.createElement('span');
   hover.className = 'range-bubble';
   const rangeMinEl = document.createElement('span');
   rangeMinEl.className = 'range-min';
   const rangeMaxEl = document.createElement('span');
   rangeMaxEl.className = 'range-max';
   rangeMinEl.innerText = `${input.min || 1}`;
   rangeMaxEl.innerText = `${input.max}`;
   div.appendChild(hover);
   // move the input element within the wrapper div
   div.appendChild(input);
   div.appendChild(rangeMinEl);
   div.appendChild(rangeMaxEl);
   input.addEventListener('input', (e) => {
   updateBubble(e.target, div);
   });
   updateBubble(input, div);
   return fieldDiv;
   }
   ```

   これにより、カスタムコンポーネントがユーザー入力とやり取りし、データを処理し、ユニバーサルエディターのフォームブロックと統合する方法が制御されます。

   カスタムのスタイル設定と機能を組み込むと、範囲コンポーネントの外観と動作が強化されます。更新されたデザインは適用されたスタイルを反映し、追加された機能は、より動的でインタラクティブなユーザーエクスペリエンスを実現します。
以下のスクリーンショットは、更新された範囲コンポーネントを示しています。

![範囲コンポーネントスタイル](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## よくある質問

* **component.css と forms.css の両方にスタイル設定を追加した場合、どちらが優先されますか？**
`component.css` と **forms.css** の両方でスタイルが定義されている場合、`component.css` が優先されます。これは、コンポーネントレベルのスタイルがより具体的で、`forms.css` からのグローバルスタイルを上書きするからです。

* **カスタムコンポーネントが、ユニバーサルエディターの使用可能なコンポーネントのリストに表示されません。これを修正するにはどうすればよいですか？**
カスタムコンポーネントが表示されない場合は、次のファイルを確認して、コンポーネントが正しく登録されていることを確認してください。
   * **component-definition.json**：コンポーネントが正しく定義されていることを確認します。
   * **component-filters.json**：適切なセクションでコンポーネントが許可されていることを確認します。
   * **component-models.json**：コンポーネントモデルが正しく設定されていることを確認します。

## ベストプラクティス

* カスタムスタイルとコンポーネントをローカルで開発するには、[ローカル AEM 開発環境を設定](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment)することをお勧めします。


## 追加バイト

### サポートされるリソースタイプ

| フィールドタイプ | リソースタイプ |
|--------------|------------------------------------------------------------------|
| テキスト入力 | core/fd/components/form/textinput/v1/textinput |
| 数値入力 | core/fd/components/form/numberinput/v1/numberinput |
| 日付入力 | core/fd/components/form/datepicker/v1/datepicker |
| パネル | core/fd/components/form/panelcontainer/v1/panelcontainer |
| チェックボックス | core/fd/components/form/checkbox/v1/checkbox |
| ドロップダウン | core/fd/components/form/dropdown/v1/dropdown |
| ラジオグループ | core/fd/components/form/radiobutton/v1/radiobutton |
| プレーンテキスト | core/fd/components/form/text/v1/text |
| ファイル入力 | core/fd/components/form/fileinput/v2/fileinput |
| メール | core/fd/components/form/emailinput/v1/emailinput |
| 画像 | core/fd/components/form/image/v1/image |
| ボタン | core/fd/components/form/button/v1/button |

### サポートされるフィールドタイプ

フォームでサポートされるフィールドタイプは次のとおりです。
* テキスト入力
* 数値入力
* 日付入力
* パネル
* チェックボックス
* ドロップダウン
* ラジオグループ
* プレーンテキスト
* ファイル入力
* メール
* 画像
* ボタン

## 関連トピック

{{universal-editor-see-also}}
