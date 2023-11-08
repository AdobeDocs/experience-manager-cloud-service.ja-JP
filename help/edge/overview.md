---
title: Edge Delivery の概要
description: Edge Delivery Services(EDS) の概要。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: 34965338015df868778a95582524df08a7c5f136
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 99%

---

# Edge Delivery の概要 {#getstart-edge}

Edge Delivery により、AEM はエンゲージメントとコンバージョンを促進する優れたエクスペリエンスを提供します。そのために AEM では、迅速に作成および開発できるインパクトの強いエクスペリエンスを提供します。これは、作成者がサイトをすばやく更新および公開できて、新しいサイトが迅速にローンチされる迅速な開発環境を可能にする、構成可能なサービスセットです。したがって、Edge Delivery を使用すると、コンバージョンを向上させ、コストを削減し、コンテンツベロシティを最大限に高めることができます。

Edge Delivery を活用すると、次のことができます。

* 申し分ない Lighthouse スコアの高速サイトを作成し、実ユーザーモニタリング（RUM）を通じてサイトのパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。標準では、AEM オーサリングとドキュメントベースのオーサリングの両方を使用できます。したがって、同じ web サイト上で複数のコンテンツソースを操作できます。
* 迅速なテスト作成、パフォーマンスに影響を与えない実行およびテスト勝者の実稼動環境への迅速なリリースが可能になる組み込みの実験フレームワークを使用します。

## Edge Delivery の仕組み {#edge-works}

Microsoft Word でコンテンツを編集して（ドキュメントベースの編集）、Edge Delivery に公開する方法を次の図に示します。また、様々なエディターを使用した従来の AEM パブリッシング方法も示します。

![Edge Delivery のアーキテクチャ](assets/edgedelivery.png)

Edge Delivery は、web サイト上のコンテンツの非常に柔軟なオーサリングを可能にする、構成可能なサービスセットです。前述のとおり、[AEM オーサリング](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=ja)と[ドキュメントベースのオーサリング](https://www.hlx.live/docs/authoring)の両方を使用できます。

例えば、Microsoft Word や Google Docs のコンテンツを直接使用できます。つまり、これらのソースのドキュメントを web サイト上のページにすることができます。さらに、見出し、リスト、画像、フォント要素などはすべて、当初のソースから web サイトに転送できます。新しいコンテンツは、再作成プロセスなしで即座に追加されます。

Edge Delivery では GitHub を利用しているので、ユーザーは自分の GitHub リポジトリから直接コードを管理およびデプロイできます。例えば、コンテンツを Google Docs または Microsoft Word で作成し、サイトの機能を GitHub の CSS と JavaScript で開発することができます。準備が整ったら、Sidekick ブラウザー拡張機能を使用して、コンテンツの更新をプレビューおよび公開できます。

参考情報：

* Edge Delivery の使用を開始する方法について詳しくは、Edge Delivery ドキュメントの[作成](https://www.hlx.live/docs/#build)の節を参照してください。
* Edge Delivery を使用してコンテンツをオーサリングおよび公開する方法については、[公開](https://www.hlx.live/docs/authoring)の節を参照してください。
* Web サイトプロジェクトを適切にローンチする方法については、[ローンチ](https://www.hlx.live/docs/#launch)の節を参照してください。

## Edge Delivery と他の Adobe Experience Cloud 製品 {#edge-other-products}

Edge Delivery は Adobe Experience Manager の構成要素なので、Edge Delivery サイトと AEM サイトは同じドメイン上に共存できます。これは、大規模な web サイトの場合に一般的なユースケースです。さらに、Edge Delivery のコンテンツは AEM Sites ページで簡単に使用でき、その逆もまた可能です。

また、Edge Delivery を Adobe Target、Analytics および Launch と組み合わせて使用することもできます。

## Edge Delivery へのアクセス {#getting-access}

Edge Delivery の使用を開始するのは簡単です。[はじめに - 開発者向けチュートリアル](https://www.hlx.live/developer/tutorial)に従って、作業に取りかかります。

## アドビからのヘルプの入手 {#adobe-gethelp}

プロビジョニングされた製品コラボレーションチャネル（アクセスについて詳しくは以下を参照）を介してアドビ製品チームと連携し、製品の使用方法やベストプラクティスに関する質問に回答できます。製品コラボレーションチャネルを介したコミュニケーションに関連するサービスレベル用語（SLT）は存在しないことに注意してください。製品の問題が追加の調査とトラブルシューティングを必要とし、応答 SLT を満たす必要がある場合は、次の[サポートプロセス](https://experienceleague.adobe.com/?lang=ja&amp;support-tab=home#support)に従ってサポートチケットを送信できます。

アドビには、Edge 配信サービスに役立つ 3 つのチャネルが用意されています。

* 一般的な問い合わせに関するコミュニティリソース情報
* 特定の質問に関する製品コラボレーションチャネルへのアクセス
* 重要な問題と重要な問題を解決するためのサポートチケットの記録

### コミュニティリソースへのアクセス {#community-resource}

アドビは、コミュニティに対して最高のエンゲージメントとサポートを提供し、Edge 配信サービスおよびドキュメントベースのオーサリングに取り組んでいます。[Experience League コミュニティ](https://adobe.ly/3Q6kTKl)に参加して、質問をしたり、意見を共有したり、ディスカッションを始めたり、アドビの専門家や AEM アドバイザー／チャンプにサポートを求めたり、同じ意見を持つユーザーとリアルタイムでつながりを持つことができます。リアルタイムのインタラクションと迅速なアイデア交換を実現する一層カジュアルなプラットフォーム、[ディスコードチャネル](https://discord.gg/aem-live)に参加してください。

### 製品コラボレーションチャネルへのアクセス方法 {#collab-channel}

お客様との直接的なコミュニケーションチャネルの価値を考慮し、ローンチ時のすべての AEM ユーザーは、スピード、重要なアップデートおよびエクスペリエンス品質に関する拡張レポートを目的として、Slack チャネルを確立します。組織に固有の Slack チャネルに参加するための招待メールがアドビから届きます。

詳しくは、[Slack ボットの使用](https://www.hlx.live/docs/slack)ドキュメントを参照してください。

### サポートチケットのログ {#support-ticket}

Admin Console を使用してサポートチケットを記録する手順は次のとおりです。

1. チケットのタイトルに「**Edge 配信**」を追加します。
2. 説明には、次の詳細を入力してください。

   * ライブ web サイトの URL。例：[www.mydomain.com]
   * オリジン web サイトの URL（.hlx URL）。

## 次の手順 {#whats-next}

まず、[Edge 配信サービスの使用](/help/edge/using.md)の記事を確認します。

## 役立つリソース {#useful-resources}

Edge 配信サービスについて詳しくは、[Edge 配信サービスドキュメント](https://www.hlx.live/docs/)を参照してください。
