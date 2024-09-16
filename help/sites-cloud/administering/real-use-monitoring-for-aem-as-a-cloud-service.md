---
title: AEM as a Cloud Service の実際の使用のモニタリング
description: クライアントサイドのデータ収集を監視できる自動サービスである、Real Use Monitoring （RUM）について説明します。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: ed52bac52618e23b9bcbe7c6767501c6711aff00
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 13%

---

# AEM as a Cloud Serviceの Real-Use モニタリングサービス {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Real Use Monitoring サービスは、クライアントサイドのデータ収集であり、自動化されたサービスです。 顧客設定は必要ありません。

>[!INFO]
>
>クライアントサイド監視は、AEM（Adobe Experience Manager）Cloud Serviceバージョン **2024.5.16461** 以降を使用しているお客様に対してのみ機能します。

## 概要 {#overview}

RUM （Real Use Monitoring）サービスは、Web サイトまたはアプリケーション上のクライアント側トラフィックをリアルタイムで監視するパフォーマンス監視技術です。 このサービスは、ユーザー自体ではなく、web サイトのエンゲージメントを監視してパフォーマンスを最適化するための鍵となる指標とデータの収集に焦点を当てています。 RUM を使用すると、URL の開始からリクエストがブラウザーに返されるまで、主要なパフォーマンス指標が追跡されます。

## 実際の使用状況の監視サービスのメリットを享受できるのは誰か {#who-can-benefit-from-rum-service}

AEMAdobeは、エンドユーザーがAEM サイトとどのようにやり取りしているかを理解するのに役立つ、実際の使用状況のモニタリングを開発しました。 実際の使用モニタリングは、パフォーマンスの問題を診断し、実験の有効性を測定します。 リアルタイムモニタリングは、サンプリングを通じて訪問者のプライバシーを保持します。つまり、すべてのページビューのごく一部のみが監視され、個人を特定できる情報（PII）は収集されません。

## Real Use Monitoring サービスとプライバシー {#rum-service-and-privacy}

AEMの Real Use Monitoring サービスは、訪問者のプライバシーを保護し、データ収集を最小限に抑えます。 訪問者として、それはあなたが訪問しているサイトまたはAdobeに利用可能になったサイトが個人情報を収集しないことを意味します。

サイトオペレーターは、この機能を通じた監視を有効にするために追加のオプトインは必要ありません。 RUM を有効にするためにエンドユーザーが受け入れるための追加のポップアップまたは同意フォームはありません。

## Real Use Monitoring サービスのデータ・サンプリング {#rum-service-data-sampling}

従来の web 分析ソリューションでは、すべての訪問者に関するデータを収集しようとします。AEM Real Use Monitoring （RUM）サービスは、少数のページ・ビューから情報を収集するだけです。 このサービスは、分析の代わりではなく、サンプリングおよび匿名化されることを目的としています。 デフォルトでは、ページのサンプリング比は 1:100 です。 現時点では、サイト演算子はサンプリングレートを増減できません。 合計トラフィックを正確に推定するために、100 回のページビューごとに 1 からデータが収集され、全体的なトラフィックの信頼性の高い概算が得られます。

データを収集するかどうかの決定は、ページビューごとに行われるため、複数のページをまたいでインタラクションを追跡することは事実上不可能になります。 デザイン上、RUM には訪問者やセッションの概念はなく、ページビューの概念しかありません。

## 収集されるデータ {#what-data-is-being-collected}

Real Use Monitoring サービスは、個人を特定できる情報の収集を防ぐように設計されています。 RUM が収集する情報の完全なセットは次のとおりです。

