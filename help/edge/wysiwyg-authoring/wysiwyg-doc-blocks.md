---
title: WYSIWYG とドキュメントベースのオーサリング用のブロック
description: WYSIWYG オーサリングとドキュメントベースのオーサリングの両方に使用できるブロックを作成する方法について説明します。
feature: Edge Delivery Services
role: User
exl-id: f039c70a-e1a0-4fcc-8f42-dfa0f8bb3764
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '235'
ht-degree: 100%

---

# WYSIWYG とドキュメントベースのオーサリング用のブロック {#wysiwyg-and-doc-blocks}

WYSIWYG オーサリングとドキュメントベースのオーサリングの両方に使用できるブロックを作成する方法について説明します。

## 概要 {#overview}

特定のプロジェクトでは、[ユニバーサルエディターを使用した WYSIWYG オーサリング](/help/edge/wysiwyg-authoring/authoring.md)と[ドキュメントベースのオーサリング](/help/edge/docs/authoring.md)の両方のサポートが必要になる場合があります。開発時間を最小限に抑え、サイトエクスペリエンスが同じになるよう、両方のユースケースをサポートするブロックのセットを 1 つ作成できます。

これを行うには、WYSIWYG オーサリング設定とドキュメントベースのオーサリング設定の両方に同じコンテンツモデリングアプローチを使用する必要があります。

## アプローチ {#approach}

AEM の WYSIWYG オーサリングでは、[モデルを宣言](/help/edge/wysiwyg-authoring/content-modeling.md)し、命名規則を指定します。次に、ドキュメントベースのオーサリングを使用して手動でテーブルを作成した場合と同じように、Edge Delivery を使用してデータがテーブルのようなブロック構造でレンダリングされます。

これを実現するために、ティーザーのようなシンプルなブロックの場合、すべてのプロパティとプロパティのグループが 1…n 行にそれぞれ 1 列ずつレンダリングされるといったように、特定の仮定を行います。1…n 個の項目を持つブロック（カルーセルやカードなど）の場合、項目はこれらの行の後に 1 行ずつ追加され、各プロパティ／プロパティグループごとに 1 列になります。

ドキュメントベースのオーサリングに同じアプローチを採用すると、WYSIWYG ブロックを再利用できます。
