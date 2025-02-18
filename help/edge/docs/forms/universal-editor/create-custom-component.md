---
title: EDS フォームのカスタムコンポーネントの作成
description: EDS フォームのカスタムコンポーネントの作成
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: bf70adcb95ddf88d0ea9a496efe3ae47f71f6a1d
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 5%

---

# WYSIWYG オーサリングでのカスタムコンポーネントの作成

Edge Delivery Services Formsは、フロントエンド開発者がカスタマイズされたフォームコンポーネントを構築できるようにするカスタマイズサービスを提供します。 これらのカスタムコンポーネントは、WYSIWYGのオーサリングエクスペリエンスにシームレスに統合されるので、フォーム作成者はフォームエディター内で簡単に追加、設定、管理できます。 カスタムコンポーネントを使用すると、作成者は、スムーズで直感的なオーサリングプロセスを確保しながら、機能を強化できます。

このドキュメントでは、ネイティブ HTML フォームコンポーネントをスタイル設定してカスタムコンポーネントを作成し、ユーザーエクスペリエンスを向上させ、フォームの視覚的な魅力を高める手順について説明します。

## 前提条件

カスタムコンポーネントの作成を開始する前に、次のことを行う必要があります。

* [ネイティブ HTML コンポーネント](/help/edge/docs/forms/form-components.md)の基本知識を持つ。
* [CSS セレクターを使用してフィールドタイプに基づいてフォームフィールドをスタイル設定](/help/edge/docs/forms/style-theme-forms.md)する方法を理解する

## カスタムコンポーネントの作成

ユニバーサルエディターでのカスタムコンポーネントの追加とは、フォーム作成者がフォームのデザイン中に使用できる新しいコンポーネントを作成することです。 これには、コンポーネントの登録、プロパティの定義、および使用可能な場所の設定が含まれます。 カスタムコンポーネントを作成する手順は次のとおりです。

