---
title: EDS フォームのカスタムコンポーネントの作成
description: EDS フォームのカスタムコンポーネントの作成
feature: Edge Delivery Services
role: Admin, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 99%

---


# アダプティブフォームブロックでのカスタムフォームコンポーネントの作成

Edge Delivery Services Forms には、カスタマイズ機能が用意されているので、フロントエンド開発者は調整されたフォームコンポーネントを作成できます。これらのカスタムコンポーネントは WYSIWYG オーサリングエクスペリエンスにシームレスに統合されるので、フォーム作成者はフォームエディター内で簡単に追加、設定、管理できます。カスタムコンポーネントを使用すると、作成者はスムーズで直感的なオーサリングプロセスを確保しながら機能を強化できます。

このドキュメントでは、ネイティブ HTML フォームコンポーネントをスタイル設定してカスタムコンポーネントを作成し、ユーザーエクスペリエンスを向上させ、フォームの視覚的な魅力を高める手順について説明します。

## アーキテクチャの概要

Forms ブロックのカスタムコンポーネントは、**MVC（モデル-ビュー-コントローラー）**&#x200B;アーキテクチャパターンに従います。

### モデル

- 各 `field/component` の JSON スキーマによって定義されます。

- オーサリング可能なプロパティは、対応する JSON ファイルで指定されます（blocks/form/models/form-components を参照）。

- これらのプロパティは、フォームビルダーで作成者が使用でき、フィールド定義（fd）の一部としてコンポーネントに渡されます。

### 表示

- 各フィールドタイプの HTML 構造について詳しくは、form-field-types を参照してください。

- これは、拡張または変更できるコンポーネントの基本構造です。

- 各 OOTB コンポーネントの基本 HTML 構造について詳しくは、form-field-types を参照してください。

### コントローラー／コンポーネントロジック

- JavaScript で、OOTB（標準）またはカスタムコンポーネントとして実装されます。- カスタムコンポーネントの場合は、`blocks/form/components` にあります。

## OOTB コンポーネント

**OOTB（標準）**&#x200B;コンポーネントは、カスタム開発の基盤を提供します。

- OOTB コンポーネントは、`blocks/form/models/form-components` にあります。

- 各 OOTB コンポーネントには、オーサリング可能なプロパティを定義する JSON ファイルがあります（例：` _text-input.json`、`_drop-down.json`）。

- これらのプロパティは、フォームビルダーで作成者が使用でき、フィールド定義（fd）の一部としてコンポーネントに渡されます。

- 各 OOTB コンポーネントの基本 HTML 構造について詳しくは、form-field-types を参照してください。

既存の OOTB コンポーネントを拡張すると、その基本構造、動作、プロパティを再利用しながら、必要に応じてカスタマイズできます。

- カスタムコンポーネントは、事前定義済みの OOTB コンポーネントのセットから拡張する必要があります。

- システムでは、フィールドの JSON の `viewType` プロパティに基づいて、拡張する OOTB コンポーネントを特定します。

- システムでは、許可されたカスタムコンポーネントバリアントのレジストリを維持します。このレジストリにリストされているバリアントのみを使用できます（例：`mappings.js` の `customComponents[]`）。

- フォームをレンダリングする際に、システムではバリアントプロパティまたは `:type/fd:viewType` を確認し、登録済みのカスタムコンポーネントと一致する場合は、`blocks/form/components` フォルダーから対応する JS ファイルと CSS ファイルを読み込みます。

- 次に、カスタムコンポーネントが OOTB コンポーネントの基本 HTML 構造に適用され、その動作と外観を強化または上書きできます。

## カスタムコンポーネントの構造

カスタムコンポーネントを作成するには、**Scaffolder CLI** を使用してコンポーネントに必要なファイルとフォルダーを設定し、カスタムコンポーネントのコードを追加します。

- カスタムコンポーネントは、`blocks/form/components` フォルダーに存在します。

