---
title: AEM as a Cloud Service の運用テレメトリ
description: クライアントサイドでのデータ収集を監視できる自動サービスである、運用テレメトリについて説明します。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: d02569f5fcca0e53c8f258be8a193663364ac31f
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 48%

---

# AEM as a Cloud Serviceの運用上のテレメトリサービス {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>運用上のテレメトリサービスは、クライアントサイドでデータを収集するもので、自動化されたサービスです。 お客様による設定は必要ありません。

>[!INFO]
>
>クライアントサイドモニタリングは、AEM（Adobe Experience Manager）Cloud Service バージョン **2024.5.16461** 以降を使用しているお客様に対してのみ機能します。

## 概要 {#overview}

運用テレメトリサービスは、web サイトまたはアプリケーション上のクライアントサイドトラフィックをリアルタイムで監視するパフォーマンス監視技術です。 このサービスは、ユーザー自身ではなく、web サイトのエンゲージメントを監視することで、パフォーマンスを最適化する重要な指標とデータを収集することに焦点を当てています。運用上のテレメトリを使用すると、URL の開始から、リクエストがブラウザーに配信されるまで、主要なパフォーマンス指標が追跡されます。

## 運用上のテレメトリサービスのメリットを享受できるのは誰ですか？ {#who-can-benefit-from-operational-telemetry-service}

運用上のテレメトリは、エンドユーザーがAEM サイトとどのようにやり取りするかを、お客様およびAdobeが理解するのに役立ちます。 運用上のテレメトリは、限られたデータ収集とサンプリングを通じて訪問者のプライバシーを保持します。すべてのページビューのごく一部のみが監視されます。

## 運用上のテレメトリサービスのデータサンプリング {#operational-telemetry-service-data-sampling}

従来の web 分析ソリューションでは、すべての訪問者に関するデータを収集しようとします。AEMの運用上のテレメトリサービスは、ほんの一部のページビューからのみ情報を取得します。 サービスは、分析の代替ではなく、サンプリングと匿名化を目的としています。デフォルトでは、ページのサンプリング率は 1:100 です。 現時点では、サイトオペレーターはサンプリングレートを増減できません。合計トラフィックを正確に推定するには、100 ページビューのうち 1 ページからのデータを収集し、全体のトラフィックの信頼できる近似値を提供します。

データが収集されるかどうかはページビューごとに決定されるので、複数のページ間のやり取りを追跡することは事実上不可能になります。仕様上、運用上のテレメトリは、訪問者やセッションという概念はなく、ページビューのみの概念です。

## 収集されるデータ {#what-data-is-being-collected}

運用上のテレメトリサービスは、データ収集を最小限に抑えるように設計されています。 運用上のテレメトリによって収集される情報の完全なセットを以下に示します。

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

## 顧客に対する運用テレメトリの仕組み {#how-operational-telemetry-works-for-a-customer}

