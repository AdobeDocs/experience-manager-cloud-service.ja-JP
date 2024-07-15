---
title: Edge Delivery Services の概要
description: AEM as a Cloud Service を使用して、Edge Delivery Services で提供されるパフォーマンスと完璧な Lighthouse スコアを活用する方法について説明します。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 100%

---


# Edge Delivery Services の概要 {#edge-delivery-services}

Edge Delivery により、AEM はエンゲージメントとコンバージョンを促進する優れたエクスペリエンスを提供します。そのために AEM では、迅速に作成および開発できるインパクトの強いエクスペリエンスを提供します。これは、作成者がサイトをすばやく更新および公開できて、新しいサイトが迅速にローンチされる迅速な開発環境を可能にする、構成可能なサービスセットです。したがって、Edge Delivery を使用すると、コンバージョンを向上させ、コストを削減し、コンテンツベロシティを最大限に高めることができます。

Edge 配信サービスを使用すると、次の操作を実行できます。

* 申し分ない Lighthouse スコアの高速サイトを作成し、実際の使用のモニタリング（RUM）を通じてサイトのパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。標準では、WYSIWYG とドキュメントベースのオーサリングの両方を使用できます。したがって、同じ web サイト上で複数のコンテンツソースを操作できます。
* 迅速なテスト作成、パフォーマンスに影響を与えない実行およびテスト勝者の実稼動環境への迅速なリリースが可能になる組み込みの実験フレームワークを使用します。

## 概要 {#overview}

Edge Delivery Services は、web サイト上のコンテンツの柔軟なオーサリングを実現する、構成可能なサービスセットです。[AEM コンテンツ管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=ja)と[ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md)を使用したWYSIWYG のオーサリングの両方と、[ドキュメントベースのオーサリング](https://www.aem.live/docs/authoring)とを使用できます。

次の図は、Microsoft Word でコンテンツを編集して（ドキュメントベースのオーサリング）、Edge Delivery Services に公開する方法を示しています。また、ユニバーサルエディターを使用した WYSIWYG の編集も示しています。

![Edge Delivery のアーキテクチャ](assets/AEM-with-EDS-publishing-simple2.png)

Microsoft Word または Google Docs から直接コンテンツを使用して、それらのソースを web サイト上のページにすることができます。さらに、見出し、リスト、画像、フォント要素などはすべて、当初のソースから web サイトに転送できます。新しいコンテンツは、再作成プロセスなしで即座に追加されます。

Edge Delivery Services では GitHub を利用しているので、自身の GitHub リポジトリから直接コードを管理およびデプロイできます。例えば、コンテンツを Google Docs または Microsoft Word で作成し、GitHub の CSS と JavaScript を使用してサイトの機能を開発できます。準備が整ったら、サイドキックブラウザー拡張機能を使用して、コンテンツの更新をプレビューおよび公開します。

詳しくは、次の Edge 配信サービスのドキュメントを参照してください。

* Edge 配信の使用を開始する方法について詳しくは、[作成](https://www.aem.live/docs/#build)の節を参照してください。
* Edge 配信を使用してコンテンツをオーサリングおよび公開する方法については、[公開](https://www.aem.live/docs/authoring)の節を参照してください。
* Web サイトプロジェクトを適切にローンチする方法については、[ローンチ](https://www.aem.live/docs/#launch)の節を参照してください。

## Edge Delivery Services と他の Adobe Experience Cloud 製品 {#edge-other-products}

Edge Delivery Services は Adobe Experience Manager の構成要素なので、Edge Delivery Services と AEM Sites は同じドメイン上に共存できます。これは、大規模な web サイトの一般的な使用例です。さらに、Edge Delivery Services のコンテンツは AEM Sites ページで簡単に使用できます。その逆も同様です。

AEM と Edge Delivery Services を使用してオーサリングする独自のプロジェクトを開始する方法について詳しくは、[Edge Delivery Services を使用した AWYSIWYG の開発者向け入門ガイド](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)を参照してください。

Edge Delivery Services は [Adobe Target](https://www.aem.live/developer/target-integration)、[実際の使用のモニタリング（RUM）](https://www.aem.live/developer/rum)と共に使用して Sites の使用状況とパフォーマンスを診断したり、[Adobe Experience Platform Launch](https://experienceleague.adobe.com/ja/docs/experience-platform/tags/home) で使用することもできます。

## Edge Delivery の概要 {#getting-started}

[はじめに - 開発者向けチュートリアルに従って、Edge Delivery Services を簡単に使い始めることができます。](https://www.aem.live/developer/tutorial)

## アドビからのヘルプの入手 {#getting-help}

アドビでは、Edge Delivery Services に役立つ 3 つのチャネルを用意しています。

* 一般的な問い合わせについては、[コミュニティリソース](#community-resources)に問い合わせてください。
* 特定の質問については、[製品コラボレーションチャネル](#collaboration-channel)にアクセスしてください。
* [サポートチケットを記録](#support-ticket)して、重大な問題を解決してください。

### コミュニティリソースへのアクセス {#community-resources}

アドビは、Edge Delivery Services、WYSIWYG、ドキュメントベースのオーサリングに関する最高クラスのコミュニティエンゲージメントとサポートを提供しています。

* [Experience League コミュニティ](https://adobe.ly/3Q6kTKl)に参加して、質問をしたり、意見を共有したり、ディスカッションを始めたり、アドビの専門家や AEM アドバイザー／チャンプにサポートを求めたり、同じ意見を持つユーザーとリアルタイムでつながりを持つことができます。
* リアルタイムのインタラクションと迅速なアイデア交換を実現する一層カジュアルなプラットフォーム、[ディスコードチャネル](https://discord.gg/aem-live)に参加してください。

### 製品コラボレーションチャネルへのアクセス方法 {#collaboration-channel}

ユーザーとの直接的なコミュニケーションチャネルの価値を考慮し、すべての AEM プロジェクトはローンチ時に、速度、重要なアップデートおよびエクスペリエンス品質に関する拡張レポートを利用できる Slack チャネルを確立します。組織に固有の Slack チャネルに参加する招待メールがアドビから届きます。

詳しくは、[Slack ボットの使用](https://www.aem.live/docs/slack)のドキュメントを参照してください。

プロビジョニングされた製品コラボレーションチャネルを介してアドビ製品チームと連携し、製品の使用方法やベストプラクティスに関する質問に回答できます。製品コラボレーションチャネルを介したコミュニケーションに関連するサービスレベルターゲット（SLT）は存在しません。

### サポートチケットのログ {#support-ticket}

製品の問題が追加の調査とトラブルシューティングを必要とし、応答 SLT を満たす必要がある場合は、Admin Console を使用して次のプロセスに従ってサポートチケットを送信できます。

1. [標準のサポートプロセスに従って、](https://experienceleague.adobe.com/?support-tab=home#support)チケットを作成します。
1. チケットのタイトルに「**Edge Delivery**」を追加します。
1. 説明では、問題の説明に加えて、次の詳細を入力します。

   * ライブ web サイトの URL。例：`www.mydomain.com`。
   * オリジン web サイトの URL（`.hlx` URL）。

## 次の手順 {#whats-next}

まず、[Edge Delivery Services の使用](/help/edge/using.md)を確認します。