- 各カスタムコンポーネントは、カードなど、コンポーネントにちなんで名前が付けられた独自のフォルダーに配置する必要があります。フォルダー内で、次のファイルを指定する必要があります。

   - **_cards.json** - OOTB コンポーネントのコンポーネント定義を拡張し、オーサリング可能なプロパティ（models[]）と読み込み時のコンテンツ構造（definitions[]）を定義する JSON ファイル。
   - **cards.js** - メインロジックを含む JavaScript ファイル。
   - **cards.css** - オプション、スタイル用。

- フォルダーの名前と JS／CSS ファイルの名前は一致する必要があります。

### カスタムコンポーネントでのフィールドの再利用と拡張

カスタムコンポーネントの JSON でフィールドを定義する際（任意のフィールドグループ、基本、検証、ヘルプなど）、保守性と一貫性を確保するために次のベストプラクティスに従います。

- 既存の共有コンテナまたはフィールド定義（例：`../form-common/_basic-input-placeholder-fields.json#/fields`、`../form-common/_basic- validation-fields.json#/fields`）を参照して、標準／共有フィールドを再利用します。これにより、すべての標準オプションが重複することなく継承されます。

- コンテナには、新規フィールドまたはカスタムフィールドのみを明示的に追加します。これにより、スキーマが DRY で焦点が当てられた状態が保持されます。

- 参照を通じて既に含まれているフィールドを削除するか、重複を回避します。コンポーネントのロジックに固有のフィールドのみを定義します。

- 一貫性と保守性を確保するために、必要に応じてヘルプコンテナやその他の共有コンテンツ（例：`../form-common/_help-container.json`）を参照します。

>[!TIP]
>
> - このパターンにより、今後ロジックを更新または拡張することが簡単になり、カスタムコンポーネントが残りのフォームシステムと一貫性を保持することが確保されます。
> - 新しい共有コンテナまたはフィールド定義を追加する前に、常に既存の共有コンテナまたはフィールド定義を確認します。

### カスタムコンポーネントの新しいプロパティの定義

- カスタムコンポーネントの新しいプロパティを作成者からキャプチャする必要がある場合は、コンポーネントの JSON でコンポーネントの `fields[]` 配列にフィールドを定義して実行できます。

- カスタムコンポーネントは :type プロパティを使用して特定されます。このプロパティは、JSON ファイルで `fd:viewType` として設定できます（例：`fd:viewType: cards`）。これにより、システムは正しいカスタムコンポーネントを認識して読み込めるので、カスタムコンポーネントでは必須です

- JSON 定義に追加した新しいプロパティは、コンポーネントの JS ロジックのフィールド定義で properties. `<propertyName>` として使用できます

## カスタムコンポーネント JavaScript API

カスタムコンポーネント JavaScript API は、カスタムフォームコンポーネントの動作、外観、反応性を制御する方法を定義します。

### Decorate 関数

**decorate** 関数は、カスタムコンポーネントのエントリポイントです。コンポーネントを初期化し、JSON 定義にリンクして、HTML 構造と動作を操作できるようにします。

>[!NOTE]
>
> カスタムコンポーネントの JavaScript ファイルは、デフォルトの関数を decorate として書き出す必要があります。

#### 関数シグネチャ：

```javascript
export default function decorate(element, fieldJson, container, formId) 
{
  // element: The HTML structure of the OOTB component you are extending
  // fieldJson: The JSON field definition (all authorable properties)
  // container: The parent element (fieldset or form)
  // formId: The id of the form

  // ... your logic here ...
}
```

次の操作を実行できます。

- **要素を変更**：イベントリスナーの追加、属性の更新、追加のマークアップの挿入を行います。

- **JSON プロパティにアクセス**：`fd.properties.<propertyName>` を使用して、JSON スキーマで定義された値を読み取り、コンポーネントロジック内で適用します。

## Subscribe 関数

