---
title: コンテンツフラグメントの分析
description: コンテンツフラグメントの構造とコンテンツ配信を理解します。 これは、ヘッドレス配信とページオーサリングの両方に関する情報を提供します。
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 2%

---


# コンテンツフラグメント構造の分析 {#analyzing-content-fragments-structure}

コンテンツフラグメントは [GraphQLを使用したヘッドレス配信](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). これは、多層構造を持つことができることを意味します。

Experience Manager(AEM) には、フラグメントの構造を表示および分析する方法がいくつか用意されています。

## 参照 {#references}

構造は「参照」(References) を使用して構築されます。

* [参照のデータタイプはコンテンツフラグメントモデルで定義されます](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* オーサリング時に、次の操作を実行できます。
   * [これらの参照を管理](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [フラグメントの親参照を検索](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## 構造ツリー {#structure-tree}

を開きます。 **構造ツリー** 」タブをクリックして、コンテンツフラグメントの階層構造とその参照を表示します。 リンクアイコンを使用して参照を開きます。

例：

![コンテンツフラグメントエディター — 構造ツリー](assets/cf-authoring-structure-tree.png)