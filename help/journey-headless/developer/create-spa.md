---
title: オプション - Adobe Experience Manager（AEM）を使用して単一ページアプリケーション（SPA）を作成する方法
description: AEM ヘッドレス開発者ジャーニーの続編であるこのオプションパートでは、AEM でヘッドレス配信と従来のフルスタック CMS 機能を組み合わせる方法について説明します。また、AEM の SPA Editor フレームワークを使用して編集可能な SPA を作成する方法についても説明します。
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 100%

---

# AEM で単一ページアプリケーション（SPA）を作成する方法 {#create-spa}

[AEM ヘッドレス開発者ジャーニー](overview.md)のこのオプションの続きでは、AEM がヘッドレス配信と従来のフルスタック CMS 機能を組み合わせる方法について説明します。また、AEM SPA エディターフレームワークを使用して編集可能な SPA を作成し、外部 SPA を統合して、必要に応じて編集機能を有効にする方法についても説明します。

## これまでの説明内容 {#story-so-far}

ここまでで、[AEM ヘッドレスデベロッパージャーニー](overview.md)をすべて完了し、AEM におけるヘッドレス配信の基本（以下の内容）を理解できました。

* ヘッドレスコンテンツ配信とヘッドフルコンテンツ配信の違い
* AEM のヘッドレス機能
* AEM ヘッドレスプロジェクトを編成する方法
* AEM でヘッドレスコンテンツを作成する方法
* AEM でヘッドレスコンテンツを取得および更新する方法
* AEM ヘッドレスプロジェクトの運用を開始する方法

ここまでで、皆さんは初めての AEM ヘッドレスプロジェクトの運用を既に開始しているか、またはそのために必要な知識を習得しています。おめでとうございます。

