---
title: Edge Delivery Services の概要
description: AEM as a Cloud Service を使用して、Edge Delivery Services で提供されるパフォーマンスと完璧な Lighthouse スコアを活用する方法について説明します。
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 991db00a833e964d4837bdde9a04ee72b3ad782d
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 72%

---


# Edge Delivery Services の概要 {#edge-delivery-services}

Edge Delivery により、AEM はエンゲージメントとコンバージョンを促進する優れたエクスペリエンスを提供します。そのために AEM では、迅速に作成および開発できるインパクトの強いエクスペリエンスを提供します。これは、作成者がサイトをすばやく更新および公開できて、新しいサイトが迅速にローンチされる迅速な開発環境を可能にする、構成可能なサービスセットです。したがって、Edge Delivery を使用すると、コンバージョンを向上させ、コストを削減し、コンテンツベロシティを最大限に高めることができます。

Edge 配信サービスを使用すると、次の操作を実行できます。

* 申し分ない Lighthouse スコアの高速サイトを作成し、実際の使用のモニタリング（RUM）を通じてサイトのパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。標準では、WYSIWYG とドキュメントベースのオーサリングの両方を使用できます。したがって、同じ web サイト上で複数のコンテンツソースを操作できます。
* 迅速なテスト作成、パフォーマンスに影響を与えない実行およびテスト勝者の実稼動環境への迅速なリリースが可能になる組み込みの実験フレームワークを使用します。

## ビジネスニーズに対するアジャイルな対応 {#agile-reaction}

Adobeは、業界で長年にわたって認められているリーダーとして、お客様にとって有意義な新しいコンテンツを迅速に作成し、公開することがいかに重要かを理解しています。 コンテンツ作成の拡大における一般的な課題は、市場によって明らかにされています。例えば、次のような課題が挙げられます。

1. **コンテンツに対する需要が成長し続けている。**
   * この需要を満たすには、新しいコンテンツ作成者を開拓する必要があります。
   * コンテンツ作成プロセスは、ビジネス全体で効果的に拡張する必要があります。
   * 作成者は、トレンドの変化に迅速に対応できる必要があります。
1. **オムニチャネルコンテンツが必要である。**
   * コンテンツの配信に関係なく、レイアウト制御が必要です。
   * 作成者には、コンテンツのレイアウトを直接変更できる権限が必要です。
1. **コンテンツの ROI を向上させるプレッシャーが高まっている。**
   * 作成者自身には、作成したコンテンツを最適化する能力が必要です。

これらのトレンドは、業界全体で一貫していることが証明されています。ただし、個々の要件はプロジェクトによって必ず異なります。 Edge Delivery Servicesプロジェクトの目標は、ユーザーに適したソリューションの検索に集中することです。

1. **機能ではなく価値に焦点を当てる。** - AEM の広範な機能セットを見失うことなく、作成者に提供する最も最適化されたワークフローを決定します。
1. **AEM の柔軟性を活用する。** - AEM の機能を単独で使用する必要はありません。ユースケースごとに必要な機能を使用します。
1. **作成者の専門知識を活用する。** - 実際のコンテンツ作成者を最初からプロジェクトに関与させ、理にかなった機能を実装することで、必要な価値を確実に提供できるようにします。

作成者にとっての価値に焦点を当てることで、Edge Delivery Services プロジェクトは、コンテンツ作成者が直面している最新の業界のニーズを満たし、お客様を満足させるコンテンツを迅速に提供できます。

## コンテンツ作成者向けの柔軟なオーサリングツール {#overview}

