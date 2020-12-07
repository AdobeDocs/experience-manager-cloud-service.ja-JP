---
title: Java APIのガイドライン
description: AEMは、多くのJava APIを公開するリッチなオープンソースソフトウェアスタック上で構築されています。
translation-type: tm+mt
source-git-commit: b927992107d7e7e4df5511a366c71449ff73ec93
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 6%

---


# Java APIガイドライン{#java-api-guidelines}

Adobe Experience Manager(AEM)は、開発中に使用する多くのJava APIを公開する、リッチなオープンソースソフトウェアスタック上に構築されています。

AEMは、次の4つの主要なJava APIセットを優先順に基づいて構築されています。

1. **Adobe Experience Manager(AEM)**  — ページ、アセット、ワークフローなどの製品概念。
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - RESTおよびリソースベースの抽象概念（リソース、値マップ、HTTP要求など）。
1. **[JCR(Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)**  — ノード、プロパティ、セッションなどのデータおよびコンテンツの抽象概念。
1. **[OSGi(Apache Felix)](https://felix.apache.org)**  — サービスや(OSGi)コンポーネントなどのOSGiアプリケーションコンテナ抽象概念。

APIがAEMで提供される場合は、Sling、JCR、OSGiよりも優先します。 AEMがAPIを提供しない場合は、JCRやOSGiよりSlingを好みます。

これらのガイドラインの詳細については、「[Java APIのベストプラクティスについて」のドキュメントを参照してください。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
