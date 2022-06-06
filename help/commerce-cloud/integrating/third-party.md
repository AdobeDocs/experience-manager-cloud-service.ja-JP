---
title: コマース統合フレームワークを使用した AEM とサードパーティのコマース統合
description: 大規模法人では、ストアフロントを強化するために、追加のサードパーティ製コマースソリューションが必要になる場合があります。I/O Runtime を使用してサードパーティのコマースソリューションを Adobe Experience Manager に接続する場合、コマース統合フレームワーク（CIF）をこのような統合シナリオで使用できます。
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c,42dd8922-540d-4a93-9e45-b5e83dc11e16
source-git-commit: a53ef07cd9da636c8d938c711de6defb9eb8e05f
workflow-type: ht
source-wordcount: '520'
ht-degree: 100%

---

# コマース統合フレームワークを使用した AEM とサードパーティのコマース統合 {#aem-third-party}

Adobe Commerce 以外のソリューションの統合は、CIF の一般的なシナリオです。様々な API やスキーマを持つサードパーティソリューションは、統合レイヤーを介して接続できます。

## アーキテクチャ {#architecture}

全体的なアーキテクチャは次のとおりです。

![AEM と Magento 以外またはサードパーティとの統合アーキテクチャの概要](../assets//AEM_nonMagento_Architecture.png)

この統合レイヤーの目的は、サードパーティの API とスキーマを、サポートされている Adobe Commerce GraphQL API と Experience Manager 外のスキーマにマッピングすることです。このカプセル化により、統合のロジックとシステムを、Experience Manager 内のコードを変更することなくアップデートできます。

## 統合のソリューション要件

Experience Manager はデータをオンデマンドで取得するため、製品カタログのリアルタイム API が必要です。

>[!TIP]
>
>リアルタイム API を使用できない場合は、API を使用した外部製品キャッシュを統合に使用する必要があります。例：[Magento オープンソース](https://magento.com/products/magento-open-source)

完全な GraphQL スキーマを実装する必要はありません。必要なユースケースを有効にするには、スキーマのオブジェクトだけを実装します。

## バックエンドの使用例

CIF は、製品カタログへのリアルタイムのアクセスと製品エクスペリエンス管理ツールで Experience Manager を拡張しています。このシームレスな統合により、作成者は、必要に応じて、コンテンツのコンテキストを離れることなく、組み込み UI を使用してコマースデータにアクセスできます。

これらのユースケースを可能にするには、製品カタログ API の統合が必要です。

## フロントエンドの使用例

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、CIF でサポートされている Adobe Commerce API を使用してデータを取得および交換します。コンポーネントを再利用するには、それぞれの API を実装する必要があります。

パフォーマンスが重要なクライアントサイドコンポーネントでは、サードパーティソリューションと直接通信して遅延を回避することが推奨されます。

## 統合の開発 {#develop-integration}

統合レイヤーには [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) を使用することをお勧めします。これは、サードパーティ用の CIF アドオンに含まれています。マイクロサービスに似たアプローチがとられており、簡単に複数のソリューションを統合するのに適しています。

[参照実装](https://github.com/adobe/commerce-cif-graphql-integration-reference)は、コマースソリューションへの統合を構築するための出発点として最適です。GraphQL がサポートされていますが、REST などの他のタイプの API と統合することもできます。

この統合レイヤーは、サードパーティのレイヤー（Mulesoft など）が使用可能な場合や、統合がサードパーティのソリューションの上に構築される場合には必要ありません。

## 事前定義済みコネクタ {#connectors}

コネクタは、プロジェクトの良い出発点となります。これには、コマースソリューション固有の接続とデフォルトの API マッピングが付属しています。これらのコネクタは、サードパーティによって作成されており、アドビで維持管理されているわけではありません。詳しくは、それぞれのパートナーに問い合わせください。

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris)（Diconium が作成）
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)（Diconium が作成）

>[!TIP]
>
>コネクタは、プロジェクトでコマース統合を速めるのに役立ちますが、プラグアンドプレイではありません。エンタープライズコマースソリューションは通常、大幅にカスタマイズされており、カスタム統合が必要になります。コマースプラットフォーム、Adobe Commerce GraphQL スキーマおよび Adobe I/O Runtime に関する十分な知識が必要です。
