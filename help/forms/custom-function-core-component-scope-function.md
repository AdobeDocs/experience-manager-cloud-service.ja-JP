---
title: カスタム関数でのオブジェクトのスコープの概要
description: フォームは、ルールの実行時に関数の最後の引数として渡されるカスタム関数のスコープオブジェクトをサポートします。
keywords: カスタム関数、グローバルオブジェクト、フィールドオブジェクトのオブジェクトをスコープ設定します。
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 248c75a5-6335-41d2-aa0a-28a20a710f88
source-git-commit: e2bc958104bd9b75845ad2c213eec18d2560a3a4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---

# カスタム関数のスコープオブジェクト

アダプティブFormsでは、ルールが実行される際に、スコープオブジェクトが関数の最後の引数として渡されます。 このパラメーターを使用して、関数の中からフォームやフィールドのプロパティを読み取り、フォームを変更することができます。 スコープオブジェクトには、フォーム、トリガーイベント、ターゲットフィールドの読み取り専用プロキシオブジェクトが含まれます。 フォームおよびフィールドのプロパティには、scope オブジェクトを使用して、`$` を追加してアクセスできます。たとえば、それぞれ `scope.form.$id` および `scope.field.$id` を追加します。

## スコープオブジェクトを使用したフォーム変更関数

Scope オブジェクトには、フォームを変更するための次の関数があります。

| 関数 | 構文 | 説明 | コードサンプル |
|-----------------|--------|-------------|-------------|
| **setProperty** | `setProperty(any $element, any $payload)` | `$payload` を使用して、ターゲットフィールドにプロパティを設定します。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) して例を表示します。 |
| **validate** | `validate([any $element])` | ターゲットフィールドで検証を実行します。 ターゲットが指定されていない場合はフォーム全体で検証を実行し、検証エラーの配列を返します。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) して例を表示します。 |
| **reset** *（非推奨）* | `reset([any $element])` | 廃止。代わりに `dispatchEvent($target, 'reset')` を使用します。 ターゲットフィールドをリセットします。ターゲットが指定されていない場合は、フォーム全体をリセットします。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) して例を表示します。 |
| **importData** | `importData(any $payload)` | 既存のフォームデータを置き換えて、データをフォームにインポートします。 `qualifiedName` が指定されている場合、データはそのコンテナフィールドにのみ読み込まれます。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) して例を表示します。 |
| **exportData** | `exportData()` | フォームのデータを返します。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) して例を表示します。 |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | フォーム送信をトリガーします。 `$payload` パラメーターを介して送信する内容を指定し、`$contentType` パラメーターを使用してコンテンツタイプを設定できます。 デフォルトでは、データは `multipart/form-data` として送信されます。 オプションの `$validateForm` パラメーターは、送信前にフォームを検証する必要があるかどうかを指定します（デフォルトは true）。 成功した場合は `submitSuccess` が実行され、失敗した場合は `submitError` が実行されます。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) して例を表示します。 |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | ターゲットフィールド（パネルまたはフォームフィールド）にフォーカスを設定します。 ターゲットが指定されていない場合、ルールをトリガーしたフィールドにフォーカスが設定されます。 オプションの `$focusOption` パラメーターは、ターゲットに関連する次の項目または前の項目にフォーカスを移動するかどうかを指定します。 サポートされている値：`'nextItem'`、`'previousItem'`。 パネルと共に使用する場合、ナビゲーションはそのパネルに制限されます。 フィールドと共に使用すると、そのフィールドの親パネル内でナビゲーションが行われます。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) して例を表示します。 |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | `$eventName` によって決定された要素でタイプ `$target` のイベントをディスパッチします。 ターゲットが指定されていない場合、イベントがフォームにディスパッチされます。 オプションの `$payload` は、イベントを処理する式で使用できます。 オプションの `$dispatch` パラメーターは、イベントの伝達動作を制御します。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) して例を表示します。 |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | `$fieldIdentifier` によって識別されたフィールドを無効としてマークし、`$validationMessage` を表示します。 オプションの `$option` パラメーターは、`$fieldIdentifier` を `id`、`dataRef` または `qualifiedName` のいずれとして解釈するかを指定します。 デフォルト値は `{useId: true}` です。サポートされている値：`{useId: true}`、`{useDataRef: true}`、`{useQualifiedName: true}`。 | [ ここをクリック ](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) して例を表示します。 |

## 関連トピック

{{see-also-rule-editor}}

