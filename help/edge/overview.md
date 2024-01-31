---
title: AEMとEdge Delivery Services
description: AEM as a Cloud Service を使用して、Edge 配信サービスで提供されるパフォーマンスと完璧な Lighthouse スコアを活用する方法について説明します。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: 7d28a3a8304d79ecc3143bdc9373134d312af49d
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 41%

---


# AEMとEdge Delivery Services {#aem-edge}

Edge Delivery により、AEM はエンゲージメントとコンバージョンを促進する優れたエクスペリエンスを提供します。そのために AEM では、迅速に作成および開発できるインパクトの強いエクスペリエンスを提供します。これは、作成者がサイトをすばやく更新および公開できて、新しいサイトが迅速にローンチされる迅速な開発環境を可能にする、構成可能なサービスセットです。したがって、Edge Delivery を使用すると、コンバージョンを向上させ、コストを削減し、コンテンツベロシティを最大限に高めることができます。

Edge Delivery Servicesを使用すると、次のことができます。

* 申し分ない Lighthouse スコアの高速サイトを作成し、実ユーザーモニタリング（RUM）を通じてサイトのパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。標準では、AEM オーサリングとドキュメントベースのオーサリングの両方を使用できます。したがって、同じ web サイト上で複数のコンテンツソースを操作できます。
* 迅速なテスト作成、パフォーマンスに影響を与えない実行およびテスト勝者の実稼動環境への迅速なリリースが可能になる組み込みの実験フレームワークを使用します。

## Edge Delivery Servicesの概要 {#edge-overview}

次の図は、Microsoft Word でコンテンツを編集し（ドキュメントベースの編集）、Edge Delivery Servicesに公開する方法を示しています。 また、ユニバーサルエディターを使用したAEMの公開方法も示します。

![Edge Delivery のアーキテクチャ](assets/AEM-with-EDS-publishing-simple2.png)

エッジ配信サービスは、Web サイト上でのコンテンツのオーサリング方法を高い柔軟性で可能にする、合成可能なサービスのセットです。 前述のように、 [AEM content management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=ja) 次を使用 [ユニバーサルエディターオーサリング](/help/implementing/universal-editor/introduction.md) 同様に [ドキュメントベースのオーサリング。](https://www.aem.live/docs/authoring)

例えば、Microsoft Word や Google Docs のコンテンツを直接使用できます。つまり、これらのソースのドキュメントを web サイト上のページにすることができます。さらに、見出し、リスト、画像、フォント要素などはすべて、当初のソースから web サイトに転送できます。新しいコンテンツは、再構築プロセスなしで即座に追加されます。

Edge Delivery Servicesでは GitHub を使用するので、ユーザーは GitHub リポジトリから直接コードを管理およびデプロイできます。 例えば、GoogleドキュメントまたはMicrosoft Word にコンテンツを書き込み、GitHub で CSS と JavaScript を使用してサイトの機能を開発できます。 準備が整ったら、Sidekick ブラウザー拡張機能を使用して、コンテンツの更新をプレビューおよび公開できます。

Edge Delivery Servicesドキュメントの詳細を読む：

* Edge 配信の開始方法について詳しくは、 [ビルドセクション。](https://www.aem.live/docs/#build)
* Edge 配信を使用してコンテンツをオーサリングおよびパブリッシュする方法については、 [公開セクション。](https://www.aem.live/docs/authoring)
* Web サイトプロジェクトを適切に起動する方法を理解するには、 [「Launch」セクション。](https://www.aem.live/docs/#launch)

## Edge Delivery Servicesおよびその他のAdobe Experience Cloud製品 {#edge-other-products}

Edge Delivery ServicesはAdobe Experience Managerに含まれているので、同じドメイン上にEdge Delivery ServicesとAEMサイトを共存させることができます。 これは、大規模な web サイトの場合に一般的なユースケースです。その上、Edge Delivery ServicesのコンテンツをAEM Sitesページで容易に利用したり、逆に利用したりできます。

詳しくは、 [Edge Delivery Servicesを使用したAEMオーサリングのための Developer Getting Guide](/help/edge/edge-dev-getting-started.md) AEMとEdge Delivery Servicesを使用して作成する独自のプロジェクトを開始する方法を説明します。

また、Adobe Target、Analytics および Launch でEdge Delivery Servicesを使用することもできます。

## Edge Delivery へのアクセス {#getting-access}

Edge Delivery Servicesの使用を簡単に開始できます。 はじめに、 [はじめに — 開発者向けチュートリアル](https://www.aem.live/developer/tutorial)

## アドビからのヘルプの入手 {#adobe-gethelp}

プロビジョニングされた製品コラボレーションチャネル（アクセスについて詳しくは以下を参照）を介してアドビ製品チームと連携し、製品の使用方法やベストプラクティスに関する質問に回答できます。製品コラボレーションチャネルを介した会話に関連付けられたサービスレベルターゲット (SLT) はありません。 製品の問題が追加の調査とトラブルシューティングを必要とし、応答 SLT を満たす必要がある場合は、次の手順に従ってサポートチケットを送信できます。 [サポートプロセス。](https://experienceleague.adobe.com/?lang=ja&amp;support-tab=home#support)

アドビには、Edge 配信サービスに役立つ 3 つのチャネルが用意されています。

* 一般的な問い合わせに関するコミュニティリソース情報
* 特定の質問に関する製品コラボレーションチャネルへのアクセス
* 重要な問題と重要な問題を解決するためのサポートチケットの記録

### コミュニティリソースへのアクセス {#community-resource}

Adobeは、コミュニティに対する最高のエンゲージメントとサポートを提供し、Edge Delivery Servicesとドキュメントベースのオーサリングに取り組んでいます。

* 参加する [Experience Leagueコミュニティ](https://adobe.ly/3Q6kTKl) 質問をしたり、意見を共有したり、ディスカッションを開始したり、Adobeの専門家やAEM Advisors/Champs に助けを求めたり、同じ意見を持つ人とリアルタイムでつながりを持つことができます。
* 参加する [Discord チャネル、](https://discord.gg/aem-live) リアルタイムのインタラクションと迅速なアイデア交換のためのよりカジュアルなプラットフォームです。

### 製品コラボレーションチャネルへのアクセス方法 {#collab-channel}

お客様との直接通信チャネルの価値を考慮すると、AEMをご利用のすべてのお客様は、エクスペリエンスの品質に関する迅速なSlack、重要な更新、拡張レポートのための通信チャネルを確立します。 組織に固有のSlackチャネルに参加するための招待メールをAdobeから受け取ります。

詳しくは、[Slack ボットの使用](https://www.aem.live/docs/slack)ドキュメントを参照してください。

### サポートチケットのログ {#support-ticket}

Admin Console を使用してサポートチケットを記録する手順は次のとおりです。

1. [標準のサポートプロセスに従って、](https://experienceleague.adobe.com/?lang=ja&amp;support-tab=home#support) チケットを作成します。
1. チケットのタイトルに「**Edge 配信**」を追加します。
1. 説明に次の詳細を入力します。

   * ライブ web サイトの URL。例：`www.mydomain.com`。
   * 元の Web サイトの URL (`.hlx` URL) です。

## 次の手順 {#whats-next}

レビューを開始する [使用Edge Delivery Services](/help/edge/using.md).
