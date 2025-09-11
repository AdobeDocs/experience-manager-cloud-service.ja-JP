---
title: EDS フォームのカスタムコンポーネントの作成
description: EDS フォームのカスタムコンポーネントの作成
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 6a63b4f839516a2ebc1eec641eb36315efca6dd5
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 4%

---


# アダプティブフォームブロックでのカスタムフォームコンポーネントの作成

Edge Delivery Services Forms には、カスタマイズ機能が用意されているので、フロントエンド開発者は調整されたフォームコンポーネントを作成できます。これらのカスタムコンポーネントは WYSIWYG オーサリングエクスペリエンスにシームレスに統合されるので、フォーム作成者はフォームエディター内で簡単に追加、設定、管理できます。カスタムコンポーネントを使用すると、作成者はスムーズで直感的なオーサリングプロセスを確保しながら機能を強化できます。

このドキュメントでは、ネイティブ HTML フォームコンポーネントをスタイル設定してカスタムコンポーネントを作成し、ユーザーエクスペリエンスを向上させ、フォームの視覚的な魅力を高める手順について説明します。

## アーキテクチャの概要

Forms ブロックのカスタムコンポーネントは、**MVC （Model-View-Controller）** アーキテクチャパターンに従います。

### モデル

- `field/component` ごとに JSON スキーマによって定義されます。

- オーサリング可能なプロパティは、対応する JSON ファイルで指定されています（blocks/form/models/form- components を参照）。

- これらのプロパティは、フォームビルダーで作成者が使用でき、フィールド定義（fd）の一部としてコンポーネントに渡されます。

### 表示

- 各フィールドタイプのHTMLの構造については、form-field-types を参照してください。

- これは、拡張または変更できるコンポーネントの基本構造です。

- 各 OOTB コンポーネントのHTMLの基本構造については、form-field-types を参照してください。

### コントローラ/コンポーネント ロジック

- JavaScriptに OOTB （標準）またはカスタムコンポーネントとして実装されます。  - カスタムコンポーネントの場合は `blocks/form/components` にあります。

## OOTB コンポーネント

**OOTB （標準）** コンポーネントは、カスタム開発の基盤となります。

- OOTB コンポーネントは `blocks/form/models/form-components` にあります。

- 各 OOTB コンポーネントには、オーサリング可能なプロパティ（例：` _text-input.json`,`_drop-down.json`）を定義する JSON ファイルがあります。

- これらのプロパティは、フォームビルダーで作成者が使用でき、フィールド定義（fd）の一部としてコンポーネントに渡されます。

- 各 OOTB コンポーネントのHTMLの基本構造については、form-field-types を参照してください。

既存の OOTB コンポーネントを拡張すると、基本構造、動作、プロパティを再利用しながら、必要に応じてカスタマイズできます。

- カスタムコンポーネントは、事前定義済みの OOTB コンポーネントのセットから拡張する必要があります。

- フィールドの JSON の `viewType` プロパティに基づいて、拡張する OOTB コンポーネントが識別されます。

- システムは、許可されたカスタムコンポーネントバリアントのレジストリを保持します。 このレジストリにリストされているバリアントのみを使用できます（例：`customComponents[]` の `mappings.js`）。

- フォームのレンダリング時には、システムはバリアントプロパティまたは `:type/fd:viewType` をチェックし、登録済みのカスタムコンポーネントと一致する場合は、対応する JS および CSS ファイルを `blocks/form/components` フォルダーから読み込みます。

- カスタムコンポーネントは OOTB コンポーネントのベース HTML構造に適用され、動作と外観を拡張またはオーバーライドできます。

## カスタムコンポーネントの構造

カスタムコンポーネントを作成するには、**基礎モード CLI** を使用して、コンポーネントに必要なファイルとフォルダーを設定し、カスタムコンポーネントのコードを追加します。

- カスタムコンポーネントは `blocks/form/components` フォルダーにあります。

