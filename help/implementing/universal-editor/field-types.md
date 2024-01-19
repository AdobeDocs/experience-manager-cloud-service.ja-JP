---
title: フィールドタイプ
description: コンポーネントレールでユニバーサルエディターが編集できる様々なタイプのフィールドについて説明し、独自のアプリの実装方法の例を示します。
exl-id: cb4567b8-ebec-477c-b7b9-53f25b533192
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 7%

---


# フィールドタイプ {#field-types}

コンポーネントレールでユニバーサルエディターが編集できる様々なタイプのフィールドについて説明し、独自のアプリの実装方法の例を示します。

{{universal-editor-status}}

## 概要 {#overview}

ユニバーサルエディターで使用する独自のアプリを適応させる場合は、コンポーネントを実装し、エディターのコンポーネントレールで操作できるデータタイプを定義する必要があります。

このドキュメントでは、使用可能なフィールドタイプの概要と設定例を説明します。

>[!TIP]
>
>ユニバーサルエディター用のアプリの実装方法がわからない場合は、ドキュメントを参照してください。 [AEM Developers 向けのユニバーサルエディターの概要。](/help/implementing/universal-editor/developer-overview.md)

## ブーリアン {#boolean}

boolean フィールドは、チェックボックスとしてレンダリングされる単純な true/false 値を格納します。

### サンプル {#sample-boolean}

```json
{
  "fields": [   
   {
      "component": "boolean",
      "valueType": "boolean",
      "name": "field1",
      "label": "Boolean Field",
      "description": "This is a boolean field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "customErrorMsg": "This is an error."
      }
    }
  ]
}
```

## チェックボックスグループ {#checkbox-group}

ブール値と同様に、チェックボックスグループを使用して複数の true/false 項目を選択できます。

### サンプル {#sample-checkbox-group}

```json
{
  "fields": [   
   {
      "component": "checkbox-group",
      "valueType": "string-array",
      "name": "field1",
      "label": "Checkbox Group",
      "description": "This is a checkbox group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "First option", "value": "one" },
        { "name": "Second option", "value": "two" },
        { "name": "Third option", "value": "three" }
      ]
    }
  ]
}
```

## 日時 {#date-time}

日付時間フィールドを使用すると、日付や時刻、またはその組み合わせを指定できます。

### サンプル {#sample-date-time}

```json
{
  "fields": [   
      {
      "component": "date-time",
      "valueType": "date-time",
      "name": "field1",
      "label": "Date Time",
      "description": "This is a date time field that stores both date and time.",
      "required": true,
      "placeholder": "YYYY-MM-DD HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Marty! You have to come back with me!"
      }
    },
    {
      "component": "date-time",
      "valueType": "date",
      "name": "field2",
      "label": "Another Date Time",
      "description": "This is another date time field that only stores the date.",
      "required": true,
      "placeholder": "YYYY-MM-DD",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Back to the future!"
      }
    },
    {
      "component": "date-time",
      "valueType": "time",
      "name": "field3",
      "label": "Yet Another Date Time",
      "description": "This is another date time field that only stores the time.",
      "required": true,
      "placeholder": "HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Great Scott!"
      }
    }
  ]
}
```

## 数値 {#number}

数値フィールドを使用して、数値を入力できます。

### サンプル {#sample-number}

```json
{
  "fields": [   
   {
      "component": "number",
      "valueType": "number",
      "name": "field1",
      "label": "Number Field",
      "description": "This is a number field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "numberMin": null,
        "numberMax": null,
        "customErrorMsg": "Please don't do that."
      }
    }
  ]
}
```

## ラジオグループ {#radio-group}

ラジオグループを使用すると、チェックボックスグループと同様のグループとしてレンダリングされる複数のオプションから、相互に排他的なオプションを選択できます。

### サンプル {#sample-radio-group}

```json
{
  "fields": [   
   {
      "component": "radio-group",
      "valueType": "string",
      "name": "field1",
      "label": "Radio Group",
      "description": "This is a radio group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ]
    }
  ]
}
```

## 参照 {#reference}

参照を使用すると、別のデータオブジェクトを現在のオブジェクトからの参照として指定できます。

## 選択 {#select}

「選択」を使用すると、ドロップダウンメニューで 1 つ以上の定義済みオプションを選択できます。

### サンプル {#sample-select}

```json
{
  "fields": [   
   {
      "component": "select",
      "valueType": "string",
      "name": "field1",
      "label": "Select",
      "description": "This is a select.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ],
      "emptyOption": true
    }
  ]
}
```

## テキスト領域 {#text-area}

テキスト領域を使用すると、複数行のテキストを入力できます。

### サンプル {#sample-text-area}

```json
{
  "fields": [   
   {
      "component": "text-area",
      "valueType": "string",
      "name": "field1",
      "label": "Text Area",
      "description": "This is a text area.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "mimeType": "text/x-markdown"
    }
  ]
}
```

## テキスト入力 {#text-input}

テキスト入力を使用すると、1 行のテキスト入力が可能になります。

### サンプル {#sample-text-input}

```json
{
  "fields": [   
   {
      "component": "text-input",
      "valueType": "string",
      "name": "field1",
      "label": "Text Input",
      "description": "This is a text input.",
      "required": true,
      "multi": true,
      "placeholder": null
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "field2",
      "label": "Another Text Input",
      "description": "This is a text input with validation.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "validation": {
        "minLength": 5,
        "maxLength": 10,
        "regExp": "^foo:.*",
        "customErrorMsg": "I'm sorry, Dave. I can't do that."
      }
    }
  ]
}
```

## タブ {#tab}

「 」タブを使用すると、他の入力フィールドを複数のタブでグループ化し、作成者がレイアウトを構成しやすくすることができます。

A `tab` 定義は、 `fields`. 次の日以降のすべて `tab` 新しい `tab` が検出された後、次の項目が新しいタブに配置されます。

すべてのタブの上に項目を表示する場合は、その項目をタブの前に定義する必要があります。

### サンプル {#sample-tab}

```json
{
  "id": "title",
  "fields": [
    {
      "component": "tab",
      "label": "Tab",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "name": "tab-response",
      "value": "",
      "placeholder": "Tab? I can't give you a tab unless you order something.",
      "label": "Lou",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Pepsi Free",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "name": "pepsi-free-response",
      "value": "",
      "placeholder": "You want a Pepsi, pal, you're gonna pay for it.",
      "label": "Mr. Carruthers",
      "valueType": "string"
    },
    {
      "component": "select",
      "name": "without-sugar",
      "value": "coffee",
      "label": "Something without sugar",
      "valueType": "string",
      "options": [
        { "name": "Coffee", "value": "coffee" },
        { "name": "Hot Coffee", "value": "hot-coffee" },
        { "name": "Hotter Coffee", "value": "hotter-coffee" }
      ]
    }
  ]
}
```
