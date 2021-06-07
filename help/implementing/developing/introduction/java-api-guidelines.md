---
title: Java API ガイドライン
description: AEM は、使用可能な多数の Java API を公開する豊富なオープンソースソフトウェアスタックに基づいて構築されています。
exl-id: 0be33ec9-a4c3-4400-99d3-ed8366c5b5f9
source-git-commit: a446efacb91f1a620d227b9413761dd857089c96
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 100%

---

# Java API ガイドライン {#java-api-guidelines}

Adobe Experience Manager（AEM）は、開発時に使用可能な多数の Java API を公開する豊富なオープンソースソフトウェアスタックに基づいて構築されています。

AEM は、優先順に次の 4 つの主要な Java API セットに基づいて構築されています。

1. **[Adobe Experience Manager（AEM）](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service-javadoc/index.html)** - 製品の抽象概念（ページ、アセット、ワークフローなど）。
1. **[Apache Sling Web フレームワーク](https://sling.apache.org/apidocs/sling11/)** - REST およびリソースベースの抽象概念（リソース、値マップ、HTTP リクエストなど）。
1. **[JCR（Apache Jackrabbit Oak）](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)** - データおよびコンテンツの抽象概念（ノード、プロパティ、セッションなど）。
1. **[OSGi（Apache Felix）](https://felix.apache.org)** - OSGi アプリケーションコンテナの抽象概念（サービスや（OSGi）コンポーネントなど）。

AEM が API を提供する場合は、それを Sling、JCR、OSGi よりも優先します。AEM が API を提供しない場合は、Sling を JCR や OSGi よりも優先します。

これらのガイドラインについて詳しくは、[Java API のベストプラクティスについて](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=ja)を参照してください。