運用テレメトリは、クライアントサイドトラフィックを自動的に監視します。 アドビのお客様の場合、このサービスは既存の設定にシームレスに統合されるので、追加の手順を実行する必要はありません。運用上のテレメトリサービスが一般提供されるようになると、この新機能のメリットが自動的に得られます。 運用上のテレメトリサービスでは、現在顧客に表示されている指標を監視することはありません。 アドビでは、この機能をできる限り早くお客様に提供できるように取り組んでいます。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Adobeでの運用上のテレメトリの使用方法 {#how-operational-telemetry-data-is-being-used}

運用上のテレメトリデータは、次の目的で使用されます。

* お客様のサイトに対してパフォーマンスのボトルネックを特定および修正する
* 互換性を高めることを目的に、AEM が同じページ上の他のスクリプト（分析、ターゲティング、外部ライブラリなど）とやり取りする方法を理解する
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their Operational Telemetry data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede Operational Telemetry data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by Operational Telemetry.

1. **Limitations in capturing headless API/JSON calls**

   * Operational Telemetry data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from Operational Telemetry service data creates variances from the content requests measured by CDN Analytics.
-->

## よくある質問 {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the Operational Telemetry service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **「次のペイントまでのインタラクション（INP）」、「最初のバイトまでの時間（TTFB）」および「コンテンツの初回ペイント（FCP）」の指標を収集していますか？**

   次のペイントまでのインタラクション（INP）と最初のバイトまでの時間（TTFB）を収集します。現時点では、コンテンツの初回ペイント（FCP）は収集しません。

1. **`/.rum` パスがサイトでブロックされています。どうすれば修正できますか？**

   運用上のテレメトリ収集が機能するには、`/.rum` のパスが必要です。 アドビの AEM as a Cloud Service の前で CDN を使用する場合は、`/.rum` パスが他の AEM コンテンツと同じ AEM 接触チャネルに転送されるようにします。また、いかなる方法でも調整されないようにしてください。 Cloud Managerまたは、`rum.hlx.page` という名前の環境変数を [ という値に設定することで ](/help/implementing/cloud-manager/environment-variables.md#add-variables) 運用上のテレメトリに使用するホストを `AEM_OPTEL_EXTERNAL` に変更するこ `true` もできます。 後で同じドメインリクエストに戻す場合は、その環境変数を再度削除するだけです。

1. **運用上のテレメトリ収集は、契約上の目的でコンテンツリクエストにカウントされますか？**

   運用テレメトリライブラリと運用テレメトリコレクションは、コンテンツリクエストとしてカウントされず、レポートされるページビュー数や API 呼び出し数を増やしません。 さらに、AEM as a Cloud Service で標準の CDN を使用するお客様の場合、[サーバーサイドのコレクション](#serverside-collection)がコンテンツリクエストの基本となります。

1. **運用上のテレメトリを無効にするにはどうすればよいですか？**

   Adobeでは、運用上のテレメトリを使用することをお勧めします。これは、大きなメリットがあるためです。また、Adobeを使用すると、web サイトのパフォーマンスを向上させて、デジタルエクスペリエンスを最適化するのに役立ちます。 このサービスは、シームレスに設計され、web サイトのパフォーマンスに影響を与えません。

   オプトアウトすると、web サイトのトラフィックエンゲージメントを向上させる機会を逃す可能性があります。ただし、問題が発生した場合は、[ という名前の環境変数を ](/help/implementing/cloud-manager/environment-variables.md#add-variables) という値に設定する `AEM_OPTEL_DISABLED`Cloud Managerで設定する `true` ことで、運用テレメトリを無効にできます。 後で運用テレメトリを再度有効にする場合は、その環境変数を再度削除するだけです。

1. **コンテンツセキュリティポリシーを nonce で使用できますか？

   運用上のテレメトリのサポートには、コンテンツセキュリティポリシーを nonce でサポートする実験的機能が含まれています。 この機能を有効にするには、[ という名前の ](/help/implementing/cloud-manager/environment-variables.md#add-variables)Cloud Managerの環境変数を `AEM_OPTEL_NONCE` 値 `true` に設定します。 後で再度無効にする場合は、その環境変数を再度削除します。

   この機能で問題が発生した場合は、Adobe サポートにお問い合わせください。

1. **特定のページに対してのみ運用上のテレメトリを有効にするにはどうすればよいですか？**

   デフォルトでは、運用上のテレメトリは、リポジトリの `/content` フォルダーの下にあるすべてのページに対して有効になっています。 [ という名前の ](/help/implementing/cloud-manager/environment-variables.md#add-variables)Cloud Managerの環境変数を設定 `AEM_OPTEL_INCLUDED_PATHS` して、リポジトリ内のコンマ区切りのパスのリストを追加すると、オペレーショナルテレメトリはそれらのページに対してのみ有効になります。 さらに、除外するリポジトリ内のパスのリストに `AEM_OPTEL_EXCLUDED_PATHS` を設定できます。 これらの 2 つの設定の組み合わせにより、運用上のテレメトリを含めるかどうかを、要件に合わせて調整できます。

