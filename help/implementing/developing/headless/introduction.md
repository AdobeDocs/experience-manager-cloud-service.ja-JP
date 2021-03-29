---
title: AEM Sites as a Cloud Service 向けヘッドレス開発
description: コンテンツモデル、コンテンツフラグメント、GraphQL APIなど、Cloud Serviceの強力なヘッドレス機能としてAEMがどのように連携し、エクスペリエンスを一元的に管理し、チャネル全体で提供できるかを学びます。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 88%

---


# AEM Sites as a Cloud Service 向けヘッドレス開発 {#headless-development}

コンテンツモデル、コンテンツフラグメント、GraphQL APIなど、Cloud Serviceの強力なヘッドレス機能としてAEMがどのように連携し、エクスペリエンスを一元的に管理し、チャネル全体で提供できるかを学びます。

## 概要 {#overview}

ヘッドレス実装は、オーディエンスの場所やチャネルに関係なく、オーディエンスにエクスペリエンスを提供する上で、ますます重要になってきています。

ヘッドレス実装は、フルスタックおよびハイブリッドソリューションにおける従来のようなページおよびコンポーネント管理ではなく、チャネルに依存しない再利用可能なコンテンツフラグメントの作成とそのクロスチャネル配信に重点を置いています。これは、Web エクスペリエンスを実装するための最新の動的な開発パターンです。

![AEM 実装モデル](assets/aem-implementation-models.png)

## ヘッドフルとヘッドレスの比較 {#headful-headless}

このドキュメントでは、AEM の完全なヘッドレス実装モデルを重点的に説明します。ただし、AEM でヘッドフルとヘッドレスは二者択一である必要はありません。ヘッドレス機能を使用すると、コンテンツを管理し様々なエンドポイントに配信できると同時に、コンテンツ作成者が単一ページアプリケーションを編集できるようになります。すべてが AEM にあります。

>[!TIP]
>
>詳しくは、[AEM におけるヘッドフルとヘッドレス](/help/implementing/developing/headful-headless.md)を参照してください。

## AEM as a Cloud Service とヘッドレス {#aem-headless}

AEM as a Cloud Service は、次の 3 つの強力なサービスを提供することで、ヘッドレス実装モデルの柔軟なツールになっています。

1. コンテンツモデル
   * コンテンツモデルはコンテンツの構造化表現です。
   * これらは、情報アーキテクトが AEM コンテンツフラグメントモデルエディターで定義します。
   * コンテンツモデルはコンテンツフラグメントの基盤となります。
1. コンテンツフラグメント
   * コンテンツフラグメントは、コンテンツモデルをインスタンス化したものです。
   * これらは、コンテンツ作成者が AEM コンテンツフラグメントエディターで作成します。
   * 作成後は AEM Assets に保存され、AEM Assets 管理 UI で管理されます。
1. 配信用のコンテンツ API
   * AEM GraphQL API では、コンテンツフラグメント配信をサポートしています。
   * AEM Assets REST API では、コンテンツフラグメントの CRUD 操作をサポートしています。
   * [コンテンツフラグメントコアコンポーネントの JSON エクスポート](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/components/content-fragment-component.html)を使用すると、直接コンテンツ配信も可能です。

## ヘッドレス入門ガイド {#getting-started}

ヘッドレス入門ガイドでは、AEM as a Cloud Service を使用したエクスペリエンスの作成、管理、配信の簡単な道筋を 5 つの手順に分けて示します。各ガイドは前のガイドに基づいているので、じっくり順番に検討することをお勧めします。

1. [設定の作成](getting-started/create-configuration.md)
1. [コンテンツフラグメントモデルの作成](getting-started/create-content-model.md)
1. [アセットフォルダーの作成](getting-started/create-assets-folder.md)
1. [コンテンツフラグメントの作成](getting-started/create-content-fragment.md)
1. [コンテンツフラグメントへのアクセスと配信](getting-started/create-api-request.md)

## 対象者 {#audience}

[ヘッドレス入門ガイド](#getting-started)で説明されているタスクは、AEM のヘッドレス機能の基本的な包括的デモに必要です。テスト用 AEM インスタンスへの管理者アクセス権を持つユーザーは誰でも、これらのガイドに従って AEM でのヘッドレスな配信を理解できますが、開発者の経験を持つユーザーが最適です。

ただし、実稼働状況では、これらのタスクは様々なペルソナによって実行され、実行回数も様々です。次に例を示します。

* **管理者**：コンテンツの初期設定とフォルダー構造を、通常は 1 回のみまたは散発的にセットアップする必要があります。
* **情報アーキテクト**：通常、組織のニーズの変化に応じて新しいモデルを追加します。
* **コンテンツ作成者**：アーキテクトが定義したモデルに基づいて、新しいコンテンツをコンテンツフラグメントとして継続的に作成します。

このヘッドレス入門ガイドでは、上記のタスクを一般に誰がどのような頻度で実行するかを説明します。

## 次のステップ {#next-step}

詳細に入る準備ができましたか？それでは、まず、ヘッドレス入門ガイドの第 1 部[設定の作成](getting-started/create-configuration.md)に目を通しましょう。
