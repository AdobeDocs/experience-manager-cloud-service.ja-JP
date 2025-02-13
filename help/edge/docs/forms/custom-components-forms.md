---
title: EDS フォームのカスタムコンポーネントの作成
description: EDS フォームのカスタムコンポーネントの作成
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d71c5d6488935de4a02c8d3828f287542b979d0f
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 96%

---

# カスタムコンポーネントの作成

AEM Forms の Edge Delivery Services を使用すると、[ネイティブ HTML フォームコンポーネント](/help/edge/docs/forms/form-components.md)をカスタマイズし、ユーザーにわかりやすいインタラクティブなフォームを作成できます。これにより、カスタム CSS（カスケーディングスタイルシート）とコンポーネントを装飾するためのカスタムコードを使用した[フォームフィールドのスタイル設定](/help/edge/docs/forms/style-theme-forms.md)の説明に従って、定義済みのマークアップを使用してフォームコンポーネントを変更し、アダプティブフォームブロック内のフォームフィールドの外観を向上させることができます。

![カスタムコンポーネント](/help/edge/assets/custom-component-image.png)

このドキュメントでは、ネイティブ HTML フォームコンポーネントをスタイル設定してカスタムコンポーネントを作成し、ユーザーエクスペリエンスを向上させ、フォームの視覚的な魅力を高める手順について説明します。

フォームに `Estimated trip cost` を表示する `range` コンポーネントの例を見てみましょう。`range` コンポーネントは直線として表示され、最小値、最大値、選択した値などの値は表示されません。

![ネイティブ範囲コンポーネント](/help/edge/assets/native-range-component.png)

CSS を使用してスタイルを追加したり、コンポーネントを装飾するカスタム関数を追加したりして、行に最小値、最大値、選択した値を表示するように `range` フィールドをカスタマイズしてみましょう。

![カスタム範囲コンポーネント](/help/edge/assets/custom-range-component.png)

この記事を最後まで読むと、CSS ファイルとカスタム関数にスタイルを追加してカスタムコンポーネントを作成する方法を理解できるようになります。

## 前提条件

カスタムコンポーネントの作成を開始する前に、次のことを行う必要があります。

* [ネイティブ HTML コンポーネント](/help/edge/docs/forms/form-components.md)の基本知識を持つ。
* [CSS セレクターを使用してフィールドタイプに基づいてフォームフィールドをスタイル設定](/help/edge/docs/forms/style-theme-forms.md)する方法を理解する


## カスタムコンポーネントの作成


