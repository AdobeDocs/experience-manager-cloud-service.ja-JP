---
title: SPA の動的モデルとコンポーネントのマッピング
description: この記事では、AEM用 JavaScript SPA SDK で動的モデルとコンポーネントのマッピングがどのようにおこなわれるかを説明します。
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 61%

---

# SPA の動的モデルとコンポーネントのマッピング {#dynamic-model-to-component-mapping-for-spas}

このドキュメントでは、AEM版 JavaScript SPA SDK で動的モデルとコンポーネントのマッピングがどのようにおこなわれるかを説明します。

## ComponentMapping モジュール {#componentmapping-module}

`ComponentMapping` モジュールは、プロントエンドプロジェクトに NPM パッケージとして提供されます。フロントエンドコンポーネントを格納し、単一ページアプリケーションがフロントエンドコンポーネントを AEM リソースタイプにマップする方法を提供します。このモジュールは、アプリケーションの JSON モデルを解析する際に、コンポーネントの動的な解決を有効にします。

モデル内の各項目には、 `:type` AEMリソースタイプを表示するフィールド。 フロントエンドコンポーネントは、マウントされると、基になるライブラリから受け取ったモデルのフラグメントを使用して自分自身をレンダリングできます。

詳しくは、 [SPA Blueprint](blueprint.md) モデル解析と、モデルへのフロントエンドコンポーネントアクセスに関する詳細がドキュメントに記載されています。

Npm パッケージ[@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) も参照してください。

## モデル駆動型単一ページアプリケーション {#model-driven-single-page-application}

AEM用 JavaScript SPA SDK を使用する単一ページアプリケーションは、モデル主導です。

1. フロントエンドコンポーネントは、自らを[コンポーネントマッピングストア](#componentmapping-module)に登録します。
1. 次に、[コンテナ](blueprint.md#container)は、 [モデルプロバイダー](blueprint.md#the-model-provider)がモデルを提供した後、そのモデルコンテンツ（`:items`）を反復します。

1. ページがある場合、その子 (`:children`) 最初に、 [コンポーネントマッピング](blueprint.md#componentmapping) 次に、インスタンス化します。

## アプリの初期化 {#app-initialization}

各コンポーネントは、[`ModelProvider`](blueprint.md#the-model-provider) の機能で拡張されます。初期化は、次の一般的な形式をとります。

1. 各モデルプロバイダーは自身を初期化し、内部コンポーネントに対応するモデルの部分に対しておこなわれる変更をリッスンします。
1. [初期化フロー](blueprint.md)で示されるとおりに、[`PageModelManager`](blueprint.md#pagemodelmanager) は初期化される必要があります。

1. 保存されると、ページモデルマネージャーはアプリの完全なモデルを返します。
1. 次に、このモデルは、アプリケーションのフロントエンドルート[コンテナ](blueprint.md#container)コンポーネントに渡されます。
1. モデルの断片は、最後に個々の子コンポーネントに伝播されます。

![アプリモデルの初期化](assets/app-model-initialization.png)
