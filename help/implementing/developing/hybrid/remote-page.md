---
title: RemotePage コンポーネント
description: RemotePage コンポーネントは、AEM 内のリモート React SPA を編集するためのカスタムページコンポーネントです。
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: ht
source-wordcount: '364'
ht-degree: 100%

---


# RemotePage コンポーネント {#remote-page-component}

外部 SPA と AEM の間で[どのレベルの統合](/help/implementing/developing/headful-headless.md)を行うかを決める際に、AEM 内で SPA を表示して編集できる必要があることはよくあります。RemotePage コンポーネントは、この目的のためのカスタムページコンポーネントです。

{{ue-over-spa}}

## 概要 {#overview}

RemotePage コンポーネントは、アプリケーションで生成された `asset-manifest.json` から必要なアセットをすべて取得し、これを使用して AEM 内の SPA +をレンダリングします。

* RemotePage を使用すると、AEM ページコンポーネントの本文に SPA のスクリプトやスタイルシートを挿入できます。
* 仮想フロントエンドコンポーネントを使用すると、AEM SPA エディターでセクションを編集可能としてマークできます。
* これとともに、異なるドメインでホストされている SPA を AEM で編集可能にすることができます。

AEM の編集可能な外部 SPA の詳細については、[AEM 内の外部 SPA の編集](editing-external-spa.md)を参照してください。

## 要件 {#requirements}

* 開発での CORS の有効化
* ページプロパティでのリモート URL の設定
* AEM での SPA のレンダリング
* Web アプリケーションは、次のいずれかのバンドラーアセットマニフェストを使用し、読み込まれるすべての CSS および JS ファイルを `entrypoints property` にリストする `asset-manifest.json` ファイルをドメインルートに公開する必要があります。
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
     ![entrypoints プロパティの例](assets/asset-manifest-entrypoints.png)
* アプリケーションは、`body` 要素の下の `<div id="root"></div>` で初期化できる必要があります。アプリケーションで異なるマークアップをインスタンス化する必要がある場合は、`sling:resourceSuperType="spa-project-core/components/remotepage` を持つプロキシコンポーネントの HTL スクリプトで適宜調整する必要があります。

## 制限事項 {#limitations}

* RemotePage コンポーネントでは、実装によりアセットマニフェストが指定されることを想定しています。アセットマニフェストの例について詳しくは、[こちら](https://github.com/shellscape/webpack-manifest-plugin)を参照してください。ただし、RemotePage コンポーネントは React フレームワーク（および remote-page-next コンポーネントを介した Next.js）で動作するようにのみテストされているので、Angular など他のフレームワークからのアプリケーションのリモート読み込みはサポートされていません。
* AEM でリモートレンダリングを行う場合、アプリケーションのルート HTML ファイルに定義された内部 CSS およびルート DOM ノードのインライン CSS は使用できません。

## 技術的詳細 {#technical-details}

AEM SPA プロジェクトの他の部分と同様、RemotePage コンポーネントもオープンソースです。RemotePage コンポーネントの技術的な詳細について詳しくは、[GitHub リポジトリを参照してください](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)。
