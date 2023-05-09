---
title: ContextHub
description: ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 73%

---

# ContextHub {#contexthub}

ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。主な機能は、[様々なペルソナをシミュレートおよび切り替えながら、コンテキストデータを表示する機能を提供する](/help/sites-cloud/authoring/personalization/contexthub.md)ことです。

ContextHub では、次のことができます。

* コンテキストデータを使用してページを作成する際に、[プレゼンテーション、表示、ペルソナの切り替え、ユーザーエクスペリエンスのシミュレーション](#presentation)を行います。
* データレイヤー表現として Web サイト上の[コンテキストデータを保持](#persistence)します。
* 選択したコンテキストの[セグメントを管理](#segmentation)します。

クライアントサイド JavaScript API を使用してデータにアクセスし、コンテンツをパーソナライズします。

## プレゼンテーション {#presentation}

マーケティング担当者と作成者は、[ContextHub ツールバー](/help/sites-cloud/authoring/personalization/contexthub.md)を使用してストアデータを表示および操作し、ページのオーサリング時にユーザーエクスペリエンスをシミュレートできます。ツールバーは、[ContextHub ストア](#persistence)へのアクセスを提供する UI モジュールのグループで構成されます。 これは、クライアント上で ContextHub データを保持します。

各 ContextHub UI モジュールは、事前定義されたモジュールタイプのインスタンスです。

* ContextHub には、次の機能が用意されています。 [サンプルモジュールタイプ](sample-modules.md).
* AEMコンソールを使用して [UI モジュールの追加](configuring-contexthub.md#adding-a-ui-module)、および [UI モードでグループ化](configuring-contexthub.md#adding-a-ui-mode).
* 開発者が実行できる操作 [カスタムモジュールタイプの作成](extending-contexthub.md#creating-contexthub-ui-module-types).

開発者は、 [ページに ContextHub コンポーネントを追加する](configuring-contexthub.md).

## 永続性 {#persistence}

ContextHub ストアは、コンテキストデータをクライアント上に保持します。ContextHub JavaScript API を使用してストアにアクセスし、必要に応じてデータを作成、更新および削除できます。したがって、ContextHub はページ上のデータレイヤーに相当します。

個々の ContextHub ストアは、事前定義されたストアタイプのインスタンスです。

* ContextHub には、次の機能が用意されています。 [サンプルストアタイプ](sample-stores.md).
* AEMコンソールを使用して [ストアを作成](configuring-contexthub.md#creating-a-contexthub-store).
* デベロッパーは、[カスタムストアタイプを作成](extending-contexthub.md#creating-custom-store-candidates)できます。
* 開発者が実行できる操作 [ストアデータにアクセス](adding-contexthub.md#interacting-with-contexthub-stores) JavaScript を使用。

## セグメント化 {#segmentation}

ContextHub には、セグメントを管理し、現在のコンテキストに対して解決されるセグメントを決定するセグメント化エンジンが含まれています。 複数のセグメントが定義されています。 JavaScript API を使用して、[解決されたセグメントを判断](adding-contexthub.md#determining-resolved-contexthub-segments)できます。