**subscribe** 関数を使用すると、コンポーネントはフィールド値またはカスタムイベントの変更に反応できます。これにより、コンポーネントとフォームのデータモデルの同期が維持され、UI を動的に更新できます。

### 関数シグネチャ：

```javascript
import { subscribe } from '../../rules/index.js';
export default function decorate(fieldDiv, fieldJson, container, formId) {
  // Access custom properties defined in the JSON
  const { initialText, finalText, time } = fieldJson?.properties;

  // ... setup logic ...

  subscribe(fieldDiv, formId, (_fieldDiv, fieldModel) => {
    fieldModel.subscribe(() => {
      // React to custom event (e.g., resetCardOption)
      // ... logic ...
    }, 'resetCardOption');
  });
}
```

次の操作を実行できます。

- **コールバックを登録**：**subscribe(element, formId, callback)** を呼び出すと、フィールドデータを変更するたびに実行するコールバックが登録されます。次の 2 つのコールバックパラメータを使用します。
   - **element**：フィールドを表す HTML 要素。
   - **fieldModel**：フィールドの状態とイベント API を表すオブジェクト。

- **変更またはイベントをリッスン**：値が変更されるか、カスタムイベントがトリガーされるたびにロジックを実行するには、`fieldModel.subscribe((event) => { ... }, 'eventName')` を使用します。イベントオブジェクトには、変更内容の詳細が含まれます。

## カスタムコンポーネントの作成

この節では、OOTB ラジオボタンコンポーネントを拡張して&#x200B;**カードカスタムコンポーネント**&#x200B;を作成するプロセスについて説明します。

