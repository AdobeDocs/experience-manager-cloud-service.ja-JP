---
title: AEMでのGraphQLの使用方法 — サンプルコンテンツとクエリ
description: AEMでのGraphQLの使用方法 — サンプルコンテンツとクエリ
translation-type: tm+mt
source-git-commit: 46e179faa7875c4b3e9da30356d2b82d4b25b130
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 6%

---


# AEMでのGraphQLの使用方法 — サンプルコンテンツとクエリ{#learn-graphql-with-aem-sample-content-queries}

>[!CAUTION]
>
>AEM GraphQL API(コンテンツフラグメント配信用)は、2021年の初めにリリースされます。
>
>関連ドキュメントは、既にプレビュー目的でご利用いただけます。

GraphQLクエリの使用を開始し、AEMコンテンツフラグメントとの連携方法を学ぶには、いくつかの実用的な例を見るのに役立ちます。

この問題を解決するには、以下を参照してください。

* [サンプルコンテンツフラグメント構造](#content-fragment-structure-graphql)

* また、サンプルコンテンツフラグメント構造（コンテンツフラグメントモデルと関連するコンテンツフラグメント）に基づく[サンプルGraphQLクエリ](#graphql-sample-queries)もいくつかあります。

## AEM用のGraphQL — 一部の拡張子{#graphql-some-extensions}

AEM用のGraphQLでのクエリの基本的な操作は、標準のGraphQL仕様に従います。 AEMを使用したGraphQLクエリの場合、いくつかの拡張子があります。

* 単一の結果が必要な場合：
   * モデル名を使用eg city

* 結果のリストを期待する場合：
   * モデル名に「リスト」を追加します。例：`cityList`

* 論理和を使用する場合：
   * use &quot; _logOp:OR&quot;

* 論理積(AND)も存在しますが、（多くの場合）暗黙的です

* コンテンツフラグメントモデル内のフィールドに対応するフィールド名にクエリできます

* モデルのフィールドに加えて、システム生成フィールドがいくつかあります（アンダースコアの前にあります）。

   * コンテンツの場合：

      * `_locale` :言葉を明かす言語マネージャーに基づく

      * `_metadata` :フラグメントのメタデータを表示するには

      * `_path` :リポジトリ内のコンテンツフラグメントへのパス

      * `_references` :参考文献を表示するリッチテキストエディターへのインライン参照の追加

      * `_variations` :コンテンツフラグメント内の特定のバリエーションを表示するには
   * 操作：

      * `_operator` :特定の演算子を適用する； `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,

      * `_apply` :特定の条件を適用する場合例えば、   `AT_LEAST_ONCE`

      * `_ignoreCase` :クエリー時にケースを無視するには


* GraphQL和集合タイプは次のようにサポートされます。

   * use `...on`


## GraphQL {#content-fragment-structure-graphql}で使用するサンプルコンテンツフラグメント構造

簡単な例を挙げるには、以下が必要です。

* 1つ以上の[サンプルコンテンツフラグメントモデル](#sample-content-fragment-models-schemas) - GraphQLスキーマの基盤を形成します。

* [上記のモデルに基づくコンテンツ](#sample-content-fragments) フラグメントのサンプル

### コンテンツフラグメントモデルのサンプル(スキーマ) {#sample-content-fragment-models-schemas}

サンプルクエリでは、次のコンテンツモデルとその相互関係（参照 —>）を使用します。

* [会社](#model-company)
-> [個人](#model-person)
    -> [賞](#model-award)

* [市区町村](#model-city)

#### 会社 {#model-company}

会社を定義する基本フィールドを次に示します。

| フィールド名 | データタイプ | リファレンス |
|--- |--- |--- |
| 会社名 | 1 行のテキスト |  |
| 最高経営責任者 | フラグメント参照（1つ） | [人](#model-person) |
| 従業員 | フラグメント参照（複数フィールド） | [人](#model-person) |

#### 人 {#model-person}

従業員にもなれる個人を定義するフィールド：

| フィールド名 | データタイプ | リファレンス |
|--- |--- |--- |
| 名前 | 1 行のテキスト |  |
| 名 | 1 行のテキスト |  |
| 賞 | フラグメント参照（複数フィールド） | [賞](#model-award) |

#### 賞{#model-award}

賞を定義するフィールドは次のとおりです。

| フィールド名 | データタイプ | リファレンス |
|--- |--- |--- |
| ショートカット/ID | 1 行のテキスト |  |
| タイトル | 1 行のテキスト |  |

#### 市区町村 {#model-city}

都市を定義するフィールドは次のとおりです。

| フィールド名 | データタイプ | リファレンス |
|--- |--- |--- |
| 名前 | 1 行のテキスト |  |
| 国 | 1 行のテキスト |  |
| 母集団 | 数値 |  |
| カテゴリ | タグ |  |

### サンプルコンテンツフラグメント{#sample-content-fragments}

適切なモデルでは、次のフラグメントが使用されます。

#### 会社 {#fragment-company}

| 会社名 | 最高経営責任者 | 従業員 |
|--- |--- |--- |
| Apple | Steve Jobs | デューク・マーシュ<br>最大のコーフィールド |
|  リトルポニー | アダム・スミス | ララ・クロフト<br>カッター・スレード |
| NextStep Inc. | Steve Jobs | ジョー・スミス<br>安倍リンカーン |

#### 人 {#fragment-person}

| 名前 | 名 | 賞 |
|--- |--- |--- |
| リンカーン |  阿部 |  |
| スミス | Adam |   |
| スライド |  カッター |  Gameblitz<br>ゲームスター |
| マーシュ |  公爵 |   |   |
|  スミス |  ジョー |   |
| クロフト |  ララ | ゲームスター |
| Caulfield |  Max |  Gameblitz |
|  ジョブ |  スティーブ |   |

#### 賞{#fragment-award}

| ショートカット/ID | タイトル |
|--- |--- |
| GB | Gameblitz |
|  GS | ゲームスター |
|  OSC | オスカー |

#### 市区町村 {#fragment-city}

| 名前 | 国 | 母集団 | カテゴリ |
|--- |--- |--- |--- |
| バーゼル | スイス | 172258 | city:emea |
| ベルリン | ドイツ | 3669491 | city:capital<br>city:emea |
| ブカレスト | ルーマニア | 1821000 |  city:capital<br>city:emea |
| サンフランシスコ |  米国 |  883306 |  city:beach<br>city:na |
| サンノゼ |  米国 |  102635 |  city:na |
| Stutgart |  ドイツ |  634830 |  city:emea |
|  チューリッヒ |  スイス |  415367 |  city:capital<br>city:emea |

## GraphQL — サンプルコンテンツフラグメント構造を使用したサンプルクエリ{#graphql-sample-queries-sample-content-fragment-structure}

クエリの作成の図とサンプル結果については、サンプルクエリを参照してください。

>[!NOTE]
>
>インスタンスに応じて、AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)に含まれる[Graph *i* QLインターフェイスに直接アクセスし、クエリの送信とテストを行うことができます。
>
>例：`http://localhost:4502/content/graphiql.html`

### サンプルクエリ — 使用可能なすべてのスキーマとデータ型{#sample-all-schemes-datatypes}

これにより、使用可能なすべてのスキーマのすべてのタイプが返されます。

**サンプルクエリ**

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### サンプルクエリ-会社のCEOと従業員の詳細{#sample-full-details-company-ceos-employees}

このクエリは、ネストされたフラグメントの構造を使用して、会社のCEOとその従業員全員の詳細を返します。

**サンプルクエリ**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### サンプルクエリ — すべての市区町村に関するすべての情報{#sample-all-information-all-cities}

すべての市区町村に関するすべての情報を取得するには、次の非常に基本的なクエリを使用できます。
**サンプルクエリ**

```xml
{
  cityList {
    items
  }
}
```

実行すると、クエリが自動的に拡張され、すべてのフィールドが含まれます。

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### サンプルクエリ — すべての市区町村の名前{#sample-names-all-cities}

これは、`city`スキーマ内のすべてのエントリの`name`を返す単純なクエリです。

**サンプルクエリ**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### サンプルクエリ — 単一の都市フラグメント{#sample-single-city-fragment}

これは、リポジトリ内の特定の場所にある単一のフラグメントエントリの詳細を返すクエリです。

**サンプルクエリ**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### サンプルクエリ — 名前付きのバリエーションのあるすべての市区町村{#sample-cities-named-variation}

`city`ベルリンに「Berlin Center」(`berlin_centre`)という名前の新しいバリエーションを作成する場合、クエリを使用してバリエーションの詳細を返すことができます。

**サンプルクエリ**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### サンプルクエリ- 「Jobs」または「Smith」 {#sample-all-persons-jobs-smith}という名前を持つすべての人

`Jobs`または`Smith`という名前を持つすべての`persons`がフィルタされます。

**サンプルクエリ**

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### サンプルクエリ- 「Jobs」の名前を持たないすべての人{#sample-all-persons-not-jobs}

`Jobs`または`Smith`という名前を持つすべての`persons`がフィルタされます。

**サンプルクエリ**

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### サンプルクエリ — ドイツまたはスイスにあり、人口が400000 ～ 99999の全都市{#sample-all-cities-d-ch-population}

ここでは、複数のフィールドの組み合わせがフィルタリングされます。 `AND`（暗黙的な）は`population`範囲の選択に使用され、`OR`（明示的な）は必要な市区町村の選択に使用されます。

**サンプルクエリ**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### サンプルクエリ:{#sample-all-cities-san-ignore-case}の場合に関係なく、名前にSANが含まれるすべての市区町村

このクエリは、`SAN`が名前に含まれるすべての都市を、大文字と小文字に関係なく調査します。

**サンプルクエリ**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### サンプルクエリ — 少なくとも1回は{#sample-array-item-occur-at-least-once}が必要な項目を含むアレイに対するフィルタ

このクエリフィルターは、少なくとも1回は発生する必要があるアイテム(`city:na`)を持つアレイ上に存在します。

**サンプルクエリ**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### サンプルクエリ — 正確な配列値でフィルタ{#sample-array-exact-value}

このクエリフィルターは、正確な配列値に対して発生します。

**サンプルクエリ**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### ネストされたコンテンツフラグメントのサンプルクエリ- 「Smith」 {#sample-companies-employee-smith}という名前を持つ従業員が少なくとも1人いるすべての会社

このクエリは、`name` &quot;Smith&quot;の`person`のフィルタリングを説明し、ネストされた2つのフラグメント（`company`と`employee`）から情報を返します。

**サンプルクエリ**

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### ネストされたコンテンツフラグメントのサンプルクエリ — すべての従業員が「Gamestar」賞を受賞したすべての会社{#sample-all-companies-employee-gamestar-award}

このクエリでは、`company`、`employee`、`award`の3つのネストされたフラグメントに対するフィルタリングについて説明します。

**サンプルクエリ**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
        awards {
          id
          title
        }
      }
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### メタデータのサンプルクエリ — 賞のメタデータのリスト（タイトル：GB {#sample-metadata-awards-gb}）

このクエリでは、`company`、`employee`、`award`の3つのネストされたフラグメントに対するフィルタリングについて説明します。

**サンプルクエリ**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**サンプル結果**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## WKNDプロジェクトを使用したサンプルクエリ{#sample-queries-using-wknd-project}

これらのサンプルクエリは、WKNDプロジェクトに基づいています。

>[!NOTE]
>
>結果は広範囲に及ぶ可能性があるので、ここでは再現されていません。

### 特定のモデルのすべてのコンテンツフラグメントの指定されたプロパティ{#sample-wknd-all-model-properties}を持つサンプルクエリ

次のサンプルクエリは、次の情報を取り調べます。

* `article`タイプのすべてのコンテンツフラグメント
* を`path`および`author`プロパティと共に使用します。

**サンプルクエリ**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### メタデータのサンプルクエリ{#sample-wknd-metadata}

このクエリは、次の情報を取り調べます。

* `adventure`タイプのすべてのコンテンツフラグメント
* メタデータ

**サンプルクエリ**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### 特定のモデル{#sample-wknd-single-content-fragment-of-given-model}の1つのコンテンツフラグメントのサンプルクエリ

次のサンプルクエリは、次の情報を取り調べます。

* 特定のモデルの単一のコンテンツフラグメント
* すべての形式のコンテンツ：
   * HTML
   * Markdown
   * プレーンテキスト
   * JSON

**サンプルクエリ**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### ネストされたコンテンツフラグメントのサンプルクエリ — 単一モデルタイプ{#sample-wknd-nested-fragment-single-model}

**サンプルクエリ**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### ネストされたコンテンツフラグメントのサンプルクエリ — 複数モデルタイプ{#sample-wknd-nested-fragment-multiple-model}

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### コンテンツ参照{#sample-wknd-fragment-specific-model-content-reference}を使用した特定のモデルのコンテンツフラグメントのサンプルクエリ

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### プリフェッチされた参照を持つ複数のコンテンツフラグメントのサンプルクエリ{#sample-wknd-multiple-fragments-prefetched-references}

```xml
{
  bookmarkList {
    _references {
       ... on ImageRef {
        _path
        type
        height
      }
      ... on MultimediaRef {
        _path
        type
        size
      }
      ... on DocumentRef {
        _path
        type
        author
      }
      ... on ArchiveRef {
        _path
        type
        format
      }
    }
  }
}
```

### 特定のモデル{#sample-wknd-single-fragment-given-model}の単一のコンテンツフラグメントのバリエーションのサンプルクエリ

**サンプルクエリ**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 特定のロケール{#sample-wknd-multiple-fragments-given-locale}の複数のコンテンツフラグメントのサンプルクエリ

**サンプルクエリ**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### RTEインライン参照を含む1つのコンテンツフラグメントのサンプルクエリ{#sample-wknd-single-fragment-rte-inline-reference}

**サンプルクエリ**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### 特定のモデルの複数のコンテンツフラグメントの名前付きのバリエーションのサンプルクエリ{#sample-wknd-variation-multiple-fragment-given-model}

**サンプルクエリ**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```
