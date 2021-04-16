---
title: コマース統合フレームワークを使用した AEM とサードパーティのコマース統合
description: 大規模法人では、ストアフロントを強化するために、追加のサードパーティ製コマースソリューションが必要になる場合があります。I/O Runtime を使用してサードパーティのコマースソリューションを Adobe Experience Manager に接続する場合、コマース統合フレームワーク（CIF）をこのような統合シナリオで使用できます。
thumbnail: cif-third-party-architecture.jpg
exl-id: 42dd8922-540d-4a93-9e45-b5e83dc11e16
translation-type: tm+mt
source-git-commit: c0a79d9ffefba06b64d48aed79e9a00baa4987df
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 20%

---

# コマース統合フレームワークを使用した AEM とサードパーティのコマース統合 {#aem-third-party}

非Adobeコマースソリューションの統合は、CIFの一般的なシナリオです。 様々なAPIやスキーマを使用するサードパーティのソリューションは、統合レイヤーを介して接続できます。

## アーキテクチャ {#architecture}

全体的なアーキテクチャは次のとおりです。

![AEM と Magento 以外またはサードパーティとの統合アーキテクチャの概要](../assets//AEM_nonMagento_Architecture.png)

この統合レイヤーの目的は、サードパーティのAPIとスキーマを、サポートされているAdobeCommerce GraphQL APIおよびExperience Manager外のスキーマに対してマッピングすることです。 このカプセル化により、Experience Manager内のコードを変更せずに、統合ロジックとシステムを更新できます。

## 統合のソリューション要件

Experience Managerがオンデマンドでデータを取得する際には、商品カタログのリアルタイムAPIが必要です。

>[!TIP]
>
>リアルタイムAPIが使用できない場合は、APIを使用した外部製品キャッシュを統合に使用する必要があります。 例[Magentoオープンソース](https://magento.com/products/magento-open-source)

完全なGraphQLスキーマを実装する必要はありません。必要なユースケースを有効にするには、スキーマのオブジェクトだけを使用します。

## バックエンドの使用例

CIFは、リアルタイムの商品カタログアクセスおよび商品体験管理ツールでExperience Managerを拡張します。 このシームレスな統合により、作成者は、コンテンツのコンテキストを離れることなく、必要に応じて埋め込みUIを使用してコマースデータにアクセスできます。

これらのユースケースのロックを解除するには、製品カタログAPIの統合が必要です。

## フロントエンドの使用例

[AEM CIFコア](https://github.com/adobe/aem-core-cif-components) コンポーネントは、CIFでサポートされているAdobeコマースAPIを使用してデータを取得および交換します。コンポーネントを再利用するには、それぞれのAPIを実装する必要があります。

パフォーマンスに重要なクライアント側のコンポーネントは、遅延を回避するために、サードパーティのソリューションと直接通信することをお勧めします。

## 統合の開発{#develop-integration}

統合レイヤーには[Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)を使用することをお勧めします。 これは、サードパーティのCIFアドオンに含まれます。 マイクロサービスに似たアプローチで機能するので、複数のソリューションを容易に統合するのに適しています。

[リファレンス実装](https://github.com/adobe/commerce-cif-graphql-integration-reference)は、コマースソリューションへの統合を構築するための最初のポイントです。 GraphQLをサポートしますが、RESTなど他のタイプのAPIと統合することもできます。

この統合レイヤーは、サードパーティのレイヤー（Mulesoftなど）が使用可能な場合や、統合がサードパーティのソリューションの上に構築される場合には必要ありません。
