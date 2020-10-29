---
title: Commerce Integration Frameworkを使用したAEMとサードパーティのコマース統合
description: エンタープライズビジネスでは、ストアフロントを強化するために、追加のサードパーティコマースソリューションが必要になる場合があります。 I/O Runtimeを使用してサードパーティのコマースソリューションをAdobe Experience Managerに接続する場合、Commerce Integration Framework(CIF)をこのような統合シナリオで使用できます。
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---


# Commerce Integration Frameworkを使用したAEMとサードパーティのコマース統合 {#aem-third-party}

エンタープライズビジネスでは、ストアフロントを強化するために、追加のサードパーティコマースソリューションが必要になる場合があります。 Commerce Integration Framework(CIF)は、Magentoに加えて、サードパーティのコマースソリューションもAEMと統合する必要がある場合に使用できます。 CIFには、アクセラレーターリファレンスストアフロント、AEM CIFコアコンポーネント、および標準搭載のMagentoで機能するオーサリングツールなどの要素が用意されています。 AEMとサードパーティのコマースソリューションを統合し、これらのCIF要素を再利用するには、追加の開発が必要です。

## アーキテクチャ {#architecture}

アーキテクチャ全体を次に示します。

![AEM非Magento/サードパーティアーキテクチャの概要](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

AEMとAEMのMagento — サードパーティのコマースの統合アーキテクチャの主な違いは、上の図に示すように、統合とデータ変換レイヤーを追加することです。 統合レイヤーは、AdobeのサーバーレスプラットフォームであるAdobe I/O Runtimeプラットフォームでホストする必要があります。 Adobe I/O Runtimeの詳細は [こちら](https://www.adobe.io/apis/experienceplatform/runtime.html)。

この統合レイヤーの目的は、非MagentoまたはサードパーティのAPIをAdobeコマースAPI(MagentoGraphQL API)に対してマッピングすることです。 このマッピングにより、 [AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components) 、およびCIFオーサリングツールで、Magento以外のソリューションからデータを取得できます。 このアプローチを使用すると、統合レイヤーは統合ロジックをカプセル化し、AEMとサードパーティのソリューションとの間に問題を分離します。 これにより、さまざまなサードパーティのソリューションで、CIF要素を不可知の方法で使用できます。 プロジェクトでCIF要素を使用する利点は、 [概要](/help/commerce-cloud/overview.md)。

## 統合の開発 {#develop-integration}

AEMに非Magento/サードパーティのソリューションを統合するために必要な統合レイヤーの構築を開始する際に役立つように、 [リファレンス実装を作成し](https://github.com/adobe/commerce-cif-graphql-integration-reference) 、これを実証します。 この参照は、プロジェクトの開始点として使用できます。