Edge Delivery Services は、web サイト上のコンテンツの柔軟なオーサリングを実現する、構成可能なサービスセットです。[ ユニバーサルエディター ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/author-publish) を使用した [AEM コンテンツ管理とWYSIWYG オーサリングの両方を使用できるほか ](/help/sites-cloud/authoring/universal-editor/authoring.md) ドキュメントベースのオーサリング ](https://www.aem.live/docs/authoring) も使用できます [。

次の図は、Microsoft Word でコンテンツを編集して（ドキュメントベースのオーサリング）、Edge Delivery Services に公開する方法を示しています。また、ユニバーサルエディターを使用した WYSIWYG の編集も示しています。

![Edge Delivery のアーキテクチャ](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services では GitHub を利用しているので、自身の GitHub リポジトリから直接コードを管理およびデプロイできます。新しいコンテンツは、再作成プロセスなしで即座に追加されます。

### ドキュメントベースのオーサリング {#document-based}

ドキュメントベースのオーサリングでは、Microsoft Word または Google Docs から直接コンテンツを使用して、それらのソースを web サイト上のページにすることができます。見出し、リスト、画像、フォント要素、ビデオはすべて、初期ソースから web サイトに転送できます。

* ドキュメントベースのオーサリングでは、すべてのマーケターが、既知のオーサリングツール（Microsoft Word、Google Docs など）を使用して、コンテンツを迅速に作成できます。
* ソースドキュメント内で直接作成、レビュー、公開できるので、コンテンツの作成が効率化されます。
* 既知のツールを使用するので、コンテンツ作成者にはオンボーディングが不要で、コンテンツの作成速度が向上します。
* サイトの機能は、GitHub で CSS と JavaScript を使用して開発できます。

![ドキュメントベースのオーサリング](assets/document-based-authoring.png)

ドキュメントベースのオーサリングに関するドキュメントの詳細な説明：

* Edge Deliveryの使用を開始する方法について詳しくは、[ ビルドの節 ](https://www.aem.live/docs/#build) を参照してください。
* Edge 配信を使用してコンテンツをオーサリングおよび公開する方法について詳しくは、[セクションの公開](https://www.aem.live/docs/authoring)を参照してください。
* Web サイトのプロジェクトを適切に起動する方法については、[ 起動の節 ](https://www.aem.live/docs/#launch) を参照してください。

### WYSIWYG オーサリング {#wysiwyg-authoring}

見たとおりに編集できる（WYSIWYG）オーサリングでは、ユニバーサルエディターを活用します。このエディターは、カスタマイズ可能なワンストッププレースで、視覚的なプレビューを使用してコンテンツをライブおよびコンテキスト内で編集します。

* WYSIWYG オーサリングでは、ヘッドレスでもヘッドフルでも作成者の効率が向上します。
* ワークフローやガバナンスを含む AEM の包括的なコンテンツ管理機能を活用できます。
* 多数の拡張ポイントを活用して、独自のプロセスと統合をサポートします。
* サイトの機能は、GitHub で CSS と JavaScript を使用して開発できます。

![WYSIWYG オーサリング](assets/wysiwyg-authoring.png)

WYSIWYG オーサリングに関するドキュメントの詳細な説明：

* ユニバーサルエディターとWYSIWYGのオーサリングの概要については、[Edge Delivery Services向けWYSIWYG コンテンツオーサリング ](/help/edge/wysiwyg-authoring/authoring.md) を参照してください。
* 開発者向けの概要については、[Edge Delivery ServicesでのWYSIWYG オーサリングの開発者向けスタートガイド ](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) を参照してください。

### オーサリング方法の決定 {#authoring-method}

AEM の柔軟性により、オーサリングのニーズを確実に満たすことができます。アドビでは、お客様の要件に最適な方法（複数可）を決定するお手伝いをいたします。

* コンテンツ作成者を常に決定に関与させます。
* 複数のオーサリングメソッドを実装できます。
* オーサリング方法は、後からいつでも変更できます。
* 実装の前に決定する必要はなく、実装の一部として決定する必要があります。

詳しくは [ オーサリング方法の選択 ](authoring-methods.md) を参照してください。

## Edge Delivery Services と他の Adobe Experience Cloud 製品 {#edge-other-products}

Edge Delivery Servicesは、Adobe Experience Managerの一部です。 そのため、Edge Delivery ServicesとAEM Sitesは、同じドメインに共存させることができます。これは、大規模な web サイトの一般的なユースケースです。 さらに、AEM Sites ページでは、Edge Delivery Servicesのコンテンツをシームレスに使用できます。逆も同様です。

独自のプロジェクトを開始してAEMとEdge Delivery Servicesでオーサリングする方法については ](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)WYSIWYG Edge Delivery Services向け開発者向け入門ガイド [ を参照してください。

また、[Adobe Target](https://www.aem.live/developer/target-integration)、[Real Use Monitoring （RUM） ](https://www.aem.live/developer/rum) および [Launch](https://experienceleague.adobe.com/ja/docs/experience-platform/tags/home) とのEdge Delivery Servicesを使用して、サイトの使用状況とパフォーマンスを診断することもできます。

## Edge Delivery Services の概要 {#getting-started}

[ 入門 – 開発者向けチュートリアル ](https://www.aem.live/developer/tutorial) に従って、Edge Delivery Servicesの使用を簡単に開始できます。

## アドビからのヘルプの入手 {#getting-help}

アドビでは、Edge Delivery Services に役立つ 3 つのチャネルを用意しています。

* 一般的な問い合わせについては、[コミュニティリソース](#community-resources)に問い合わせてください。
* 特定の質問については、[製品コラボレーションチャネル](#collaboration-channel)にアクセスしてください。
* [サポートチケットを記録](#support-ticket)して、重大な問題を解決してください。

### コミュニティリソースへのアクセス {#community-resources}

アドビは、Edge Delivery Services、WYSIWYG、ドキュメントベースのオーサリングに関する最高クラスのコミュニティエンゲージメントとサポートを提供しています。

* [Experience League コミュニティに参加して ](https://adobe.ly/3Q6kTKl) 質問をしたり、フィードバックを共有したり、ディスカッションを開始したり、Adobeの専門家やAEM アドバイザー/チャンピオンから支援を求めたり、志を同じくする個人とリアルタイムでつながったりします。
* よりカジュアルなプラットフォームである [Discord チャンネル ](https://discord.gg/aem-live) に参加して、リアルタイムのインタラクションと迅速なアイデア交換を行いましょう。

### 製品コラボレーションチャネルへのアクセス方法 {#collaboration-channel}

ユーザーとの直接コミュニケーションチャネルの価値を考えると、すべてのAEM プロジェクトの立ち上げ時に、速度、重要なアップデート、エクスペリエンスの質に関する大規模なレポート作成のためのSlackチャネルを確立します。 組織に固有の Slack チャネルに参加するための招待メールがアドビから届きます。

詳しくは、[Slack ボットの使用](https://www.aem.live/docs/slack)のドキュメントを参照してください。

プロビジョニングされた製品コラボレーションチャネルを介してアドビ製品チームと連携し、製品の使用方法やベストプラクティスに関する質問に回答できます。製品コラボレーションチャネルを介したコミュニケーションに関連するサービスレベルターゲット（SLT）は存在しません。

### サポートチケットのログ {#support-ticket}

{{support-ticket}}

## 次の手順 {#whats-next}

まず、[Edge 配信サービスの使用](/help/edge/using.md)を確認します。