- 各カスタムコンポーネントは、コンポーネントにちなんで名前が付けられた独自のフォルダー（カードなど）に配置する必要があります。 フォルダー内で、次のファイルを指定します。

   - **_cards.json** - OOTB コンポーネントのコンポーネント定義を拡張する JSON ファイル。オーサリング可能なプロパティ（model[]）と読み込み時のコンテンツ構造（definitions[]）を定義します。
   - **cards.js** - メインロジックを含むJavaScript ファイル。
   - **cards.css** - オプション。スタイル用。

- フォルダー名と JS/CSS ファイルは一致する必要があります。

### カスタムコンポーネントでのフィールドの再利用と拡張

カスタムコンポーネントの JSON でフィールドを定義する場合（任意のフィールドグループ、基本、検証、ヘルプなど）、保守性と一貫性については、次のベストプラクティスに従います。

- 既存の共有コンテナまたはフィールド定義（`../form-common/_basic-input-placeholder-fields.json#/fields`、`../form-common/_basic- validation-fields.json#/fields` など）を参照して、標準/共有フィールドを再利用します。 これにより、すべての標準オプションを複製せずに継承できます。

- 新規フィールドまたはカスタムフィールドのみをコンテナに明示的に追加します。 これにより、スキーマが乾燥し、フォーカスされた状態が維持されます。

- 参照を介して既に含まれているフィールドの重複を削除または回避します。 コンポーネントのロジックに固有のフィールドのみを定義します。

- 一貫性と保守性を保つために、必要に応じて、ヘルプコンテナやその他の共有コンテンツ（`../form-common/_help-container.json` など）を参照します。

>[!TIP]
>
> - このパターンにより、将来のロジックの更新や拡張が容易になり、カスタムコンポーネントが残りのフォームシステムとの一貫性を保つようになります。
> - 新しい共有コンテナまたはフィールド定義を追加する前に、必ず既存の共有コンテナまたはフィールド定義を確認してください。

### カスタムコンポーネントの新しいプロパティの定義

- カスタムコンポーネントの新しいプロパティを作成者から取得する必要がある場合は、コンポーネントの JSON 内のコンポーネントの `fields[]` 配列にフィールドを定義することで行うことができます。

- カスタムコンポーネントは、:type プロパティを使用して識別され、JSON ファイルで `fd:viewType` のように設定できます（例：`fd:viewType: cards`）。 これにより、システムは正しいカスタムコンポーネントを認識して読み込めるので、カスタムコンポーネントにはこの操作が必須です

- JSON 定義に追加された新しいプロパティは、フィールド定義でプロパティとして使用できます。 コンポーネントの JS ロジックの `<propertyName>`

## カスタムコンポーネントJavaScript API

カスタムコンポーネント JavaScript API では、カスタムフォームコンポーネントの動作、外観、反応性を制御する方法を定義します。

### Decorate 関数

**decorate** 関数は、カスタムコンポーネントのエントリポイントです。 コンポーネントを初期化し、JSON 定義とリンクし、HTMLの構造と動作を操作できるようにします。

>[!NOTE]
>
> カスタムコンポーネントのJavaScript ファイルでは、デフォルトの関数を decorate としてエクスポートする必要があります。

#### 関数のシグネチャ：

```javascript
export default function decorate(element, fieldJson, container, formId) {
// element: The HTML structure of the OOTB component you are extending
// fieldJson: The JSON field definition (all authorable properties)
// container: The parent element (fieldset or form)
// formId: The id of the form
// ... your logic here ...
}
```

次の操作が可能です。

- **要素の変更**：イベントリスナーの追加、属性の更新、追加のマークアップの挿入をおこないます。

- **JSON プロパティへのアクセス**:`fd.properties.<propertyName>` を使用して、JSON スキーマで定義された値を読み取り、コンポーネントロジック内に適用します。

## Subscribe 関数

