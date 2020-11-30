---
title: AEM Commerce as a Cloud Service の概要
description: Experience Manager Commerce as a Cloud Service は、Commerce Integration Framework（CIF）で構成されます。これは、Magento および他のサードパーティのコマースソリューションのコマースサービスを Experience Cloud と統合および拡張するための推奨パターンです。
thumbnail: introducing-aem-commerce.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 100%

---


# AEM Commerce as a Cloud Service の概要 {#commerce-intro}

Experience Manager Commerce as a Cloud Service は、Commerce Integration Framework（CIF）で構成されます。これは、Magento および他のサードパーティのコマースソリューションのコマースサービスを Experience Cloud と統合および拡張するための推奨パターンです。これにより、アドビのお客様は、最先端のテクノロジーに基づく、個々の顧客に合わせた卓越したショッピングエクスペリエンスを提供できます。

Commerce Integration Framework は、Experience Manager as a Cloud Service 用のアドオンモジュールで、Experience Manager as a Cloud とコマースソリューション間の統合の開発を促進するためのオーサリングツール、コンポーネント、参照用ストアフロントを提供します。

## CIF の利点 {#cif-benefits}

主な利点は次のとおりです。

* 統合は、複数のシステムとの統合を標準化およびカプセル化する抽象レイヤーです。

* CIF はヘッドレス／オムニチャネルエクスペリエンスをサポートします。

   * 単一ページアプリケーションと複数ページアプリケーション
   * GraphQL エンドポイント

* CIF は、カスタマイズやコマースサービスの拡張をおこなうための、サーバレスのマイクロサービスベースのプロセスとビジネスロジックレイヤーを提供します。

* CIF は、AEM や Magento などのアドビソリューションとの統合を標準搭載しています。

## CIF 要素 {#cif-elements}

![CIF 要素](/help/commerce-cloud/assets/cif-overview1.jpg)


### オーサリングツール用 CIF アドオン {#add-on-authoring-tools}

CIF アドオンを使用すると、作成者は、製品コンソール、製品とカテゴリの選択、製品検索などのコマースオーサリングツールにアクセスして、マーケティングやコマースのコンテンツで豊富なエクスペリエンスを作成できます。アドオンは、GraphQL を介して Magento（または代替コマースシステム）へのバックエンド接続も管理します。プロビジョニングされたアドオンは、AEM as a Cloud Service 環境に自動的にデプロイされます。

### AEM CIF コアコンポーネント {#aem-cif-core}

AEM CIF コアコンポーネントは、Magento の GraphQL サポートを持つサーバーサイドおよびクライアントサイドのレンダリングコンポーネントです。AEM テクノロジーを基に、静的で、キャッシュ可能で、SEO フレンドリーなコマースストアフロントを作成するのに使用されます。

