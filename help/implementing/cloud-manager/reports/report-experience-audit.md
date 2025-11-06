---
title: エクスペリエンス監査ダッシュボード
description: エクスペリエンス監査でデプロイメントプロセスを検証して、変更内容がパフォーマンス、アクセシビリティ、ベストプラクティスおよび SEO のベースライン標準を満たしていることを確認する方法について説明します。これらの指標を追跡するための、明確で有益なダッシュボードインターフェイスが用意されています。
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 87%

---


# エクスペリエンス監査ダッシュボード {#experience-audit-dashboard}

<!-- Engineer architect over this feature was Bogdan Anton; scrum master Alexandru Nica -->

エクスペリエンス監査でデプロイメントプロセスを検証して、変更内容がパフォーマンス、アクセシビリティ、ベストプラクティスおよび SEO（検索エンジン最適化）のベースライン標準を満たしていることを確認する方法について説明します。これらの指標を追跡するための、明確で有益なダッシュボードインターフェイスが用意されています。

## 概要 {#overview}

エクスペリエンス監査により、デプロイメントプロセスが検証され、次の変更がデプロイされていることを確認できます。

1. パフォーマンス、アクセシビリティ、ベストプラクティス、SEO のベースライン標準を満たしている。
1. リグレッションを導入しない。

Cloud Manager のエクスペリエンス監査を使用すると、サイト上でのユーザーのエクスペリエンスが最も高い標準に準拠します。

監査結果は参考情報であり、デプロイメントマネージャーはスコアと、現在および以前のスコアとの間の変化を確認できます。このインサイトは、現在のデプロイメントで前のバージョンになかった不具合が導入されたかどうかを判断するのに役立ちます。

エクスペリエンス監査は、Google のオープンソースツールである [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) を活用し、すべての Cloud Manager 実稼動パイプラインで有効になります。

## 入手方法 {#availability}

エクスペリエンス監査は、Cloud Manager で使用できます。

* （デフォルト）Sites 実稼動パイプライン。
* （オプション）フルスタックパイプラインの開発。
* （オプション）フロントエンドパイプラインの開発。

