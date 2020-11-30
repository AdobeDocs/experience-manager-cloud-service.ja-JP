---
title: コマース統合フレームワークを使用した AEM とサードパーティのコマース統合
description: 大規模法人では、ストアフロントを強化するために、追加のサードパーティ製コマースソリューションが必要になる場合があります。I/O Runtimeを使用してサードパーティのコマースソリューションをAdobe Experience Managerに接続する場合、Commerce Integration Framework(CIF)をこのような統合シナリオで使用できます。
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 92%

---


# コマース統合フレームワークを使用した AEM とサードパーティのコマース統合 {#aem-third-party}

大規模法人では、ストアフロントを強化するために、追加のサードパーティ製コマースソリューションが必要になる場合があります。コマース統合フレームワーク（CIF）は、Magento に加えてサードパーティ製のコマースソリューションも AEM と統合する必要がある場合に使用できます。CIF には、アクセラレーター参照ストアフロント、AEM CIF コアコンポーネント、オーサリングツールなど、デフォルト設定で Magento と連携できる要素が用意されています。AEM とサードパーティ製コマースソリューションを統合し、これらの CIF 要素を再利用するには、追加の開発が必要です。

## アーキテクチャ {#architecture}

全体的なアーキテクチャは次のとおりです。

![AEM と Magento 以外またはサードパーティとの統合アーキテクチャの概要](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

AEM - Magento と AEM - サードパーティ製コマースソリューションの統合アーキテクチャの主な違いは、上図に示すように、統合およびデータ変換レイヤーが追加されていることです。統合レイヤーは、アドビのサーバーレスプラットフォームであるAdobe I/O Runtime プラットフォームでホストする必要があります。Adobe I/O Runtime について詳しくは、[こちら](https://www.adobe.io/apis/experienceplatform/runtime.html)を参照してください。

この統合レイヤーの目的は、Magento 以外またはサードパーティの API を Adobe コマース API（Magento GraphQL API）に対してマッピングすることです。このマッピングにより、[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components) と CIF オーサリングツールで、Magento 以外のソリューションからデータを取得できるようになります。このアプローチを使用すると、統合レイヤーは統合ロジックをカプセル化し、AEM とサードパーティ製ソリューションの間で関心事の分離をおこないます。その結果、様々なサードパーティ製ソリューションで、一貫した方法で CIF 要素を使用できるようになります。プロジェクトで CIF 要素を使用する利点については、[AEM Commerce as a Cloud Service の概要](/help/commerce-cloud/overview.md)を参照してください。

## 統合の開発 {#develop-integration}

Magento 以外またはサードパーティのソリューションと AEM を統合するために必要な統合レイヤーの作成を開始しやすいように、[参照実装](https://github.com/adobe/commerce-cif-graphql-integration-reference)をデモとして作成し提供しています。この参照実装をプロジェクトの出発点にすることができます。
