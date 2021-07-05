---
title: AEM Extension for PWA Studioの概要
description: AEMを使用して、ヘッドレスコンテンツおよびコマースプロジェクトをデプロイする方法についてPWA Studioします。
topics: Commerce
feature: コマース統合フレームワーク
thumbnail: 37843.jpg
source-git-commit: 2d5207733a0ad5d88a321826727eb02440765faf
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---


# AEM Extension for PWA Studioの概要 {#getting-started-pwa}

PWA Studioは、GraphQLを通じてAdobeコマースとシームレスに統合され、革新的で魅力的なストアフロントやその他のデジタルエクスペリエンスを作成する無制限のオプションを提供します。

コンテンツフラグメントは、GraphQLを様々な形式（JSON、Markdownなど）でAPIとして使用し、独立してレンダリングする、ヘッドレスな方法で利用できる、事前定義された構造を持つコンテンツの断片です。 コンテンツフラグメントには、GraphQLでアプリケーションが使用可能なデータのみを要求し、期待されるデータを受け取るために必要なすべてのデータタイプとフィールドが含まれます。 構造の観点から柔軟性を提供することで、複数の場所や複数のチャネルでの使用に最適です。

Adobe Experience Manager内のコンテンツフラグメントモデルエディターを使用すると、必要な構造を簡単にデザインできます。 Adobe Experience Managerコンテンツフラグメント（またはその他のデータ）をPWA Studioアプリケーションに統合する際の主な課題は、複数のGraphQLエンドポイントからデータを取得することです。 これは、デフォルトで、PWA Studioが単一のAdobeCommerce GraphQLエンドポイントで機能するためです。

## アーキテクチャ {#architecture}

![PWAヘッドレスアーキテクチャ](/help/commerce-cloud/assets/PWA-Studio_Architecture.png)

## 設定PWA Studio {#setup-pwa}

Adobeコマースの[PWA Studioのドキュメント](https://magento.github.io/pwa-studio/tutorials/)に従って、PWA Studioアプリを設定します。

PWA StudioをAEMのGraphQLエンドポイントに接続するには、[AEM Extension forPWA Studio](https://github.com/adobe/aem-pwa-studio-extensions)を使用します。

1. リポジトリをチェックアウトします。

1. PWA Studioアプリケーションで、拡張機能を開発依存関係として追加します。

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Apollo LinkラッパーをPWA Studioアプリケーションに追加します。 pwa-root/src/index.jsで、次の変更を行います。

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   詳しくは、[linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js)を参照してください。

1. ブログエントリを使用してナビゲーションコンポーネントを拡張するには、 pwa-root/local-intercept.jsに次の適応を追加します。

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   ナビゲーションコンポーネントのカスタマイズの詳細については、 [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js)と、PWA Studioの[Extensibility Framework](https://magento.github.io/pwa-studio/pwa-buildpack/extensibility-framework/)ドキュメントを参照してください。

1. Apolloクライアントは、AEM GraphQLエンドポイントが<https://pwa-studio/endpoint.js>になることを期待します。 エンドポイントをこの場所にマッピングするには、PWA StudioアプリケーションのUPPOUD設定をカスタマイズする必要があります。
a.AEM_CFM_GRAPHQL変数をpwa-root/.envに追加し、AEMコンテンツフラグメントGraphQLエンドポイントを指すように調整します。

   例：AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b.プロキシリゾルバーをUPPOURD設定に追加します。 上向き設定の例を次に示します。

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## セットアップAEM {#setup-aem}

AEMコンテンツフラグメントのドキュメントに従って、 AEMプロジェクトのGraphQLエンドポイントを設定します。 さらに、AEMプロジェクトに次の設定を追加して、PWA StudioアプリケーションがGraphQLエンドポイントにアクセスできるようにします。

* AdobeGraniteクロスオリジンリソース共有ポリシー(com.adobe.granite.cors.impl.CORSPolicyImpl)

   allowedoriginプロパティに、PWAアプリケーションの完全なホスト名を設定します。

   例:  <https://pwa-studio-test-vflyn.local.pwadev:9366>

* Apache Sling Referrer Filter(org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   allow.hostsプロパティをPWA・アプリケーションのホスト名に設定します。

   例：pwa-studio-test-vflyn.local.pwadev

両方の設定の完全な例については、次を参照してください。<https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

GraphQLエンドポイントを紹介するために、コンテンツパッケージを介して、サンプルコンテンツフラグメントモデルとデータをいくつか用意しました。 これらは、拡張機能に付属するReactコンポーネントとうまく連携してPWA Studioします。

## 使用方法 {#how-to-use}

この拡張機能は、GraphQLを使用してPWA Studioを取得し、レンダリングする、コンテンツアプリケーションとAEMを接続する方法の実装例と見なされます。

使用事例に応じて、独自のカスタムコンテンツフラグメントモデルを作成し、カスタムGraphQLスキーマを作成して、独自のReactコンポーネントで使用できます。

実稼動環境の設定は、様々な面で異なる場合があります。

* Apolloクライアントをカスタマイズする代わりに、AEMとMagentoのGraphQLデータを組み合わせた単一のフェデレーテッドGraphQLエンドポイントを使用できます。
* PWA Studioアプリケーションは、UPOUPを使用するプロキシなしで、AEM GraphQLエンドポイントURLを直接使用できます。 プロキシは別のレイヤー（CDNなど）に移動することもできます。
* どのアプローチがお客様に最適かは、エンドユーザーにPWA Studio・アプリケーションを提供する方法に大きく依存します。

この拡張機能には2つの例が用意されています。

### ブログ {#blog}

一部のコンテンツフラグメントモデルに基づいてブログ投稿を表示します。 さらに、AEM GraphQLエンドポイントと連携するようApolloクライアントを設定する方法と、ナビゲーションコンポーネントをPWA Studioで拡張する方法の例も含まれています。 詳しくは、[GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension)を参照してください。

### PDPエンリッチメント {#pdp-enrichment}

マーケティング担当者は、コンテンツフラグメントとして管理される追加のコンテンツを使用して、PDPを容易に強化できます。  詳しくは、[GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension)を参照してください。