![カードカスタムコンポーネント](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;1. コードの設定

#### 1.1 ファイルとフォルダー

最初の手順では、カスタムコンポーネントの必要なファイルを設定し、リポジトリ内のコードに接続します。このプロセスは、**AEM Forms Scaffolder CLI** により自動的に実行されるので、必要なファイルの基礎モードと接続が迅速になります。

>[!VIDEO](https://video.tv.adobe.com/v/3474752)

1. ターミナルを開き、フォームプロジェクトのルートに移動します。
2. 次のコマンドを実行します。

```bash
npm install
npm run create:custom-component
```

![Scaffolder CLI](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

次のようになります。

- 新しいコンポーネントに&#x200B;**名前を付けるプロンプトが表示されます**。例えば、この場合は「cards」を使用します。
- 基本コンポーネント（ラジオグループを選択）を&#x200B;**選択するよう求められます**

これにより、次を含む、すべての必要なフォルダーとファイルが作成されます。

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

さらに、CLI の出力に示されているように、リポジトリ内の残りのコードと接続します。
次の機能が自動的に実行されます。

- フィルターにカードを追加して、アダプティブフォームブロック内での追加を可能にします。
- 新しいカードコンポーネントを含めるために、`mappings.js` の許可リストを更新します。
- ユニバーサルエディターの&#x200B;**カスタムコンポーネント**&#x200B;リストにカードコンポーネントの定義を登録します。

>[!NOTE]
>
> 手動（レガシー）の方法を使用してカスタムコンポーネントを作成することもできます。詳しくは、[手動またはレガシーの方法](#manual-or-legacy-method-to-create-custom-component)のカスタムコンポーネントの作成の節を参照してください。

#### 1.2 ユニバーサルエディターでのコンポーネントの使用

1. **ユニバーサルエディターを更新**：ユニバーサルエディターでフォームを開き、ページを更新して、リポジトリから最新のコードが読み込まれるようにします。

2. **カスタムコンポーネントを追加します**

   1. フォームキャンバスの「**追加（+）**」ボタンをクリックします。
   2. 「カスタムコンポーネント」セクションまでスクロールします。
   3. 新しく作成された&#x200B;**カードコンポーネント**&#x200B;を選択して、フォームに挿入します。

      ![カスタムコンポーネントを選択](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

`cards.js` 内にコードが存在しないので、カスタムコンポーネントはラジオグループとしてレンダリングされます。

#### 1.3 ローカルでのプレビューとテスト

フォームにカスタムコンポーネントが含まれるようになったので、フォームをプロキシしてローカルで変更し、変更を確認できます。

1. ターミナルに移動し、`aem up` を実行します。

2. `http://localhost:3000/{path-to-your-form}` で開始されたプロキシサーバーを開きます（パスの例：`/content/forms/af/custom-component-form`）


### &#x200B;2. カスタムコンポーネントのカスタム動作の実装

#### 2.1 カスタムコンポーネントのスタイル設定

スタイル設定のためにコンポーネントにクラス **card** を追加し、各ラジオに画像を追加します。次のコードを使用します。

**card.js を使用したコンポーネントのスタイル設定**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper) => {
    const image = createOptimizedPicture(
      'https://main--afb--jalagari.hlx.live/lab/images/card.png',
      'card-image'
    );
    radioWrapper.appendChild(image);
  });

  return element;
}
```

**cards.css を使用した実行時の動作の追加**

```javascript
.card .radio-wrapper {
  min-width: 320px; /* or whatever width fits your design */
  max-width: 340px;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  flex: 0 0 auto;
  scroll-snap-align: start;
  padding: 24px 16px;
  margin-bottom: 0;
  position: relative;
  transition: box-shadow 0.2s;
  display: flex;
  align-items: flex-start;
  gap: 12px;
}
```

カードコンポーネントは次のようになります。

![カードの css と js を追加](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2 Subscribe 関数を使用した動的動作の追加

ドロップダウンを変更すると、カードが取得され、ラジオグループの定義済みリストに設定されます。ただし、現在、ビューではこの処理は行われません。そのため、次のようにレンダリングされます。

![subscribe 関数](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

API を呼び出すと、フィールドモデルが設定されます。変更をリッスンして、それに応じてビューをレンダリングする必要があります。これは、**subscribe 関数**&#x200B;を使用して実現されます。

前の手順のビューコードを関数に変換し、次に示すように、`cards.js` の subscribe 関数内でこれを呼び出します。

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

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

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

**Subscribe 関数を使用して、cards.js のイベントの変更をリッスン**

ドロップダウンを変更すると、次に示すようにカードに値が入力されます。

![subscribe 関数](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3 ビューの更新とフィールドモデルの同期

ビューの変更をフィールドモデルに同期するには、選択したカードの値を設定する必要があります。そのため、次に示すように、cards.js に次の変更イベントリスナーを追加します。

**cards.js での Field Model API の使用**

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

    // Attach index to input element for later reference
    radioWrapper.querySelector('input').dataset.index = index;

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

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

![カードカスタムコンポーネント](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;3. 変更のコミットとプッシュ

カスタムコンポーネントの JavaScript と CSS を実装し、ローカルで検証したら、変更をコミットして Git リポジトリにプッシュします。

```bash
git add . && git commit -m "Add card custom component" && git push
```

いくつかのシンプルな手順で、複雑なカスタムカード選択コンポーネントを正常に作成しました。

+++ **カスタムコンポーネントを作成する手動またはレガシーの方法**

これを実行するレガシーの方法では、次に説明する手順を手動で実行します。

1. 拡張する **OOTB コンポーネントを選択します**（例：ボタン、ドロップダウン、テキスト入力など）。この場合は、ラジオコンポーネントを拡張します。

2. コンポーネントの名前（この場合は cards）で、`blocks/form/components` に&#x200B;**フォルダーを作成します**。

3. 同じ名前の **JS ファイルを追加します**。
   - `blocks/form/components/cards/cards.js`。

4. （オプション）カスタムスタイルの **CSS ファイルを追加します**。
   - `blocks/form/components/cards/cards.css.`

5. **コンポーネント JS ファイル**（`blocks/form/components/cards/_cards.json`）と同じフォルダーに&#x200B;**新しい JSON ファイルを定義します**（例：` _cards.json`）。この JSON は既存のコンポーネントを拡張し、その定義で `fd:viewType` をコンポーネントの名前（この場合は cards）に設定する必要があります。

   - すべてのフィールドグループ（基本、検証、ヘルプなど）に対して、カスタムフィールドを明示的に追加します。

6. **JS および CSS ロジックを実装します。**
   - 上記の説明に従って、デフォルトの関数を書き出します。
   - **element** パラメーターを使用して、基本 HTML 構造を変更します。
   - 標準フィールドデータに必要な場合は、**fieldJson** パラメーターを使用します。
   - 必要に応じて、**subscribe** 関数を使用してフィールドの変更またはカスタムイベントをリッスンします。

     >[!NOTE]
     >
     >上記の説明に従って、カスタムコンポーネントの JS および CSS ロジックを実装します。

7. フォームビルダーでコンポーネントをバリアントとして登録し、バリアントプロパティまたは
   JSON の `fd:viewType/:type` をコンポーネントの名前に設定します。例えば、`definitions[]` の `fd:viewType` 値をカードとして、`id="form` を持つオブジェクトのコンポーネント配列に追加します。

   ```
       {
     "definitions": [
       {
         "title": "Cards",
         "id": "cards",
         "plugins": {
           "xwalk": {
             "page": {
               "resourceType": "core/fd/components/form/radiobutton/v1/radiobutton",
               "template": {
                 "jcr:title": "Cards",
                 "fieldType": "radio-button",
                 "fd:viewType": "cards",
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

8. **mappings.js を更新**：コンポーネントの名前を **OOTBComponentDecorators**（OOTB スタイルのコンポーネントの場合）または **customComponents** リストに追加して、システムにより認識および読み込まれるようにします。

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

10. **_component-definition.json を更新**：`models/_component-definition.json` で、`id custom-components` を持つグループ内の配列を次の方法でオブジェクトに更新します。

   ```javascript
   {
   "...":"../blocks/form/components/cards/_cards.json#/definitions"
   }
   ```

   これは、残りのコンポーネントと共に作成される新しいカードコンポーネントへの参照を提供するためのものです

11. **build:json スクリプトを実行**：`npm run build:json` を実行して、すべてのコンポーネント JSON 定義をコンパイルし、サーバーから提供される単一のファイルに結合します。これにより、新しいコンポーネントのスキーマが結合された出力に含まれます。

12. 変更をコミットして Git リポジトリにプッシュします。

これで、カスタムコンポーネントをフォームに追加できます。

+++

## 複合コンポーネントの作成

複合コンポーネントは、複数のコンポーネントを組み合わせて作成されます。
例えば、利用条件の複合コンポーネントは、次を含む親パネルで構成されます。

- 利用条件を表示するためのプレーンテキストフィールド

- ユーザーの同意をキャプチャするためのチェックボックス

この構成構造は、各コンポーネントの JSON ファイル内のテンプレートとして定義されます。次の例では、利用条件コンポーネントのテンプレートを定義する方法を示します。

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

- **コンポーネントロジックに焦点を当てた状態を保持**：カスタム動作に必要なもののみを追加／上書きします

- **基本構造を活用**：OOTB HTML を開始点として使用します

- **オーサリング可能なプロパティを使用**：JSON スキーマを通じて設定可能なオプションを表示します

- **CSS に名前空間を設定**：一意のクラス名を使用してスタイルの競合を回避します

## 参照

- [form-field-types](/help/edge/docs/forms/eds-form-field-properties.md)：すべてのフィールドタイプのベース HTML構造およびプロパティ。

- **blocks/for/models/from-components**：OOTB およびカスタムコンポーネントプロパティの定義。

- **blocks/form/components**：カスタムコンポーネントの場所。例：`blocks/form/components/countdown-timer/_countdown-timer.json` に、基本コンポーネントを拡張して新しいプロパティを追加する方法を示します。
