---
title: カスタマイズの検出
description: カスタマイズの検出
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 7%

---


# カスタマイズの検出 {#cust-pattern}

このページでは、カスタマイズの検出パターンコードについて説明します。

## 背景 {#background}

このパターンコードは、AEMインスタンスに対して行われたカスタマイズを識別するために使用されます。 AEMのカスタマイズは一般的なので、このパターンが必ずしも問題を示しているわけではありません。 カスタマイズの記録を識別し、アップグレード計画への影響に関して評価できるようにします。

検出されるカスタマイズには次のものがあります。

* 顧客コード（パッケージ）と設定
* サードパーティパッケージ
* サードパーティのサービスとの統合
* 非標準Oakインデックス

## パターンデータ {#pattern-data}

パターンのJSON表現には、次のオブジェクトが含まれます。

* **item.message**: は、パターンのメッセージを指します。
* **item.context**: は、概要情報に関する追加情報を示します。
   * *type*: customization.detected.
   * *data*: カスタマイズを説明するデータを含むJSONオブジェクト

### 可能性のある影響およびリスク {#possible-implications}

適用なし.

### 可能な解決策  {#possible-solutions}

適用なし.
