---
title: 命名規則
description: リポジトリのノードは、Java コンテンツリポジトリーの命名規則の対象です
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 61%

---

# 命名規則{#naming-conventions}

リポジトリのノードは、Java コンテンツリポジトリーの命名規則の対象です。ただし、AEM によってページノード名に追加の規則が課せられます。

## ページの命名規則 {#naming-conventions-for-pages}

これらの命名規則は、以下のような様々なレベルで実装されます。

* JcrUtil:のAEM実装 [JCR ユーティリティ](#jcr-utilities).
* ページマネージャー：[ページマネージャー](#page-manager)は、ページレベルの操作用のメソッドを提供します。
* AEM UI 内 {#ui-behavior}

### JCR ユーティリティ {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) は、JCR ユーティリティのAEM実装です。 名前の検証に特に関心があるのは、文字マッピングを制御し、次の検証を行う点です。

* `isValidName`
   * 名前が空でなく、有効な文字のみを含んでいるかどうかをチェックします。
   * 提案された名前が有効かどうかを確認するために使用できます。
* `createValidName`
   * 任意の文字列から有効なラベルを作成します。
   * タイトルから名前を作成するのに使用できます。

### ページマネージャー {#page-manager}

[ページマネージャー](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html)は、[JCRUtil](#jcr-utilities) に基づいて、ページレベル操作用のメソッドを提供します。

### AEM UI の動作 {#ui-behavior}

コンテンツを管理する際の AEM UI の動作は次のとおりです。

* 次のいずれかの場合に、PageManager が課した制限に従って名前を検証します。
   * ノード名に変換するために、ページタイトルが指定されます。
   * 明示的なノード名が提供されています
