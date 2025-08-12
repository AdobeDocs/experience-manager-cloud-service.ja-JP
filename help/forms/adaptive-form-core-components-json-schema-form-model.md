---
title: アダプティブフォームのコアコンポーネントの JSON スキーマをデザインする方法
description: アダプティブフォームのコアコンポーネントの JSON スキーマを作成し、そのスキーマに基づいてアダプティブフォーム（コアコンポーネント）を作成して、スキーマ準拠のデータを生成する方法について説明します。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 185b12bc-cea9-45c8-9b57-dc313bd0cfaa
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 100%

---

# アダプティブフォームの JSON スキーマのデザイン（コアコンポーネント）{#creating-adaptive-forms-using-json-schema}


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| 基盤 | [ここをクリックしてください](/help/forms/adaptive-form-json-schema-form-model.md) |
| コアコンポーネント | この記事 |


## 前提条件 {#prerequisites}

フォームモデルとして JSON スキーマを使用し、コアコンポーネントに基づくアダプティブフォームをオーサリングする場合、JSON スキーマの基本を理解している必要があります。この記事を読む前に、次のコンテンツを読んでおくことをお勧めします。

* [コアコンポーネントに基づくアダプティブフォームの作成](/help/forms/creating-adaptive-form-core-components.md)
* [JSON スキーマ](https://json-schema.org/)

## フォームモデルとしての JSON スキーマの使用  {#using-a-json-schema-as-form-model}

Adobe Experience Manager Forms では、既存の JSON スキーマをフォームモデルとして使用し、コアコンポーネントに基づくアダプティブフォームの作成がサポートされています。JSON スキーマは、組織内のバックエンドシステムによってデータが作成または使用される構造を表します。使用する JSON スキーマは、[v4 仕様](https://json-schema.org/draft-04/schema)に準拠している必要があります。

JSON スキーマの使用上の主な特長を以下に示します。

* JSON の構造は、アダプティブフォームのオーサリングモードの「コンテンツファインダー」タブでツリーとして表示されます。JSON 階層からコアコンポーネントに基づくアダプティブフォームに要素をドラッグして追加できます。
* 関連付けられたスキーマに準拠する JSON を使用して、フォームに事前入力できます。
* ユーザーが入力したデータは、送信時には関連付けられたスキーマに適合する JSON として送信されます。
* [2012-20 バージョン](https://json-schema.org/draft/2020-12/release-notes)の仕様に従って、JSON スキーマに基づいたフォームを作成することもできます。

JSON スキーマは、単純型要素と複合型要素で構成されています。要素には、その要素にルールを追加する属性が含まれています。これらの要素や属性がアダプティブフォーム上にドラッグされると、自動的に該当するアダプティブフォームコンポーネントにマッピングされます。

JSON 要素とアダプティブフォームコンポーネントのマッピングは、以下のように行われます。

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>JSON の要素、プロパティ、属性</strong></th>
   <th><strong>アダプティブフォームコンポーネント</strong></th>
  </tr>
  <tr>
   <td><p>enum および enumNames 制約を含む string プロパティ。</p> <p>構文</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>ドロップダウンコンポーネント：</p>
    <ul>
     <li>enumNames にリストされた値はドロップボックスに表示されます。</li>
     <li>enum にリストされた値は計算に使用されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>format 制約を含む string プロパティ。例えば、メール、日付など。</p> <p>構文</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>type が string で format が email の場合、メールコンポーネントがマップされます。</li>
     <li>type が string で format が hostname の場合、検証を含むテキストボックスコンポーネントがマップされます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> テキストフィールド<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>number プロパティ<br /> </td>
   <td>サブタイプが float に設定された数値フィールド<br /> </td>
  </tr>
  <tr>
   <td>integer プロパティ<br /> </td>
   <td>サブタイプが integer に設定された数値フィールド<br /> </td>
  </tr>
  <tr>
   <td>boolean プロパティ<br /> </td>
   <td>切り替え<br /> </td>
  </tr>
  <tr>
   <td>object プロパティ<br /> </td>
   <td>パネル<br /> </td>
  </tr>
  <tr>
   <td>array プロパティ</td>
   <td>minItems および maxItems にそれぞれ等しい min および max を持つ繰り返し可能なパネル。同種の配列のみがサポートされます。そのため、項目制限は、配列でなくオブジェクトである必要があります。<br /> </td>
  </tr>
 </tbody>
</table>

### 共通のスキーマプロパティ {#common-schema-properties}

アダプティブフォームは JSON スキーマで使用可能な情報を使用して、生成された各フィールドをマッピングします。具体的には、以下のようになります。

* `title` プロパティは、アダプティブフォームコンポーネントのラベルとして機能します。
* `description` プロパティは、アダプティブフォームコンポーネントの詳細な説明として設定されます。
* `default` プロパティは、アダプティブフォームフィールドの初期値として機能します。
* `maxLength` プロパティは、テキストフィールドコンポーネントの `maxlength` 属性として設定されます。
* `minimum`、`maximum`、`exclusiveMinimum` および `exclusiveMaximum` プロパティは、数値ボックスコンポーネントに使用されます。
* `DatePicker component` の範囲をサポートするために、追加の JSON スキーマプロパティ `minDate` および `maxDate` が用意されています。
* `minItems` および `maxItems` プロパティは、パネルコンポーネントに追加または削除される可能性のある項目／フィールドの数を制限するために使用されます。
* `readOnly` プロパティは、アダプティブフォームコンポーネントの `readonly` 属性を設定します。
* `required` プロパティは、アダプティブフォームフィールドを必須としてマークします。一方、パネル（タイプがオブジェクト）の場合、最終的に送信された JSON データには、そのオブジェクトに対応する空の値を持つフィールドがあります。
* `pattern` プロパティは、アダプティブフォームで検証パターン（正規表現）として設定されます。
* JSON スキーマファイルの拡張子は、.schema.json を維持する必要があります。例えば、&lt;filename>.schema.json のように指定します。

## JSON スキーマのサンプル {#sample-json-schema}

>[!BEGINTABS]

>[!TAB JSON スキーマ v4]

```json
  {
  "$schema": "https://json-schema.org/draft-04/schema#",
  "definitions": {
    "employee": {
    "type": "object",
    "properties": {
      "userName": {
       "type": "string"
     },
      "dateOfBirth": {
       "type": "string",
       "format": "date"
      },
      "email": {
      "type": "string",
      "format": "email"
      },
      "language": {
       "type": "string"
     },
      "personalDetails": {
       "$ref": "#/definitions/personalDetails"
     },
      "projectDetails": {
       "$ref": "#/definitions/projectDetails"
      }
    },
    "required": [
     "userName",
     "dateOfBirth",
     "language"
    ]
    },
      "personalDetails": {
     "type": "object",
    "properties": {
       "GeneralDetails": {
      "$ref": "#/definitions/GeneralDetails"
     },
      "Family": {
       "$ref": "#/definitions/Family"
      },
      "Income": {
       "$ref": "#/definitions/Income"
     }
     }
       },
    "projectDetails": {
     "type": "array",
     "items": {
     "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```


>[!TAB JSON スキーマ 2012-20]


```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://example.com/employee.schema.json",
  "$defs": {
    "employee": {
      "type": "object",
      "properties": {
        "userName": {
          "type": "string"
        },
        "dateOfBirth": {
          "type": "string",
          "format": "date"
        },
        "email": {
          "type": "string",
          "format": "email"
        },
        "language": {
          "type": "string"
        },
        "personalDetails": {
          "$ref": "#/$defs/personalDetails"
        },
        "projectDetails": {
          "$ref": "#/$defs/projectDetails"
        }
      },
      "required": [
        "userName",
        "dateOfBirth",
        "language"
      ]
    },
    "personalDetails": {
      "type": "object",
      "properties": {
        "GeneralDetails": {
          "$ref": "#/$defs/GeneralDetails"
        },
        "Family": {
          "$ref": "#/$defs/Family"
        },
        "Income": {
          "$ref": "#/$defs/Income"
        }
      }
    },
    "projectDetails": {
      "type": "array",
      "items": {
        "properties": {
          "name": {
            "type": "string"
          },
          "age": {
            "type": "number"
          },
          "projects": {
            "$ref": "#/$defs/projects"
          }
        }
      },
      "minItems": 1,
      "maxItems": 4
    },
    "projects": {
      "type": "array",
      "items": {
        "properties": {
          "name": {
            "type": "string"
          },
          "age": {
            "type": "number"
          },
          "projectsAdditional": {
            "$ref": "#/$defs/projectsAdditional"
          }
        }
      },
      "minItems": 1,
      "maxItems": 4
    },
    "projectsAdditional": {
      "type": "array",
      "items": {
        "properties": {
          "Additional_name": {
            "type": "string"
          },
          "Additional_areacode": {
            "type": "number"
          }
        }
      },
      "minItems": 1,
      "maxItems": 4
    },
    "GeneralDetails": {
      "type": "object",
      "properties": {
        "age": {
          "type": "number"
        },
        "married": {
          "type": "boolean"
        },
        "phone": {
          "type": "number",
        },
        "address": {
          "type": "string"
        }
      }
      }
  }
  }
```

>[!ENDTABS]

JSON スキーマ v4 からバージョン 2020-12 仕様への主な変更点は次のとおりです。

* ID は `$id` として宣言されます
* 定義は `$defs` として宣言されます

### 再使用可能なスキーマ定義 {#reusable-schema-definitions}

定義キーを使用して、再使用可能なスキーマを識別します。再使用可能なスキーマ定義を使用して、フラグメントを作成します。<!-- It is similar to identifying complex types in XSD.-->定義を含む JSON スキーマのサンプルを以下に示します。

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

上記の例では、各顧客が発送先と請求先の両方の住所を持つ顧客レコードを定義します。どちらの住所も構造（都道府県、市区町村、番地など）が同じ場合は、住所が重複しないようにすることをお勧めします。また、今後変更が行われたときに、簡単にフィールドを追加したり削除したりできます。

<!--
## Pre-Configuring fields in JSON Schema Definition {#pre-configuring-fields-in-json-schema-definition}

You can use the **aem:afProperties** property to preconfigure JSON Schema field to map to a custom Adaptive Form component. An example is listed below:

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}

```
-->

<!-- 
## Configure scripts or expressions for form objects  {#configure-scripts-or-expressions-for-form-objects}

JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. You can pre-configure form objects to [evaluate an expression](adaptive-form-expressions.md) on a form event.

Use the aem:afproperties property to preconfigure Adaptive Form expressions or scripts for Adaptive Form components. For example, when the initialize event is triggered, the below code sets value of telephone field and prints a value to the log :

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

You should be a member of the [forms-power-user group](forms-groups-privileges-tasks.md) to configure scripts or expressions for form object. The below table lists all the script events supported for an Adaptive Form component.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Component \ Event</th>
   <th>initialize <br /> </th>
   <td>Calculate</td>
   <td>Visibility</td>
   <td>Validate</td>
   <td>Enabled</td>
   <td>Value Commit</td>
   <td>Click </td>
   <td>Options</td>
  </tr>
  <tr>
   <td>Text Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Stepper</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Radio Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Telephone</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Switch</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Check Box</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Drop-down</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Image Choice</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Date Input Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Date Picker</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Email</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>File Attachment</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Image</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Some examples of using events in a JSON are hiding a field on initialize event and configure value of another field on value commit event. For detailed information about creating expressions for the script events, see [Adaptive Form Expressions](adaptive-form-expressions.md).

Here is the sample JSON code for previously mentioned examples.

### Hiding a field on initialize event {#hiding-a-field-on-initialize-event}

```json

"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configure value of another field on value commit event {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}

```
-->

## アダプティブフォームコンポーネントの許容値の制限 {#limit-acceptable-values-for-an-adaptive-form-component}

JSON スキーマの要素に次の制限を追加して、アダプティブフォームコアコンポーネントで許容される値を制限できます。

<table>
 <tbody>
  <tr>
   <td><p><strong> スキーマプロパティ</strong></p> </td>
   <td><p><strong>データタイプ</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
   <td><p><strong>コンポーネント</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>文字列</p> </td>
   <td><p>数値および日付の上限を指定します。デフォルトでは、最大値が含まれます。</p> </td>
   <td>
    <ul>
     <li>数値ボックス</li>
     <li>数値ステッパー<br /> </li>
     <li>日付選択</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>文字列</p> </td>
   <td><p>数値および日付の下限を指定します。デフォルトでは、最小値が含まれます。</p> </td>
   <td>
    <ul>
     <li>数値ボックス</li>
     <li>数値ステッパー</li>
     <li>日付選択</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>ブール値</p> </td>
   <td><p>true の場合、フォームのコンポーネントで指定された数値または日付は、maximum プロパティに指定された数値または日付よりも小さい値である必要があります。</p> <p>false の場合、フォームのコンポーネントで指定された数値または日付は、maximum プロパティに指定された数値または日付以下の値である必要があります。</p> </td>
   <td>
    <ul>
     <li>数値ボックス</li>
     <li>数値ステッパー</li>
     <li>日付選択</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>ブール値</p> </td>
   <td><p>true の場合、フォームのコンポーネントで指定された数値または日付は、minimum プロパティに指定された数値または日付よりも大きい値である必要があります。</p> <p>false の場合、フォームのコンポーネントで指定された数値または日付は、minimum プロパティに指定された数値または日付以上の値である必要があります。</p> </td>
   <td>
    <ul>
     <li>数値ボックス</li>
     <li>数値ステッパー</li>
     <li>日付選択</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>文字列</p> </td>
   <td><p>コンポーネントで許可される最小文字数を指定します。最小の長さは 0 以上である必要があります。</p> </td>
   <td>
    <ul>
     <li>テキストボックス</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>文字列</td>
   <td>コンポーネントで許可される最大文字数を指定します。最大の長さは 0 以上である必要があります。</td>
   <td>
    <ul>
     <li>テキストボックス</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>文字列</p> </td>
   <td><p>文字のシーケンスを指定します。文字が指定されたパターンに適合すると、コンポーネントはその文字を受け入れます。</p> <p>この pattern プロパティは、対応するアダプティブフォームコンポーネントの検証パターンにマップされます。</p> </td>
   <td>
    <ul>
     <li>XSD スキーマにマップされるすべてのアダプティブフォームコンポーネント </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>文字列</td>
   <td>配列の項目の最大数を指定します。項目の最大数は 0 以上である必要があります。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>文字列</td>
   <td>配列の項目の最小数を指定します。項目の最小数は 0 以上である必要があります。</td>
   <td> </td>
  </tr>
 </tbody>
</table>


## スキーマ準拠データの有効化 {#enablig-schema-compliant-data}

フォーム送信時にすべての JSON スキーマベースのアダプティブフォームでスキーマに準拠したデータを生成できるようにするには、次の手順に従います。

1. `https://server:host/system/console/configMgr` で Experience Manager web コンソールに移動します。
1. **[!UICONTROL アダプティブフォームおよびインタラクティブ通信 web チャネルの設定]**&#x200B;を見つけます。
1. その設定を選択して編集モードで開きます。
1. **[!UICONTROL スキーマ準拠データを生成]**&#x200B;チェックボックスをオンにします。
1. 設定を保存します。

![アダプティブフォームおよびインタラクティブ通信 web チャネルの設定](/help/forms/assets/af-ic-web-channel-configuration.png)


## サポート対象外の構成  {#non-supported-constructs}

アダプティブフォームは以下の JSON スキーマ構成をサポートしていません。

* Null タイプ
* any などの Union タイプ
* OneOf、AnyOf、AllOf、NOT
* 同種の配列のみがサポートされます。そのため、項目制限は、配列でなくオブジェクトである必要があります。
* $ref での URI 参照

## よくある質問 {#frequently-asked-questions}

**繰り返し可能なサブフォーム（minOccurs 値または maxOccurs 値が 1 より大きい）では、サブフォーム（任意の複合型から生成された構造）の個々の要素をドラッグできないのはなぜですか？**

繰り返し可能なサブフォームでは、完全なサブフォームを使用する必要があります。選択した一部のフィールドのみを使用する場合は、構造全体を使用し、不要部分を削除します。

**コンテンツファインダーに長く複雑な構造があります。特定の要素を見つけるにはどうすればよいですか？**

以下の 2 つのオプションがあります。

* ツリー構造をスクロールする
* 検索ボックスを使用して、要素を検索する

**JSON スキーマファイルの拡張子は何ですか。**

JSON スキーマファイルの拡張子は、.schema.json にする必要があります。例えば、&lt;filename>.schema.json のように指定します。

**コアコンポーネントに基づくアダプティブフォームでは、`aem:afProperties` は JSON スキーマの一部としてサポートされていますか？**

いいえ、`aem:afProperties` は、コアコンポーネントではサポートされていません。このプロパティは、基盤コンポーネントに対してのみサポートされています。

## 関連トピック {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Design XML Schema for an Adaptive Form](/help/forms/adaptive-form-xml-schema-form-model.md)

-->
