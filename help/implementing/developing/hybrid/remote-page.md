---
title: RemotePageコンポーネント
description: RemotePageコンポーネントは、AEM内のリモートReact SPAを編集するためのカスタムページコンポーネントです。
translation-type: tm+mt
source-git-commit: 9a1048f6d185d2d3229bab05b8e827845444d11c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# RemotePageコンポーネント{#remote-page-component}

外部SPAとAEMの間でどのレベルの統合を行うかを決める際に、AEM内でSPAを表示して編集できる必要があることはよくあります。 [](/help/implementing/developing/headful-headless.md)RemotePageコンポーネントは、この目的のためのカスタムページコンポーネントです。

## 概要 {#overview}

RemotePageコンポーネントは、アプリケーションで生成された`asset-manifest.json`から必要なアセットをすべて取得し、これを使用してAEM内のSPAをレンダリングします。

* RemotePageを使用すると、AEM Pageコンポーネントの本文にSPAのスクリプトやスタイルシートを挿入できます。
* 仮想フロントエンドコンポーネントを使用すると、AEM SPAエディタでセクションを編集可能としてマークできます。
* 1つのSPAを組み合わせて、異なるドメインでホストされているをAEMで編集可能にすることができます。

AEMの編集可能な外部SPAの詳細については、「AEM](editing-external-spa.md)内の外部SPAの編集」を参照してください。[

## 要件 {#requirements}

* 開発でのCORSの有効化
* ページプロパティでのリモートURLの設定
* AEMでSPAをレンダリングする

## 制限事項 {#limitations}

* 現在のRemotePageコンポーネントの実装では、リモートのReactアプリケーションのみがサポートされています。
* AEMでリモートレンダリングを行う場合、アプリケーションのルートHTMLファイルに定義された内部CSSと、ルートDOMノードのインラインCSSは使用できません。

## 技術的詳細 {#technical-details}

AEM SPAプロジェクトの他の部分と同様、RemotePageコンポーネントもオープンソースです。 RemotePageコンポーネントの技術的な詳細については、[GitHubリポジトリを参照してください。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
