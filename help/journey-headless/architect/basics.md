---
title: Learn Content Modeling Basics
description: Learn the basic of modeling content for your Headless CMS using Content Fragments.
exl-id: dc460490-dfc8-4a46-a468-3d03e593447d
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 46%

---

# Learn the Content Modeling Basics for Headless with AEM {#content-modeling-headless-basics}

## The Story so Far {#story-so-far}

[](overview.md)[](introduction.md)

This article builds on these so you understand how to model your content for your AEM headless project.

## 目的 {#objective}

* **オーディエンス**：初心者
* ****

## Content Modeling with Content Fragment Models {#architect-content-fragment-models}

Content (Data) Modeling is a set of established techniques, often used when developed relationship databases, so what does Content Modeling mean for AEM Headless?

### 使用する理由 {#why}

アプリケーションが AEM から必要なコンテンツを一貫して効率的に要求し、受け取れるようにするには、このコンテンツが構造化されている必要があります。

つまり、アプリケーションは、事前に応答の形式を把握し、その処理方法を把握しています。これは、自由形式のコンテンツを受け取るよりもはるかに簡単です。自由形式のコンテンツを受け取る場合は、そのコンテンツの内容と使用方法を判断するために解析する必要があります。

### 仕組みの概要 {#how}

AEM は、コンテンツフラグメントを使用して、コンテンツをアプリケーションにヘッドレスに配信するために必要な構造を提供します。

コンテンツモデルの構造には次が当てはまります。

* コンテンツフラグメントモデルの定義によって実現される。
* コンテンツ生成に使用されるコンテンツフラグメントの基礎として使用される。

>[!NOTE]
>
>The Content Fragment Models are also used as the basis of the AEM GraphQL Schemas, used for retrieving your content - more about that in the Developer Journey.

コンテンツのリクエストは、標準の GraphQL API のカスタマイズされた実装である AEM GraphQL API を使用しておこなわれます。The AEM GraphQL API allows applications to perform (complex) queries on your Content Fragments, with each query being according to a specific model type.

返されたコンテンツは、アプリケーションで使用できます。

## コンテンツフラグメントモデルを使用した構造の作成 {#create-structure-content-fragment-models}

コンテンツフラグメントモデルは、コンテンツの構造を定義するための様々なメカニズムを提供します。

コンテンツフラグメントモデルは、エンティティを記述します。

>[!NOTE]
>Content Fragment functionality must be enabled in the Configuration Browser so that you can create new models.

>[!TIP]
>
>コンテンツフラグメントの作成時に選択するモデルをコンテンツ作成者が把握できるように、モデルに名前を付ける必要があります。

モデル内：

1. **データタイプ**&#x200B;を使用すると、個々の属性を定義できます。例えば、教師の名前を持つフィールドを **Text** とし、その勤続年数を **Number** と定義します。
1. **コンテンツ参照**&#x200B;および&#x200B;**フラグメント参照**&#x200B;データタイプを使用すると、AEM 内の他のコンテンツとの関係を作成できます。
1. **フラグメント参照**&#x200B;データタイプを使用すると、（モデルタイプに従って）コンテンツフラグメントをネストすることで、複数レベルの構造を実現できます。これは、コンテンツモデリングに不可欠です。

次に例を示します。

![](assets/headless-modeling-01.png "")

## データタイプ {#data-types}

AEM では、コンテンツをモデル化するための次のデータタイプが提供されます。

* 1 行のテキスト
* 複数行テキスト
* 数値
* ブール値
* 日時
* 列挙
* タグ
* コンテンツ参照
* フラグメント参照
* JSON オブジェクト

>[!NOTE]
>
>Further details are available under Content Fragment Models - Data Types.

## 参照とネストされたコンテンツ {#references-nested-content}

2 つのデータタイプは、特定のフラグメント外のコンテンツへの参照を提供します。

* **コンテ
ンツの参照**&#x200B;任意のタイプの他のコンテンツへの簡単な参照を提供します。例えば、指定した場所で画像を参照できます。

* **フラグメ
ントの参照**&#x200B;他のコンテンツフラグメントへの参照を提供します。このタイプの参照は、ネストされたコンテンツを作成するために使用され、コンテンツのモデル化に必要な関係を導き出します。このデータタイプは、フラグメント作成者が次の操作をおこなえるように設定可能です。
   * 参照先フラグメントの直接編集
   * 適切なモデルに基づいた新しいコンテンツフラグメントの作成

>[!NOTE]
>
>You can also create ad hoc references by using links within Text blocks.

## Levels of Structure (Nested Fragments) {#levels-of-structure-nested-fragments}

****

** This allows the headless application to follow the connections and access the content as necessary.

>[!NOTE]
>
>**

Fragment References do just that - they allow you to reference another fragment.

For example, you might have the following Content Fragment Models defined:

* City
* 会社
* Person
* awards（受賞歴）

Seems pretty straightforward, but of course a Company has both a CEO and Employees....and these are all people, each defined as a Person.

And a Person can have an Award (or maybe two).

* My Company - Company
   * CEO - Person
   * Employee(s) - Person
      * Personal Award(s) - Award

And that&#39;s just for starters. Depending on the complexity, an Award could be Company-specific, or a Company could have its main office in a specific City.

Representing these interrelationships can be achieved with Fragment References, as they are understood by you (the architect), your content author and the headless applications.

## 次の手順 {#whats-next}

[](model-structure.md)This will introduce and discuss the various references available, and how to create levels of structure with the Fragment References - a key part of modeling for headless.

## その他のリソース {#additional-resources}

* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)

   * [Content Fragment Models - Data Types](/help/assets/content-fragments/content-fragments-models.md#data-types)

* [オーサリングに関する概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [](/help/sites-cloud/authoring/getting-started/basic-handling.md)************

* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)
