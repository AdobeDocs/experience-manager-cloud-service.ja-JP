---
title: Cloud ServiceとしてのAEMコマースの概要
description: Cloud ServiceとしてのExperience Managerコマースは、Commerce Integration Framework(CIF)で構成されます。これは、Magentoおよび他のサードパーティのコマースソリューションのコマースサービスをExperience Cloudと統合および拡張するためのAdobeの推奨パターンです。
thumbnail: introducing-aem-commerce.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 2%

---


# Introducing AEM Commerce as a Cloud Service {#commerce-intro}

Cloud ServiceとしてのExperience Managerコマースは、Commerce Integration Framework(CIF)で構成されます。これは、Magentoおよび他のサードパーティのコマースソリューションのコマースサービスをExperience Cloudと統合および拡張するためのAdobeの推奨パターンです。 これにより、Adobeのお客様は、最先端のテクノロジーに基づく、個々の顧客に合わせた卓越した買い物体験を提供できます。

Commerce Integration Frameworkは、Cloud ServiceとしてのExperience Manager用のアドオンモジュールで、Cloud ServiceとコマースのソリューションとしてのExperience Manager間の統合の開発を促進するための一連のオーサリングツール、コンポーネント、リファレンスストアフロントを提供します。

## CIFの利点 {#cif-benefits}

主な利点は次のとおりです。

* 統合は、複数のシステムとの統合を標準化およびカプセル化する抽象レイヤーです。

* CIFはheadless/omnichannelエクスペリエンスをサポートします。

   * 単一ページアプリと複数ページアプリ
   * GraphQLエンドポイント

* CIFは、カスタマイズやコマースサービスの拡張を行うための、サーバレスのマイクロサービスベースのプロセスとビジネスロジックレイヤーを提供します。

* CIFは、AEMやMagentoなどのAdobeソリューションとの統合を標準搭載

## CIF要素 {#cif-elements}

![CIF要素](/help/commerce-cloud/assets/cif-overview1.jpg)


### オーサリングツール用CIFアドオン {#add-on-authoring-tools}

CIFアドオンを使用すると、製品コンソール、製品とカテゴリの選択、または作成者の製品検索など、コマースオーサリングツールにアクセスして、マーケティングやコマースのコンテンツで豊富なエクスペリエンスを作成できます。 アドオンは、GraphQLを介してMagento（または代替コマースシステム）へのバックエンド接続も管理します。 アドオンがプロビジョニングされると、AEM環境としてCloud Serviceに自動的にデプロイされます。

### AEM CIFコアコンポーネント {#aem-cif-core}

AEM CIFコアコンポーネントは、MagentoのGraphQLサポートを持つサーバー側およびクライアント側のレンダリングコンポーネントです。 AEMテクノロジーを基に静的でキャッシュ可能でSEOに優しい商取引ストアを作るのに使われます

基本的なコンポーネントが提供され、製品の詳細、製品のリスト、ナビゲーション、検索など、コマースの実装間で共通です。 そのまま使用することも、拡張することもできます。

