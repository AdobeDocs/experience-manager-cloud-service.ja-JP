---
title: 実稼動環境とステージ環境のヘルスアセスメント
description: Cloud Managerのヘルスアセスメントの活用方法を学びましょう。 AEM環境のスキャン、レポートの実行とレビュー、問題の詳細の表示、PDFの書き出し、過去の実行の管理を行うことができます。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 5467a311-727d-4f67-ba43-4b6548431061
source-git-commit: 8c5c34018aee84a1ec54d3f1d0bc77b8c660869c
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 15%

---

# 健全性の評価 {#about-health-assessment}

Health Assessmentは、AEM as a Cloud Service内のCloud Managerの実稼動環境とステージ環境を自動的に検出する非侵入型スキャンです。 コンテンツ、コード、設定を評価し、ベストプラクティスから逸脱するパターンを特定することで、セキュリティとパフォーマンスを向上させます。

健康評価サービスでは、次の操作を行います。

* 環境をスキャンし、パフォーマンスのボトルネック、非効率性、リスクを特定します。
* ブループリント、ライブコピー、顧客設定などのコンテンツ構造を分析します。
* AEM SDKやサードパーティライブラリなどの古い依存関係を検出します。
* 誤った注釈や非効率的なパターンなど、コード品質の問題を検出します。
* ダッシュボードに実用的なガイダンスを提供（Action Centerなど）。
* システムのパフォーマンスを向上させるためのプロアクティブな修正を有効にします。

各実行では、問題の重大度、ガイダンスおよび推奨される修正へのリンクが一覧表示され、レポートのPDF書き出しがサポートされます。 現在の状態の&#x200B;**最新レポート** ビューと&#x200B;**過去レポート**&#x200B;を使用して、実行を比較できます。

