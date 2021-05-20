---
title: オプション — AEMを使用したシングルページアプリケーション(SPA)の作成方法
description: AEMヘッドレス開発者ジャーニーのこのオプションの続きでは、AEMがヘッドレス配信を従来のフルスタックCMS機能と組み合わせる方法、およびAEM SPA Editorフレームワークを使用して編集可能なSPAを作成する方法について説明します。
hide: true
hidefromtoc: true
index: false
exl-id: 80b43aae-0027-45c8-b079-e3931d58597f
source-git-commit: 9e06419f25800199dea92b161bc393e6e9670697
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 34%

---

# AEM {#create-spa}を使用したシングルページアプリケーション(SPA)の作成方法

>[!CAUTION]
>
>古い — このドラフトコンテンツは、新しい[ヘッドレス開発者ジャーニードキュメントに置き換えられました。](/help/journey-headless/developer/overview.md)

[AEMヘッドレス開発者ジャーニー（オプション）の続きでは、AEMが従来のフルスタックCMS機能とヘッドレス配信を組み合わせる方法、AEM SPA Editorフレームワークを使用した編集可能なSPAの作成方法、および外部SPAを統合し、必要に応じて編集機能を有効にします。](overview.md)

## {#story-so-far}までの話

この時点で、[AEMヘッドレス開発者ジャーニー](overview.md)全体を完了し、次の内容を理解し、AEMのヘッドレス配信の基本を理解する必要があります。

* ヘッドレスコンテンツ配信とヘッドフルコンテンツ配信の違い。
* AEMヘッドレス機能
* ヘッドレスプロジェクトの整理とAEMの方法。
* AEMでヘッドレスコンテンツを作成する方法。
* AEMでヘッドレスコンテンツを取得して更新する方法。
* AEMヘッドレスプロジェクトの運用方法。

これで、最初のAEMヘッドレスプロジェクトを使用するか、または実行に必要な知識をすべて取得できます。 バリデーターが

