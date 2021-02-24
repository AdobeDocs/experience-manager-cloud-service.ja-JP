---
title: AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ
description: AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ。
translation-type: tm+mt
source-git-commit: 6a60238b13d66ea2705063670295a62e3cbf6255
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 68%

---


# AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ {#learn-graphql-with-aem-sample-content-queries}

>[!NOTE]
>
>このページは、次の内容と共に読む必要があります。
>
>* [コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)
>* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
>* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)


GraphQL クエリの基本と、AEM コンテンツフラグメントとの連携方法を学ぶには、いくつかの実践的な例が参考になります。

以下を参照してください。

* [サンプルコンテンツフラグメント構造](#content-fragment-structure-graphql)

* サンプルコンテンツフラグメント構造（コンテンツフラグメントモデルと関連するコンテンツフラグメント）に基づくいくつかの[サンプル GraphQL クエリ](#graphql-sample-queries)

## AEM用のGraphQL — 拡張子の概要{#graphql-extensions}

AEM 用の GraphQL でのクエリの基本操作は、標準の GraphQL 仕様に従います。AEM での GraphQL クエリには、次のような拡張機能があります。

* 結果が 1 つだけ必要な場合：
   * モデル名（例：city）を使用します

* 結果のリストを想定している場合：
   * モデル名に`List`を追加；例：`cityList`
   * [サンプルクエリ — すべての市区町村に関するすべての情報](#sample-all-information-all-cities)を参照

* 論理和（OR）を使用する場合：
   * ` _logOp: OR` を使用します
   * [サンプルクエリ- &quot;Jobs&quot;または&quot;Smith&quot;](#sample-all-persons-jobs-smith)の名前を持つすべての人を参照

* 論理積（AND）も存在しますが、（多くの場合）暗黙的です

* コンテンツフラグメントモデル内のフィールドに対応するフィールド名に対してクエリを実行できます
   * [サンプルクエリ-会社のCEOおよび従業員の詳細](#sample-full-details-company-ceos-employees)を参照

* モデルのフィールドに加えて、システム生成フィールドがいくつかあります（前にアンダースコアが付いています）。

   * コンテンツの場合：

      * `_locale`：言語を表示します（言語マネージャーに基づく）
         * [特定のロケールの複数のコンテンツフラグメントに対するサンプルクエリ](#sample-wknd-multiple-fragments-given-locale)を参照
      * `_metadata`：フラグメントのメタデータを表示します
         * [メタデータのサンプルクエリ — 賞のメタデータのリスト（タイトル：GB](#sample-metadata-awards-gb)）を参照
      * `_model` :コンテンツフラグメントモデルのクエリを許可（パスとタイトル）
         * 「[モデルからのコンテンツフラグメントモデルのサンプルクエリ](#sample-wknd-content-fragment-model-from-model)」を参照してください。
      * `_path` :リポジトリ内のコンテンツフラグメントへのパス
         * [サンプルクエリ — 単一の特定の都市のフラグメント](#sample-single-specific-city-fragment)を参照
      * `_reference`：参照（リッチテキストエディターでのインライン参照など）を表示します
         * [参照が事前に取得された複数のコンテンツフラグメントのサンプルクエリ](#sample-wknd-multiple-fragments-prefetched-references)を参照
      * `_variation`：コンテンツフラグメント内の特定のバリエーションを表示します
         * [サンプルクエリ — 名前の付いたバリエーションのあるすべての市区町村](#sample-cities-named-variation)を参照
   * 操作の場合：

      * `_operator` :特定の演算子を適用する； `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`
         * [サンプルクエリ- &quot;Jobs&quot;の名前を持たないすべての人を参照](#sample-all-persons-not-jobs)
      * `_apply`：特定の条件（例：`AT_LEAST_ONCE`）を適用します
         * [サンプルクエリ — 少なくとも1回は](#sample-array-item-occur-at-least-once)を含むアレイのフィルタを参照
      * `_ignoreCase`：クエリの実行時に大文字と小文字を区別しません
         * [サンプルクエリ — 名前にSANが含まれるすべての都市（大文字と小文字を区別しない）を参照](#sample-all-cities-san-ignore-case)









* GraphQL のユニオン型がサポートされています

   * `... on` を使用します
      * 「[コンテンツ参照を使用した特定のモデルのコンテンツフラグメントのサンプルクエリ](#sample-wknd-fragment-specific-model-content-reference)」を参照してください。

## GraphQL - サンプルコンテンツフラグメント構造を使用したサンプルクエリ {#graphql-sample-queries-sample-content-fragment-structure}

作成クエリの図とサンプル結果については、以下のサンプルクエリを参照してください。

>[!NOTE]
>
>インスタンスによっては、[AEM GraphQL API に付属している Graph *i* QL インターフェイス](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)に直接アクセスして、クエリの送信とテストをおこなうことができます。
>
>例：`http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>サンプルクエリは、GraphQL](#content-fragment-structure-graphql)で使用する[サンプルコンテンツフラグメント構造に基づいています

### サンプルクエリ - 使用可能なすべてのスキーマとデータタイプ {#sample-all-schemes-datatypes}

これは、使用可能なすべてのスキーマのすべての`types`を返します。

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

### サンプルクエリ - すべての都市に関するすべての情報 {#sample-all-information-all-cities}

すべての都市に関するすべての情報を取得するには、次のような非常に基本的なクエリを使用します。
**サンプルクエリ**

```xml
{
  cityList {
    items
  }
}
```

実行時にクエリが自動的に展開されて、次のように、すべてのフィールドが組み込まれます。

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

### サンプルクエリ - すべての都市の名前 {#sample-names-all-cities}

これは、`city` スキーマ内のすべてのエントリの `name` を返す単純なクエリです。

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

### サンプルクエリ- 1つの特定の都市フラグメント{#sample-single-specific-city-fragment}

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

### サンプルクエリ - 名前付きバリエーションを持つすべての都市 {#sample-cities-named-variation}

`city` Berlin の新しいバリエーションを「Berlin Center」（`berlin_centre`）という名前で作成する場合は、クエリを使用してバリエーションの詳細を返すことができます。

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

### サンプルクエリ - ある会社の CEO と従業員の詳細 {#sample-full-details-company-ceos-employees}

このクエリでは、ネストされたフラグメントの構造を使用して、ある会社の CEO とすべての従業員の詳細を返します。

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

### サンプルクエリ - 「Jobs」または「Smith」という名前を持つすべての人物 {#sample-all-persons-jobs-smith}

`Jobs` または `Smith` という名前を持つすべての `persons` が抜き出されます。

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

### サンプルクエリ - 「Jobs」という名前を持たないすべての人物 {#sample-all-persons-not-jobs}

`Jobs` という名前を持たないすべての `persons`（`Smith` など）が抜き出されます。

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

### サンプルクエリ - ドイツまたはスイスにあり、人口が 400000 から 999999 範囲にあるすべての都市 {#sample-all-cities-d-ch-population}

ここでは、フィールドの組み合わせに基づいてフィルタリングされます。`AND`（暗黙的）を使用して `population` の範囲を選択しつつ、`OR`（明示的）を使用して必要な都市を選択しています。

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

### サンプルクエリ - 名前に SAN が含まれるすべての都市（大文字と小文字を区別しない場合） {#sample-all-cities-san-ignore-case}

このクエリでは、名前に `SAN` が含まれるすべての都市を、大文字と小文字を区別せずに検索します。

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

### サンプルクエリ - 少なくとも 1 回は現れる項目を含んだ配列をフィルタリング {#sample-array-item-occur-at-least-once}

このクエリでは、少なくとも 1 回は現れる項目（`city:na`）を含んだ配列を抜き出します。

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

### サンプルクエリ - 配列値が正確に一致するものだけをフィルタリング {#sample-array-exact-value}

このクエリでは、配列値が正確に一致するものだけを抜き出します。

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

### ネストされたコンテンツフラグメントのサンプルクエリ - 「Smith」という名前を持つ従業員が少なくとも 1 人いるすべての会社 {#sample-companies-employee-smith}

このクエリでは、「Smith」という `name` の `person` をフィルタリングし、ネストされた 2 つのフラグメント（`company` と `employee`）から取得した情報を返します。

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

### ネストされたコンテンツフラグメントのサンプルクエリ - すべての従業員が「Gamestar」賞を受賞したすべての会社 {#sample-all-companies-employee-gamestar-award}

このクエリは、ネストされた 3 つのフラグメント（`company`、`employee`、`award`）にわたるフィルタリングの例を示しています。

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

### メタデータのサンプルクエリ - 「GB」という賞のメタデータのリスト {#sample-metadata-awards-gb}

このクエリは、ネストされた 3 つのフラグメント（`company`、`employee`、`award`）にわたるフィルタリングの例を示しています。

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

## WKND プロジェクトを使用したサンプルクエリ {#sample-queries-using-wknd-project}

これらのサンプルクエリは WKND プロジェクトに基づいています。これには次のものがあります。

* コンテンツフラグメントモデルは次の場所で利用できます。
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 次の場所で利用可能なコンテンツフラグメント（およびその他のコンテンツ）
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>結果は膨大な量になる可能性があるので、ここでは再現されていません。

### 特定モデルのコンテンツフラグメントのうち指定のプロパティを持つものをすべて取得するサンプルクエリ {#sample-wknd-all-model-properties}

このサンプルクエリでは次のものを検索します。

* `article` タイプのすべてのコンテンツフラグメントについて
* `path` および `author` プロパティを持つもの。

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

### メタデータのサンプルクエリ {#sample-wknd-metadata}

このクエリでは次のものを検索します。

* `adventure` タイプのすべてのコンテンツフラグメントについて
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

### 特定モデルの 1 つのコンテンツフラグメントのサンプルクエリ {#sample-wknd-single-content-fragment-of-given-model}

このサンプルクエリでは次のものを検索します。

* 特定のパスにあるタイプ`article`の単一のコンテンツフラグメント
   * その中で、コンテンツのすべての形式を次のように指定します。
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

### モデル{#sample-wknd-content-fragment-model-from-model}からのコンテンツフラグメントモデルのサンプルクエリ

このサンプルクエリでは次のものを検索します。

* 単一のコンテンツフラグメント用
   * 基になるコンテンツフラグメントモデルの詳細

**サンプルクエリ**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### ネストされたコンテンツフラグメントのサンプルクエリ - 単一モデルタイプ {#sample-wknd-nested-fragment-single-model}

このクエリでは次のものを検索します。

* 特定のパスにあるタイプ`article`の単一のコンテンツフラグメント
   * その中で、参照先（ネストされた）フラグメントのパスと作成者

>[!NOTE]
>
>フィールド`referencearticle`のデータ型は`fragment-reference`です。

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

### ネストされたコンテンツフラグメントのサンプルクエリ - 複数モデルタイプ {#sample-wknd-nested-fragment-multiple-model}

このクエリでは次のものを検索します。

* タイプ`bookmark`の複数のコンテンツフラグメント
   * を、特定のモデルタイプ`article`および`adventure`の他のフラグメントへのフラグメント参照と共に使用します。

>[!NOTE]
>
>フィールド`fragments`のデータタイプは`fragment-reference`で、モデル`Article`、`Adventure`が選択されています。

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

### コンテンツ参照を含む特定のモデルのコンテンツフラグメントのサンプルクエリ{#sample-wknd-fragment-specific-model-content-reference}

このクエリには2種類あります。

1. すべてのコンテンツ参照を返す場合。
1. `attachments`型の特定のコンテンツ参照を返す。

次のクエリが問い合わされます。

* タイプ`bookmark`の複数のコンテンツフラグメント
   * （他のフラグメントへのコンテンツ参照を含む）

#### プリフェッチされた参照を含んだ複数のコンテンツフラグメントのサンプルクエリ {#sample-wknd-multiple-fragments-prefetched-references}

次のクエリは、`_references`を使用して、すべてのコンテンツ参照を返します。

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
    items {
        _path
    }
  }
}
```

#### 添付ファイル付き複数のコンテンツフラグメントのサンプルクエリ{#sample-wknd-multiple-fragments-attachments}

次のクエリは、すべての`attachments` — タイプ`content-reference`の特定のフィールド（サブグループ）を返します。

>[!NOTE]
>
>フィールド`attachments`のデータ型は`content-reference`で、様々なフォームが選択されています。

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

### RTE インライン参照を含んだ 1 つのコンテンツフラグメントのサンプルクエリ {#sample-wknd-single-fragment-rte-inline-reference}

このクエリでは次のものを検索します。

* 特定のパスにあるタイプ`bookmark`の単一のコンテンツフラグメント
   * その中で、RTEインライン参照

>[!NOTE]
>
>RTEインライン参照は、`_references`内で水和されます。

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

### 特定モデルの 1 つのコンテンツフラグメントバリエーションのサンプルクエリ {#sample-wknd-single-fragment-given-model}

このクエリでは次のものを検索します。

* 特定のパスにあるタイプ`article`の単一のコンテンツフラグメント
   * その中で、変動に関連するデータが次のようになります。`variation1`

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

### 特定モデルの複数のコンテンツフラグメントの名前付きバリエーションを取得するサンプルクエリ {#sample-wknd-variation-multiple-fragment-given-model}

このクエリでは次のものを検索します。

* 特定のバリエーションを持つ`article`タイプのコンテンツフラグメントの場合：`variation1`

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

### 特定ロケールの複数のコンテンツフラグメントのサンプルクエリ {#sample-wknd-multiple-fragments-given-locale}

このクエリでは次のものを検索します。

* `fr`ロケール内のタイプ`article`のコンテンツフラグメント

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

## サンプルコンテンツフラグメント構造（GraphQLで使用） {#content-fragment-structure-graphql}

サンプルクエリは次の構造に基づいています。この構造では、次の値を使用します。

* 1 つ以上の[サンプルコンテンツフラグメントモデル](#sample-content-fragment-models-schemas) - GraphQL スキーマの基盤となります

* 上記のモデルに基づく[サンプルコンテンツフラグメント](#sample-content-fragments)

### サンプルコンテンツフラグメントモデル（スキーマ） {#sample-content-fragment-models-schemas}

サンプルクエリでは、次のコンテンツモデルとその相互関係（参照関係「->」）を使用します。

* [Company](#model-company)
-> [Person](#model-person)
    -> [Award](#model-award)

* [City](#model-city)

#### Company {#model-company}

会社を定義する基本フィールドは次のとおりです。

| フィールド名 | データタイプ | 参照 |
|--- |--- |--- |
| name（会社名） | 1 行のテキスト |  |
| ceo（最高経営責任者） | フラグメント参照（1 つ） | [Person](#model-person) |
| employees（従業員） | フラグメント参照（複数フィールド） | [人](#model-person) |

#### Person {#model-person}

人物（従業員になることも可能）を定義するフィールドは次のとおりです。

| フィールド名 | データタイプ | 参照 |
|--- |--- |--- |
| name（氏名） | 1 行のテキスト |  |
| firstName（名） | 1 行のテキスト |  |
| awards（受賞歴） | フラグメント参照（複数フィールド） | [Award](#model-award) |

#### Award {#model-award}

賞を定義するフィールドは次のとおりです。

| フィールド名 | データタイプ | 参照 |
|--- |--- |--- |
| id（賞の ID） | 1 行のテキスト |  |
| title（タイトル） | 1 行のテキスト |  |

#### City {#model-city}

都市を定義するフィールドは次のとおりです。

| フィールド名 | データタイプ | 参照 |
|--- |--- |--- |
| name（氏名） | 1 行のテキスト |  |
| country（国） | 1 行のテキスト |  |
| population（人口） | 数値 |  |
| categories（カテゴリ） | タグ |  |

### サンプルコンテンツフラグメント {#sample-content-fragments}

適切なモデルでは次のフラグメントが使用されます。

#### 会社{#fragment-company}

| name | ceo | employees |
|--- |--- |--- |
| Apple Inc. | Steve Jobs | Duke Marsh<br>Max Caulfield |
|  Little Pony, Inc. | Adam Smith | Lara Croft<br>Cutter Slade |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### ユーザー{#fragment-person}

| name | firstName | awards |
|--- |--- |--- |
| Lincoln |  Abe |  |
| Smith | Adam |   |
| Slade |  Cutter |  Gameblitz<br>Gamestar |
| Marsh |  Duke |   |   |
|  Smith |  Joe |   |
| Croft |  Lara | Gamestar |
| Caulfield |  Max |  Gameblitz |
|  Jobs |  Steve |   |

#### 賞{#fragment-award}

| id | title |
|--- |--- |
| GB | Gameblitz |
|  GS | ゲームスター |
|  OSC | Oscar |

#### 市区町村{#fragment-city}

| name | country | population | categories |
|--- |--- |--- |--- |
| Basel | Switzerland | 172258 | city:emea |
| Berlin | Germany | 3669491 | city:capital<br>city:emea |
| Bucharest | Romania | 1821000 |  city:capital<br>city:emea |
| San Francisco |  USA |  883306 |  city:beach<br>city:na |
| San Jose |  米国 |  102635 |  city:na |
| Stuttgart |  Germany |  634830 |  city:emea |
|  Zurich |  Switzerland |  415367 |  city:capital<br>city:emea |
