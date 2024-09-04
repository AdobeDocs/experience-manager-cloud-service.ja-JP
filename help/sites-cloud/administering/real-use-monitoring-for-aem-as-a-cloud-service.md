---
title: AEM as a Cloud Service の実際の使用のモニタリング
description: Real Use Monitoring （RUM）を使用して、web サイトやアプリケーションのデジタルユーザーエクスペリエンスをリアルタイムでキャプチャおよび分析する方法を説明します。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 917e9496dcbb8c6fe72b7a718211ee5bbecb3323
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 14%

---

# AEM as a Cloud Serviceの Real-Use モニタリングサービス {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Real Use Monitoring サービスは、クライアントサイドのデータ収集であり、自動化されたサービスです。 顧客設定は必要ありません。

>[!INFO]
>
>クライアントサイド監視は、AEM（Adobe Experience Manager）Cloud Serviceバージョン **2024.5.16461** 以降を使用しているお客様に対してのみ機能します。

## 概要 {#overview}

RUM （Real Use Monitoring）サービスは、Web サイトやアプリケーションのデジタル・ユーザー・エクスペリエンスをリアルタイムでキャプチャし、分析するパフォーマンス監視技術です。 Web アプリケーションのリアルタイムパフォーマンスを可視化し、エンドユーザーエクスペリエンスに関するより深いインサイトを提供します。 このサービスは、ユーザー自身ではなく web サイトのエンゲージメントを監視することで、パフォーマンスを最適化することに焦点を当てています。

RUM を使用すると、URL の開始からリクエストがブラウザーに返されるまで、主要なパフォーマンス指標が追跡されます。 これにより、開発者はアプリケーションを強化して、エンドユーザーが簡単に使用できるようになります。

>[!INFO]
>
>「実際のユーザー監視」は、サービスの真の本質をより適切に反映するため、「実際の使用監視」にブランド変更されました。

## 実際の使用状況の監視サービスのメリットを享受できるのは誰か {#who-can-benefit-from-rum-service}

AEMは、お客様やAdobeがAEM サイトとのやり取りを理解するのに役立つ RUM を開発しました。 RUM を使用すると、パフォーマンスの問題を診断し、実験の有効性を測定できます。 RUM は、サンプリングを通じて訪問者のプライバシーを保持します。つまり、すべてのページビューのごく一部のみが監視され、個人を特定できる情報（PII）は収集されません。

## Real Use Monitoring サービスとプライバシー {#rum-service-and-privacy}

AEMの Real Use Monitoring サービスは、訪問者のプライバシーを保護し、データ収集を最小限に抑えるように設計されています。 訪問者として、それはあなたが訪問しているサイトまたはAdobeに利用可能になったサイトが個人情報を収集しないことを意味します。

サイトオペレーターは、この機能を通じた監視を有効にするために追加のオプトインは必要ありません。 RUM を有効にするためにエンドユーザーが受け入れるための追加のポップアップまたは同意フォームはありません。

## Real Use Monitoring サービスのデータ・サンプリング {#rum-service-data-sampling}

従来の web 分析ソリューションでは、すべての訪問者に関するデータを収集しようとします。AEM RUM サービスは、ほんの一部のページビューから情報を取得するだけです。 このサービスは、分析の代わりではなく、サンプリングおよび匿名化されることを目的としています。 デフォルトでは、ページのサンプリング比は 1:100 です。 現時点では、サイト演算子はサンプリングレートを増減できません。 合計トラフィックを正確に推定するために、100 回のページビューごとに 1 からデータが収集され、全体的なトラフィックの信頼性の高い概算が得られます。

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

実際の使用状況の監視では、クライアントサイドのトラフィックが自動的に監視され、有益なインサイトが得られます。 Adobeのお客様は、このサービスが既存の設定にシームレスに統合されているので、追加の手順を実行する必要はありません。 一般提供（GA）ロールアウトでは、この新機能のメリットが自動的に得られます。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Real Use Monitoring Service データの使用方法 {#how-rum-service-data-is-being-used}

RUM データは、次の目的で有益です。

* お客様のサイトに対してパフォーマンスのボトルネックを特定および修正する
* ページビューを含む自動トラフィック検索を効率化する。
* 互換性を向上させるために、AEMが同じページ上の他のスクリプト（分析、ターゲティング、外部ライブラリなど）とどのようにやり取りするかを理解する。

## ページビュー数とパフォーマンス指標の制限事項と相違について {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

RUM データを分析する際、ページビューやその他のパフォーマンス指標に違いが生じる場合があります。 これらの差異は、リアルタイムのクライアントサイドのモニタリングに固有のいくつかの要因に起因する可能性があります。お客様が RUM データを解釈する際に留意すべき重要な考慮事項を以下に示します。

1. **トラッカーブロッカー**

   * トラッカーブロッカーやプライバシー拡張機能を使用するエンドユーザーは、これらのツールがトラッキングスクリプトの実行を制限するので、RUM データ収集を妨げる可能性があります。 この制限により、報告が少ないページビューやユーザーのインタラクションが生じ、実際のサイトアクティビティと RUM によって取り込まれるデータとの間に不一致が生じる可能性があります。

1. **ヘッドレス API/JSON 呼び出しのキャプチャに関する制限事項**

   * RUM データサービスはクライアントサイドのエクスペリエンスに重点を置いており、現時点では、AEM以外のヘッドレスアプリから行われたバックエンド API または JSON 呼び出しを取得しません。 RUM サービスデータからのこれらの呼び出しを除外すると、CDN Analytics によって測定されたコンテンツリクエストとの相違が生じます。

## FAQ {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the RUM service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **「次のペイントへのインタラクション」、「最初のバイトまでの時間」、「最初の内容を含むペイント」の web バイタルメトリクスは収集されていますか？**

   次のペイントまでのインタラクション（INP）と最初のバイトまでの時間（TTFB）が収集されます。  現時点では、コンテンツの初回ペイント（FCP）は収集しません。

1. **サイトで `/.rum` パスがブロックされています。修正する方法を教えてください。**

   RUM コレクションが機能するには、`/.rum` のパスが必要です。 AdobeのAEM as a Cloud Serviceの前で CDN を使用している場合は、`/.rum` パスが他のAEM コンテンツと同じAEM オリジンに転送されることを確認します。 また、いかなる方法でも調整されないようにしてください。

1. **RUM コレクションは、契約上の目的でコンテンツリクエストにカウントされますか？**

   RUM ライブラリと RUM コレクションは、コンテンツリクエストとしてカウントされず、レポートされるページビュー数や API 呼び出し数を増やしません。 さらに、AEM as a Cloud Serviceに標準搭載の CDN を使用する場合は、[ サーバーサイド収集 ](#serverside-collection) がコンテンツリクエストの基盤になります。

1. **オプトアウトするにはどうすればよいですか？**

   Adobeでは、大きなメリットがあり、デジタルエクスペリエンスを最適化できるので、Real Use Monitoring （RUM）を使用することをお勧めします。 Web サイトのパフォーマンスの向上に役立つ貴重なインサイトを提供できます。 このサービスはシームレスに動作するように設計されており、Web サイトのパフォーマンスには影響しません。

   オプトアウトするということは、これらのインサイトが欠落していることを意味します。 ただし、問題が発生した場合は、Adobeサポートにお問い合わせください。
