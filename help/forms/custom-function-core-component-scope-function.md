---
title: カスタム関数でのオブジェクトのスコープの概要
description: フォームは、ルールの実行時に関数の最後の引数として渡されるカスタム関数のスコープオブジェクトをサポートします。
keywords: カスタム関数、グローバルオブジェクト、フィールドオブジェクトのオブジェクトをスコープ設定します。
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: af211649a4f22d06f4e8669335a8267ee948a408
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# カスタム関数内のオブジェクトのスコープ

アダプティブFormsでは、ルールが実行される際に、スコープオブジェクトが関数の最後の引数として渡されます。 このパラメーターを使用して、関数の中からフォームやフィールドのプロパティを読み取り、フォームを変更することができます。 スコープオブジェクトには、フォーム、トリガーイベント、ターゲットフィールドの読み取り専用プロキシオブジェクトが含まれます。 フォームおよびフィールドのプロパティには、scope オブジェクトを使用して、`$` を追加してアクセスできます。たとえば、それぞれ `scope.form.$id` および `scope.field.$id` を追加します。

## スコープオブジェクトを使用したフォーム変更関数

Scope オブジェクトには、フォームを変更するための次の関数があります。

| 関数 | 構文 | 説明 | コードサンプル |
|-----------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------|
| **setProperty** | `setProperty(any $element, any $payload)` | `$payload` を使用して `$element` のプロパティを設定します。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) して例を表示します。 |
| **validate** | `validate([any $element])` | `$element` に対して検証を実行します。 要素が指定されていない場合は、フォーム全体が検証されます。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) して例を表示します。 |
| **reset** | `reset([any $element])` | `$element` をリセットします。 要素が指定されていない場合は、フォーム全体がリセットされます。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) して例を表示します。 |
| **importData** | `importData(any $payload)` | 既存のフォームデータを置き換えて、データをフォームにインポートします。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) して例を表示します。 |
| **exportData** | `exportData()` | フォームのデータを返します。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) して例を表示します。 |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | フォーム送信をトリガーします。 `$data` パラメーターは、送信する内容を指定 `$submit_as`、コンテンツタイプを定義します（デフォルトは「multipart/form-data」）。 オプションの `$validate_form` で、フォームを検証するかどうかを指定します（デフォルトは true）。 成功した場合は `submitSuccess` が実行され、失敗した場合は `submitError` が実行されます。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) して例を表示します。 |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | フォーカスを `$element` に設定します（パネルまたはフィールドを指定可能）。 要素が指定されていない場合は、ルールをトリガーしたフィールドにフォーカスが設定されます。 オプションの `$focusOption` パラメーター（列挙型 `FocusOption`）は、`$element` を基準とする「nextItem」または「previousItem」のどちらにフォーカスするかを指定します。 パネルが指定されている場合、ナビゲーションはそのパネルに制限されます。フィールドを使用している場合、ナビゲーションは親パネルで行われます。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) して例を表示します。 |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | `$element` で指定された要素でタイプ `$eventName` のイベントをディスパッチします。 要素が指定されていない場合、イベントがフォームでディスパッチされます。 オプションの `$payload` は、イベントを処理する式で使用できます。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) して例を表示します。 |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | `$fieldIdentifier` で識別されたフィールドを無効としてマークし、検証メッセージを `$validationMessage` に設定します。 オプションの `$option` パラメーターは、`$fieldIdentifier` を `id`、`name` または `dataRef` のいずれとして解釈するかを指定します。 デフォルト値は `{useId: true}` で、サポートされている値は `{useId: true}`、`{useDataRef: true}`、`{useQualifiedName: true}` です。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) して例を表示します。 |

## 関連トピック

{{see-also-rule-editor}}