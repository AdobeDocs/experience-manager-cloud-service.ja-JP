---
title: Edge 配信サービスの概要
description: AEM as a Cloud Service を使用して、Edge Delivery Services で提供されるパフォーマンスと完璧な Lighthouse スコアを活用する方法について説明します。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: bf6d0ff2f4aebb6620be46704072743578b096d2
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 48%

---


# Edge 配信サービスの概要 {#edge-delivery-services}

Edge Delivery により、AEM はエンゲージメントとコンバージョンを促進する優れたエクスペリエンスを提供します。そのために AEM では、迅速に作成および開発できるインパクトの強いエクスペリエンスを提供します。これは、作成者がサイトをすばやく更新および公開できて、新しいサイトが迅速にローンチされる迅速な開発環境を可能にする、構成可能なサービスセットです。したがって、Edge Delivery を使用すると、コンバージョンを向上させ、コストを削減し、コンテンツベロシティを最大限に高めることができます。

Edge 配信サービスを使用すると、次の操作を実行できます。

* 申し分ない Lighthouse スコアの高速サイトを作成し、実ユーザーモニタリング（RUM）を通じてサイトのパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。標準では、AEM オーサリングとドキュメントベースのオーサリングの両方を使用できます。したがって、同じ web サイト上で複数のコンテンツソースを操作できます。
* 迅速なテスト作成、パフォーマンスに影響を与えない実行およびテスト勝者の実稼動環境への迅速なリリースが可能になる組み込みの実験フレームワークを使用します。

## 概要 {#overview}

Edge Delivery Servicesは、web サイト上のコンテンツの作成方法を高度に柔軟に設定できる、構成可能なサービスセットです。 両方を使用できます [AEM コンテンツ管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=ja) を使用したAEM ベースのオーサリング [ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md) も [ドキュメントベースのオーサリング](https://www.aem.live/docs/authoring)

次の図は、Microsoft Word でコンテンツを編集（ドキュメントベースのオーサリング）して、Edge Delivery Servicesに公開する方法を示しています。 また、ユニバーサルエディターを使用したAEM ベースの編集も示します。

![Edge Delivery のアーキテクチャ](assets/AEM-with-EDS-publishing-simple2.png)

Microsoft Word またはGoogle Docs のコンテンツを直接使用して、それらのソースを web サイト上のページにすることができます。 さらに、見出し、リスト、画像、フォント要素などはすべて、当初のソースから web サイトに転送できます。新しいコンテンツは、再作成プロセスなしで即座に追加されます。

Edge Delivery Servicesは GitHub を使用しているので、GitHub リポジトリから直接コードを管理およびデプロイできます。 例えば、コンテンツをGoogle ドキュメントまたはMicrosoft Word で記述し、GitHub の CSS と JavaScript を使用してサイトの機能を開発できます。 準備が整ったら、Sidekickブラウザー拡張機能を使用して、コンテンツの更新をプレビューし、公開します。

詳しくは、次の Edge 配信サービスのドキュメントを参照してください。

* Edge 配信の使用を開始する方法について詳しくは、[作成](https://www.aem.live/docs/#build)の節を参照してください。
* Edge 配信を使用してコンテンツをオーサリングおよび公開する方法については、[公開](https://www.aem.live/docs/authoring)の節を参照してください。
* Web サイトプロジェクトを適切にローンチする方法については、[ローンチ](https://www.aem.live/docs/#launch)の節を参照してください。

## Edge Delivery Servicesその他Adobe Experience Cloud製品 {#edge-other-products}

Edge Delivery ServicesはAdobe Experience Managerの一部なので、Edge Delivery ServicesとAEM サイトは同じドメインに共存できます。これは、大規模な web サイトの一般的なユースケースです。 また、AEM Sites ページでEdge Delivery Servicesのコンテンツを簡単に利用することも、その逆も可能です。

AEM と Edge Delivery Services を使用してオーサリングする独自のプロジェクトを開始する方法については、[Edge Delivery Services を使用した AEM オーサリングの開発者向け入門ガイド](/help/edge/aem-authoring/edge-dev-getting-started.md)を参照してください。

でEdge Delivery Servicesを使用することもできます [Adobe Target](https://www.aem.live/developer/target-integration) [実際のユーザーの監視（RUM）](https://www.aem.live/developer/rum) サイトの使用状況およびパフォーマンスを診断するには、以下を行います。 [ローンチ。](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Edge Delivery の概要 {#getting-started}

次の手順に従うことで、Edge Delivery Servicesの使用を開始できます [はじめに – 開発者チュートリアル。](https://www.aem.live/developer/tutorial)

## アドビからのヘルプの入手 {#getting-help}

アドビには、Edge 配信サービスに役立つ 3 つのチャネルが用意されています。

* ～に関与する [コミュニティリソース](#community-resources) 一般的なお問い合わせ。
* へのアクセス [製品コラボレーションチャネル](#collaboration-channel) 具体的な質問については、を参照してください。
* [サポートチケットを記録](#support-ticket) 重大かつ重大な問題を解決するため

### コミュニティリソースへのアクセス {#community-resources}

Adobeは、Edge Delivery Services、AEM ベースおよびドキュメントベースのオーサリングに対する最高のコミュニティエンゲージメントとサポートを提供することに全力を注いでいます。

* [Experience League コミュニティ](https://adobe.ly/3Q6kTKl)に参加して、質問をしたり、意見を共有したり、ディスカッションを始めたり、アドビの専門家や AEM アドバイザー／チャンプにサポートを求めたり、同じ意見を持つユーザーとリアルタイムでつながりを持つことができます。
* リアルタイムのインタラクションと迅速なアイデア交換を実現する一層カジュアルなプラットフォーム、[ディスコードチャネル](https://discord.gg/aem-live)に参加してください。

### 製品コラボレーションチャネルへのアクセス方法 {#collaboration-channel}

ユーザーとの直接コミュニケーションチャネルの価値を考えると、すべてのAEM プロジェクトの立ち上げ時に、速度、重要な更新、エクスペリエンスの質に関するレポートの拡張を行うためのSlackチャネルが確立されます。 組織に固有の Slack チャネルに参加するための招待メールがアドビから届きます。

詳しくは、ドキュメントを参照してください [Slackボットの使用](https://www.aem.live/docs/slack) を参照してください。

プロビジョニングされたAdobeコラボレーションチャネルを通じて製品製品チームと連携すると、製品の使用やベストプラクティスに関する質問に答えることができます。 製品コラボレーションチャネルを介した会話に関連するサービスレベルターゲット（SLT）はありません。

### サポートチケットのログ {#support-ticket}

製品の問題に詳細な調査とトラブルシューティングが必要で、対応 SLT を満たす必要がある場合は、Admin Consoleを使用してこのプロセスに従ってサポートチケットを送信できます。

1. [標準のサポートプロセスに従い、](https://experienceleague.adobe.com/?support-tab=home#support) チケットを作成します。
1. チケットのタイトルに「**Edge 配信**」を追加します。
1. 説明に、問題の説明に加えて、次の詳細を入力します。

   * ライブ web サイトの URL。例：`www.mydomain.com`。
   * オリジン web サイトの URL（`.hlx` URL）。

## 次の手順 {#whats-next}

のレビューから始める [Edge Delivery Servicesを使用します。](/help/edge/using.md)
