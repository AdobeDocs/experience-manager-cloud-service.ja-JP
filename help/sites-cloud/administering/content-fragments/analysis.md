---
title: コンテンツフラグメントの分析
description: コンテンツフラグメントの構造を理解します。ヘッドレス配信とページオーサリングの両方に関連する情報について説明します。
feature: Content Fragments
role: User, Developer
badgeSaas: label="AEM Sites" type="Positive" tooltip="AEM Sitesに適用）。"
exl-id: d9268c1a-bfe6-4df7-bad9-6007dd79e0aa
solution: Experience Manager Sites
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 97%

---

# コンテンツフラグメント構造の分析 {#analyzing-content-fragments-structure}

コンテンツフラグメントは、[GraphQL を使用したヘッドレス配信](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)用に設計されています。つまり、多層構造にすることができます。

Experience Manager（AEM）には、フラグメントの構造を表示および分析する方法がいくつか用意されています。

## 参照 {#references}

多層構造は、参照を使用して作成します。

* [参照のデータタイプはコンテンツフラグメントモデルで定義されます](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* オーサリング時には、次の操作を実行できます。
   * [これらの参照の管理](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [フラグメントの親参照の検索](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## 構造ツリー {#structure-tree}

エディターのツールバーから「**構造ツリー**」タブを開いて、コンテンツフラグメントの階層構造とその参照を表示します。 リンクアイコンを使用して参照を開きます。

次に例を示します。

![コンテンツフラグメントエディター - 構造ツリー](assets/cf-authoring-structure-tree.png)