それでは、ジャーニーの続編であるこのオプションパートになぜ取り組むのでしょうか。[はじめに](getting-started.md#integration-levels)のパートでは、AEM でヘッドレス配信と従来のフルスタックモデルだけでなく、両方の利点を組み合わせたハイブリッドモデルもサポートできることについて説明したことを思い出してください。従来のヘッドレスモデルでは不可能ですが、このようなハイブリッドモデルでは、特定のプロジェクトに対して、かつてないほどの柔軟性をもたらすことができます。

この記事では、AEM で編集可能な独自の単一ページアプリケーション（SPA）を作成する方法を詳しく説明することで、AEM ヘッドレスに関する知識をさらに強固なものにします。この方法では、コンテンツを作成して SPA にヘッドレスに配信できますが、その SPA は AEM で編集可能なままです。

## 目的 {#objective}

このドキュメントは、AEM SPA Editor フレームワークを使用して単一ページアプリケーションを開発する方法を理解するのに役立ちます。このドキュメントを読み終えると、次のことが可能になります。

* SPA エディターの基本的な機能を理解する。
* 完全に編集可能な AEM 対応 SPA を作成するための要件がわかる。
* 外部 SPA を AEM に統合する方法を理解する。
* サーバーサイドレンダリングがどのように実装できるか、または実装できないかを説明する。

## 要件と前提条件 {#requirements-prerequisites}

AEM で SPA の使用を開始するには、いくつかの要件があります。

### 知識 {#knowledge}

* React または Angular フレームワークを使用した SPA の開発経験
* AEM の基本的なスキル - コンテンツフラグメントの作成とエディターの使用
* 可能な SPA 統合の様々なレベルを理解するには、[AEM におけるヘッドフルとヘッドレス](/help/implementing/developing/headful-headless.md)のドキュメントを必ず確認してください。

### ツール {#tools}

* プロジェクトの導入をテストするためのサンドボックスへのアクセス
* ローカル開発モデリングとテスト用のデータインスタンス
* 既存の外部 SPA（オプション、選択した統合モデルによる）
* AEM プロジェクトアーキタイプ

## SPA について？ {#what-is-a-spa}

単一ページアプリケーション（SPA）は、クライアントサイドでレンダリングされ、主に JavaScript 主導であり、Ajax 呼び出しに依存してデータを読み込み、ページを動的に更新する点で、従来のページとは異なります。ほぼすべてのコンテンツは、1 回のページ読み込みで 1 回取得され、ユーザーによるページとのやり取りに基づいて、必要に応じて追加のリソースが非同期に読み込まれます。

この機能により、ページを更新する必要性が減り、シームレスで高速な、ネイティブアプリのエクスペリエンスに近いものをユーザーに提供できます。

AEM SPA エディターを使用すると、フロントエンド開発者は AEM のサイトに統合できる SPA を作成でき、コンテンツ作成者は SPA コンテンツを他の AEM コンテンツと同様に簡単に編集できます。

## SPA が注目される理由  {#why-spa}

SPA は、より速く、流動的で、ネイティブアプリケーションに近いものになることで、魅力的なエクスペリエンスになります。Web ページの訪問者だけでなく、SPA の仕組みが持つ性質により、マーケターや開発者にとっても有益です。

SPA とその使用理由について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## AEM での SPA の処理方法

AEM で単一ページアプリケーションを開発する場合、フロントエンド開発者は SPA を作成する際に標準的なベストプラクティスを順守するものと想定します。フロントエンド開発者は、次の一般的なベストプラクティスと AEM 固有の原則に従うと、SPA を AEM とそのコンテンツオーサリング機能で利用できるようになります。

* **移動可能** - その他のあらゆるコンポーネントと同様に、SPA コンポーネントは可能な限り移動可能な状態で構築する必要があります。SPA は、移動可能で再利用可能なコンポーネントを使用して構築する必要があります。
* **AEM を主軸にしたサイト構築** - フロントエンド開発者はコンポーネントを作成し、内部構造を所有しますが、AEM に依存してサイトのコンテンツ構造を定義します。
* **動的レンダリング** - すべてのレンダリングは動的である必要があります。
* **動的ルーティング** - SPA がルーティングを担当し、AEM がリッスンしてそれに基づいて取得します。どのルーティングも動的である必要があります。

AEM での SPA の処理方法について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## AEM SPA Editor {#aem-spa-editor}

React や Angular などの一般的なSPAフレームワークを使用して構築された Sites は、動的 JSON を使用してコンテンツを読み込みます。これらは、AEM ページエディターが編集コントロールを配置できるようにするために必要な HTML 構造を提供しません。

AEM 内で SPA の編集を有効にするには、SPA の JSON 出力と AEM リポジトリのコンテンツモデルとの間でマッピングを行い、変更をコンテンツに保存できるようにする必要があります。

AEM の SPA サポートでは、ページエディターに読み込まれたときにイベントを送信できる SPA JavaScript コードとやり取りするシン JavaScript レイヤーが導入されています。編集コントロールの場所をアクティベートして、コンテキスト内の編集を可能にすることができます。この機能は、コンテンツサービス API エンドポイントの概念に基づいて構築されています。SPA のコンテンツは、コンテンツサービスを使用して読み込む必要があるからです。

AEM SPA Editor について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## 既存の SPA への対応 {#existing-spas}

既存の SPA がある場合、それを AEM に埋め込んで AEM エディターでコンテンツ作成者に表示することができます。この機能は、コンテンツフラグメントを使用して作成したコンテンツを、そのコンテンツが消費される最終アプリケーションのコンテキストで表示する場合に非常に役立ちます。

さらに、わずかな変更だけで、AEM エディター内の外部 SPA に対して特定の編集機能を有効にできます。

RemotePage コンポーネントを使用すると、AEM で外部 SPA をレンダリングできます。

外部 SPA を AEM で編集可能にする方法について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## 次の手順 {#what-is-next}

独自の AEM 対応 SPA の開発に取りかかるには、次のドキュメントを確認してください。

* [SPA WKND チュートリアル](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [React の使用を開始する](/help/implementing/developing/hybrid/getting-started-react.md)
* [Angular の使用を開始する](/help/implementing/developing/hybrid/getting-started-angular.md)

既存の SPA を AEM で使用するように適応させる必要がある場合は、次のドキュメントを確認してください。

* [RemotePage コンポーネント](/help/implementing/developing/hybrid/remote-page.md)
* [AEM 内での外部 SPA の編集](/help/implementing/developing/hybrid/editing-external-spa.md)

AEM の SPA トピックをさらに詳しく解説する[その他のリソース](#additional-resources)については、以下を参照してください。

## その他のリソース {#additional-resources}

以下の追加リソースでは、このドキュメントで言及したいくつかの概念について詳しく説明しています。

* [AEM におけるヘッドフルとヘッドレス](/help/implementing/developing/headful-headless.md) - AEM で使用可能な様々な配信モデルの説明
* [SPA の概要およびガイド](/help/implementing/developing/hybrid/introduction.md) - AEM での SPA の優れた入門ガイド。
* [AEM 向け SPA の開発](/help/implementing/developing/hybrid/developing.md) - AEM 対応 SPA の開発方法に関するガイドライン
* [SPA エディターの概要](/help/implementing/developing/hybrid/editor-overview.md) - SPA エディターの仕組みの説明
* [SPA リファレンスドキュメント](/help/implementing/developing/hybrid/reference-materials.md) - JavaScript API リファレンスと、オープンソースの AEM SPA GitHub プロジェクトへのリンク
* [コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments) - コンテンツフラグメントの作成方法
* [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) - Web サイトの出発点として、ベストプラクティスに基づいた最小限の Adobe Experience Manager（AEM）プロジェクトを作成する Maven テンプレート
