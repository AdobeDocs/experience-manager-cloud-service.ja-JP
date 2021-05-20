---
title: RemotePage コンポーネント
description: RemotePage コンポーネントは、AEM 内のリモート React SPA を編集するためのカスタムページコンポーネントです。
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
source-git-commit: eaa59b6ecfa50c4a6b4e316e5e305e48cb3d5676
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 55%

---

# RemotePage コンポーネント {#remote-page-component}

外部 SPA と AEM の間で[どのレベルの統合](/help/implementing/developing/headful-headless.md)を行うかを決める際に、AEM 内で SPA を表示して編集できる必要があることはよくあります。RemotePage コンポーネントは、この目的のためのカスタムページコンポーネントです。

## 概要 {#overview}

RemotePage コンポーネントは、アプリケーションで生成された `asset-manifest.json` から必要なアセットをすべて取得し、これを使用して AEM 内の SPA +をレンダリングします。

* RemotePageを使用すると、AEM Pageコンポーネントの本文にSPAのスクリプトとスタイルシートを挿入できます。
* 仮想フロントエンドコンポーネントを使用すると、AEM SPA Editorで編集可能としてセクションをマークできます。
* 一緒に、別のドメインでホストされるSPAをAEMで編集可能にできます。

AEMでの編集可能な外部SPAについて詳しくは、 AEM](editing-external-spa.md)内での外部SPAの編集の記事[を参照してください。

## 要件 {#requirements}

* 開発での CORS の有効化
* ページプロパティでのリモート URL の設定
* AEM での SPA のレンダリング
* Webアプリケーションは、次のいずれかのバンドラーアセットマニフェストを使用し、読み込まれるすべてのCSSおよびJSファイルを`entrypoints property`にリストするドメインルートに`asset-manifest.json`ファイルを公開する必要があります。
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
      ![entrypointsプロパティの例](assets/asset-manifest-entrypoints.png)
* アプリケーションは、`body`要素の下の`<div id="root"></div>`で初期化できる必要があります。 アプリケーションが異なるマークアップをインスタンス化する必要がある場合は、`sling:resourceSuperType="spa-project-core/components/remotepage`を持つプロキシコンポーネントのHTLスクリプトで適宜調整する必要があります。

## 制限事項 {#limitations}

* 現在の RemotePage コンポーネントの実装では、リモートの React アプリケーションのみがサポートされています。
* AEM でリモートレンダリングをおこなう場合、アプリケーションのルート HTML ファイルに定義された内部 CSS と、ルート DOM ノードのインライン CSS は使用できません。

## 技術的詳細 {#technical-details}

AEM SPA プロジェクトの他の部分と同様、RemotePage コンポーネントもオープンソースです。RemotePage コンポーネントの技術的な詳細については、[GitHub リポジトリーを参照してください。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