AEM CIFコアコンポーネント [(](https://github.com/adobe/aem-core-cif-components) CIF Core Components [)は](https://github.com/adobe/aem-core-wcm-components) AEM Sitesコアコンポーネントと同様に機能しますが、コマース固有の使用例に特化したものです。

次のコンポーネントの主な利点があります。

* プロジェクトでは簡単に使用できます。
* 現状のまま、または最小限の変更で使用できます。
* GraphQL APIまたはREST APIを使用したMagentoとの接続に関するベストプラクティスを提供します

AEM作成者がAEMでマーケティングコンテンツとコマースコンテンツを組み合わせてエクスペリエンスページを作成できるように、製品ティーザーや製品カルーセルなどのコンポーネントが用意されています。 これらのコンポーネントは、AEMで作成されたコンテンツページに簡単にドラッグ&amp;ドロップでき、Cloud Serviceの製品やカテゴリ選択などのCIFオーサリングツールを使用して特定の製品やカテゴリにリンクできます。

すべてのコンポーネントはGitHub上にオープンソースで [す](https://github.com/adobe/aem-core-cif-components)。 これにより、今後行われる変更に対する完全な透明性が示され、最新バージョンを簡単に入手できます。 また、改善点やバグ修正のプルリクエストを組み込むこともできます。

### AEM Venia Storefront {#aem-venia-storefront}

AEM [Venia Storefront](https://github.com/adobe/aem-cif-guides-venia) は、B2Cコマースの基本的な遍歴を紹介する、製作用に適した最新のリファレンスストアフロントです。 AEM、CIF、Magentoを使用して、コマースプロジェクトを開始し、プロジェクトを高速化するために使用できます。 AEMとMagentoの統合のベストプラクティスを示し、 [AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components) と [](https://github.com/adobe/aem-core-wcm-components) AEM Sitesコアコンポーネントの使用方法を示します。また、AdobeコマースグラフQLエンドポイントをサポートします。 また、AEMとMagentoの統合をデモするためのリファレンスサイトをプリセールスに提供します。

AEM Venia Storefrontは、AEMがガラスとMagentoを所有している混在ページアプリケーションで、コマースバックエンドにヘッドレス方式で電力を供給します。 サーバー側のレンダリングとクライアント側のレンダリングの両方が、ストアフロントで使用されます。 サーバー側のレンダリングは静的コンテンツの配信に使用され、クライアント側のレンダリングは動的コンテンツの配信に使用されます。

製品ページとカタログページは比較的静的で、AEMで作成した汎用テンプレート上の製品の詳細や製品のリストなど、AEM CIFコアコンポーネントを使用してサーバー側にレンダリングされます。 これらのコンポーネントは、GraphQL APIを介してMagentoからデータを取得します。
これらのページは動的に作成され、サーバー上でレンダリングされ、AEMディスパッチャー上でキャッシュされて、ブラウザーに配信されます。
在庫や価格など、より動的な属性の場合は、クライアント側のコンポーネントが使用されます。 クライアント側のコンポーネントまたはWebコンポーネントは、GraphQL APIを介してMagentoからデータを直接取得し、コンテンツをブラウザにレンダリングします。

#### チェックアウト {#checkout}

この参照ストアフロントは、買い物かごとチェックアウトフォームをレンダリングするクライアント側の買い物かごコンポーネントを使用し、完全なエクスペリエンス統合パターンを示します。このパターンでは、Magentoが完全にヘッドレスで実行され、AEMがガラスを所有します。 提示されている抽象支払い方法を使用することをお勧めします。 これにより、Adobeクライアントは支払ゲートウェイプロバイダーと直接通信でき、MagentoクラウドもPCIの機密データを保持または受け渡すことができなくなります。

#### アカウント管理 {#account-management}

アカウント管理はMagentoによって処理され、参照ストアフロントはクライアント側のReactベースのコンポーネントを使用して、AEMが次の機能でエクスペリエンスをレンダリングできるようにします。アカウントを作成し、サインインし、パスワードを忘れた場合。

AEM Venia Storefrontプロジェクトはオープンソースで、詳しくは [AEM Venia Storefrontを参照してください](https://github.com/adobe/aem-cif-guides-venia)。

### AEM プロジェクトアーキタイプ {#aem-project-archtype}

The [AEM Project Archetype](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html) can be used to create a minimal, best-practices-based Adobe Experience Manager project as a starting point for your own AEM projects. オプションで、 [AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components) ( CIF Core Components)を新しく生成したプロジェクトに含めることができます。

### CIF拡張レイヤー {#cif-extension}

CIF拡張レイヤーは、複雑なビジネスロジックをホストする中間レイヤーです。 AdobeのサーバレスプラットフォームであるAdobe I/O Runtimeプラットフォーム上で動作します。 マイクロサービスレベルでビジネスロジックとプロセスロジックを注入することで、エンドツーエンドのサービス呼び出しを拡張できます。 例えば、場所とチャネルを使用して在庫戦略を決定する場合などがビジネスロジックです。 プロセスロジックは、例えば、パーソナライズされた情報を取得する場合などに使用します。

### CIF統合レイヤ {#cif-integration-layer}

CIF統合レイヤーは、他のコマースソリューションとの統合を標準化するために使用します。 これは、AdobeのサーバーレスプラットフォームであるAdobe I/O Runtimeプラットフォーム上で実行され、サードパーティのAPIをAdobeコマースAPIに対してマッピングすることで、マイクロサービスレベルでの統合を可能にします。 AEMとのサードパーティ製Magentoの構築を開始するために、 [](https://github.com/adobe/commerce-cif-graphql-integration-reference) リファレンス実装を作成し、AdobeコマースAPI(MagentoGraphQL API)を使用して非コマースバックエンドを統合する方法を示しました。

## AEMコマース統合パターン {#aem-commerce-integration}

一般的に実装されるAEMコマース統合パターンの一部を次に示します。

![AEM CIF統合パターン](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### 統合パターン1 {#integration-pattern-one}

これは、AEMがガラス全体を所有し、AdobeコマースGraphQL APIを介してコマースサービスを統合する場合に推奨される統合パターンです。 このパターンは、AEMの柔軟性を最大限に解除し、複数のデバイスにわたってリッチメディアサイトのデザインをカスタマイズします。 この統合パターンは、CIFが標準のソリューションとしてサポートしています。


### 統合パターン2 {#integration-pattern-two}

このパターンは、コンテンツやコマースを完全にヘッドレスに配信する方法を表しています。 配信は完全にクライアント側です。 このパターンのコンテンツはAPI経由で配信され、HTMLとコマースのデータはGraphQL経由で配信されます。 このパターンは、CIFの標準でサポートされていません。


### 統合パターン3 {#integration-pattern-three}

このパターンでは、Magentoはガラスを所有し、AEMオーサリング済みコンテンツを埋め込みます。 AEMで作成したコンテンツは、エクスペリエンスフラグメントまたはコンテンツフラグメントを介して配信できます。 この統合パターンはプロジェクト固有の作業を必要とし、CIFを使用してすぐに実装することはできません。


### 統合パターン4 {#integration-pattern-four}

これは、ガラスまたはプレゼンテーションレイヤーがAEMとコマースソリューションの間で分割される一般的な統合パターンです。 通常、コマースソリューションはチェックアウトやマイアカウントなどのマーケティング以外のページを提供し、AEMはマーケティングページとストアフロントカタログエクスペリエンスを提供します。 このパターンでは、ユーザーが別々に操作するのを避けるために、買い物かごとユーザーセッションが2つのシステムの間で適切に処理されるようにする必要があります。 例えば、Magentoは買い物かごとユーザーセッションをcookieに保存し、AEMとMagento間で共有できます。 このパターンはプロジェクト固有の作業が必要になり、CIFを使用してすぐに使用できる状態では実装できません。
