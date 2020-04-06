---
title: AEMシステムの概要
description: AEMシステムの概要
translation-type: tm+mt
source-git-commit: aa6bb878ea4c58ba1e2fbf82d53effaa1a72d668

---


# AEMシステムの概要 {#aem-system}

このページでは、Adobe Experience Manager(AEM)のシステム概要について説明します。

## 背景 {#background}

このパターンは、AEMシステムの概要を提供する一般情報を識別するために使用されます。 次のような情報を含めることができます。

AEMバージョン使用するAEM製品（サイト、アセット、フォームなど）ノード数（ページ、アセットなど）

## パターンデータ {#pattern-data}

パターンのJSON表現には、次のオブジェクトが含まれます。

* **item.message**:は、パターンのメッセージを指します。
* **item.context**:は、概要情報に関する追加情報を示します。
   * *type*:コンテキストデータのタイプ(「aem.version」、「aem.product」、「node.count」)。
   * *data*:次のタイプに対応するデータを含むJSONオブジェクト。&quot;version&quot; （文字列）、&quot;product&quot; （文字列）または&quot;count&quot; （整数）。

### 可能性のある影響およびリスク {#possible-implications}

適用なし.

### 可能な解決策  {#possible-solutions}

適用なし.
