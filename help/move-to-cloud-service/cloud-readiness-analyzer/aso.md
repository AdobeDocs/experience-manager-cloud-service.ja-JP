---
title: AEMシステムの概要
description: AEMシステムの概要
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 8%

---


# AEMシステムの概要 {#aem-system}

このページでは、Adobe Experience Manager(AEM)のシステム概要について説明します。

## 背景 {#background}

このパターンは、AEMシステムの概要を提供する一般的な情報を識別するために使用されます。 情報には、次のような項目が含まれます。

AEMバージョン使用するAEM製品（サイト、アセット、フォームなど）ノード数（ページ、アセットなど）

## パターンデータ {#pattern-data}

パターンのJSON表現には、次のオブジェクトが含まれます。

* **item.message**: は、パターンのメッセージを指します。
* **item.context**: は、概要情報に関する追加情報を示します。
   * *type*: コンテキストデータのタイプ(「aem.version」、「aem.product」、「node.count」)。
   * *data*: 次のタイプに対応するデータを含むJSONオブジェクト。 &quot;version&quot; (string)、&quot;product&quot; (string)または&quot;count&quot; (integer)。

### 可能性のある影響およびリスク {#possible-implications}

適用なし.

### 可能な解決策  {#possible-solutions}

適用なし.
