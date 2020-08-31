---
title: SPAの動的モデルとコンポーネントのマッピング
description: この記事では、AEM向けJavaScript SPA SDKで、動的モデルとコンポーネントとのマッピングがどのように行われるかを説明します。
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# SPAの動的モデルとコンポーネントのマッピング {#dynamic-model-to-component-mapping-for-spas}

このドキュメントでは、AEM用JavaScript SPA SDKで、動的モデルとコンポーネントとのマッピングがどのように行われるかを説明します。

## ComponentMapping モジュール {#componentmapping-module}

The `ComponentMapping` module is provided as an NPM package to the front-end project. フロントエンドコンポーネントが格納され、シングルページアプリケーションがフロントエンドコンポーネントをAEMリソースタイプにマップする方法を提供します。 これにより、アプリケーションのJSONモデルを解析する際に、コンポーネントの動的な解決が可能になります。

モデル内の各項目には、AEMリソースタイプを表示する `:type` フィールドが含まれます。 マウントすると、フロントエンドコンポーネントは、基になるライブラリから受け取ったモデルのフラグメントを使用して自分自身をレンダリングできます。

モデル解析とモデルへのフロントエンドコンポーネントアクセスの詳細については、 [SPA Blueprint](blueprint.md) ドキュメントを参照してください。

npmパッケージも参照してください。 [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## モデル駆動型シングルページアプリ {#model-driven-single-page-application}

AEM向けJavaScript SPA SDKを利用する単一ページアプリケーションは、モデル駆動です。

1. フロントエンドコンポーネントは、それ自体を [コンポーネントマッピングストアに登録します](#componentmapping-module)。
1. 次に、 [コンテナ](blueprint.md#container)は、 [モデルプロバイダーがモデルを提供した後、そのモデルコンテンツ](blueprint.md#the-model-provider)(`:items`)を反復します。

1. ページの場合、その子(`:children`)は、最初に [](blueprint.md#componentmapping) コンポーネントマッピングからコンポーネントクラスを取得し、次にインスタンス化します。

## アプリの初期化 {#app-initialization}

各コンポーネントは、の機能で拡張され [`ModelProvider`](blueprint.md#the-model-provider)ます。 初期化は、次の一般的な形式をとります。

1. 各モデルプロバイダは自身を初期化し、内部コンポーネントに対応するモデルの部分に対して行われた変更をリッスンします。
1. 初期化フローで示されるとおりに、 [`PageModelManager`](blueprint.md#pagemodelmanager) 初期化する [必要があります](blueprint.md)。

1. 保存すると、ページモデルマネージャーはアプリの完全なモデルを返します。
1. 次に、このモデルは、アプリケーションのフロントエンドルート [コンテナ](blueprint.md#container) ・コンポーネントに渡されます。
1. モデルの断片は、最後に個々の子コンポーネントに伝播されます。

![アプリモデルの初期化](assets/app-model-initialization.png)