**subscribe** 関数を使用すると、フィールド値やカスタムイベントの変更にコンポーネントを反応させることができます。 これにより、コンポーネントとフォームのデータモデルの同期が保たれ、UI を動的に更新できます。

### 関数のシグネチャ：

```JavaScript
import { subscribe } from '../../rules/index.js';

export default function decorate(fieldDiv, fieldJson, container, formId) {
// Access custom properties defined in the JSON
const { initialText, finalText, time } = fieldJson?.properties;
// ... setup logic ...
subscribe(fieldDiv, formId, (_fieldDiv, fieldModel) => { fieldModel.subscribe(() => {
// React to custom event (e.g., resetCardOption)
// ... logic ...
}, 'resetCardOption');
});
}
```

次の操作が可能です。

- **コールバックの登録**:**subscribe （element, formId, callback）** を呼び出すと、フィールドデータが変更されるたびに実行するコールバックが登録されます。次の 2 つのコールバックパラメーターを使用します。
   - **element**：フィールドを表すHTML要素。
   - **fieldModel**：フィールドの状態 API とイベント API を表すオブジェクト。

- **変更またはイベントをリッスン**:`fieldModel.subscribe((event) => { ... }, 'eventName')` を使用すると、値が変更されるたびに、またはカスタムイベントがトリガーされるたびにロジックを実行します。 イベントオブジェクトには、変更内容の詳細が含まれています。

## カスタムコンポーネントの作成

この節では、OOTB ラジオボタンコンポーネントを拡張して **カードカスタムコンポーネント** を作成するプロセスについて説明します。

