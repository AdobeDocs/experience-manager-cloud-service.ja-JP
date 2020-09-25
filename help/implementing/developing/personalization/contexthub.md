---
title: ContextHub
description: ContextHubは、コンテキストデータの保存、操作、表示のためのフレームワークです
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 57%

---


# ContextHub {#contexthub}

ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。主な機能は、様々なパーソナルをシミュレートおよび切り替えながら、コンテキストデータを [表示する機能を提供することです。](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHubでは、次のことができます。

* [コンテキストデータを使用してページを作成する際に、プレゼンテーション、表示、切り替えの個人](#presentation) 、ユーザーエクスペリエンスのシミュレートを行います。
* [Webサイト上のコンテキストデータ](#persistence) をデータレイヤー表現として保持します。
* [選択したコンテキストのセグメント](#segmentation) を管理します。

クライアント側のJavaScript APIを使用すると、コンテンツのパーソナライズ用にデータにアクセスできます。

## プレゼンテーション {#presentation}

マーケティング担当者と作成者は、[ContextHub ツールバー](/help/sites-cloud/authoring/personalization/contexthub.md)を使用してストアデータを表示および操作し、ページのオーサリング時にユーザーエクスペリエンスをシミュレートできます。ツールバーは、ContextHubストアへのアクセスを提供するUIモジュールのグループで構成されます。 [このグループは](#persistence) 、クライアント上でContextHubデータを保持します。

各 ContextHub UI モジュールは、事前定義されたモジュールタイプのインスタンスです。

* ContextHub には、いくつかの[モジュールタイプのサンプル](sample-modules.md)が用意されています。
* AEM コンソールを使用して [UI モジュールを追加](configuring-contexthub.md#adding-a-ui-module)し、[UI モードにグループ化](configuring-contexthub.md#adding-a-ui-mode)します。
* 開発者は、[カスタムモジュールタイプを作成](extending-contexthub.md#creating-contexthub-ui-module-types)できます。

開発者は、[ContextHub コンポーネントをページに追加](configuring-contexthub.md)する必要があります。

## 永続性 {#persistence}

ContextHub ストアは、コンテキストデータをクライアント上に保持します。ContextHub Javascript APIを使用すると、ストアにアクセスし、必要に応じてデータを作成、更新、削除できます。 したがって、ContextHub はページ上のデータレイヤーに相当します。

個々の ContextHub ストアは、事前定義されたストアタイプのインスタンスです。

* ContextHub には、いくつかの[ストアタイプのサンプル](sample-stores.md)が用意されています。
* AEM コンソールを使用して[ストアを作成](configuring-contexthub.md#creating-a-contexthub-store)します。
* Developers can [create custom store types](extending-contexthub.md#creating-custom-store-candidates).
* 開発者は、JavaScript を使用して[ストアデータにアクセス](adding-contexthub.md#interacting-with-contexthub-stores)できます。

## セグメント化 {#segmentation}

ContextHub には、セグメントの管理や、現在のコンテキストで解決されるセグメントの判断をするセグメント化エンジンが含まれています。いくつかのセグメントが定義されています。JavaScript API を使用して、[解決されたセグメントを判断](adding-contexthub.md#determining-resolved-contexthub-segments)できます。
