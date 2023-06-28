---
title: オプション — Adobe Experience Manager(AEM) を使用したシングルページアプリケーション (SPA) の作成方法
description: AEM ヘッドレスデベロッパージャーニーの続編であるこのオプションパートでは、AEM でヘッドレス配信と従来のフルスタック CMS 機能を組み合わせる方法について説明します。また、AEM の SPA Editor フレームワークを使用して編集可能な SPA を作成する方法についても説明します。
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 48%

---

# AEM で単一ページアプリケーション（SPA）を作成する方法 {#create-spa}

このオプションの継続では、 [AEMヘッドレス開発者ジャーニー](overview.md)では、AEMがヘッドレス配信を従来のフルスタック CMS 機能と組み合わせる方法を学びます。 また、AEM SPA Editor Framework を使用して編集可能なSPAを作成し、外部SPAを統合して、必要に応じて編集機能を有効にする方法についても説明します。

## これまでの説明内容 {#story-so-far}

ここまでで、[AEM ヘッドレスデベロッパージャーニー](overview.md)をすべて完了し、AEM におけるヘッドレス配信の基本（以下の内容）を理解できました。

* ヘッドレスコンテンツ配信とヘッドフルコンテンツ配信の違い
* AEM のヘッドレス機能
* AEM ヘッドレスプロジェクトを編成する方法
* AEM でヘッドレスコンテンツを作成する方法
* AEM でヘッドレスコンテンツを取得および更新する方法
* AEM ヘッドレスプロジェクトの運用を開始する方法

これまでは、最初のAEMヘッドレスプロジェクトを利用した運用を開始したか、またはその必要な知識を持っています。 おめでとうございます。

