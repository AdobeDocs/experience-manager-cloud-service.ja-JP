---
title: RemotePage コンポーネント
description: RemotePage コンポーネントは、AEM 内のリモート React SPA を編集するためのカスタムページコンポーネントです。
translation-type: tm+mt
source-git-commit: 9a1048f6d185d2d3229bab05b8e827845444d11c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 74%

---

# RemotePage コンポーネント {#remote-page-component}

外部 SPA と AEM の間で[どのレベルの統合](/help/implementing/developing/headful-headless.md)を行うかを決める際に、AEM 内で SPA を表示して編集できる必要があることはよくあります。RemotePage コンポーネントは、この目的のためのカスタムページコンポーネントです。

## 概要 {#overview}

RemotePage コンポーネントは、アプリケーションで生成された `asset-manifest.json` から必要なアセットをすべて取得し、これを使用して AEM 内の SPA +をレンダリングします。

* RemotePageを使用すると、AEM Pageコンポーネントの本文にSPAのスクリプトやスタイルシートを挿入できます。
* 仮想フロントエンドコンポーネントを使用すると、AEM SPAエディタでセクションを編集可能としてマークできます。
* 1つのSPAを組み合わせて、異なるドメインでホストされているをAEMで編集可能にすることができます。

AEMの編集可能な外部SPAの詳細については、「AEM](editing-external-spa.md)内の外部SPAの編集」を参照してください。[

## 要件 {#requirements}

* 開発での CORS の有効化
* ページプロパティでのリモート URL の設定
* AEM での SPA のレンダリング

## 制限事項 {#limitations}

* 現在の RemotePage コンポーネントの実装では、リモートの React アプリケーションのみがサポートされています。
* AEM でリモートレンダリングをおこなう場合、アプリケーションのルート HTML ファイルに定義された内部 CSS と、ルート DOM ノードのインライン CSS は使用できません。

## 技術的詳細 {#technical-details}

AEM SPA プロジェクトの他の部分と同様、RemotePage コンポーネントもオープンソースです。RemotePage コンポーネントの技術的な詳細については、[GitHub リポジトリーを参照してください。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