![ カードカスタムコンポーネント ](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;1. コードのセットアップ

#### 1.1 ファイルとフォルダ

最初の手順では、カスタムコンポーネントの必要なファイルを設定し、リポジトリのコードにワイヤリングします。 このプロセスは、**AEM Forms基礎モード CLI** によって自動的に実行されます。これにより、基礎モードを設定して必要なファイルをワイヤリングする作業が迅速になります。

>[!VIDEO](https://video.tv.adobe.com/v/3474752)

1. ターミナルを開き、フォームプロジェクトのルートに移動します。
2. 次のコマンドを実行します。

```bash
npm install
npm run create:custom-component
```

![ 基礎モード CLI](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

次のようになります。

- **新しいコンポーネントに名前を付けるよう求めるプロンプト** 表示されます。 例えば、この場合はカードを使用します。
- **選択を依頼** ベースコンポーネント （ラジオグループを選択）

これにより、以下を含む、必要なすべてのフォルダーとファイルが作成されます。

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

さらに、CLI の出力に示されているように、このコードをリポジトリ内の残りのコードとワイヤリングします。
次の機能が自動的に実行されます。

- フィルターにカードを追加して、アダプティブフォームブロック内に追加できるようにします。
- 新しいカードコンポーネントを含むように `mappings.js` の許可リストを更新しました。
- ユニバーサルエディターの **カスタムコンポーネント** リストの下にカードコンポーネントの定義を登録します。

>[!NOTE]
>
> 手動（レガシー）方式を使用してカスタムコンポーネントを作成することもできます。 詳しくは、[ 手動または従来の方法 ](#manual-or-legacy-method-to-create-custom-component) によるカスタムコンポーネントの作成」の節を参照してください。

#### 1.2 ユニバーサルエディターでのコンポーネントの使用

1. **ユニバーサルエディターを更新**：ユニバーサルエディターでフォームを開き、ページを更新して、リポジトリから最新のコードが読み込まれるようにします。

2. **カスタムコンポーネントの追加**

   1. フォームキャンバスの「**追加（+）**」ボタンをクリックします。
   2. カスタムコンポーネント セクションまでスクロールします。
   3. 新しく作成した **カードコンポーネント** を選択して、フォームに挿入します。

      ![ カスタムコンポーネントを選択 ](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

内にコードが存在しないので `cards.js` カスタムコンポーネントはラジオグループとしてレンダリングされます。

#### 1.3 ローカルでのプレビューとテスト

これで、フォームにカスタムコンポーネントが含まれたので、フォームをプロキシし、ローカルで変更して、変更内容を確認できます。

1. ターミナルに移動し、`aem up` を実行します。

2. `http://localhost:3000/{path-to-your-form}` で開始したプロキシサーバーを開きます（パスの例：`/content/forms/af/custom-component-form`）


### &#x200B;2. カスタムコンポーネントのカスタム動作の実装

#### 2.1 カスタムコンポーネントのスタイル設定

スタイル設定のためにクラス **card** をコンポーネントに追加し、各ラジオに画像を追加しましょう。これには以下のコードを使用します。

**cards.js の decorate 関数を使用したカスタムコンポーネントのスタイル設定**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';

export default function decorate(element, fieldJson, container, formId) { element.classList.add('card');
element.querySelectorAll('.radio-wrapper').forEach((radioWrapper) => { const image = createOptimizedPicture('https://main--afb--
jalagari.hlx.live/lab/images/card.png', 'card-image'); radioWrapper.appendChild(image);
});
return element;
}
```

**cards.css のカスタムコンポーネントの実行時の動作を追加**

```javascript
.card .radio-wrapper { min-width: 320px;
/* or whatever width fits your design */ max-width: 340px;
background: #fff;
border-radius: 16px;
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
flex: 0 0 auto;
scroll-snap-align: start; padding: 24px 16px;
margin-bottom: 0;
position: relative;
transition: box-shadow 0.2s; display: flex;
align-items: flex-start; gap: 12px;
}
```

カードコンポーネントは次のようになります。

![ カード css と js の追加 ](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2 Subscribe 関数を使用した動的動作の追加

ドロップダウンが変更されると、カードが取得され、ラジオグループの列挙に設定されます。 ただし、現在のところ、ビューではこの処理は行われません。 つまり、次のようにレンダリングされます。

![subscribe 関数 ](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

API を呼び出すと、フィールドモデルが設定され、変更をリッスンしてビューをレンダリングする必要があります。 これは、**subscribe 関数** を使用して行います。

次に、前の手順のビューコードを関数に変換し、`cards.js` の subscribe 関数内でこれを呼び出します。

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';  

import { subscribe } from '../../rules/index.js';  
function createCard(element, enums) {  

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {  

    if (enums[index]?.name) {  

      let label = radioWrapper.querySelector('label');  

      if (!label) {  

        label = document.createElement('label');  

        radioWrapper.appendChild(label);  

      }  

      label.textContent = enums[index]?.name;  

    }  

    const image = createOptimizedPicture(enums[index].image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png', 'card-image');  

   radioWrapper.appendChild(image);  

  });  

}  
export default function decorate(element, fieldJson, container, formId) {  

    element.classList.add('card');  

    createCard(element, fieldJson.enum);  

    subscribe(element, formId, (fieldDiv, fieldModel) => {  

        fieldModel.subscribe((e) => {  

            const { payload } = e;  

            payload?.changes?.forEach((change) => {  

                if (change?.propertyName === 'enum') {  

                    createCard(element, change.currentValue);  

                }  

            });  

        });  

    });  
    return element;  

} 
```

**Subscribe 関数を使用して、cards.js のイベントの変更をリッスンする**

ドロップダウンを変更すると、次に示すようにカードに値が入力されます。

![subscribe 関数 ](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3 ビューの更新とフィールドモデルの同期

ビューの変更をフィールドモデルに同期するには、選択したカードの値を設定する必要があります。 そのため、次に示すように、cards.js に次の変更イベントリスナーを追加します。

**cards.js でのフィールドモデル API の使用**

```javascript
 

import { createOptimizedPicture } from '../../../../scripts/aem.js';  

import { subscribe } from '../../rules/index.js';  

  

  

function createCard(element, enums) {  

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {  

    if (enums[index]?.name) {  

      let label = radioWrapper.querySelector('label');  

      if (!label) {  

        label = document.createElement('label');  

        radioWrapper.appendChild(label);  

      }  

      label.textContent = enums[index]?.name;  

    }  

    radioWrapper.querySelector('input').dataset.index = index;  

    const image = createOptimizedPicture(enums[index].image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png', 'card-image');  

   radioWrapper.appendChild(image);  

  });  

}  
export default function decorate(element, fieldJson, container, formId) {  

    element.classList.add('card');  
    createCard(element, fieldJson.enum);  

    subscribe(element, formId, (fieldDiv, fieldModel) => {  

        fieldModel.subscribe((e) => {  

            const { payload } = e;  

            payload?.changes?.forEach((change) => {  

                if (change?.propertyName === 'enum') {  

                    createCard(element, change.currentValue);  

                }  

            });  

        });  
        element.addEventListener('change', (e) => {  

            e.stopPropagation();  

            const value = fieldModel.enum?.[parseInt(e.target.dataset.index, 10)];  

            fieldModel.value = value.name;  

        });  

    });  

    return element;  
} 
```

次に示すように、カスタムカードコンポーネントが表示されます。

![ カードカスタムコンポーネント ](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

## 変更のコミットとプッシュ

カスタムコンポーネントのJavaScriptと CSS を実装し、ローカルで検証したら、変更内容をコミットして Git リポジトリにプッシュします。

```bash
git add . && git commit -m "Add card custom component" && git push
```

いくつかの簡単な手順で、複雑なカスタムカード選択コンポーネントを正常に作成しました。

## カスタムコンポーネントを作成するための手動または従来の方法

従来の方法では、次に説明する手順を手動で実行します。

1. **拡張する OOTB コンポーネントを選択** （ボタン、ドロップダウン、テキスト入力など）。 この場合は、ラジオコンポーネントを拡張します。

2. **フォルダーを作成** し、`blocks/form/components` にコンポーネントの名前（この場合はカード）を指定します。

3. 同じ名前の **JS ファイルを追加します**。
   - `blocks/form/components/cards/cards.js`。

4. （オプション） **CSS ファイルを追加** カスタムスタイルの場合：
   - `blocks/form/components/cards/cards.css.`

5. **コンポーネント JS ファイル** （` _cards.json`）と同じフォルダーに **新しい JSON ファイル** （例：`blocks/form/components/cards/_cards.json`）を定義します。 この JSON は、既存のコンポーネントを拡張し、その定義で、`fd:viewType` をコンポーネントの名前（この場合はカード）に設定する必要があります。

   - すべてのフィールドグループ（基本、検証、ヘルプなど）に対して、カスタムフィールドを明示的に追加します。

6. **JS および CSS ロジックの実装：**
   - 前述のように、デフォルトの関数をエクスポートします。
   - **element** パラメーターを使用して、HTMLの基本構造を変更します。
   - 必要に応じて、**fieldJson** パラメーターを標準のフィールドデータに使用します。
   - **subscribe** 関数を使用して、必要に応じてフィールドの変更やカスタムイベントをリッスンします。

     >[!NOTE]
     >
     >前述のように、カスタムコンポーネントの JS および CSS ロジックを実装します。

7. コンポーネントをフォームビルダーでバリアントとして登録し、バリアント プロパティを設定する。または
   コンポーネントの名前に JSON で `fd:viewType/:type` 力します。例えば、`fd:viewType` の `definitions[]` 値をカードとして、`id="form` を持つオブジェクトのコンポーネント配列に追加します。

   ```javascript
   {
   "definitions": [
   {
   "title": "Cards",
   "id": "cards", "plugins": {
   "xwalk": {
   "page": {
   "resourceType":
   "core/fd/components/form/radiobutton/v1/radiobutton", "template": {
   "jcr:title": "Cards",
   "fieldType": "radio-button", "fd:viewType": "cards",
   "enabled": true, "visible": true}
   }
   } }
   }
   ]}
   ```

8. **mappings.js の更新**：システムで認識および読み込まれるように、コンポーネントの名前を **OOTBomponentDecorators** （OOTB スタイルコンポーネントの場合）または **customComponents** リストに追加します。

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **_form.json を更新**：コンポーネントの名前を `filters.components` 配列に追加して、オーサリング UI にドロップできるようにします。

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **Update _component-definition.json**:`models/_component-definition.json` の手順で、グループ内の配列を `id custom-components` でオブジェクトで更新します。

   ```javascript
   {
   "...":"../blocks/form/components/cards/_cards.json#/definitions"
   }
   ```

   これは、残りのコンポーネントと共に構築する新しいカードコンポーネントへの参照を提供することです

11. **ビルド :json スクリプトを実行**:`npm run build:json` を実行して、コンポーネントのすべての JSON 定義をコンパイルし、サーバーから提供される 1 つのファイルに結合します。 これにより、新しいコンポーネントのスキーマが結合された出力に確実に含まれます。

12. 変更をコミットして Git リポジトリにプッシュします。

これで、カスタムコンポーネントをフォームに追加できます。

## 複合コンポーネントの作成

複合コンポーネントは、複数のコンポーネントを組み合わせて作成します。
例えば、利用条件の複合コンポーネントは、以下を含む親パネルで構成されます。

- 用語を表示するためのプレーンテキストフィールド

- ユーザーの同意を取得するためのチェックボックス

このコンポジション構造は、各コンポーネントの JSON ファイル内のテンプレートとして定義されます。 次の例では、利用条件コンポーネント用のテンプレートを定義する方法を示します。

```javascript
{ 

  "definitions": [ 

    { 

      "title": "Terms and conditions", 

      "id": "tnc", 

      "plugins": { 

        "xwalk": { 

          "page": { 

            "resourceType": "core/fd/components/form/termsandconditions/v1/termsandconditions", 

            "template": { 

              "jcr:title": "Terms and conditions", 

              "fieldType": "panel", 

              "fd:viewType": "tnc", 

              "text": { 

                "value": "Text related to the terms and conditions come here.", 

                "sling:resourceType": "core/fd/components/form/text/v1/text", 

                "fieldType": "plain-text", 

                "textIsRich": true 

              }, 

              "approvalcheckbox": { 

                "name": "approvalcheckbox", 

                "jcr:title": "I agree to the terms & conditions.", 

                "sling:resourceType": "core/fd/components/form/checkbox/v1/checkbox", 

                "fieldType": "checkbox", 

                "required": true, 

                "type": "string", 

                "enum": [ 

                  "true" 

                ] 

              } 

            } 

          } 

        } 

      } 

    } 

  ], 

  ... 

} 
```

## ベストプラクティス

独自のカスタムコンポーネントを作成する前に、次の点に注意してください。

- **コンポーネントロジックに集中する**：カスタム動作に必要なもののみを追加/上書きします

- **基本構造の活用**:OOTB HTMLを開始点として使用します

- **オーサリング可能なプロパティを使用：** JSON スキーマを介して設定可能なオプションを公開します

- **CSS の名前空間**：一意のクラス名を使用して、スタイルの競合を回避します

## 参照

- form-field-types：すべてのフィールドタイプのベース HTML構造およびプロパティ。 フォームフィールドの構造とプロパティについて詳しくは、[ ここをクリック ](/help/edge/docs/forms/eds-form-field-properties) を参照してください。

- **blocks/form/models/form-components**:OOTB およびカスタムコンポーネントプロパティ定義。

- **ブロック/フォーム/コンポーネント**：カスタムコンポーネントの場所。 例：`blocks/form/components/countdown-timer/_countdown-timer.json` に、基本コンポーネントを拡張し、新しいプロパティを追加する方法を示します。