オプション環境の監査を設定する方法について詳しくは、[設定の節](#configuration)を参照してください。

監査はパイプラインの一部として実行されます。監査は、パイプライン外で [&#x200B; オンデマンドで実行 &#x200B;](#on-demand) することもできます。

## 設定 {#configuration}

実稼動パイプラインでは、エクスペリエンス監査をデフォルトで使用できます。フルスタックパイプラインとフロントエンドパイプラインの開発に対して、オプションで有効にすることができます。どのような場合でも、パイプライン実行中に評価されるコンテンツパスを定義する必要があります。

1. 設定するパイプラインのタイプに応じて、次のいずれかの操作を行います。

   * [実稼動パイプラインを追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)して、監査で評価するパスを定義します。
   * フロントエンドまたは開発フルスタックパイプラインで監査を有効にする場合は、[実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)します。
   * [既存のパイプラインを編集](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)し、既存のオプションを更新します。

1. 実稼動以外のパイプラインを追加または編集する際にエクスペリエンス監査を使用するには、「**エクスペリエンス監査**」チェックボックスをオンにします。このオプションは「**ソースコード**」タブにあります。

   ![エクスペリエンス監査の有効化](/help/implementing/cloud-manager/reports/assets/experience-audit-enable.jpg)

   * 実稼動以外のパイプラインの場合にのみ必要です。
   * 「**エクスペリエンス監査**」タブは、チェックボックスが選択されていると表示されます。

1. 実稼動および実稼動以外の両方のパイプラインでは、「**エクスペリエンス監査**」タブでエクスペリエンス監査に含めるパスを定義します。

   * ページのパスは `/` で始める必要があり、サイトに対する相対パスです。
   * 例えば、サイトが `wknd.site` で、エクスペリエンス監査に `https://wknd.site/us/en/about-us.html` を含める場合は、`/us/en/about-us.html` というパスを入力します。

   ![エクスペリエンス監査に含めるパスの定義](/help/implementing/cloud-manager/reports/assets/experience-audit-add-page.png)

1. 「**ページを追加**」をクリックすると、パスが使用中の環境のアドレスで自動的に補完され、パスのテーブルに追加されます。

   ![テーブルへのパスの保存](/help/implementing/cloud-manager/reports/assets/experience-audit-page-added.png)

1. 上記の 2 つの手順を繰り返して、必要なパスを追加します。

   * 最大 25 個のパスを追加できます。
   * パスを定義しない場合は、デフォルトでサイトのホームページがエクスペリエンス監査に含められます。

1. 「**保存**」をクリックします。

## エクスペリエンス監査結果 {#results}

エクスペリエンス監査の結果は、[本番稼動パイプライン実行ページ](/help/implementing/cloud-manager/deploy-code.md)を介した本番稼動パイプラインの&#x200B;**ステージテスト**&#x200B;フェーズで表示されます。

![パイプライン内のダッシュボード](/help/implementing/cloud-manager/reports/assets/experience-audit-dashboard.png)

エクスペリエンス監査では、[設定済みのページ](#configuration)の Google Lighthouse スコアの中央値と、前回のスキャンとのスコアの差を提供します。

パイプラインの&#x200B;**ステージテスト**&#x200B;フェーズのこの概要ビューには、次の 2 つのオプションがあります。

* **[最も低速のページを表示](#view-slowest-pages)**
* **[フルレポートを表示](#view-full-report)**

Cloud Manager ダッシュボードの「**レポート**」タブをクリックすると、完全な監査結果にアクセスできます。パイプライン実行の詳細に表示される概要に加えて、[完全なレポート](#view-full-report)を直接表示することもできます。

>[!TIP]
>
>次の節では、エクスペリエンス監査の結果を表示する方法について説明します。
>
>* 監査の仕組みについて詳しくは、[エクスペリエンス監査評価の詳細](#details)を参照してください。
>* エクスペリエンス監査をオンデマンドで実行する方法については、[オンデマンド監査レポート](#on-demand)を参照してください。
>* 監査で問題が発生した場合は、[エクスペリエンス監査で発生した問題](#issues)を参照してください。

### 最も低速のページを表示 {#view-slowest-pages}

「**最も低速のページを表示**」をクリックして **最も低速の 5 ページ**&#x200B;ダイアログボックスを開きます。[監査対象として設定](#configuration)した、最もパフォーマンスの低い 5 つのページが表示されます。

![最も低速の 5 ページ](/help/implementing/cloud-manager/reports/assets/experience-audit-slowest-five.png)

Cloud Managerは、スコアを&#x200B;**パフォーマンス**、**アクセシビリティ**、**ベストプラクティス**、**SEO** 別に分類し、以前の監査からの各指標の偏差を示します。

デフォルトでは、ダイアログボックスが開き、モバイルデバイスのスコアが表示されます。ダイアログボックスの上部付近にある「**デバイス**」切替スイッチを使用すれば、デスクトップスコアを表示できます。

このダイアログボックスは、概要をすばやく理解できるように設計されています。詳しくは、「**フルレポートを表示**」をクリックします。

### フルレポートを表示 {#view-full-report}

エクスペリエンス監査のフルレポートは、次の方法で表示できます。

* **[最も低速の 5 ページ](#view-slowest-pages)**&#x200B;ダイアログの「**`View full report`**」をクリックします。
* [パイプラインの実行](#results)を表示する際に、「**`View full report`**」をクリックします。
* Cloud Manager の「**レポート**」タブをクリックします。

Cloud Manager の「**レポート**」タブが開き、**エクスペリエンス監査**&#x200B;が表示されます。

![エクスペリエンス監査レポート](/help/implementing/cloud-manager/reports/assets/experience-audit-reports.png)

レポートは 2 つの領域に分割されています。

* **[ページスコア - トレンド](#trend)**
* **[エクスペリエンス監査スキャン結果](#results)**

#### ページスコア - トレンド {#trend}

デフォルトでは、**ページスコア - トレンド**&#x200B;の選択されたビューは、**昨年**&#x200B;の&#x200B;**中央値スコア**&#x200B;です。

凡例のカテゴリ名をクリックすると、特定の Lighthouse カテゴリのトレンドを表示するように選択できます。

![トレンド選択可能](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-selectable.png)

グラフの上部にあるドロップダウン **選択** を使用してページ固有の詳細を選択し、下部にある **表示** および **トリガー** ドロップダウンを使用して、それぞれ異なる時間枠とトリガータイプを選択します。

**表示**&#x200B;ドロップダウンでは、プリセットされた時間枠や、より具体的な表示用のカスタム間隔を選択できます。

![トレンド表示](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-view.png)

グラフ上でマウスを移動すると、特定の時点での Google Lighthouse カテゴリの値がツールヒントに表示されます。

![トレンドの詳細](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-details.png)

特定の時点でチャートをクリックすると、ポップが開き、そのスキャンの詳細が表示されます。**開いているエクスペリエンス監査スキャン**&#x200B;をクリックすると、そのスキャン結果が「**[エクスペリエンス監査スキャン結果](#scan-results)**」セクションに読み込まれます。

![別のスキャンを選択](/help/implementing/cloud-manager/reports/assets/experience-audit-open-scan.png)

#### エクスペリエンス監査スキャン結果 {#scan-results}

「**エクスペリエンス監査スキャン結果**」セクションには、スキャンされたすべてのページのスコアの詳細が表示されます。「**前へ**」ボタンと「**次へ**」ボタンを使用すると、結果のページを移動したり、表示のページ番号を選択したりできます。

![スキャンされたページ](/help/implementing/cloud-manager/reports/assets/experience-audit-scanned-pages.png)

特定のページのリンクをクリックすると、「**ページスコア – トレンド**」セクションのフィルター [**選択** が更新され &#x200B;](#trend) ページのすべての監査のスコアを表示する「**生のレポート**」タブが表示されます。 **Lighthouse レポート**&#x200B;列のレポート日付をクリックして、生データの JSON ファイルを取得します。

![生レポート](/help/implementing/cloud-manager/reports/assets/experience-audit-raw-reports.png)

ブラウザーに新しいタブが開き、`https://googlechrome.github.io/lighthouse/viewer/` に移動します。 選択したページの Lighthouse の生の JSON レポートを含んだ署名付き URL が自動的に読み込まれ、詳細な検査が可能になります。

![生レポートの表示](/help/implementing/cloud-manager/reports/assets/experience-audit-view-raw-report.png)

## オンデマンドスキャン監査レポート {#on-demand}

エクスペリエンス監査レポートは、パイプラインの実行中に実行されるだけでなく、オンデマンドで生成することもできます。 このオプションは、パイプラインを実行しなくてもページをすばやくスキャンできる優れたソリューションです。

オンデマンド スキャンを実行するには、[**レポート**] タブに移動して完全な監査レポートを表示し、[**スキャンの実行**] ボタンをクリックします。

![オンデマンドスキャン](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand.png)

「**スキャンを実行**」ボタンが使用できなくなり、オンデマンドスキャンが既に実行中の場合は時計のアイコンが付いたバッジが表示されます。

![オンデマンドスキャンの実行](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-running.png)

オンデマンドスキャンは、最新の 25 の[設定済みページ](#configuration)のエクスペリエンス監査をトリガーし、通常は数分で終了します。

完了すると、スコアグラフが自動的に更新され、パイプライン実行スキャンと同様に結果を正確に検査できます。

**トリガー**&#x200B;セレクターを使用すると、トリガータイプに基づいてスコアグラフをフィルタリングできます。

![トリガーフィルター](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>オンデマンドスキャンは、環境が削除されておらず、同じ環境に他の保留中のスキャンがない場合にのみ開始できます。

## エクスペリエンス監査で発生した問題 {#issues}

監査対象として[設定したページ](#configuration)が利用できなかった場合や、監査にその他のエラーがあった場合は、エクスペリエンス監査にその事実が反映されます。

パイプラインには、アクセスできなかった相対 URL パスを表示するための展開可能なエラーセクションが表示されます。

![エクスペリエンス監査で発生した問題](/help/implementing/cloud-manager/reports/assets/experience-audit-issues.png)

フルレポートを表示すると、「**[エクスペリエンス監査スキャン結果](#results)**」セクションに詳細が表示され、展開することもできます。

![フルレポートの問題](/help/implementing/cloud-manager/reports/assets/experience-audit-issues-report.png)

ページが使用できない理由は、次のとおりです。

* 設定により、アクセスがブロックされる。
* ページが存在しない。
* ページにより、基本認証以外の認証を必要とするリダイレクトが行われる。
* 内部的な問題が発生した。

>[!TIP]
>
>ページの[生レポートにアクセス](#scan-results)すると、ページが監査できなかった理由の詳細を示すことができます。

## エクスペリエンス監査評価の詳細 {#details}

次に、エクスペリエンス監査でのサイトの評価方法に関する追加情報を示します。これらは、機能の一般的な使用には必要ではなく、完全を期すためにここに提供されます。

* 監査では、パブリッシャーの[設定済みエクスペリエンス監査ページパス](#configuration)に含まれるオリジン（`.com`）ドメインをスキャンして、実際のユーザーエクスペリエンスをシミュレートし、web サイトの管理と最適化に関してより適切な意思決定を行うのに役立ちます。
* 実稼動のフルスタックパイプラインでは、ステージング環境がスキャンされます。監査中に関連する詳細が監査で提供されるようにするには、ステージング環境のコンテンツをできる限り本番環境に近づける必要があります。
* **ページスコア – トレンド**」セクションのドロップダウン [**選択** に表示されるページは &#x200B;](#trend) エクスペリエンス監査が過去にスキャンしたすべての既知のページです。
