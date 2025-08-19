---
title: AEM Extension for PWA Studio の概要
description: PWA Studio で、ヘッドレスの AEM Content and Commerce プロジェクトをデプロイする方法について説明します。
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: a7c187ba-885e-45bf-a538-3c235b09a0f1
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 91%

---


# AEM Extension for PWA Studio の概要 {#getting-started-pwa}

PWA Studio は GraphQL により初期設定で Adobe Commerce とシームレスに統合されており、革新的で魅力的なストアフロントやその他のデジタルエクスペリエンスを作成するためのオプションを無制限に提供します。

コンテンツフラグメントは、構造が事前定義されたコンテンツの要素です。この構造により、GraphQL を様々な形式（JSON や Markdown など）の API として使用しながら、ヘッドレスな方法でコンテンツを利用し、独立してレンダリングすることができます。コンテンツフラグメントには、GraphQL に必要なすべてのデータタイプとフィールドが含まれているので、アプリケーションは利用可能な情報のみをリクエストして、期待する情報だけを受け取ることができます。コンテンツフラグメントの構造は柔軟なので、複数の場所や複数のチャネルでの使用にも適しています。

Adobe Experience Manager のコンテンツフラグメントモデルエディターを使用すれば、必要な構造を簡単に設計できます。Adobe Experience Manager コンテンツフラグメント（または他の任意のデータ）を PWA Studio アプリケーションと統合するうえでの主な課題は、複数の GraphQL エンドポイントからデータを取得することです。これは、PWA Studio が、初期設定では、単一の Adobe Commerce GraphQL エンドポイントで機能するようになっているからです。

## アーキテクチャ {#architecture}

![PWA ヘッドレスアーキテクチャ](/help/commerce-cloud/cif-storefront/assets/PWA-Studio_Architecture.png)

## PWA Studio のセットアップ {#setup-pwa}

PWA Studio アプリをセットアップするには、Adobe Commerce の [PWA Studio のドキュメント](https://developer.adobe.com/commerce/pwa-studio/tutorials/)に従います。

PWA StudioをAEMのGraphQL エンドポイントに接続するには、[AEM Extension for PWA Studio.](https://github.com/adobe/aem-pwa-studio-extensions) を使用します。

1. リポジトリをチェックアウトします。

1. PWA Studio アプリケーションで、この拡張機能を開発依存コンポーネントとして追加します。

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. PWA Studio アプリケーションに Apollo Link ラッパーを追加します。`pwa-root/src/index.js` で、次の変更を行います。

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Apollo Client のカスタマイズについて詳しくは、[linkWrapper.js.](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js) を参照してください

1. ブログエントリを使用してナビゲーションコンポーネントを拡張するには、`pwa-root/local-intercept.js` を次のように変更します。

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   ナビゲーションコンポーネントのカスタマイズについて詳しくは、[addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) と、PWA Studio の[拡張フレームワーク](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/)に関するドキュメントを参照してください。

1. Apollo Client は、`<https://pwa-studio/endpoint.js>` に AEM GraphQL エンドポイントがあることを想定します。エンドポイントをこの場所にマッピングするには、PWA Studio アプリケーションの UPWARD 設定を次のようにカスタマイズします。
a. AEM_CFM_GRAPHQL 変数 pwa-root/.env に追加し、AEM コンテンツフラグメントの GraphQL エンドポイントを参照するように変数を調整します。

   例：`AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>`

   b. UPWARD 設定にプロキシリゾルバーを追加します。UPWARD 設定は例えば次のようになります。

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

## AEM のセットアップ {#setup-aem}

AEM コンテンツフラグメントのドキュメントに従って、AEM プロジェクトの GraphQL エンドポイントをセットアップします。さらに、AEM プロジェクトに次の設定を追加して、PWA Studio アプリケーションから GraphQL エンドポイントにアクセスできるようにします。

* Adobe Granite クロスオリジンリソース共有ポリシー（com.adobe.granite.cors.impl.CORSPolicyImpl）

  allowedorigin プロパティに PWA アプリケーションの完全なホスト名を設定します。

  例：`<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Apache Sling Referrer Filter（org.apache.sling.security.impl.ReferrerFilter.cfg.json）

  allow.hosts プロパティに PWA アプリケーションのホスト名を設定します。

  例：`pwa-studio-test-vflyn.local.pwadev`

両方の設定の完全な例については、[ こちら ](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config) を参照してください。

GraphQL エンドポイントを紹介するために、サンプルコンテンツフラグメントのモデルとデータを、コンテンツパッケージでいくつか用意しています。これらは、PWA Studio 用拡張機能に付属する React コンポーネントとうまく連携して機能します。

## 使用方法 {#how-to-use}

この拡張機能は、PWA Studio アプリケーションを AEM に接続して、GraphQL でコンテンツを取得し、レンダリングする方法の実装例と考えることができます。

ユースケースに応じて、独自のカスタムコンテンツフラグメントモデルを作成します。このモデルが、独自の React コンポーネントで利用できるカスタム GraphQL スキーマになります。

実稼動のセットアップは、様々な点で異なるものになる可能性があります。

* Apollo クライアントをカスタマイズする代わりに、AEM と Adobe Commerce GraphQL データを組み合わせて、単一の連合 GraphQL エンドポイントにできます。
* PWA Studio アプリケーションでは、UPWARD 設定のプロキシを介さずに、AEM GraphQL エンドポイント URL を直接使用することもできます。プロキシは別のレイヤー（CDN など）に移動することもできます。
* どのアプローチが最適かは、ユーザーへの PWA Studio アプリケーションの提供方法によっても大きく異なります。

この拡張機能には 2 つの例が用意されています。

### ブログ {#blog}

いくつかのコンテンツフラグメントモデルに基づいてブログ投稿を表示します。さらに、AEM GraphQL エンドポイントと連携するように Apollo Client を設定する方法と、ナビゲーションコンポーネントを PWA Studio で拡張する方法の例も含まれています。詳しくは、[GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) を参照してください。

### PDP エンリッチメント {#pdp-enrichment}

マーケターが、コンテンツフラグメントとして管理される追加コンテンツを使用して PDP を簡単に拡充できます。詳しくは、[GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) を参照してください。