[1. 新しいカスタムコンポーネントの構造 ](#1-adding-structure-for-new-custom-component) 追加
[2。 オーサリング用のカスタムコンポーネントのプロパティの定義 ](#2-defining-the-properties-of-your-custom-component-for-authoring)
[3。  カスタムコンポーネントをWYSIWYG コンポーネントリストに表示する ](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4。 カスタムコンポーネントの登録 ](#4-registering-your-custom-component)
[5。 カスタムコンポーネントの実行時の動作の追加 ](#5-adding-the-runtime-behaviour-for-your-custom-component)

例として、「**範囲**」という新しいカスタムコンポーネントを作成する場合を見てみましょう。 範囲コンポーネントは直線で表示され、最小値、最大値、選択値などの値が表示されます。

![ 範囲コンポーネントスタイル ](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

この記事を最後まで学習すると、カスタムコンポーネントを最初から作成する方法を理解できます。

### 1.新しいカスタムコンポーネントの構造の追加

カスタムコンポーネントを使用する前に、ユニバーサルエディターで使用可能なオプションとして認識されるように登録する必要があります。 これは、一意の識別子、デフォルトプロパティ、コンポーネントの構造を含むコンポーネント定義によって実現されます。カスタムコンポーネントをフォームオーサリングで使用できるようにするには、次の手順を実行します。

1. **新しいフォルダーとファイルの追加**
AEM プロジェクトに新しいカスタムコンポーネント用の新しいフォルダーとファイルを追加します。
   1. AEM プロジェクトを開き、`../blocks/form/components/` に移動します。
   1. `../blocks/form/components/<component_name>` でカスタムコンポーネントの新しいフォルダーを追加します。 この例では、`range` という名前のフォルダーを作成します。
   1. `../blocks/form/components/<component_name>` に新しく作成したフォルダーに移動します。 例えば、`../blocks/form/components/range` に移動して、次のファイルを追加します。
      * `/blocks/form/components/range/_range.json`：カスタムコンポーネントの定義が含まれます。
      * `../blocks/form/components/range/range.css`: カスタムコンポーネントのスタイル設定を定義します。
      * `../blocks/form/components/range/range.js`：実行時にカスタムコンポーネントをカスタマイズします。

        ![ オーサリング用のカスタムコンポーネントの追加 ](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > JSON ファイルのファイル名にプレフィックスとしてアンダースコア（_）が含まれていることを確認してください。

1. `/blocks/form/components/range/_range.json` ファイルに移動し、カスタムコンポーネントのコンポーネント定義を追加します。

1. **コンポーネント定義の追加**

   定義を追加するには、`_range.json` ファイルに次のフィールドを追加する必要があります。

   * **タイトル**：ユニバーサルエディターに表示されるコンポーネントのタイトル。
   * **id**: コンポーネントの一意の識別子。
   * **fieldType**:Formsでは、特定の種類のユーザー入力を取り込むために、様々な **fieldType** をサポートしています。 [ サポートされている fieldType は、Extra Byte セクション ](#supported-fieldtypes) にあります。
   * **resourceType**：各カスタムコンポーネントは、fieldType に基づいてリソースタイプを関連付けます。 [ サポートされている resourceType は、Extra Byte セクション ](#supported-resourcetype) にあります。
   * **jcr:title**：タイトルに似ていますが、コンポーネントの構造内に保存されます。
   * **fd:viewType**：カスタムコンポーネントの名前を表します。 これは、コンポーネントの一意の ID です。 コンポーネントのカスタマイズされたビューを作成する必要があります。

コンポーネント定義を追加した後の `_range.json` ファイルを次に示します。

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
> フォーム関連のすべてのコンポーネントは、ユニバーサルエディターにブロックを追加する場合、サイトと同じアプローチに従います。 詳しくは、[ ユニバーサルエディターで使用するために実装されたブロックの作成 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block) の記事を参照してください。

### 2. オーサリング用のカスタムコンポーネントのプロパティの定義

カスタムコンポーネントには、フォーム作成者が設定可能なプロパティを指定するコンポーネントモデルが含まれています。 これらのプロパティは、ユニバーサルエディターの **プロパティ** ダイアログに表示され、作成者がラベル、検証ルール、スタイル、その他の属性などの設定を調整できます。 プロパティを定義するには：

1. `/blocks/form/components/range/_range.json` ファイルに移動し、カスタムコンポーネントのコンポーネントモデルを追加します。

1. **コンポーネントモデルを追加**

   カスタムコンポーネントのコンポーネントモデルを定義するには、関連するフィールドを `_range.json` ファイルに追加する必要があります。

   1. **新しいモデルを作成**

      * models 配列に、新しいオブジェクトを追加し、コンポーネント定義で以前に設定した `fd:viewType` プロパティと一致するようにコンポーネントモデルの `id` を設定します。
      * このオブジェクト内にフィールド配列を含めます。

   2. **プロパティダイアログのフィールドの定義**

      * fields 配列の各オブジェクトは、**プロパティ** ダイアログにタブとして表示できる、コンテナタイプのコンポーネントである必要があります。
      * 一部のフィールドでは、`models/form-common` で使用可能な再利用可能なプロパティを参照できます。

   3. **既存のコンポーネントモデルを参照として使用**

      * 選択したコンポー `fieldType` ントに対応する既存のコンポーネントモデルの内容をコピーし、必要に応じて変更できます。 例えば、`number-input` コンポーネントを拡張して **range** コンポーネントを作成し、`models/form-components/_number-input.json` の models 配列を参照として使用できます。

   コンポーネントモデルを追加した後の `_range.json` ファイルを次に示します。

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
   > カスタムコンポーネントの **プロパティ** ダイアログに新しいフィールドを追加するには、[ 定義されたスキーマ ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model) に従います。

   また、カスタムコンポーネントに [ カスタムプロパティを追加 ](#adding-custom-properties-for-your-custom-component) して、その機能を拡張することもできます。

#### カスタムコンポーネントへのカスタムプロパティの追加

カスタムプロパティを使用すると、コンポーネントのプロパティダイアログで設定された値に基づいて特定の動作を定義できます。 これは、コンポーネントの機能とカスタマイズオプションを拡張するのに役立ちます。

この例では、ステップ値をカスタムプロパティとして範囲コンポーネントに追加します。

![ ステップ値のカスタムプロパティ ](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

ステップ値のカスタムプロパティを追加するには、ファイルに次のコード行を含むコンポーネントモデルを追加し ` _<component>.json` す。

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

JSON スニペットは、**範囲** コンポーネントに **ステップ値** と呼ばれるカスタムプロパティを定義します。 各フィールドの分類を次に示します。

* **component**: プロパティダイアログで使用される入力フィールドのタイプを指定します。 この場合、`number` は、フィールドが数値を受け入れることを示します。
* **name**: プロパティの識別子。コンポーネントのロジックで参照するために使用されます。 ここで、`stepValue` は範囲のステップ値の設定を表します。
* **label**: プロパティダイアログに表示されるプロパティの表示名。
* **valueType**：プロパティに必要なデータタイプを定義します。 `number` では、数値の入力のみが許可されます。

`range.js` の JSON プロパティでカスタムプロパティとして `stepValue` を使用し、実行時にその値に基づいて動的な動作を実装できるようになりました。

したがって、コンポーネント定義、コンポーネントモデル、カスタムプロパティを追加した後の最終的な `_range.json` ファイルは次のようになります。

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

![ コンポーネント定義とモデル ](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)


### 3. カスタムコンポーネントをWYSIWYG コンポーネントリストに表示する

フィルターは、ユニバーサルエディターでカスタムコンポーネントを使用できるセクションを定義します。 これにより、コンポーネントは適切なセクションでのみ使用でき、構造と操作性が維持されます。

WYSIWYGでのフォームのオーサリング時に、使用可能なコンポーネントのリストにカスタムコンポーネントが表示されるようにするには、次の手順を実行します。

1. `/blocks/form/_form.json` ファイルに移動します。
1. `id="form"` を持つオブジェクト内のコンポーネント配列を見つけます。
1. `definitions[]` の `fd:viewType` 値を、`id="form"` を持つオブジェクトのコンポーネント配列に追加します。

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

![ コンポーネントフィルター ](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

### 4. カスタムコンポーネントの登録

フォームブロックがカスタムコンポーネントを認識できるようにし、フォームのオーサリング時にコンポーネントモデルで定義されたプロパティを読み込むには、`fd:viewType` の値をコンポーネント定義から `mappings.js` ファイルに追加します。
コンポーネントを登録するには：
1. `/blocks/form/mappings.js` ファイルに移動します。
1. `customComponents[]` アレイを見つけます。
1. `definitions[]` 配列から `customComponents[]` 配列に `fd:viewType` 値を追加します。

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

![ コンポーネントマッピング ](/help/edge/docs/forms/universal-editor/assets/custom-component-mapping-file.png)

上記の手順を完了すると、カスタムコンポーネントがユニバーサルエディター内のフォームのコンポーネントリストに表示されます。 その後、フォームセクションにドラッグ&amp;ドロップできます。

![ 範囲コンポーネント ](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

次のスクリーンショットは、コンポーネントモデルに追加された `range` コンポーネントのプロパティを示しています。このプロパティは、フォーム作成者が設定できるプロパティを指定しています。

![ 範囲コンポーネントのプロパティ ](/help/edge/docs/forms/universal-editor/assets/range-properties.png)

スタイルと機能を追加して、カスタムコンポーネントの実行時の動作を定義できるようになりました。

### 5. カスタムコンポーネントのランタイム動作の追加

[ フォームフィールドのスタイル設定 ](/help/edge/docs/forms/style-theme-forms.md) で説明されているように、事前定義済みのマークアップを使用してカスタムコンポーネントを変更できます。 これを実現するには、カスタム CSS （カスケーディングスタイルシート）とカスタムコードを使用して、コンポーネントの外観を向上します。 コンポーネントのランタイム動作を追加するには：

1. スタイル設定を追加するには、`/blocks/form/components/range/range.css` ファイルに移動し、次のコード行を追加します。

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
   このコードは、カスタムコンポーネントのスタイル設定と外観の定義に役立ちます。

1. 機能を追加するには、`/blocks/form/components/range/range.js` ファイルに移動し、次のコード行を追加します。

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

   カスタムコンポーネントがユーザー入力とどのように相互作用し、データを処理し、ユニバーサルエディターのフォームブロックとどのように統合するかを制御します。

   カスタムスタイル設定と機能を組み込むと、範囲コンポーネントの外観と動作が強化されます。 更新されたデザインは、適用されたスタイルを反映し、追加された機能は、より動的でインタラクティブなユーザーエクスペリエンスを保証します。
次のスクリーンショットは、更新された範囲コンポーネントを示しています。

![ 範囲コンポーネントスタイル ](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## よくある質問

* **component.css と forms.css の両方のスタイル設定を追加する場合、どちらが優先されますか？**
スタイルが `component.css` と **forms.css** の両方で定義されている場合は、`component.css` が優先されます。 これは、コンポーネントレベルのスタイルがより具体的で、`forms.css` のグローバルスタイルを上書きするからです。

* **ユニバーサルエディターで使用可能なコンポーネントのリストにカスタムコンポーネントが表示されません。 これを修正するにはどうすればよいですか？**
カスタムコンポーネントが表示されない場合は、次のファイルを確認して、コンポーネントが正しく登録されていることを確認してください。
   * **component-definition.json**: コンポーネントが正しく定義されていることを確認します。
   * **component-filters.json**：適切なセクションでコンポーネントが許可されていることを確認します。
   * **component-models.json**：コンポーネントモデルが正しく設定されていることを確認します。

## ベストプラクティス

* カスタムスタイルやコンポーネントをローカルで開発する場合は、[ ローカル AEM開発環境をセットアップ ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment) することをお勧めします。


## 余分なバイト

### サポートされる resourceType

| フィールドタイプ | リソースタイプ |
|--------------|------------------------------------------------------------------|
| テキスト入力 | core/fd/components/form/textinput/v1/textinput |
| 数値入力 | core/fd/components/form/numberinput/v1/numberinput |
| 日付 – 入力 | core/fd/components/form/datepicker/v1/datepicker |
| panel | core/fd/components/form/panelcontainer/v1/panelcontainer |
| チェックボックス | core/fd/components/form/checkbox/v1/checkbox |
| ドロップダウン | core/fd/components/form/dropdown/v1/dropdown |
| radio-group | core/fd/components/form/radiobutton/v1/radiobutton |
| プレーンテキスト | core/fd/components/form/text/v1/text |
| file-input | core/fd/components/form/fileinput/v2/fileinput |
| email | core/fd/components/form/emailinput/v1/emailinput |
| 画像 | core/fd/components/form/image/v1/image |
| button | core/fd/components/form/button/v1/button |

### サポートされる fieldTypes

フォームでサポートされる fieldType は次の通りです。
* テキスト入力
* 数値入力
* 日付 – 入力
* panel
* チェックボックス
* ドロップダウン
* radio-group
* プレーンテキスト
* file-input
* email
* 画像
* button

## 関連トピック

{{see-more-forms-eds}}