![カスタムコンポーネントの作成手順](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

各手順を詳しく理解しましょう。

<!--Refer to the [enquiry spreadsheet](/help/edge/docs/forms/assets/enquiry.xlsx) to customize the `range` component, by following the steps as explained below.-->

### コンポーネントを装飾するカスタム関数の追加

`[../Form Block/components]` に追加したカスタム関数は、次の要素で構成されます。

* **関数宣言**：関数名とそのパラメーターを定義します。
* **ロジック実装**：コンポーネントのカスタム動作を追加するロジックを書き込みます。
* **関数の書き出し**：`[Form Block]` で関数にアクセスできるようにします。

カスタム関数を追加するには：

1. `[../Form Block/components]` に移動します。
1. `range.js` という名前のファイルを見つけます。 存在しない場合は作成します。
1. 次のコード行を追加します。

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
   '--total-steps': Math.ceil((max - min) /    step),
   '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   // eslint-disable-next-line no-unused-vars
   export default function decorateRange(fieldDiv, field) {
   loadCSS('/blocks/form/components/range/range.css');
   const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 1;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper';
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
   // as a best practice add a custom css class to apply custom styling
   fieldDiv.classList.add('decorated');
   return fieldDiv;    
   }
   ```

1. 変更を保存します。

### フォームブロックへのデコレーターの挿入

`[Form Block]` では、セマンティック HTML を使用して、入力フィールド、ラベル、ヘルプテキストなどのフォームフィールドを、アクセシビリティの標準属性を使用してレンダリングします。`[Form Block]` に対し、指定したコンポーネントにカスタムデコレーターを使用させるには、`mappings.js` ファイルで定義します。`mappings.js` ファイルは、特定のコンポーネントの装飾を行うモジュールを返す関数を読み込みます。この関数はフィールドのプロパティを受け取り、フォームフィールドのデコレーター関数を返します。

この場合、関数はフィールドの `fieldType` プロパティをチェックし、`[../Form Block/components]` に存在する `range.js` ファイルからカスタム範囲デコレーターを返します。

フォームブロックにデコレーターを挿入するには：

1. `[../Form Block/]` に移動し、`mapping.js` を開きます。
1. 次のコード行を追加します。

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default(element,fd);
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. 変更を保存します。

### CSS ファイルでコンポーネントにスタイルを追加する

CSS セレクターを使用して、フィールドタイプとフィールド名に基づいてフォームフィールドの外観を変更し、要件に基づいて一貫したスタイルを設定したり、独自のスタイルを設定したりできます。コンポーネントをスタイル設定するには、`form.css` ファイルにコードを追加して、フォームのコンポーネントのルックアンドフィールを変更します。

`range` コンポーネントのスタイルをカスタマイズするには、フォーム内の `range` 入力要素とその関連コンポーネントをスタイル設定する CSS コードスニペットを含めます。これは、`.form` や `.range-wrapper` などのクラスを含む構造化された HTML レイアウトを想定しています。

CSS ファイルでコンポーネントのスタイルを追加するには：
1. `[../Form Block/]` に移動し、`form.css` を開きます。
1. 次のコード行を追加します。

   ```javascript
       /** styling for range */
   main .form .range-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, var(--button-primary-color) calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #fff;
   border: 3px solid var(--button-primary-color);
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: var(--button-primary-color);
   }
   
   .range-wrapper.decorated .range-bubble {
   color: #17252e;
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   }
   
   .range-wrapper.decorated .range-min,
   .range-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-wrapper.decorated .range-max {
   float: right;
   }
   ```
1. 変更を保存します。

### ファイルをデプロイしてプロジェクトをビルド

更新された `range.js`、`mapping.js`、`form.css` ファイルを GitHub プロジェクトにデプロイし、ビルドが成功したことを確認します。

### AEM Sidekick を使用してフォームをプレビュー

`range` コンポーネントをスタイル設定する新しく実装された関数を使用して、フォームをプレビューします。

![カスタムコンポーネントフォーム](/help/edge/assets/custom-componet-form.png)

`range` コンポーネントの新しいスタイルでは、CSS とカスタム関数（コンポーネントのデコレーターを含む）を使用してスタイルを追加することで、行に最小値、最大値、選択した値が表示されます。
<!--
Now, you can extend the created custom component for WYSIWYG based authoring.

## Enable Component for WYSIWYG authoring

To enable component for WYSIWYG authoring:

1. Navigate to  `[../Form Block/components]`.
2. Locate a file named `_range.json`. if not present, create it.
3. Add the following code in the  `_range.json` file:

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

    The above code snippet in the `_range.json` file includes the component definition, component model and custom properties for your custom component.


    ![component definition and model](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)

4. Navigate to the `/blocks/form/_form.json` file and add the `fd:viewType` value from the `definitions[]` to the components array of the object with `id="form"`.

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

    The above code snippet defines the section in which the custom component can be used in Universal Editor.
    
    ![component filter](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

5. Navigate to the `/blocks/form/mappings.js` file and add the `fd:viewType` value from the `definitions[]` array to the `customComponents[]` array.

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

The above code snippet enables the form block to recognize the custom component and load its properties defined in the component model during form authoring in Universal Editor.

![component mapping](/help/edge/docs/forms/universal-editor/assets/custom-component-mapping-file.png)

Now, you can see your custom component in the WYSIWYG based authoring:

![Range component](/help/edge/docs/forms/universal-editor/assets/custom-component-range-doc-based.png)

>[!NOTE]
>
> For detailed steps on creating a custom component for the Universal Editor, refer to the [Create Custom Component in WYSIWYG based authoring](/help/edge/docs/forms/universal-editor/create-custom-component) article. -->

## 関連トピック

{{see-more-forms-eds}}




