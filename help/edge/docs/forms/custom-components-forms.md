---
title: EDS フォームのカスタムコンポーネントの作成
description: EDS フォームのカスタムコンポーネントの作成
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---

# カスタムコンポーネントの作成

AEM Forms Edge Delivery Servicesを使用すると、[ ネイティブHTMLのフォームコンポーネント ](/help/edge/docs/forms/form-components.md) をカスタマイズして、使いやすいインタラクティブなフォームを作成できます。 [ フォームフィールドのスタイル設定 ](/help/edge/docs/forms/style-theme-forms.md) カスタム CSS （カスケーディングスタイルシート）とコンポーネントを装飾するためのカスタムコードを使用します。これにより、アダプティブFormsブロック内のフォームフィールドの外観が向上します。

![ カスタムコンポーネント ](/help/edge/assets/custom-component-image.png)

このドキュメントでは、HTMLのネイティブフォームコンポーネントのスタイルを設定してカスタムコンポーネントを作成し、ユーザーエクスペリエンスを向上し、フォームの視覚的な魅力を高める手順について説明します。

フォームに `Estimated trip cost` を表示する `range` コンポーネントの例を見てみましょう。 `range` コンポーネントは、最小値、最大値、選択値などの値を表示せずに、直線として表示されます。

![ ネイティブ範囲コンポーネント ](/help/edge/assets/native-range-component.png)

CSS を使用してスタイルを追加し、コンポーネントをデコレートするカスタム関数を追加して、行に最小値、最大値、選択値を表示するように「`range`」フィールドをカスタマイズしてみましょう。

![ カスタム範囲コンポーネント ](/help/edge/assets/custom-range-component.png)

この記事を最後まで、CSS ファイルとカスタム関数にスタイルを追加してカスタムコンポーネントを作成する方法を説明します。

## 前提条件

カスタムコンポーネントの作成を開始する前に、次のことを行う必要があります。

* [ ネイティブHTMLコンポーネント ](/help/edge/docs/forms/form-components.md) の基本知識
* CSS セレクターを使用し、フィールドタイプに基づいてフォームフィールドのスタイルを設定する [ 方法を理解する ](/help/edge/docs/forms/style-theme-forms.md)


## カスタムコンポーネントの作成


![ カスタムコンポーネントの作成手順 ](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

各手順を詳しく説明します。

以下に説明する手順に従って、[ 問い合わせスプレッドシート ](/help/edge/docs/forms/assets/enquiry.xlsx) を参照して `range` コンポーネントをカスタマイズします。

### コンポーネントをデコレートするカスタム関数の追加

`[../Form Block/components]` に追加されたカスタム関数は、次の要素で構成されます。

* **関数宣言**：関数名とそのパラメーターを定義します。
* **ロジック実装**：コンポーネントのカスタム動作を追加するロジックを記述します。
* **関数のエクスポート**:`[Form Block]` で関数にアクセスできるようにします。

範囲コンポーネントのスタイルを設定するために、`range.js` という名前のJavaScript ファイルを作成します。 カスタム関数を追加するには：

1. Google ドライブまたはSharePointのAEM プロジェクトフォルダーに移動します。
1. `[../Form Block/components]` に移動します。
1. `range.js` という名前の新規ファイルを追加します。
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

### フォームブロックへのデコレータの挿入

`[Form Block]` では、セマンティックHTMLを使用して、アクセシビリティの標準属性を持つフォームフィールド（入力フィールド、ラベル、ヘルプテキストなど）をレンダリングします。 `[Form Block]` で指定したコンポーネントにカスタムデコレーターを使用するには、`mappings.js` ファイルでカスタムデコレーターを定義します。 `mappings.js` ファイルは、特定のコンポーネントのデコレートを担当するモジュールを返す関数を読み込みます。 この関数は、フィールドプロパティを受け取り、フォームフィールドのデコレーター関数を返します。

この場合、この関数はフィールドの `fieldType` プロパティをチェックし、`[../Form Block/components]` に存在する `range.js` ファイルからカスタム範囲デコレーターを返します。

フォームブロックにデコレータを挿入するには、次の手順を実行します。

1. `[../Form Block/]` に移動し、`mapping.js` を開きます。
1. 次のコード行を追加します。

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default;
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. 変更を保存します。

### CSS ファイルでコンポーネントのスタイルを追加します

CSS セレクターを使用して、フィールドタイプとフィールド名に基づいてフォームフィールドの外観を変更し、要件に基づいて一貫した、または一意のスタイル設定を行うことができます。 コンポーネントのスタイルを設定するには、`form.css` ファイルにコードを追加して、フォームのコンポーネントのルックアンドフィールを変更します。

`range` コンポーネントのスタイルをカスタマイズするには、フォーム内の `range` 入力要素とその関連コンポーネントをスタイル設定する CSS コードスニペットを含めます。 これは、`.form` や `.range-wrapper` などのクラスを持つ構造化されたHTMLレイアウトを前提としています。

CSS ファイルでコンポーネントのスタイルを追加するには、次の手順を実行します。
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

### ファイルをデプロイしてプロジェクトをビルドします

更新された `range.js`、`mapping.css` および `form.css` ファイルを GitHub プロジェクトにデプロイし、ビルドが正常に完了したことを確認します。

### AEM サイドキックを使用したフォームのプレビュー

[AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用して、`range` コンポーネントのスタイルを設定する新しく実装された関数を含むフォームをプレビューします。

![ カスタムコンポーネントフォーム ](/help/edge/assets/custom-componet-form.png)

`range` コンポーネントの新しいスタイル設定は、CSS と、コンポーネントのデコレーターを含むカスタム関数を使用してスタイルを追加することにより、行の最小値、最大値、選択値を表示します。


## 関連トピック

{{see-more-forms-eds}}



