---
title: AEM as a Cloud Service の実際の使用のモニタリング
description: クライアントサイドのデータ収集を監視できる自動化サービスである実際の使用のモニタリング（RUM）について説明します。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: f3091a3868ac57150afd6f1640709ce3e9566bac
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 95%

---

# AEM as a Cloud Service の実際の使用のモニタリングサービス {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>クライアントサイドのデータ収集である実際の使用のモニタリングサービスは、自動化されたサービスです。お客様による設定は必要ありません。

>[!INFO]
>
>クライアントサイドモニタリングは、AEM（Adobe Experience Manager）Cloud Service バージョン **2024.5.16461** 以降を使用しているお客様に対してのみ機能します。

## 概要 {#overview}

RUM（実際の使用のモニタリング）サービスは、web サイトまたはアプリケーションのクライアントサイドトラフィックをリアルタイムで監視するパフォーマンスモニタリングテクノロジーです。このサービスは、ユーザー自身ではなく、web サイトのエンゲージメントを監視することで、パフォーマンスを最適化する重要な指標とデータを収集することに焦点を当てています。RUM を使用すると、URL の開始からリクエストがブラウザーに返されるまで、主要なパフォーマンス指標が追跡されます。

## 実際の使用のモニタリングサービスは、どのようなユーザーにメリットがあるか？ {#who-can-benefit-from-rum-service}

実際の使用のモニタリングは、エンドユーザーが AEM サイトでどのようなやり取りを行っているかをお客様とアドビが理解するのに役立ちます。リアルタイムモニタリングは、限られたデータ収集とサンプリングを通じて訪問者のプライバシーを保持し、すべてのページビューのごく一部のみを監視します。

## 実際の使用のモニタリングサービスのデータサンプリング {#rum-service-data-sampling}

従来の web 分析ソリューションでは、すべての訪問者に関するデータを収集しようとします。AEM の実際の使用のモニタリング（RUM）サービスでは、ページビューのごく一部からの情報のみをキャプチャします。サービスは、分析の代替ではなく、サンプリングと匿名化を目的としています。デフォルトでは、ページのサンプリングレートは 1:100 です。現時点では、サイトオペレーターはサンプリングレートを増減できません。合計トラフィックを正確に推定するには、100 ページビューのうち 1 ページからのデータを収集し、全体のトラフィックの信頼できる近似値を提供します。

データが収集されるかどうかはページビューごとに決定されるので、複数のページ間のやり取りを追跡することは事実上不可能になります。RUM には、訪問者またはセッションの概念がなく、ページビューのみが含まれる設計となっています。

## 収集されるデータ {#what-data-is-being-collected}

Real Use Monitoring サービスは、データ収集を最小限に抑えるように設計されています。 RUM で収集される完全な情報セットを以下に示します。

* 訪問しているサイトのホスト名（例：`experienceleague.adobe.com`）
* `desktop:windows` や `mobile:ios` など、ページの表示に使用される幅広いユーザーエージェントタイプとオペレーティングシステム
* `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)` など、データ収集の時間
* 訪問しているページの URL（例：`https://experienceleague.adobe.com/docs`）
* リファラー URL（ユーザーがリンクをたどった場合、現在のページにリンクしているページの URL）
* `2Ac6` のような形式で、ランダムに生成されたページビューの ID
* `100` など、サンプリングレートの重み付けまたはその逆つまり、100 ページビューのうち 1 つしか記録されません。
* チェックポイント（ページの読み込みシーケンスまたは訪問者としてのページとのやり取りのシーケンスにおける特定のイベントの名前）。
* ソース（上記のチェックポイントでユーザーがやり取りする DOM 要素の識別子）。例えば、これは画像の可能性があります
* ターゲット（上記のチェックポイントでユーザーがやり取りする外部ページまたはリソースへのリンク）。例：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 訪問者のエクスペリエンスの質を表す[コア web バイタル（CWV）](https://web.dev/articles/lcp)パフォーマンス指標、[最大コンテンツの描画（LCP）](https://web.dev/articles/lcp)、[次のペイントまでのインタラクション（INP）](https://web.dev/articles/inp)および[累積レイアウトシフト（CLS）](https://web.dev/articles/cls)。

## お客様に対する実際の使用のモニタリングの仕組み {#how-rum-works-for-a-customer}

実際の使用のモニタリングは、クライアントサイドのトラフィックを自動的に監視します。アドビのお客様の場合、このサービスは既存の設定にシームレスに統合されるので、追加の手順を実行する必要はありません。実際の使用のモニタリング（RUM）サービスが一般提供されると、この新しい機能のメリットが自動的に得られます。実際の使用のモニタリングサービスでは、現在、監視対象となるお客様向けの指標は公開されていません。アドビでは、この機能をできる限り早くお客様に提供できるように取り組んでいます。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## アドビでの実際の使用のモニタリングを使用する仕組み {#how-rum-data-is-being-used}

実際の使用のモニタリングデータは、次の目的で使用されます。

* お客様のサイトに対してパフォーマンスのボトルネックを特定および修正する
* 互換性を高めることを目的に、AEM が同じページ上の他のスクリプト（分析、ターゲティング、外部ライブラリなど）とやり取りする方法を理解する
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their RUM data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede RUM data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by RUM.

1. **Limitations in capturing headless API/JSON calls**

   * RUM data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from RUM service data creates variances from the content requests measured by CDN Analytics.
-->

## よくある質問 {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the RUM service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **「次のペイントまでのインタラクション（INP）」、「最初のバイトまでの時間（TTFB）」および「コンテンツの初回ペイント（FCP）」の指標を収集していますか？**

   次のペイントまでのインタラクション（INP）と最初のバイトまでの時間（TTFB）を収集します。現時点では、コンテンツの初回ペイント（FCP）は収集しません。

1. **`/.rum` パスがサイトでブロックされています。どうすれば修正できますか？**

   `/.rum` パスは、RUM 収集が機能するのに必要です。アドビの AEM as a Cloud Service の前で CDN を使用する場合は、`/.rum` パスが他の AEM コンテンツと同じ AEM 接触チャネルに転送されるようにします。また、どのような場合においても調整されないようにしてください。

1. **RUM コレクションは、契約上の目的でコンテンツリクエストにカウントされますか？**

   RUM ライブラリと RUM コレクションはコンテンツリクエストとしてカウントされず、レポートされるページビュー数や API 呼び出し数は増加しません。さらに、AEM as a Cloud Service で標準の CDN を使用するお客様の場合、[サーバーサイドのコレクション](#serverside-collection)がコンテンツリクエストの基本となります。

1. **RUM を無効にするにはどうすればよいですか？**

   アドビでは、実際の使用のモニタリング（RUM）の使用をお勧めします。これは、RUM には大きなメリットがあり、web サイトのパフォーマンスを改善することでデジタルエクスペリエンスを最適化できるようになるからです。このサービスは、シームレスに設計され、web サイトのパフォーマンスに影響を与えません。

   オプトアウトすると、web サイトのトラフィックエンゲージメントを向上させる機会を逃す可能性があります。ただし、問題が発生した場合は、アドビサポートにお問い合わせください。