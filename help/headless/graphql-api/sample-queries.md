---
title: AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ
description: GraphQL を AEM と共に使用し、サンプルコンテンツとクエリを調べて、コンテンツをヘッドレスに提供する方法を説明します。
feature: Headless, Content Fragments,GraphQL API
exl-id: b60fcf97-4736-4606-8b41-4051b8b0c8a7
role: Admin, Developer
source-git-commit: 6f90bfebf2c9898bf8c1ad2643f8edc4ff4dda53
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 99%

---

# AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ {#learn-graphql-with-aem-sample-content-queries}

GraphQL を AEM と共に使用し、サンプルコンテンツとクエリを調べて、コンテンツをヘッドレスに提供する方法を説明します。

>[!NOTE]
>
>このページと併せて、以下のページも確認してください。
>
>* [コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/overview.md)
>* [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
>* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)

GraphQL クエリの基本と、AEM コンテンツフラグメントとの連携方法を学ぶには、いくつかの実践的な例が参考になります。

以下を参照してください。

* [サンプルコンテンツフラグメント構造](#content-fragment-structure-graphql)

* サンプルコンテンツフラグメント構造（コンテンツフラグメントモデルと関連するコンテンツフラグメント）に基づく、いくつかの[サンプル GraphQL クエリ](#graphql-sample-queries)。

>[!CONTEXTUALHELP]
>id="aemcloud_headless_graphql_sample"
>title="AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ"
>abstract="GraphQL を AEM と共に使用し、サンプルコンテンツとクエリを調べて、コンテンツをヘッドレスに提供する方法を説明します。"

## GraphQL - サンプルコンテンツフラグメント構造を使用したサンプルクエリ {#graphql-sample-queries-sample-content-fragment-structure}

クエリの作成とサンプル結果については、これらのサンプルクエリを参照してください。

>[!NOTE]
>
>インスタンスによっては、[AEM GraphQL API に付属している GraphiQL インターフェイス](/help/headless/graphql-api/graphiql-ide.md)に直接アクセスして、クエリの送信とテストを行うことができます。
>
>クエリエディターには、次のいずれかの方法でアクセスできます。
>
>* **ツール**／**一般**／**GraphQL クエリエディター**
>* 直接アクセス（例：`http://localhost:4502/aem/graphiql.html`）

>[!NOTE]
>
>サンプルクエリは、[GraphQL で使用するコンテンツフラグメント構造のサンプル](#content-fragment-structure-graphql)に基づいています。

### サンプルクエリ - 使用可能なすべてのスキーマとデータタイプ {#sample-all-schemes-datatypes}

使用可能なすべてのスキーマの `types` をすべて返します。

**サンプルクエリ**

```graphql
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

```json
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

すべての都市に関するすべての情報を取得するには、次のような基本的なクエリを使用します。
**サンプルクエリ**

```graphql
{
  cityList {
    items
  }
}
```

実行時にクエリが自動的に展開されて、次のように、すべてのフィールドが組み込まれます。

```graphql
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

```json
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

`city` スキーマ内のすべてのエントリの `name` を返す単純なクエリです。

**サンプルクエリ**

```graphql
query {
  cityList {
    items {
      name
    }
  }
}
```

**サンプル結果**

```json
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

### サンプルクエリ - 1 つの特定の都市フラグメント {#sample-single-specific-city-fragment}

リポジトリ内の特定の場所にある 1 つのフラグメントエントリの詳細を返すクエリです。

**サンプルクエリ**

```graphql
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

```json
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

```graphql
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

```json
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

### サンプルクエリ - 市区町村の区切り文字としてタグ付けされた、すべての都市の名前 {#sample-names-all-cities-tagged-city-breaks}

次の場合：

* `Tourism` : `Business`、`City Break`、`Holiday` という名前の様々なタグを作成し、
* これらを様々な `City` インスタンスのマスターバリエーションに割り当てます

この場合、クエリを使用して、`city` スキーマで都市滞在型休暇としてタグ付けされたすべてのエントリの `name` および `tags` の詳細を返すことができます。

**サンプルクエリ**

```graphql
query {
  cityList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "tourism:city-break", _operator: CONTAINS}]}}
  ){
    items {
      name,
      _tags
    }
  }
}
```

**サンプル結果**

```json
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Berlin",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        },
        {
          "name": "Zurich",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
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

```graphql
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

```json
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

名前が `Jobs` または `Smith` であるすべての `persons` をフィルタリングするクエリ

**サンプルクエリ**

```graphql
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

```json
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

名前が `Jobs` または `Smith` であるすべての `persons` をフィルタリングするクエリ

**サンプルクエリ**

```graphql
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

```json
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

### サンプルクエリ - `_path` が特定の接頭辞で始まるすべてのアドベンチャー {#sample-wknd-all-adventures-cycling-path-filter}

`_path` が特定の接頭辞（`/content/dam/wknd/en/adventures/cycling`）で始まるすべての `adventures`。

**サンプルクエリ**

```graphql
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**サンプル結果**

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### サンプルクエリ - ドイツまたはスイスにあり、人口が 400000 から 999999 の範囲にあるすべての都市 {#sample-all-cities-d-ch-population}

ここでは、フィールドの組み合わせに基づいてフィルタリングされます。`AND`（暗黙的）を使用して `population` の範囲を選択しつつ、`OR`（明示的）を使用して必要な都市を選択しています。

**サンプルクエリ**

```graphql
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

```json
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

```graphql
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

```json
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

```graphql
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

```json
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

```graphql
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

```json
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

```graphql
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

```json
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

```graphql
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

```json
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

```graphql
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

```json
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

これらのサンプルクエリは WKND プロジェクトに基づいています。以下の項目があります。

* 次の URL で入手できるコンテンツフラグメントモデル：
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 次の URL で入手できるコンテンツフラグメント（およびその他のコンテンツ）：
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
  `http://<hostname>:<port>/assets.html/content/dam/wknd-shared/en`

>[!NOTE]
>
>結果は膨大な量になる可能性があるので、ここでは再現されていません。

### 特定モデルのコンテンツフラグメントのうち指定のプロパティを持つものをすべて取得するサンプルクエリ {#sample-wknd-all-model-properties}

このサンプルクエリでは次のものを検索します。

* `article` タイプのすべてのコンテンツフラグメントについて
* `_path` と、`authorFragment` のプロパティを備えたもの。

**サンプルクエリ**

```graphql
{
  articleList {
    items {
      _path
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
    }
 }
}
```

### メタデータのサンプルクエリ {#sample-wknd-metadata}

このクエリでは次のものを問い合わせます。

* `adventure` タイプのすべてのコンテンツフラグメントについて
* メタデータ

**サンプルクエリ**

```graphql
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

* 特定のパスにある `article` タイプの 1 つのコンテンツフラグメントについて
   * そのフラグメントの中の、次のすべてのコンテンツ形式
      * HTML
      * マークダウン
      * プレーンテキスト
      * JSON

**サンプルクエリ**

```graphql
{
  articleByPath(_path: "/content/dam/wknd-shared/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        authorFragment {
          _path
          firstName
          lastName
          birthDay
        }
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

### モデルからのコンテンツフラグメントモデルのサンプルクエリ {#sample-wknd-content-fragment-model-from-model}

このサンプルクエリでは次のものを検索します。

* 1 つのコンテンツフラグメントについて
   * 基になるコンテンツフラグメントモデルの詳細

**サンプルクエリ**

```graphql
{
  adventureByPath(_path: "/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van") {
    item {
      _path
      title
      _model {
        _path
        title
      }
    }
  }
}
```

### ネストされたコンテンツフラグメントのサンプルクエリ - 単一モデルタイプ{#sample-wknd-nested-fragment-single-model}

このクエリでは次のものを問い合わせます。

* 特定のパスにある `article` タイプの 1 つのコンテンツフラグメントについて
   * そのフラグメントの中の、参照されている（ネストされた）フラグメントのパスと作成者

>[!NOTE]
>
>フィールド `referencearticle` のデータタイプは `fragment-reference` です。

**サンプルクエリ**

```graphql
{
  adventureByPath(_path: "/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van") {
    item {
      _path
      title
      _model {
        _path
        title
      }
    }
  }
}
```

### ネストされたコンテンツフラグメントのサンプルクエリ - 複数モデルタイプ{#sample-wknd-nested-fragment-multiple-model}

#### 単一の参照モデルタイプ

このクエリでは次のものを問い合わせます。

* `bookmark` タイプの複数のコンテンツフラグメントについて
   * 特定のモデルタイプ `Article` の他のフラグメントへのフラグメント参照を含むもの

>[!NOTE]
>
>フィールド `fragments` のデータタイプは `fragment-reference` で、モデル `Article` が選択されています。クエリは `fragments` を `[Article]` の配列として配信します。

```graphql
{
  bookmarkList {
    items {
        fragments {
          _path
          author
        }
     }
  }
}
```

#### 複数の参照モデルタイプ

このクエリでは次のものを問い合わせます。

* `bookmark` タイプの複数のコンテンツフラグメントについて
   * 特定のモデルタイプ `Article` および `Adventure` の他のフラグメントへのフラグメント参照を含むもの

>[!NOTE]
>
>フィールド `fragments` のデータタイプは `fragment-reference` で、モデル `Article` および `Adventure` が選択されています。クエリは `fragments` を `[AllFragmentModels]` の配列として配信します。これはユニオン型でデリファレンスされます。

```graphql
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

### 特定モデルのコンテンツフラグメントのうちコンテンツ参照を含んだものを取得するサンプルクエリ{#sample-wknd-fragment-specific-model-content-reference}

このクエリには次の 2 種類があります。

1. すべてのコンテンツ参照を返すもの。
1. `attachments` タイプの特定のコンテンツ参照を返すもの。

これらのクエリでは次のものを検索します。

* `bookmark` タイプの複数のコンテンツフラグメントについて
   * 他のフラグメントへのコンテンツ参照を含むもの

#### プリフェッチされた参照を含んだ複数のコンテンツフラグメントのサンプルクエリ {#sample-wknd-multiple-fragments-prefetched-references}

次のクエリは、`_references` を使用して、すべてのコンテンツ参照を返します。

<!-- need replacement query -->

```graphql
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

#### 添付ファイルを含んだ複数のコンテンツフラグメントのサンプルクエリ {#sample-wknd-multiple-fragments-attachments}

次のクエリは、すべての `attachments`（`content-reference` タイプの特定のフィールド（サブグループ））を返します。

>[!NOTE]
>
>フィールド `attachments` のデータタイプは `content-reference` で、様々な形式が選択されています。

<!-- need replacement query -->

```graphql
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

### UUID 参照を使用した特定のモデルのコンテンツフラグメントのサンプルクエリ {#sample-wknd-fragment-specific-model-uuid-references}

これらのクエリでは次のものを検索します。

* コンテンツフラグメントの UUID、および参照されるコンテンツフラグメントまたはアセットの UUID
* 結果は、JSON プロパティ `_id` を使用して返されます

#### UUID 参照を使用した特定のモデルのコンテンツフラグメントのサンプルクエリ {#sample-wknd-fragment-specific-model-using-a-uuid-reference}

次のクエリは、`_id` と `_path` を使用して、すべてのコンテンツ参照を返します。

```graphql
{
  articleList {
    items {
        _id
        _path
        title
        featuredImage {
          ... on ImageRef {
            _id
            _path           
          }
        }
        authorFragment {
          firstName
          lastName
          profilePicture {
            ... on ImageRef {
              _id
              _path
            }
          }
        }
      }
  }
}
```

#### UUID 参照によるコンテンツフラグメントのサンプルクエリ {#sample-wknd-fragment-specific-model-by-uuid-reference}

次のクエリは、特定の `_id` に関連するすべてのコンテンツ参照を返します。

```graphql
{
  articleById(_id: "3ce2bf53-7436-4d3e-b19a-2793bc2ca63e") {
    item {
      _id
      _path
      title
      featuredImage {
        ... on ImageRef {
          _id
          _path
        }
      }
      authorFragment {
        firstName
        lastName
        profilePicture {
          ... on ImageRef {
            _id
            _path
          }
        }
      }
    }
  }
}
```

### RTE インライン参照を含んだ 1 つのコンテンツフラグメントのサンプルクエリ {#sample-wknd-single-fragment-rte-inline-reference}

このクエリでは次のものを問い合わせます。

* 特定のパスにある `bookmark` タイプの 1 つのコンテンツフラグメントについて
   * その中の RTE インライン参照

>[!NOTE]
>
>RTE インライン参照は、`_references` 内に含まれます。

<!-- need replacement query -->

**サンプルクエリ**

```graphql
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

このクエリでは次のものを問い合わせます。

* 特定のパスにある `author` タイプの 1 つのコンテンツフラグメントについて
   * そのフラグメントの中の、バリエーション `another` に関するデータ

**サンプルクエリ**

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/ian-provo", variation: "another") {
    item {
        _path
        _variation
        firstName
        lastName
        birthDay
    }
  }
}
```

### 特定モデルの複数のコンテンツフラグメントの名前付きバリエーションを取得するサンプルクエリ {#sample-wknd-variation-multiple-fragment-given-model}

このクエリでは次のものを問い合わせます。

* 特定のバリエーション `another` を持つ `author` タイプのコンテンツフラグメント

>[!NOTE]
>
>このクエリにより、指定した名前の[バリエーション](/help/headless/graphql-api/content-fragments.md#variations)がないコンテンツフラグメントのフォールバックが示されます。

**サンプルクエリ**

```graphql
{
  authorList(variation: "another") {
    items {
        _path
        _variation
        firstName
        lastName
        birthDay
    }
  }
}
```

### 特定モデルの複数のコンテンツフラグメントとそのバリエーションのサンプルクエリ {#sample-wknd-multiple-fragment-variations-given-model}

このクエリでは次のものを問い合わせます。

* `article` タイプのコンテンツフラグメントとすべてのバリエーション

**サンプルクエリ**

```graphql
query {
  articleList(
    includeVariations: true  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### 特定のタグが設定された特定モデルのコンテンツフラグメントバリエーションのサンプルクエリ{#sample-wknd-fragment-variations-given-model-specific-tag}

このクエリでは次のものを問い合わせます。

* タグ `WKND : Activity / Hiking` の付いた 1 つ以上のバリエーションを持つ `article` タイプのコンテンツフラグメント

**サンプルクエリ**

```graphql
{
  articleList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "wknd:activity/hiking", _operator: CONTAINS}]}}
  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### 特定ロケールの複数のコンテンツフラグメントのサンプルクエリ {#sample-wknd-multiple-fragments-given-locale}

このクエリでは次のものを問い合わせます。

* `fr` ロケール内の `article` タイプのコンテンツフラグメント

**サンプルクエリ**

```graphql
{ 
  articleList(_locale: "fr") {
    items {
      _path
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
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

### オフセットと制限を使用したサンプルリストクエリ {#sample-list-offset-limit}

このクエリでは次のものを問い合わせます。

* *完全*&#x200B;な結果リストの 5 番目の記事から始まる最大 5 つの記事を含む結果のページ

**サンプルクエリ**

```graphql
{
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
      _path
    }
  }
}
```

### first と after を使用したサンプルページネーションクエリ  {#sample-pagination-first-after}

このクエリでは次のものを問い合わせます。

* *完全*&#x200B;な結果リストで指定したカーソル項目から始まる最大 5 つのアドベンチャーを含む結果のページについて

**サンプルクエリ**

```graphql
{
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

### _tags ID でフィルタリングされた、バリエーションを含まないサンプルクエリ {#sample-filtering-tag-not-variations}

このクエリでは次のものを問い合わせます。

* タグ `big-block` の付いた `vehicle` タイプのコンテンツフラグメント
* バリエーションを含まない

**サンプルクエリ**

```graphql
query {
  vehicleList(
    filter: {
    _tags: {
      _expressions: [
        {
          value: "vehicles:big-block"
          _operator: CONTAINS
        }
      ]
    }
  }) {
    items {
      _variation
      _path
      type
      name
      model
      fuel
      _tags
    }
  }
} 
```

### _tags ID でフィルタリングされた、バリエーションを含むサンプルクエリ {#sample-filtering-tag-with-variations}

このクエリでは次のものを問い合わせます。

* タグ `big-block` の付いた `vehicle` タイプのコンテンツフラグメント
* バリエーションを含む

**サンプルクエリ**

```graphql
{
  enginePaginated(after: "SjkKNmVkODFmMGQtNTQyYy00NmQ4LTljMzktMjhlNzQwZTY1YWI2Cmo5", first: 9 ,includeVariations:true, sort: "name",
    filter: {
    _tags: {
      _expressions: [
        {
          value: "vehicles:big-block"
          _operator: CONTAINS
        }
      ]
    }
  }) {
    edges{
    node {
        _variation
        _path
        name
        type
        size
        _tags
        _metadata {
          stringArrayMetadata {
            name
            value
          }
        }
    }
      cursor
    }
  }
} 
```

## DAM および Dynamic Media アセット配信のサンプルクエリ {#sample-queries-delivery-DAM-DM}

Web に最適化された画像配信（DAM アセット）の場合：

* [すべてのパラメーターを使用した web に最適化された画像配信用サンプルクエリ](/help/headless/graphql-api/content-fragments.md#web-optimized-image-delivery-full-parameters)

* [単一の指定パラメーターを使用した web に最適化された画像配信用サンプルクエリ](/help/headless/graphql-api/content-fragments.md#web-optimized-image-delivery-single-query-variable)

Dynamic Media アセットへの URL 配信の場合

* [URL による Dynamic Media アセット配信のサンプルクエリ - 画像参照](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-asset-delivery-by-url-imageref)を参照してください

* [URL による Dynamic Media アセット配信のサンプルクエリ - 複数の参照](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs)を参照してください

コンテンツフラグメントエディターから、現在の AEM インスタンスに対してローカルではないリモートアセットを配信する場合

* 詳しくは、[OpenAPI アセットサポートの Dynamic Media のサンプルクエリ（リモートアセット）](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-for-openapi-asset-support)を参照してください

## GraphQL で使用するコンテンツフラグメント構造のサンプル {#content-fragment-structure-graphql}

サンプルクエリは次の構造に基づいています。

* 1 つ以上の[サンプルコンテンツフラグメントモデル](#sample-content-fragment-models-schemas) - GraphQL スキーマの基盤となります

* 上記のモデルに基づく[サンプルコンテンツフラグメント](#sample-content-fragments)

### サンプルコンテンツフラグメントモデル（スキーマ） {#sample-content-fragment-models-schemas}

サンプルクエリでは、次のコンテンツモデルとその相互関係（参照関係「->」）を使用します。

* [Company](#model-company)
-> [Person](#model-person)
    -> [Award](#model-award)

* [City（市区町村）](#model-city)

#### Company（会社） {#model-company}

会社を定義する基本フィールドは次のとおりです。

| フィールド名 | データタイプ | 参照 |
|--- |--- |--- |
| 会社名 | 1 行のテキスト | |
| CEO | フラグメント参照（1 つ） | [Person](#model-person) |
| 従業員数 | フラグメント参照（複数フィールド） | [Person](#model-person) |

#### Person（人物） {#model-person}

人物（従業員になることも可能）を定義するフィールドは次のとおりです。

| フィールド名 | データタイプ | 参照 |
|--- |--- |--- |
| 名前 | 1 行のテキスト | |
| 名 | 1 行のテキスト | |
| 授賞歴 | フラグメント参照（複数フィールド） | [Award](#model-award) |

#### 賞 {#model-award}

賞を定義するフィールドは次のとおりです。

| フィールド名 | データタイプ | 参照 |
|--- |--- |--- |
| ショートカット／ID | 1 行のテキスト | |
| タイトル | 1 行のテキスト | |

#### City（市区町村） {#model-city}

都市を定義するフィールドは次のとおりです。

| フィールド名 | データタイプ | 参照 |
|--- |--- |--- |
| 名前 | 1 行のテキスト | |
| 国 | 1 行のテキスト | |
| 人口 | 数値 | |
| カテゴリ | タグ | |

### サンプルコンテンツフラグメント {#sample-content-fragments}

適切なモデルでは次のフラグメントが使用されます。

#### Company（会社） {#fragment-company}

| 会社名 | CEO | 従業員数 |
|--- |--- |--- |
| Apple Inc. | Steve Jobs | Duke Marsh<br>Max Caulfield |
| Little Pony, Inc. | Adam Smith | Lara Croft<br>Cutter Slade |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Person（人物） {#fragment-person}

| 名前 | 名 | 授賞歴 |
|--- |--- |--- |
| Lincoln | Abe | |
| Smith | Adam | |
| Slade | Cutter | Gameblitz<br>Gamestar |
| Marsh | Duke | |
| Smith | Joe | |
| Croft | Lara | Gamestar |
| Caulfield | Max | Gameblitz |
| ジョブ | Steve | |

#### 賞 {#fragment-award}

| ショートカット／ID | タイトル |
|--- |--- |
| GB | Gameblitz |
| GS | Gamestar |
| OSC | Oscar |

#### 都市 {#fragment-city}

| 名前 | 国 | 人口 | カテゴリ |
|--- |--- |--- |--- |
| Basel | スイス | 172258 | 市区町村 :emea |
| Berlin | Germany | 3669491 | city:capital<br>city:emea |
| Bucharest | Romania | 1821000 | city:capital<br>city:emea |
| サンフランシスコ | 米国 | 883306 | city:beach<br>city:na |
| サンノゼ | 米国 | 102635 | 市区町村 :na |
| シュトゥットガルト | ドイツ | 634830 | 市区町村 :emea |
| チューリッヒ | スイス | 415367 | city:capital<br>city:emea |