製品の詳細、製品のリスト、ナビゲーション、検索など、コマースの実装間で共通の基本的なコンポーネントが提供されます。そのまま使用することも、拡張することもできます。

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は [AEM Sites コアコンポーネント](https://github.com/adobe/aem-core-wcm-components)同様に機能しますが、コマース固有の使用例に特化したものです。

次はコンポーネントの主な利点です。

* プロジェクトで簡単に使用できます。
* 現状のまま、または最小限に変更して使用できます。
* GraphQL API または REST API を介した Magento への接続のベストプラクティスを提供します。

AEM 作成者が AEM でマーケティングコンテンツとコマースコンテンツを組み合わせてエクスペリエンスページを作成できるように、製品ティーザーや製品カルーセルなどのコンポーネントが用意されています。これらのコンポーネントは、AEM で作成されたコンテンツページに簡単にドラッグ＆ドロップでき、Cloud Service の製品やカテゴリ選択などの CIF オーサリングツールを使用して特定の製品やカテゴリにリンクできます。

すべてのコンポーネントはオープンソースで [GitHub](https://github.com/adobe/aem-core-cif-components) にあります。これにより、今後おこなわれる変更に対する完全な透明性が確保され、最新バージョンを簡単に入手できます。また、改善点やバグ修正のプルリクエストをおこなうこともできます。

### AEM Venia ストアフロント {#aem-venia-storefront}

AEM [Venia ストアフロント](https://github.com/adobe/aem-cif-guides-venia)は、B2C コマースの基本的なジャーニーを紹介する、製作に適した最新の参照用ストアフロントです。AEM、CIF、Magento を使用して、コマースプロジェクトを開始し、プロジェクトを高速化するために使用できます。AEM と Magento の統合のベストプラクティスと、[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)および [AEM Sites コアコンポーネント](https://github.com/adobe/aem-core-wcm-components)の使用方法を示します。また、Adobe Commerce GraphQL エンドポイントをサポートしています。また、AEM と Magento の統合をデモするための参照用サイトをプリセールスに提供します。

AEM Venia ストアフロントは、AEM がエクスペリエンスを提供し Magento がヘッドレスにコマースバックエンドを提供している混在ページアプリケーションです。ストアフロントでは、サーバーサイドのレンダリングとクライアントサイドのレンダリングの両方が使用されます。サーバーサイドのレンダリングは静的コンテンツの配信に使用され、クライアントサイドのレンダリングは動的コンテンツの配信に使用されます。

製品ページとカタログページは比較的静的で、AEM で作成した汎用テンプレート上の製品の詳細や製品のリストなど、AEM CIF コアコンポーネントを使用してサーバーサイドにレンダリングされます。これらのコンポーネントは、GraphQL API を介して Magento からデータを取得します。
これらのページは動的に作成され、サーバー上でレンダリングされ、AEM Dispatcher 上でキャッシュされて、ブラウザーに配信されます。
在庫や価格など、より動的な属性に対しては、クライアントサイドコンポーネントが使用されます。クライアントサイドコンポーネントまたは Web コンポーネントは、GraphQL API を介して Magento からデータを直接取得し、コンテンツをブラウザーにレンダリングします。

#### チェックアウト {#checkout}

この参照ストアフロントは、買い物かごとチェックアウトフォームをレンダリングするクライアントサイドの買い物かごコンポーネントを使用して、Magento が完全にヘッドレスで実行されて AEM がエクスペリエンスを提供する、完全なエクスペリエンス統合パターンを示しています。提供されている抽象支払い方法を使用することをお勧めします。これにより、ブラウザークライアントは支払いゲートウェイプロバイダーと直接通信し、アドビも Magento クラウドも PCI 機密データを保持したり受け渡したりしないようになります

#### アカウント管理 {#account-management}

アカウント管理は Magento によって処理され、参照ストアフロントでは、クライアントサイドの React ベースのコンポーネントを使用して、AEM がアカウント作成、サインイン、パスワードを忘れた場合のエクスペリエンスをレンダリングできるようにします。

AEM Venia ストアフロントプロジェクトはオープンソースです。詳しくは「[AEM Venia ストアフロント](https://github.com/adobe/aem-cif-guides-venia)」を参照してください。

### AEM プロジェクトアーキタイプ {#aem-project-archtype}

[AEM プロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)は、最小限のベストプラクティスベースの Adobe Experience Manager プロジェクトを独自の AEM プロジェクトの起点として作成するために使用できます。オプションで、[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)を新しく生成したプロジェクトに含めることができます。

### CIF 拡張レイヤー {#cif-extension}

CIF 拡張レイヤーは、複雑なビジネスロジックをホストする中間レイヤーです。アドビのサーバレスプラットフォームである Adobe I/O Runtime プラットフォーム上で動作します。マイクロサービスレベルでビジネスロジックとプロセスロジックを注入することで、エンドツーエンドのサービス呼び出しを拡張できます。ビジネスロジックの例は、場所とチャネルを使用して在庫戦略を決定する場合です。プロセスロジックの例は、パーソナライズされた情報を取得する場合です。

### CIF 統合レイヤー {#cif-integration-layer}

CIF 統合レイヤーは、他のコマースソリューションとの統合を標準化するために使用します。アドビのサーバーレスプラットフォームである Adobe I/O Runtime プラットフォーム上で実行され、サードパーティの API を Adobe Commerce API に対してマッピングすることで、マイクロサービスレベルでの統合を可能にします。AEM とのサードパーティ製統合の作成を開始するのに役立つように、[参照用実装](https://github.com/adobe/commerce-cif-graphql-integration-reference)を作成し、Adobe Commerce API（Magento GraphQL API）を使用して Magento 以外のコマースバックエンドを統合する方法を示しています。

## AEM のコマース統合パターン {#aem-commerce-integration}

一般的に実装される AEM のコマース統合パターンの一部を次に示します。

![AEM CIF 統合パターン](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### 統合パターン 1 {#integration-pattern-one}

これは、AEM がエクスペリエンス全体を提供し、Adobe Commerce GraphQL API を介してコマースサービスを統合する場合に推奨される統合パターンです。このパターンでは、AEM の柔軟性を最大限に活かして、複数のデバイスでリッチメディアのサイトデザインをカスタマイズできます。この統合パターンは、CIF 標準ソリューションとしてサポートされています。


### 統合パターン 2 {#integration-pattern-two}

このパターンは、コンテンツやコマースを完全にヘッドレスに配信する方法を表しています。配信は完全にクライアントサイドです。このパターンのコンテンツは API 経由で配信され、HTML とコマースのデータは GraphQL 経由で配信されます。このパターンは、CIF では標準でサポートされていません。


### 統合パターン 3 {#integration-pattern-three}

このパターンでは、Magento がエクスペリエンスを提供し、AEM がオーサリングしたコンテンツを埋め込みます。AEM で作成したコンテンツは、エクスペリエンスフラグメントまたはコンテンツフラグメントを介して配信できます。この統合パターンにはプロジェクト固有の作業が必要であり、CIF ですぐに実装することはできません。


### 統合パターン 4 {#integration-pattern-four}

これは、エクスペリエンスレイヤーまたはプレゼンテーションレイヤーが AEM とコマースソリューションの間で分割される一般的な統合パターンです。通常、コマースソリューションがチェックアウトやマイアカウントなどのマーケティング以外のページを提供し、AEM がマーケティングページとストアフロントカタログエクスペリエンスを提供します。このパターンでは、ユーザーエクスペリエンスが不統一になるのを避けるために、買い物かごとユーザーセッションが 2 つのシステムの間で適切に処理されるようにする必要があります。例えば、Magento は買い物かごとユーザーセッションを Cookie に保存し、AEM と Magento 間で共有できます。このパターンにはプロジェクト固有の作業が必要でありと、CIF ですぐに実装することはできません。
