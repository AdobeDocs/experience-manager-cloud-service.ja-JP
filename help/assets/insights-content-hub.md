---
title: Content Hubでのアセットインサイトの表示
description: ' [!DNL Content Hub] でアセットインサイトを表示する方法を説明します。'
role: User
exl-id: 29cbe017-856d-486b-acf3-aa47dbd90f3f
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 5%

---

# [!DNL Content Hub] のAssets Insights {#assets-insights}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Assets インサイト ](assets/asset-insights-banner.jpg)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

[!DNL Content Hub] は、マーケティングキャンペーン、チャネル、様々な地域で使用されるアセットの使用状況統計など、マーケティング関係者が頻繁に発生する一般的な課題に対処し、アセットに関する貴重なインサイトを提供します。 アセットのパフォーマンスと人気を明確に理解することで、ユーザーエクスペリエンスの向上に不可欠な実用的なインサイトを提供します。

## 前提条件 {#prerequisites}

[Content Hub ユーザー ](deploy-content-hub.md#onboard-content-hub-users) は、この記事で説明されるアクションを実行できます。

## アップロードしたアセットの統計の表示{#view-statistics-for-uploaded-assets}

「**[!UICONTROL インサイト]**」タブに移動すると、アップロードされたアセットとコレクションの統計を表示できます。 年次、月次、日次のアセットアップロード表示で、アセットのアップロード履歴を追跡します。

![ アセット統計のアップロード ](assets/assets-insights.jpg)

<!-- You can track the upload history of your assets over the past 30 days or gain a more comprehensive view with data spanning the last 12 months. This feature enables you to evaluate the upload count of assets.  -->

<!-- Go to the **[!UICONTROL [!DNL Insights]]** tab.

2. Select the desired time frame to view the statistics; you can opt for either last 30 days or last 12 months.

Data for the selected time frame is displayed, including the upload count for the specified duration. -->

## 詳細な統計分析の表示{#view-detailed-statistical-analysis}

Content Hubでは、ファイル形式、キャンペーン、チャネル、地域に基づいて、アセット数の統計を表示できます。 十分な情報に基づいた意思決定や戦略的計画を促進する、アセット配布に関する貴重なインサイトを得ることができます。

この表は、様々なアセットの詳細な概要を、それらの数やリポジトリ内のそれぞれの割合も含めて示しています。 列サイズを調整し、アセット名、カウント、割合でアセットを並べ替えることができます。

円グラフは、アセットの合計数をファイル形式で視覚的に表し、個々のアセットの数とそれに対応する割合を明確に示します。

![ アセットタイプ統計別のアセット数 ](assets/insights-categorial-view.jpg)

以下を表示することもできます。

* **日と月ごとのアクティブユーザー**：アクティブユーザーの数（日または月ごとに）が折れ線グラフで表示されます。
* **[!UICONTROL キャンペーン別Assets]**: キャンペーンに基づいたアセット数とそれぞれの割合。
* **[!UICONTROL チャネル別のAssets]**：アセット数と、使用されているチャネルに基づくそれぞれのパーセンテージ。
* **[!UICONTROL 地域別のAssets]**：アセット数と、アセット使用の地域に基づくそれぞれの割合。
