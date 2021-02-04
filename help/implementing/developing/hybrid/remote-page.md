---
title: RemotePageコンポーネント
description: RemotePageコンポーネントは、AEM内のリモートReact SPAを編集するためのカスタムページコンポーネントです。
translation-type: tm+mt
source-git-commit: 6a88b93a4005b858eec222fd7ae15df9db269d31
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 2%

---

# RemotePageコンポーネント{#remote-page-component}

外部SPAとAEMの間でどのレベルの統合を行うかを決める際に、AEM内でSPAを表示して編集できる必要があることはよくあります。 [](/help/implementing/developing/headful-headless.md)RemotePageコンポーネントは、この目的のためのカスタムページコンポーネントです。

## 概要 {#overview}

RemotePageコンポーネントは、アプリケーションで生成された`asset-manifest.json`から必要なアセットをすべて取得し、これを使用してAEM内のSPAをレンダリングします。

## 要件 {#requirements}

* 開発でのCORSの有効化
* ページプロパティでのリモートURLの設定
* AEMでSPAをレンダリングする

## 制限事項 {#limitations}

* 現在のRemotePageコンポーネントの実装では、リモートのReactアプリケーションのみがサポートされています。
* AEMでリモートレンダリングを行う場合、アプリケーションのルートHTMLファイルに定義された内部CSSと、ルートDOMノードのインラインCSSは使用できません。

## 技術的詳細 {#technical-details}

AEM SPAプロジェクトの他の部分と同様、RemotePageコンポーネントもオープンソースです。 RemotePageコンポーネントの技術的な詳細については、[GitHubリポジトリを参照してください。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
