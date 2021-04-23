---
title: オプション — AEMを使用した単一ページアプリ(SPA)の作成方法
description: AEMヘッドレス開発者ジャーニーのこのオプションの継続では、AEMで従来のフルスタックCMS機能とヘッドレス配信を組み合わせる方法と、AEM SPA Editorフレームワークを使用して編集可能なSPAを作成する方法を学びます。
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 1b6dbf401ff921964537f6c79d12544789e93c92
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 34%

---


# AEM {#create-spa}を使用したシングルページアプリ(SPA)の作成方法

>[!CAUTION]
>
>作業中 — このドキュメントの作成は現在進行中で、完全なもの、最終的なもの、または実稼働目的で使用するものとして理解してはなりません。

この[AEM Headless Developerジャーニーのオプションの続きでは、AEMが従来のフルスタックCMS機能とヘッドレス配信を組み合わせる方法、AEM Editor frameworkを使用して編集可能なSPAを作成する方法、外部SPAを使用し、必要に応じて編集機能を実現します。](overview.md)

## {#story-so-far}

この時点で、[AEM Headless Developerジャーニー](overview.md)の全体を完成させ、AEMのヘッドレス配信の基本を理解し、以下の事項を理解する必要があります。

* ヘッドレスコンテンツとヘッドフルコンテンツの配信の違い。
* AEMヘッドレス機能
* ヘッドレスプロジェクトの編成とAEM化の方法。
* AEMでヘッドレスコンテンツを作成する方法。
* AEMでヘッドレスコンテンツを取得して更新する方法。
* AEM Headlessプロジェクトとの連携方法。

これで、最初のAEMヘッドレスプロジェクトを使用するか、そのために必要な知識をすべて手に入れるかのどちらかです。 バリデーターが