ではなぜこの旅の続きを読み取るのでしょう？ これは [はじめに](getting-started.md#integration-levels)AEMがヘッドレス配信と従来のフルスタックモデルをサポートするだけでなく、両方の利点を組み合わせたハイブリッドモデルをサポートする方法について説明しました。 従来のヘッドレスモデルでは不可能ですが、このようなハイブリッドモデルでは、特定のプロジェクトに対して、かつてないほどの柔軟性をもたらすことができます。

この記事は、AEMで編集可能な独自のシングルページアプリケーション (SPA) を作成する方法を詳しく調べ、AEMヘッドレスに関するお客様の知識に基づいて構築されます。 この方法では、コンテンツを作成してヘッドレスにSPAに配信できますが、SPAはAEMで編集可能なままです。

## 目的 {#objective}

このドキュメントは、AEM SPA Editor フレームワークを使用して単一ページアプリケーションを開発する方法を理解するのに役立ちます。このドキュメントを読み終えると、次をできるようになります。

* SPA エディターの基本的な機能を理解する。
* 完全に編集可能な AEM 対応 SPA を作成するための要件がわかる。
* 外部 SPA を AEM に統合する方法を理解する。
* サーバーサイドレンダリングを実装する方法を説明します。

## 要件と前提条件 {#requirements-prerequisites}

AEMでSPAの使用を開始する前に、いくつかの要件があります。

### 知識 {#knowledge}

* React または Angular フレームワークを使用した SPA の開発経験
* AEM の基本的なスキル - コンテンツフラグメントの作成とエディターの使用
* ドキュメントを必ず確認してください [AEMのヘッドフルとヘッドレス](/help/implementing/developing/headful-headless.md) そのため、様々なレベルのSPA統合を理解できます。

### ツール {#tools}

* プロジェクトの導入をテストするためのサンドボックスへのアクセス
* ローカル開発モデリングとテスト用のデータインスタンス
* 既存の外部 SPA（オプション、選択した統合モデルによる）
* AEM プロジェクトアーキタイプ

## SPA について  {#what-is-a-spa}

単一ページアプリケーション (SPA) は、クライアントサイドでレンダリングされ、主に JavaScript 主導で、Ajax 呼び出しに依存してデータを読み込み、ページを動的に更新する点で、従来のページとは異なります。 ほとんどの場合、またはすべての場合、コンテンツは、単一のページ読み込みで 1 回取得され、ユーザーによるページとのやり取りに基づいて、必要に応じて追加のリソースが非同期で読み込まれます。

この機能により、ページを更新する必要が減り、シームレスで高速な、ネイティブアプリのエクスペリエンスに近いエクスペリエンスをユーザーに提供できます。

AEM SPA エディターを使用すると、フロントエンド開発者は AEM のサイトに統合できる SPA を作成でき、コンテンツ作成者は SPA コンテンツを他の AEM コンテンツと同様に簡単に編集できます。

## SPA が注目される理由  {#why-spa}

より速く、流動的で、よりネイティブアプリケーションのようになることで、SPAは魅力的なエクスペリエンスになります。 Web ページの訪問者だけでなく、SPAの仕組みの性質上、マーケターや開発者にも役立ちます。

SPA とその使用理由について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## AEM での SPA の処理方法

AEM で単一ページアプリケーションを開発する場合、フロントエンド開発者は SPA を作成する際に標準的なベストプラクティスを順守するものと想定します。フロントエンド開発者は、次の一般的なベストプラクティスとAEM固有の原則に従うと、SPAとAEMおよびコンテンツオーサリング機能を利用できるようになります。

* **移動可能** - その他のあらゆるコンポーネントと同様に、SPA コンポーネントは可能な限り移動可能な状態で構築する必要があります。SPA は、移動可能で再利用可能なコンポーネントを使用して構築する必要があります。
* **AEM Drives サイト構造**  — フロントエンド開発者はコンポーネントを作成し、内部構造を所有しますが、AEMを利用してサイトのコンテンツ構造を定義します。
* **動的レンダリング** - すべてのレンダリングは動的である必要があります。
* **動的ルーティング** - SPA がルーティングを担当し、AEM がリッスンしてそれに基づいて取得します。どのルーティングも動的である必要があります。

AEM での SPA の処理方法について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## AEM SPA Editor {#aem-spa-editor}

React やAngularなどの一般的なSPAフレームワークを使用して構築されたサイトは、動的 JSON を使用してコンテンツを読み込みます。 AEMページエディターで編集コントロールをHTMLするために必要な編集構造は提供されていません。

AEM内でSPAの編集を有効にするには、SPAの JSON 出力とAEMリポジトリ内のコンテンツモデルとの間のマッピングが必要です。そのため、コンテンツに対する変更を保存できます。

AEMでのSPAのサポートでは、イベントを送信できるページエディターに読み込む際にSPA JavaScript コードとやり取りする、シンな JavaScript レイヤーが導入されます。 編集コントロールの場所を有効にして、コンテキスト内編集を許可することができます。 この機能は、SPAのコンテンツを Content Services を使用して読み込む必要があるので、Content Services API エンドポイントの概念に基づいて構築されます。

AEM SPA Editor について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## 既存の SPA への対応 {#existing-spas}

既存のSPAがある場合、AEMではAEMへの埋め込みがサポートされているので、AEMエディターでコンテンツ作成者に表示できます。 この機能は、コンテンツが消費されるエンドアプリケーションのコンテキストで、コンテンツフラグメントを介して作成するコンテンツを表示する場合に役立ちます。

また、AEM Editor 内で、特定の編集機能を外部SPAに対して有効にすることもできます。

RemotePage コンポーネントを使用すると、AEM で外部 SPA をレンダリングできます。

外部 SPA を AEM で編集可能にする方法について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## 次の手順 {#what-is-next}

独自の AEM 対応 SPA の開発に取りかかるには、次のドキュメントを確認してください。

* [SPA WKND チュートリアル](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [React の使用を開始する](/help/implementing/developing/hybrid/getting-started-react.md)
* [Angular の使用を開始する](/help/implementing/developing/hybrid/getting-started-angular.md)

既存のSPAをAEMで使用するように適応させる必要がある場合は、次のドキュメントを確認します。

* [RemotePage コンポーネント](/help/implementing/developing/hybrid/remote-page.md)
* [AEM 内での外部 SPA の編集](/help/implementing/developing/hybrid/editing-external-spa.md)

AEM の SPA トピックをさらに詳しく解説する[その他のリソース](#additional-resources)については、以下を参照してください。

## その他のリソース {#additional-resources}

以下の追加リソースでは、このドキュメントで言及したいくつかの概念について詳しく説明しています。

* [AEM におけるヘッドフルとヘッドレス](/help/implementing/developing/headful-headless.md) - AEM で使用可能な様々な配信モデルの説明
* [SPAの概要およびガイド](/help/implementing/developing/hybrid/introduction.md) - AEMでのSPAの良い紹介。
* [AEM 向け SPA の開発](/help/implementing/developing/hybrid/developing.md) - AEM 対応 SPA の開発方法に関するガイドライン
* [SPA エディターの概要](/help/implementing/developing/hybrid/editor-overview.md) - SPA エディターの仕組みの説明
* [サーバーサイドレンダリング](/help/implementing/developing/hybrid/ssr.md) - SSR をAEM SPA用に設定する方法
* [SPA Reference Documents](/help/implementing/developing/hybrid/reference-materials.md)  — オープンソースのAEM SPA GitHub プロジェクトへの JavaScript API リファレンスとリンク
* [コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/content-fragments.md) - コンテンツフラグメントの作成方法
* [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) - Web サイトの出発点として、ベストプラクティスに基づいた最小限の Adobe Experience Manager（AEM）プロジェクトを作成する Maven テンプレート
