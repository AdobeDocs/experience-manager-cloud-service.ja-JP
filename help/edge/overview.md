---
title: AEM および Edge 配信サービスの基本を学ぶ
description: AEM as a Cloud Service を使用して、Edge Delivery Services で提供されるパフォーマンスと完璧な Lighthouse スコアを活用する方法について説明します。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: ht
source-wordcount: '874'
ht-degree: 100%

---


# AEM および Edge 配信サービスの基本を学ぶ {#aem-edge}

Edge Delivery により、AEM はエンゲージメントとコンバージョンを促進する優れたエクスペリエンスを提供します。そのために AEM では、迅速に作成および開発できるインパクトの強いエクスペリエンスを提供します。これは、作成者がサイトをすばやく更新および公開できて、新しいサイトが迅速にローンチされる迅速な開発環境を可能にする、構成可能なサービスセットです。したがって、Edge Delivery を使用すると、コンバージョンを向上させ、コストを削減し、コンテンツベロシティを最大限に高めることができます。

Edge 配信サービスを使用すると、次の操作を実行できます。

* 申し分ない Lighthouse スコアの高速サイトを作成し、実ユーザーモニタリング（RUM）を通じてサイトのパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。標準では、AEM オーサリングとドキュメントベースのオーサリングの両方を使用できます。したがって、同じ web サイト上で複数のコンテンツソースを操作できます。
* 迅速なテスト作成、パフォーマンスに影響を与えない実行およびテスト勝者の実稼動環境への迅速なリリースが可能になる組み込みの実験フレームワークを使用します。

## Edge 配信サービスの概要 {#edge-overview}

Microsoft Word でコンテンツを編集して（ドキュメントベースの編集）、Edge 配信サービスに公開する方法を次の図に示します。また、ユニバーサルエディターを使用した AEM パブリッシング方法も示します。

![Edge Delivery のアーキテクチャ](assets/AEM-with-EDS-publishing-simple2.png)

Edge 配信サービスは、web サイト上のコンテンツの非常に柔軟なオーサリングを可能にする、構成可能なサービスセットです。前述のように、[AEM コンテンツ管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=ja)と[ユニバーサルエディターオーサリング](/help/implementing/universal-editor/introduction.md)および[ドキュメントベースのオーサリング](https://www.aem.live/docs/authoring)の両方を使用できます。

例えば、Microsoft Word や Google Docs のコンテンツを直接使用できます。つまり、これらのソースのドキュメントを web サイト上のページにすることができます。さらに、見出し、リスト、画像、フォント要素などはすべて、当初のソースから web サイトに転送できます。新しいコンテンツは、再作成プロセスなしで即座に追加されます。

Edge 配信サービスでは GitHub を利用しているので、ユーザーは自分の GitHub リポジトリから直接コードを管理およびデプロイできます。例えば、コンテンツを Google Docs または Microsoft Word で作成し、サイトの機能を GitHub の CSS と JavaScript で開発することができます。準備が整ったら、Sidekick ブラウザー拡張機能を使用して、コンテンツの更新をプレビューおよび公開できます。

詳しくは、次の Edge 配信サービスのドキュメントを参照してください。

* Edge 配信の使用を開始する方法について詳しくは、[作成](https://www.aem.live/docs/#build)の節を参照してください。
* Edge 配信を使用してコンテンツをオーサリングおよび公開する方法については、[公開](https://www.aem.live/docs/authoring)の節を参照してください。
* Web サイトプロジェクトを適切にローンチする方法については、[ローンチ](https://www.aem.live/docs/#launch)の節を参照してください。

## Edge 配信サービスと他の Adobe Experience Cloud 製品 {#edge-other-products}

Edge 配信サービスは Adobe Experience Manager の構成要素なので、Edge 配信サービスサイトと AEM Sites は同じドメイン上に共存できます。これは、大規模な web サイトの場合に一般的なユースケースです。さらに、Edge 配信サービスのコンテンツは AEM Sites ページで簡単に使用でき、その逆もまた可能です。

AEM と Edge 配信サービスを使用してオーサリングする独自のプロジェクトを開始する方法については、[Edge 配信サービスを使用した AEM オーサリングの開発者向け入門ガイド](/help/edge/edge-dev-getting-started.md)を参照してください。

また、Edge 配信サービスを Adobe Target、Analytics および Launch と共に使用することもできます。

## Edge Delivery へのアクセス {#getting-access}

Edge 配信サービスの使用を開始するのは簡単です。[はじめに - 開発者向けチュートリアル](https://www.aem.live/developer/tutorial)に従って、作業に取りかかります。

## アドビからのヘルプの入手 {#adobe-gethelp}

プロビジョニングされた製品コラボレーションチャネル（アクセスについて詳しくは以下を参照）を介してアドビ製品チームと連携し、製品の使用方法やベストプラクティスに関する質問に回答できます。製品コラボレーションチャネルを介したコミュニケーションに関連するサービスレベルターゲット（SLT）は存在しません。製品の問題が追加の調査とトラブルシューティングを必要とし、応答 SLT を満たす必要がある場合は、次の[サポートプロセス](https://experienceleague.adobe.com/?support-tab=home#support)に従ってサポートチケットを送信できます。

アドビには、Edge 配信サービスに役立つ 3 つのチャネルが用意されています。

* 一般的な問い合わせに関するコミュニティリソース情報
* 特定の質問に関する製品コラボレーションチャネルへのアクセス
* 重要な問題と重要な問題を解決するためのサポートチケットの記録

### コミュニティリソースへのアクセス {#community-resource}

アドビは、コミュニティに対して最高のエンゲージメントとサポートを提供し、Edge 配信サービスおよびドキュメントベースのオーサリングに取り組んでいます。

* [Experience League コミュニティ](https://adobe.ly/3Q6kTKl)に参加して、質問をしたり、意見を共有したり、ディスカッションを始めたり、アドビの専門家や AEM アドバイザー／チャンプにサポートを求めたり、同じ意見を持つユーザーとリアルタイムでつながりを持つことができます。
* リアルタイムのインタラクションと迅速なアイデア交換を実現する一層カジュアルなプラットフォーム、[ディスコードチャネル](https://discord.gg/aem-live)に参加してください。

### 製品コラボレーションチャネルへのアクセス方法 {#collab-channel}

お客様との直接的なコミュニケーションチャネルの価値を考慮し、ローンチ時、すべての AEM ユーザーは、スピード、重要なアップデートおよびエクスペリエンス品質に関する拡張レポートを利用できる Slack チャネルを確立します。組織に固有の Slack チャネルに参加するための招待メールがアドビから届きます。

詳しくは、[Slack ボットの使用](https://www.aem.live/docs/slack)ドキュメントを参照してください。

### サポートチケットのログ {#support-ticket}

Admin Console を使用してサポートチケットを記録する手順は次のとおりです。

1. [標準のサポートプロセスに従って、](https://experienceleague.adobe.com/?support-tab=home#support)チケットを作成します。
1. チケットのタイトルに「**Edge 配信**」を追加します。
1. 説明には、次の詳細を入力します。

   * ライブ web サイトの URL。例：`www.mydomain.com`。
   * オリジン web サイトの URL（`.hlx` URL）。

## 次の手順 {#whats-next}

まず、[Edge 配信サービスの使用](/help/edge/using.md)を確認します。