なぜジャーニーの続きを読むのでしょう？ 「[はじめに](getting-started.md#integration-levels)」で、AEMがヘッドレス配信と従来のフルスタックモデルをサポートするだけでなく、両方の利点を組み合わせたハイブリッドモデルをサポートする方法について簡単に説明したことを思い出してください。 従来のヘッドレスモデルではありませんが、このようなハイブリッドモデルは、特定のプロジェクトに対して前例のない柔軟性をオファーできます。

この記事は、AEMで実際に編集可能な独自のシングルページアプリ(SPA)を作成する方法について詳しく調べることで、AEMヘッドレスの知識を基に作成されます。 このようにして、コンテンツを作成し、SPAに対して無理に配信できますが、SPAはAEMで編集可能なままです。

## 目的 {#objective}

このドキュメントは、AEM SPA Editorフレームワークを使用してシングルページアプリが開発される方法を理解するのに役立ちます。 このドキュメントを読んだ後は、次の操作を行う必要があります。

* SPAエディタの基本的な機能について説明します。
* AEM用に完全に編集可能なSPAを構築するための要件を理解しておく必要があります。
* 外部SPAをAEMに統合する方法を理解します。
* サーバー側のレンダリングを実装する必要があるか、実装しないかを理解します。

## 要件と前提条件{#requirements-prerequisites}

AEMでSPAを使用する前に、いくつかの要件があります。

### 知識{#knowledge}

* ReactまたはAngularフレームワークを使用したSPAの開発エクスペリエンスの作成
* AEMの基本的なスキルでコンテンツフラグメントを作成し、エディターを使用する
* 可能なSPA統合の様々なレベルを理解するために、必ずAEM](/help/implementing/developing/headful-headless.md)のドキュメント[ヘッドフルとヘッドレスを確認してください。

### ツール {#tools}

* プロジェクトの展開をテストするためのSandboxへのアクセス
* データのモデリングとテストのローカル開発インスタンス
* 既存の外部SPA（選択する統合モデルに応じたオプション）
* AEM プロジェクトアーキタイプ

## SPA について {#what-is-a-spa}

単一ページアプリケーション（SPA）は、クライアントサイドでレンダリングされ、主に JavaScript 主導であり、Ajax 呼び出しに依存してデータを読み込み、ページを動的に更新する点で、従来のページとは異なります。ほぼすべてのコンテンツは、1 回のページ読み込みで 1 回取得され、ユーザーによるページとのやり取りに基づいて、必要に応じて追加のリソースが非同期に読み込まれます。

これにより、ページを更新する必要が減り、シームレスで高速な、ネイティブアプリのエクスペリエンスに近いものををユーザーに提供できます。

AEM SPA エディターを使用すると、フロントエンド開発者は AEM のサイトに統合できる SPA を作成でき、コンテンツ作成者は SPA コンテンツを他の AEM コンテンツと同様に簡単に編集できます。

## SPA が注目される理由 {#why-spa}

より速く、流動的で、よりネイティブアプリケーションに近い SPA は、Web ページの訪問者だけでなく、SPA の仕組みの性質上、マーケターや開発者にとっても非常に魅力的なエクスペリエンスとなります。

SPAの詳細な説明と使用理由については、[追加のリソース](#additional-resources)を参照してください。

## AEMでのSPAの処理方法

AEM で単一ページアプリケーションを開発する場合、フロントエンド開発者は SPA を作成する際に標準的なベストプラクティスを順守するものと想定します。次の一般的なベストプラクティスには AEM 固有の原則はほぼなく、フロントエンド開発者がそれに従うことで、SPA は AEM とコンテンツオーサリング機能と共に機能します。

* **移植性**  — 任意のコンポーネントと同様に、SPAコンポーネントは可能な限り持ち運び可能な状態で構築する必要があります。SPA は、移動可能で再利用可能なコンポーネントを使用して構築する必要があります。
* **AEM を主軸にしたサイト構築** - フロントエンド開発者はコンポーネントを作成し、内部構造を所有しますが、AEM に依存してサイトのコンテンツ構造を定義します。
* **動的レンダリング** - すべてのレンダリングは動的である必要があります。
* **動的ルーティング** - SPA がルーティングを担当し、AEM がリッスンしてそれに基づいて取得します。どのルーティングも動的である必要があります。

AEMでのSPAの処理方法の詳細については、[追加のリソース](#additional-resources)を参照して、詳細なドキュメントへのリンクを参照してください。

## AEM SPAエディタ{#aem-spa-editor}

React や Angular などの一般的な SPA フレームワークを使用して構築したサイトは、Dynamic JSON を使用してコンテンツを読み込みます。サイトには、AEM ページエディターが編集コントロールを配置するために必要な HTML 構造がありません。

AEM 内で SPA の編集を有効にするには、SPA の JSON 出力と AEM リポジトリのコンテンツモデルとの間でマッピングをおこない、変更をコンテンツに保存できるようにする必要があります。

AEM の SPA サポートにより、シン JS レイヤーが導入されました。このレイヤーは、ページエディターに読み込まれると、SPA の JS コードとやり取りします。これにより、イベントを送信したり、編集コントロールの場所をアクティブにしてコンテキスト内で編集したりできます。この機能は、コンテンツサービス API エンドポイントの概念に基づいて構築されています。SPA のコンテンツは、コンテンツサービスを使用して読み込む必要があるからです。

AEM SPAエディタの詳細な説明については、[追加のリソース](#additional-resources)の節を参照してください。

## 既存のSPAに対応{#existing-spas}

既存のSPAがある場合、AEMではAEMへの埋め込みがサポートされているので、AEMエディターでコンテンツ作成者に対して表示されます。 これは、コンテンツフラグメントを介して作成するコンテンツを、そのコンテンツが使用されるエンドアプリケーションのコンテキストで表示する場合に非常に役立ちます。

さらに、わずかな変更のみで、AEMエディタ内の外部SPAに対して特定の編集機能を有効にすることができます。

RemotePageコンポーネントを使用すると、AEMで外部SPAをレンダリングできます。

AEMで外部SPAを編集可能にする方法の詳細については、[追加のリソース](#additional-resources)を参照して、詳細なドキュメントへのリンクを参照してください。

## 次の作業{#what-is-next}

独自のAEM向けSPAの開発を開始するには、次のドキュメントを確認します。

* [SPA WKND チュートリアル](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Reactを使用する前に](/help/implementing/developing/hybrid/getting-started-react.md)
* [angular使用の手引き](/help/implementing/developing/hybrid/getting-started-angular.md)

既存のSPAをAEMで使用するために適応させる必要がある場合は、次のドキュメントを確認します。

* [RemotePage コンポーネント](/help/implementing/developing/hybrid/remote-page.md)
* [AEM 内での外部 SPA の編集](/help/implementing/developing/hybrid/editing-external-spa.md)

AEMのSPAトピックを詳しく解説できる[追加のリソース](#additional-resources)を以下に示します。

## その他のリソース {#additional-resources}

以下に、このドキュメントで説明する概念について詳しく調べるためのその他のリソースをいくつか示します。

* [headful and Headless in AEM](/help/implementing/developing/headful-headless.md)  - AEMで使用可能な様々な配信モデルの説明
* [SPA の概要およびガイド.](/help/implementing/developing/hybrid/introduction.md) - AEMでのSPAの良い紹介
* [AEM用SPAの開発](/help/implementing/developing/hybrid/developing.md) -AEM用SPAの開発方法に関するガイドライン
* [SPAエディタの概要](/help/implementing/developing/hybrid/editor-overview.md) -SPAエディタの動作の詳細
* [サーバ側のレンダリング](/help/implementing/developing/hybrid/ssr.md) - AEM SPA用にSSRを設定する方法
* [SPAリファレンスドキュメント](/help/implementing/developing/hybrid/reference-materials.md) - JavaScript APIリファレンスとオープンソースのSPA GitHubプロジェクトへのリンク
* [コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)  — コンテンツフラグメントの作成方法
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)  - Mavenテンプレート。Webサイトの起点として最小限のベストプラクティスベースのAdobe Experience Manager(AEM)プロジェクトを作成します。
