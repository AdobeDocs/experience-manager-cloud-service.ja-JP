---
title: 'AEM Commerce Integration Framework（CIF）の概要 '
description: Experience Manager コンテンツおよびCommerce as a Cloud ServiceをCIFと共に使用および管理する方法を説明します。
thumbnail: introducing-aem-commerce.jpg
feature: Commerce Integration Framework
role: Admin
exl-id: 3f18f976-ff8a-4726-b4c5-db4e19ae7cee
source-git-commit: e707bddc17208d599491d27c5bc0134cb41233e0
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 61%

---


# AEM Commerce Integration Framework（CIF）の概要  {#cif-intro}

コマースソリューションは、Adobe Commerce Cloud などの商用ソリューションから一連のカスタムコマースサービスまで、何でもかまいません。この統合は、ユースケースとエコシステムに大きく依存しています。 通常は、様々なシステムに影響し、様々な種類があります。

* 複雑で動的なエコシステムの統合（製品カタログなど）
* 企業は、製品コンテンツを独自のライフサイクルで効率的かつオムニチャネル方式で管理する必要があります
* 様々な個人に対応する複雑でパーソナライズされたショッピングジャーニーの構築
* バックエンドとフロントエンドで迅速に適応および革新できる能力
* 統合検索やキャッシュ管理など、ピークパフォーマンス（フラッシュセール、ブラックフライデーなど）に対応できる、拡張性と安定性に優れた E2E インフラストラクチャの実行

こうした複雑が、潜在的な障害点、TCO の増加、遅延、価値実現の低下の原因になります。これらの理由により、Experience Manager のアドオンである Commerce Integration Framework（CIF）が開発されました。CIF は、Experience Manager にコマース機能を追加するもので、コマースエンジンとの統合を標準化します。その結果、TCO （総所有コスト）を削減し、将来性のある、安定した拡張性の高いソリューションが実現します。 それを利用すれば、俊敏性の高いツールおよびシームレスに統合された機能で技術とビジネスのイノベーションを切り拓いて、魅力的なコマースエクスペリエンスを構築できます。

![CIF 要素](./assets/CIF/CIF_Overview.png)

## CIF の利点 {#cif-benefits}

CIF には、カスタムコードの必要性を軽減する標準搭載のコマースコアコンポーネントが用意されているので、ブランドが市場投入までの時間を短縮できます。すべてのコアコンポーネントは、アドビのクライアントサイドデータレイヤーと標準で統合されており、統合プロファイルなどの顧客プロファイルを改善します。このプロファイルには、訪問者の行動が詳細にとらえられているので、カスタマージャーニーをリアルタイムで予測およびパーソナライズする目的で使用できます。

CIF アドオンは、Experience Manager に製品コンテキストを導入し、製品コンソールや製品／カテゴリピッカーなどのオーサリングツールを提供します。これらのツールをマーケターが利用すれば、開発者に頼らずに Experience Manager でショッパブルエクスペリエンスを作成して提供できます。以下のような利点があります。

* [魅力的なエクスペリエンス](#experiences)
* [迅速な価値創出](#ttv)
* [堅牢な統合](#integrations)

### エクスペリエンス {#experiences}

AEM の強力な CIF ツールを使用すると、コンテンツ作成者は、配信にとらわれない拡張可能な形で、機能豊富なパーソナライズされたコマースエクスペリエンスを迅速に構築して、ビジネスチャンスを十分に生かすことができます。

![CIF 要素](./assets/CIF/CIF_Product_Experience_Management.png)

### 価値創出までの時間（TTV） {#ttv}

CIFは、[AEM コアコンポーネント ](https://www.aemcomponents.dev/)、[AEM Venia 参照ストアフロント ](https://github.com/adobe/aem-cif-guides-venia)、[AEM プロジェクトアーキタイプ ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)、PWA （プログレッシブ web アプリ）の統合パターン（ヘッドレスコンテンツおよびコマース）などで、プロジェクトの開発を促進します。

CIFは、常に最新のアドオンを使用した継続的なイノベーションを目的として構築されており、新機能や改善された機能にアクセスできます。

### 統合 {#integrations}

[Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)、マイクロサービスベースのサーバーレス PaaS、[CIF の参照実装](https://github.com/adobe/commerce-cif-graphql-integration-reference)などを使用して、エコシステム（例：コマースソリューション）を Experience Cloud に接続します。

## 実証済みのパターンとベストプラクティス {#proven}

CIFは、ベストプラクティスに基づく標準化された統合パターンでユーザーをサポートします。 これにより、現在のビジネスを成功に導き、ビジネスの成長に合わせて拡張でき、将来の要件にも柔軟に対応できるようになります。

* 製品カタログの統合に関して、次のような一般的な問題が発生する可能性があります。
   * カタログの量や複雑さの増大に伴ってパフォーマンスが低下
   * ステージング済みデータにアクセスできない
   * リアルタイムの製品データおよびエクスペリエンスが必要
* デジタル成熟度が高まると、エクスペリエンス管理が必要になります
* 
   * CIF には、追加の IT 作業を行わずに増分的に組み込むことができる製品エクスペリエンス管理機能が付属しています。
* オムニチャネルへの準備完了
   * CIFは、パターン、アクセラレーター、コアコンポーネントで様々なタッチポイントテクノロジー（サーバーサイド、ハイブリッド、クライアントサイド）をサポートしています。

## ジャーニー {#journey}

コマースジャーニーを続けている場合は、次の手順に進んでください。

* [AEM コンテンツ作成者ジャーニー](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/getting-started.md)
