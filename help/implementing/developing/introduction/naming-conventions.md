---
title: 命名規則
description: リポジトリのノードは、Java コンテンツリポジトリの命名規則の対象です
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 90%

---

# 命名規則{#naming-conventions}

リポジトリのノードは、Java コンテンツリポジトリの命名規則の対象です。ただし、AEM によってページノード名に追加の規則が課せられます。

## ページの命名規則 {#naming-conventions-for-pages}

これらの命名規則は、以下のような様々なレベルで実装されます。

* JcrUtil：[JCR ユーティリティ](#jcr-utilities)の AEM 実装。
* ページマネージャー：[ページマネージャー](#page-manager)は、ページレベルの操作用のメソッドを提供します。
* AEM UI 内 {#ui-behavior}

### JCR ユーティリティ {#jcr-utilities}

[JcrUtil](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/day/cq/commons/jcr/JcrUtil.html) は JCR ユーティリティの AEM 実装です。名前の検証では特に、文字マッピングと次の点が確認されます。

* `isValidName`
   * 名前が空でなく、有効な文字のみが含まれるかどうかを確認します。
   * 推奨される名前が有効かどうかを確認するのに使用できます。
* `createValidName`
   * 任意の文字列から有効なラベルを作成します。
   * タイトルから名前を作成するのに使用できます。

### ページマネージャー {#page-manager}

[ページマネージャー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html)は、[JCRUtil](#jcr-utilities) に基づいて、ページレベル操作用のメソッドを提供します。

### AEM UI の動作 {#ui-behavior}

コンテンツを管理する際の AEM UI の動作は次のとおりです。

* 次のいずれかの場合、ページマネージャーによって課せられる制約に従って名前が確認されます。
   * ノード名に変換されるようにページタイトルが提供されている。
   * 明示的なノード名が提供されている。