ルールの定義と修復の詳細については、[&#x200B; ヘルスアセスメントパターン &#x200B;](#ha-patterns)も参照してください。

## ヘルスアセスメントページへのアクセス {#access-health-assessment}

1. [experience.adobe.com](https://experience.adobe.com)でCloud Managerにログインします。
1. **クイックアクセス** セクションで、**Experience Manager**&#x200B;をクリックします。
1. 左側のパネルで、**Cloud Manager**&#x200B;をクリックします。
1. Cloud Managerで、ページの右上隅付近にある、アクセスする組織を選択します。 以下の画像は参照用に提供されています。組織を選択してください。

   ![Cloud Managerでの組織の選択](/help/implementing/cloud-manager/reports/assets/ha-org.png)

1. **マイプログラム** コンソールで、レポートを表示するプログラムをクリックします。

1. 次のいずれかの操作を行います。
   * **環境** カードで、環境名の右側にある![省略記号アイコンまたは詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/ui_18/More.svg)をクリックし、メニューから「**ヘルスアセスメント**」を選択します。

     ![環境カードの省略記号メニューからヘルスアセスメントを選択](/help/implementing/cloud-manager/reports/assets/ha-myprograms-environments-card.png)

   * 左側のサイドメニューの&#x200B;**サービス**&#x200B;で、![データアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)「**環境**」をクリックします。 環境ページで、環境名の右側にある![省略記号アイコンまたは詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/ui_18/More.svg)をクリックし、メニューから「**ヘルスアセスメント**」を選択します。

     ![環境ページの省略記号メニューからヘルスアセスメントを選択する](/help/implementing/cloud-manager/reports/assets/ha-environments-page.png)

## 選択した環境に対する新しいレポートの実行 {#run-report}

1. [&#x200B; ヘルス評価ページにアクセス &#x200B;](#access-health-assessment)。
1. **ヘルスアセスメント** ページの右上隅で、評価するターゲット環境を確認します。

   環境が正しくない場合は、![&#x200B; シェブロンのダウンメニューまたはドロップダウンメニューをクリックして、別の環境](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)を選択し、リストから正しい環境を選択します。

1. 「**レポートを実行**」をクリックします。

   ![&#x200B; ヘルスアセスメントページの「新しいレポートを生成」ボタンをクリック &#x200B;](/help/implementing/cloud-manager/reports/assets/ha-run-report.png)

   選択した環境でレポートを実行する間、プロセスが完了するまで&#x200B;**レポートの実行**&#x200B;は無効のままです。

   ![実行中のレポート &#x200B;](/help/implementing/cloud-manager/reports/assets/ha-running-report.png)

   レポートが完了すると、**ヘルスアセスメント** ページの&#x200B;**最新レポート** セクションに表示されます。

## 最新のレポートを見る {#view-latest-report}

* **ヘルスアセスメント** ページで、**最新レポート** セクションで次の情報を確認してください。

   * 最新の実行の結果。
   * 実行日時：
   * 問題の合計数。
   * 重要な課題のハイライト：
   * アクション：**[詳細を表示](#view-report-details)**&#x200B;または&#x200B;**[すべての問題のPDF](#download-pdf-report)**&#x200B;をダウンロードします。

  ![選択した環境の新しいレポートの生成後の最新の評価ページ &#x200B;](/help/implementing/cloud-manager/reports/assets/ha-latest-report-page.png)

### 最新のレポートの詳細 {#view-report-details}

* **健康評価** ページで、**最新レポート** タイトルの右側にある![省略記号アイコンまたはそれ以上のアイコン &#x200B;](https://spectrum.adobe.com/static/icons/ui_18/More.svg)をクリックし、**詳細を表示**&#x200B;または&#x200B;**ダウンロード**&#x200B;をクリックします。

  **詳細を表示** オプションを使用すると、次の情報を確認できます。

   * 課題の包括的なリスト。
   * 調査結果と問題の説明を表示する機能。
   * 潜在的な修正を含むドキュメントを表示する機能。

     ![問題の説明と検索条件](/help/implementing/cloud-manager/reports/assets/ha-issue-descriptions-and-findings.png)

   * **ダウンロード** オプションを使用すると、個々の問題レポートをPDFでダウンロードできます。

     ![個々の問題レポートのPDFをダウンロード &#x200B;](/help/implementing/cloud-manager/reports/assets/ha-details-page-doc-links.png)


### レポート全体のPDFをダウンロード {#download-pdf-report}

* レポートページの右上隅付近にある「**ダウンロード**」をクリックします。

  レポートで検出されたすべての問題に関するPDFを含むZIP ファイルが生成されます。

  ![&#x200B; レポートで見つかったすべての問題のPDFをダウンロード &#x200B;](/help/implementing/cloud-manager/reports/assets/ha-download-pdf.png)


## 過去のレポートを見る {#review-past-reports}

**ヘルスアセスメント** ページで、**過去レポート** セクションで次の情報を確認してください。

* 以前のレポートの詳細を表示します。
* 各実行の日付を表示します。
* レポートは、PDFからダウンロードできます。
* 日付、イシュー数、または環境で並べ替えます。

![過去のレポートを確認](/help/implementing/cloud-manager/reports/assets/ha-past-reports.png)

* 「**過去のレポート**」の見出しの右側にある「![&#x200B; シェブロン」の下またはドロップダウンメニューをクリックして、別の環境](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)を選択し、過去のレポートを日付別に並べ替えます。
* レポートの右端にある![省略記号アイコンまたは詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/ui_18/More.svg)をクリックし、**詳細を表示**&#x200B;または&#x200B;**ダウンロード**&#x200B;をクリックします。


## 健康評価パターン {#ha-patterns}

次に、AEM as a Cloud ServiceでHealth Assessmentが検出するベストプラクティスと問題から逸脱するパターンの完全なリストを示します。 この表では、Content Analysis、Code Analysis、Cloud Service Optimizer パターンの3つのタイプに分類され、各パターンについて説明します。

| パターン名 | カテゴリ | 種類 | 説明 | 影響 | 自動修正しますか？ |
| --- | --- | --- | --- | --- | --- |
| Direct User Additionsを使用したカスタム AEM グループ | セキュリティ | コンテンツ分析 | ユーザーは、IMS グループをメンバーとして追加する代わりに、AEM グループに直接追加されました。 | 権限管理やセキュリティガバナンスは複雑になりがちです。 [IMS サポート &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/ims-support) | いいえ |
| ページにJCR コンテンツノードがありません | リポジトリ構造 | コンテンツ分析 | ページ内に`jcr:content` ノードがありません。 | Experience Manager as a Cloud Serviceの機能の制限。 [&#x200B; パターン検出 – ACV](https://experienceleague.adobe.com/ja/docs/experience-manager-pattern-detection/table-of-contents/acv) | いいえ |
| ページにSling リソースタイプがありません | リポジトリ構造 | コンテンツ分析 | ページに`sling:resourceType`がありません。 | Experience Manager as a Cloud Serviceの機能の制限。 [&#x200B; パターン検出 – ACV](https://experienceleague.adobe.com/ja/docs/experience-manager-pattern-detection/table-of-contents/acv) | いいえ |
| ノード数が多すぎるページ | パフォーマンス | コンテンツ分析 | ページには、構造内に多数のノードが含まれています。 | ページの読み込み速度が遅いことと、ユーザーエクスペリエンスが貧弱。 [&#x200B; パターン検出 – PCX](https://experienceleague.adobe.com/ja/docs/experience-manager-pattern-detection/table-of-contents/pcx) | いいえ |
| 過度な実行ワークフローインスタンス | パフォーマンス | コンテンツ分析 | 実行中のワークフローインスタンスが多すぎます。 | 全体的なシステムパフォーマンスの低下： [&#x200B; メンテナンスタスク &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/operations/maintenance) | いいえ |
| 完了した未消去のワークフローインスタンス | パフォーマンス | コンテンツ分析 | 完了した古いワークフローインスタンスはパージされません。 | システム効率の低減とストレージコストの増大： [&#x200B; メンテナンスタスク &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/operations/maintenance) | いいえ |
| コンテンツフラグメント使用統計 | 統計 | コンテンツ分析 | 使用中のコンテンツフラグメントの数を追跡します。 | 該当なし | 該当なし |
| コンテンツフラグメントモデル使用統計 | 統計 | コンテンツ分析 | 使用中のコンテンツフラグメントモデルの数を追跡します。 | 該当なし | 該当なし |
| MSM多数のブループリント | 統計 | コンテンツ分析 | ブループリントの数を追跡します。 | 管理が複雑になり、コンテンツガバナンスがより困難になる可能性があります。 | 該当なし |
| ブループリントごとのMSM ページ | 統計 | コンテンツ分析 | ブループリントごとのページ数を追跡します。 | 管理が複雑になり、コンテンツガバナンスがより困難になる可能性があります。 | 該当なし |
| MSMの過度なライブコピー | 統計 | コンテンツ分析 | ライブコピーの数を追跡します。 | ロールアウト中にパフォーマンスの問題が発生し、コンテンツの同期が複雑になる可能性があります。 | 該当なし |
| ブループリントごとのMSMの過剰なライブコピー | 統計 | コンテンツ分析 | ブループリントごとのライブコピー数を追跡します。 | ロールアウト中にパフォーマンスの問題が発生し、コンテンツの同期が複雑になる可能性があります。 | 該当なし |
| Assets数 | 統計 | コンテンツ分析 | アセット数を追跡します。 | 該当なし | 該当なし |
| サイト数 | 統計 | コンテンツ分析 | サイト数を追跡します。 | 該当なし | 該当なし |
| Forms数 | 統計 | コンテンツ分析 | フォーム数を追跡します。 | 該当なし | 該当なし |
| フォームフラグメント | 統計 | コンテンツ分析 | フォームフラグメントの数を追跡します。 | 該当なし | 該当なし |
| Interaction Communications | 統計 | コンテンツ分析 | フォームの通信インタラクション数を追跡します。 | 該当なし | 該当なし |
| FDM | 統計 | コンテンツ分析 | フォームデータモデルの数を追跡します。 | 該当なし | 該当なし |
| 古い依存関係 | 依存関係 | コード分析 | 顧客リポジトリ内の古い依存関係をハイライト表示します。 | 新しいAEMのバージョンとの互換性がありません。潜在的なセキュリティ上の脆弱性。 | いいえ |
| AEM SDK バージョンの不一致 | 依存関係 | コード分析 | （n-2）より古いバージョンとCloud Managerのバージョンを比較します。 | Cloud Managerでビルドエラーが発生したり、ローカル開発環境で問題が発生したりする可能性があります。 | いいえ |
| 古いMockito コア依存関係 | 依存関係 | コード分析 | 4.x.x未満のバージョンは、AEM as a Cloud Serviceでは古いものとみなされます。 | Cloud Managerでビルドエラーが発生したり、ローカル開発環境で問題が発生したりする可能性があります。 | いいえ |
| サポートされていない注釈 | 依存関係 | コード分析 | お客様のCloud Manager リポジトリでサポートされていない注釈。 | アプリケーションの潜在的な障害とパフォーマンスの低下。 | いいえ |
| Sling モデルでの@Inject注釈 | 依存関係 | コード分析 | 非推奨の`@Inject`注釈。 | 射出解像度のオーバーヘッドにより、アプリケーションのパフォーマンスが低下します。 | いいえ |
| アウトバウンド HTTP リクエスト | パフォーマンス | Cloud Service Optimizerのアンチパターン | リクエストコンテキストでの問題のある使用、タイムアウトが多い、または接続を閉じていない。 | 全体的なシステムパフォーマンスの低下と考えられる障害。 | はい |
| 処理に時間のかかるクエリ | パフォーマンス | Cloud Service Optimizerのアンチパターン | 顧客コード内のクエリの動作が遅い。 | システムのパフォーマンスの低下とタイムアウトの可能性。 | はい |

### カテゴリ {#ha-patterns-categories}

| カテゴリ | 説明 |
| --- | --- |
| セキュリティ | セキュリティの取り組み、ユーザー管理、アクセス制御に関連するパターン。 |
| パフォーマンス | アプリケーションとシステムのパフォーマンスに影響を与えるパターン。 |
| リポジトリ構造 | JCR リポジトリの組織と構造に関連するパターン。 |
| 依存関係 | コードの依存関係とバージョン管理に関連するパターン。 |
| 統計 | 利用状況の統計と指標を表すパターン。 |