* 訪問しているサイトのホスト名（例：`experienceleague.adobe.com`）
* ページの表示に使用される幅広いユーザーエージェントタイプおよびオペレーティングシステム（例：`desktop:windows` または `mobile:ios`）。
* `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)` など、データ収集の時間
* 訪問しているページの URL（例：`https://experienceleague.adobe.com/docs`）
* リファラー URL（ユーザーがリンクをたどった場合、現在のページにリンクしているページの URL）
* `2Ac6` のような形式で、ランダムに生成されたページビューの ID
* `100` など、サンプリングレートの重み付けまたはその逆つまり、100 回に 1 回のページビューのみが記録されます
* ページを読み込んだシーケンスの中の特定のイベントのチェックポイント、または名前。 または、訪問者として操作します
* 前述のチェックポイントでユーザーがやり取りする DOM 要素のソースまたは識別子。 例えば、画像を指定できます
* ターゲット（上記のチェックポイントでユーザーがやり取りする外部ページまたはリソースへのリンク）。例：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 訪問者のエクスペリエンスの品質を表す、Largest Contentful Paint （LCP）、First Input Delay （FID）、Cumulative Layout Shift （CLS）、Time to First Byte （TTFB）などの Core Web Vitals （CWV）パフォーマンス指標。

## 顧客に対するリアルタイムモニタリングの仕組み {#how-rum-works-for-a-customer}

実際の使用状況の監視では、クライアントサイドのトラフィックが自動的に監視されます。 Adobeのお客様は、このサービスが既存の設定にシームレスに統合されているので、追加の手順を実行する必要はありません。 実使用監視（RUM）は一般提供（GA）なので、この新機能のメリットを自動的に受けることができます。 実際の使用状況の監視サービスでは、ビジュアライゼーションツールを使用して現在指標を公開していません。 アドビでは、この機能をできる限り早くお客様に提供できるように取り組んでいます。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Adobeでの実際の使用状況のモニタリング {#how-rum-data-is-being-used}

実際の使用状況の監視データは、次の目的で使用されます。

* お客様のサイトに対してパフォーマンスのボトルネックを特定および修正する
* 互換性を向上させるために、AEMが同じページ上の他のスクリプト（分析、ターゲティング、外部ライブラリなど）とどのようにやり取りするかを理解する。
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their RUM data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede RUM data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by RUM.

1. **Limitations in capturing headless API/JSON calls**

   * RUM data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from RUM service data creates variances from the content requests measured by CDN Analytics.
-->

## FAQ {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the RUM service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **「次のペイントへのインタラクション」、「最初のバイトまでの時間」、「最初の内容を含んだペイント」の指標が収集されていますか？**

   次のペイントまでのインタラクション（INP）と最初のバイトまでの時間（TTFB）が収集されます。  現時点では、コンテンツの初回ペイント（FCP）は収集しません。

1. **サイトで `/.rum` パスがブロックされています。修正する方法を教えてください。**

   RUM コレクションが機能するには、`/.rum` のパスが必要です。 AdobeのAEM as a Cloud Serviceの前で CDN を使用している場合は、`/.rum` パスが他のAEM コンテンツと同じAEM オリジンに転送されることを確認します。 また、いかなる方法でも調整されないようにしてください。

1. **RUM コレクションは、契約上の目的でコンテンツリクエストにカウントされますか？**

   RUM ライブラリと RUM コレクションは、コンテンツリクエストとしてカウントされず、レポートされるページビュー数や API 呼び出し数を増やしません。 さらに、AEM as a Cloud Serviceに標準搭載の CDN を使用する場合は、[ サーバーサイド収集 ](#serverside-collection) がコンテンツリクエストの基盤になります。

1. **オプトアウトするにはどうすればよいですか？**

   Adobeでは、Real Use Monitoring （RUM）を使用すると大きなメリットがあり、Web サイトのパフォーマンスを向上させてデジタルエクスペリエンスを最適化する際にAdobeが役立つことをお勧めします。 このサービスはシームレスに動作するように設計されており、Web サイトのパフォーマンスには影響しません。

   オプトアウトは、web サイトでのトラフィックエンゲージメントを向上させる機会を逃すことを意味する場合があります。 ただし、問題が発生した場合は、Adobeサポートにお問い合わせください。
