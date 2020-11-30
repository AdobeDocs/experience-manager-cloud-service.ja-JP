---
title: ContextHub
description: ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 100%

---


# ContextHub {#contexthub}

ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。主な機能は、[様々なペルソナをシミュレートおよび切り替えながら、コンテキストデータを表示する機能を提供する](/help/sites-cloud/authoring/personalization/contexthub.md)ことです。

ContextHub では、次のことができます。

* コンテキストデータを使用してページを作成する際に、[プレゼンテーション、表示、ペルソナの切り替え、ユーザーエクスペリエンスのシミュレーション](#presentation)をおこないます。
* データレイヤー表現として Web サイト上の[コンテキストデータを保持](#persistence)します。
* 選択したコンテキストの[セグメントを管理](#segmentation)します。

クライアントサイド JavaScript API を使用してデータにアクセスし、コンテンツをパーソナライズします。

## プレゼンテーション {#presentation}

マーケティング担当者と作成者は、[ContextHub ツールバー](/help/sites-cloud/authoring/personalization/contexthub.md)を使用してストアデータを表示および操作し、ページのオーサリング時にユーザーエクスペリエンスをシミュレートできます。ツールバーは、[ContextHub ストア](#persistence)へのアクセスを提供する UI モジュールのグループで構成されます。 これは、クライアント上で ContextHub データを保持します。

各 ContextHub UI モジュールは、事前定義されたモジュールタイプのインスタンスです。

* ContextHub には、いくつかの[モジュールタイプのサンプル](sample-modules.md)が用意されています。
* AEM コンソールを使用して [UI モジュールを追加](configuring-contexthub.md#adding-a-ui-module)し、[UI モードにグループ化](configuring-contexthub.md#adding-a-ui-mode)します。
* 開発者は、[カスタムモジュールタイプを作成](extending-contexthub.md#creating-contexthub-ui-module-types)できます。

開発者は、[ContextHub コンポーネントをページに追加](configuring-contexthub.md)する必要があります。

## 永続性 {#persistence}

ContextHub ストアは、コンテキストデータをクライアント上に保持します。ContextHub JavaScript API を使用してストアにアクセスし、必要に応じてデータを作成、更新および削除できます。したがって、ContextHub はページ上のデータレイヤーに相当します。

個々の ContextHub ストアは、事前定義されたストアタイプのインスタンスです。

* ContextHub には、いくつかの[ストアタイプのサンプル](sample-stores.md)が用意されています。
* AEM コンソールを使用して[ストアを作成](configuring-contexthub.md#creating-a-contexthub-store)します。
* デベロッパーは、[カスタムストアタイプを作成](extending-contexthub.md#creating-custom-store-candidates)できます。
* 開発者は、JavaScript を使用して[ストアデータにアクセス](adding-contexthub.md#interacting-with-contexthub-stores)できます。

## セグメント化 {#segmentation}

ContextHub には、セグメントの管理や、現在のコンテキストで解決されるセグメントの判断をするセグメント化エンジンが含まれています。いくつかのセグメントが定義されています。JavaScript API を使用して、[解決されたセグメントを判断](adding-contexthub.md#determining-resolved-contexthub-segments)できます。