ではなぜこの旅の続きを読むのか？ [はじめに](getting-started.md#integration-levels)で、AEMがヘッドレス配信と従来のフルスタックモデルをサポートするだけでなく、両方の利点を組み合わせたハイブリッドモデルをサポートする方法について簡単に説明したことを思い出してください。 従来のヘッドレスモデルではありませんが、このようなハイブリッドモデルは、特定のプロジェクトに対して前例のない柔軟性を提供できます。

この記事は、AEMで実際に編集可能な独自のシングルページアプリケーション(SPA)を作成する方法を詳しく説明することで、AEMヘッドレスに関するお客様の知識に基づいて構築されます。 この方法では、コンテンツを作成してSPAにヘッドレスに配信できますが、SPAはAEMで編集可能なままです。

## 目的 {#objective}

このドキュメントでは、AEM SPA Editorフレームワークを使用してシングルページアプリケーションを開発する方法を説明します。 このドキュメントを読んだ後、次の操作を行う必要があります。

* SPA Editorの基本的な機能を理解します。
* 完全に編集可能なAEM用SPAを構築するための要件を理解します。
* 外部SPAをAEMに統合する方法を説明します。
* サーバーサイドレンダリングを実装する方法と実装しない方法を理解します。

## 要件と前提条件{#requirements-prerequisites}

AEMでSPAの使用を開始する前に、いくつかの要件があります。

### 知識 {#knowledge}

* ReactまたはReactフレームワークを使用したSPAの作成Angularエクスペリエンス
* AEMの基本的なスキルコンテンツフラグメントの作成とエディターの使用
* 可能なSPA統合の様々なレベルを理解するには、AEM](/help/implementing/developing/headful-headless.md)の「ヘッドフル」と「ヘッドレス」のドキュメントを必ず確認してください。[

### ツール {#tools}

* プロジェクトのデプロイをテストするためのサンドボックスアクセス
* ローカル開発モデリングとテスト用のデータインスタンス
* 既存の外部SPA（選択した統合モデルに応じてオプション）
* AEM プロジェクトアーキタイプ

## SPA について {#what-is-a-spa}

単一ページアプリケーション（SPA）は、クライアントサイドでレンダリングされ、主に JavaScript 主導であり、Ajax 呼び出しに依存してデータを読み込み、ページを動的に更新する点で、従来のページとは異なります。ほぼすべてのコンテンツは、1 回のページ読み込みで 1 回取得され、ユーザーによるページとのやり取りに基づいて、必要に応じて追加のリソースが非同期に読み込まれます。

これにより、ページを更新する必要が減り、シームレスで高速な、ネイティブアプリのエクスペリエンスに近いものををユーザーに提供できます。

AEM SPA エディターを使用すると、フロントエンド開発者は AEM のサイトに統合できる SPA を作成でき、コンテンツ作成者は SPA コンテンツを他の AEM コンテンツと同様に簡単に編集できます。

## SPA が注目される理由 {#why-spa}

より速く、流動的で、よりネイティブアプリケーションに近い SPA は、Web ページの訪問者だけでなく、SPA の仕組みの性質上、マーケターや開発者にとっても非常に魅力的なエクスペリエンスとなります。

SPAの詳細な説明と使用理由については、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクを参照してください。

## AEMによるSPAの処理方法

AEM で単一ページアプリケーションを開発する場合、フロントエンド開発者は SPA を作成する際に標準的なベストプラクティスを順守するものと想定します。次の一般的なベストプラクティスには AEM 固有の原則はほぼなく、フロントエンド開発者がそれに従うことで、SPA は AEM とコンテンツオーサリング機能と共に機能します。

* **移植性**  — あらゆるコンポーネントと同様に、SPAコンポーネントは可能な限り移動可能な状態で構築する必要があります。SPA は、移動可能で再利用可能なコンポーネントを使用して構築する必要があります。
* **AEM を主軸にしたサイト構築** - フロントエンド開発者はコンポーネントを作成し、内部構造を所有しますが、AEM に依存してサイトのコンテンツ構造を定義します。
* **動的レンダリング** - すべてのレンダリングは動的である必要があります。
* **動的ルーティング** - SPA がルーティングを担当し、AEM がリッスンしてそれに基づいて取得します。どのルーティングも動的である必要があります。

AEMによるSPAの処理方法について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクを確認してください。

## AEM SPA Editor {#aem-spa-editor}

React や Angular などの一般的な SPA フレームワークを使用して構築したサイトは、Dynamic JSON を使用してコンテンツを読み込みます。サイトには、AEM ページエディターが編集コントロールを配置するために必要な HTML 構造がありません。

AEM 内で SPA の編集を有効にするには、SPA の JSON 出力と AEM リポジトリのコンテンツモデルとの間でマッピングをおこない、変更をコンテンツに保存できるようにする必要があります。

AEM の SPA サポートにより、シン JS レイヤーが導入されました。このレイヤーは、ページエディターに読み込まれると、SPA の JS コードとやり取りします。これにより、イベントを送信したり、編集コントロールの場所をアクティブにしてコンテキスト内で編集したりできます。この機能は、コンテンツサービス API エンドポイントの概念に基づいて構築されています。SPA のコンテンツは、コンテンツサービスを使用して読み込む必要があるからです。

AEM SPA Editorの詳細な説明については、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクを確認してください。

## 既存のSPAへの対応{#existing-spas}

既存のSPAがある場合、AEMではAEMへの埋め込みがサポートされているので、AEMエディターでコンテンツ作成者に表示されます。 これは、コンテンツフラグメントを介して作成したコンテンツを、そのコンテンツが使用されるエンドアプリケーションのコンテキストで表示する場合に非常に役立ちます。

さらに、わずかな変更のみで、AEMエディター内の外部SPAに対して特定の編集機能を有効にすることができます。

RemotePageコンポーネントを使用すると、AEMで外部SPAをレンダリングできます。

外部SPAをAEMで編集可能にする方法について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクを確認してください。

## 次の手順{#what-is-next}

独自のAEM向けSPAの開発を開始するには、次のドキュメントを確認します。

* [SPA WKND チュートリアル](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Reactの使用を開始する](/help/implementing/developing/hybrid/getting-started-react.md)
* [使用の手引きAngular](/help/implementing/developing/hybrid/getting-started-angular.md)

既存のSPAをAEMで使用するように適応させる必要がある場合は、次のドキュメントを確認してください。

* [RemotePage コンポーネント](/help/implementing/developing/hybrid/remote-page.md)
* [AEM 内での外部 SPA の編集](/help/implementing/developing/hybrid/editing-external-spa.md)

AEMのSPAトピックをさらに深く掘り下げる[追加のリソース](#additional-resources)については、以下を参照してください。

## その他のリソース {#additional-resources}

以下に、このドキュメントで取り上げるいくつかの概念について詳しく説明する追加リソースを示します。

* [AEMのヘッドフルとヘッドレス](/help/implementing/developing/headful-headless.md)  - AEMで使用可能な様々な配信モデルの説明
* [SPA の概要およびガイド.](/help/implementing/developing/hybrid/introduction.md) - AEMでのSPAの良い紹介
* [SPA for AEMの開発](/help/implementing/developing/hybrid/developing.md)  - AEM向けSPAの開発方法に関するガイドライン
* [SPAエディターの概要](/help/implementing/developing/hybrid/editor-overview.md)  - SPAエディターの仕組みの詳細
* [サーバーサイドレンダリング](/help/implementing/developing/hybrid/ssr.md)  - AEM SPA用のSSRの設定方法
* [SPAリファレンスドキュメント](/help/implementing/developing/hybrid/reference-materials.md)  - JavaScript APIリファレンスと、オープンソースのAEM SPA GitHubプロジェクトへのリンク
* [コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)  — コンテンツフラグメントの作成方法
* [AEMプロジェクトのアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)  - Webサイトの出発点として最小限のベストプラクティスベースのAdobe Experience Manager(AEM)プロジェクトを作成するMavenテンプレート
