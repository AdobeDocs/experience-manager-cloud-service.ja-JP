---
title: 実稼動環境およびステージング環境のヘルスアセスメント
description: Cloud Managerのヘルスアセスメントの使用方法を説明します。 AEM環境のスキャン、レポートの実行とレビュー、イシューの詳細の表示、PDF のエクスポート、過去の実行の管理を行うことができます。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 9%

---


# 健全性の評価 {#about-health-assessment}

ヘルスアセスメントは、AEM as a Cloud Service内のCloud Managerの実稼動環境およびステージング環境に対する、透過的な自動スキャンです。 コンテンツ、コード、設定を評価して、アンチパターンを見つけ、ベストプラクティスから逸脱し、セキュリティとパフォーマンスを向上させます。

正常性評価サービスでは、以下の処理を行います。

* 環境をスキャンし、パフォーマンスのボトルネック、非効率性、リスクを明らかにします。
* ブループリント、ライブコピー、顧客設定などのコンテンツ構造を分析します。
* AEM SDKやサードパーティライブラリなど、古い依存関係を検出します。
* 誤った注釈や非効率的なパターンなど、コード品質の問題にフラグを付けます。
* ダッシュボード（アクションセンターなど）で実用的なガイダンスを提供します。
* プロアクティブな修復を実行して、システムのパフォーマンスを向上させます。

各実行では、重要度別の問題、ガイダンスと推奨される修正点へのリンクがリスト表示され、レポートのPDF書き出しがサポートされます。 現在の状態の **最新レポート** ビューと **過去のレポート** を使用して、実行を比較できます。

ルールの定義と修正の詳細については、[ 正常性評価パターン ](#ha-patterns) も参照してください。

## 正常性評価ページへのアクセス {#access-health-assessment}

1. [experiece.adobe.com](https://experience.adobe.com) で Cloud Manager にログインします。
1. 「**クイックアクセス**」セクションで、「**Experience Manager**」をクリックします。
1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。
1. 必要な組織を選択します。 以下の画像は説明用です。 独自の組織名を選択します。

   ![Cloud Managerでの組織の選択 ](/help/implementing/cloud-manager/reports/assets/ha-org.png)

1. **マイプログラム** コンソールで、レポートを表示するプログラムをクリックします。

1. 次のいずれかの操作を行います。
   * **環境** カードで、環境名の右側にある ![ 省略記号アイコンまたは詳細アイコン ](https://spectrum.adobe.com/static/icons/ui_18/More.svg) をクリックし、メニューから **状態評価** を選択します。

     ![ 環境カードの省略記号メニューから「正常性の評価」を選択 ](/help/implementing/cloud-manager/reports/assets/ha-myprograms-environments-card.png)

   * 左側のメニューの **サービス** で、![ データアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)**環境** をクリックします。 環境ページで、環境名の右側にある ![ 省略記号アイコンまたは詳細アイコン ](https://spectrum.adobe.com/static/icons/ui_18/More.svg) をクリックし、メニューから **状態評価** を選択します。

     ![ 環境ページの省略記号メニューから「正常性の評価」を選択 ](/help/implementing/cloud-manager/reports/assets/ha-environments-page.png)

## 選択した環境に対して新しいレポートを実行 {#run-report}

1. [ 正常性評価ページにアクセス ](#access-health-assessment)。
1. **状態評価** ページの右上隅で、評価するターゲット環境を確認します。

   環境が正しくない場合は、![ 山形記号の付いたメニューまたはドロップダウンメニューをクリックして、別の環境を選択 ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) し、リストから正しい環境を選択します。

1. 「**レポートを実行**」をクリックします。

   ![[ 正常性評価 ] ページの [ 新しいレポートの生成 ] ボタンをクリックしてください ](/help/implementing/cloud-manager/reports/assets/ha-run-report.png)

   選択した環境に対してレポートが実行される間、レポートが完了するまで **レポートを実行** は無効のままになります。

   ![ 走行中の通報 ](/help/implementing/cloud-manager/reports/assets/ha-running-report.png)

   レポートが完成すると、レポートは **正常性の評価** ページの **最新のレポート** セクションに表示されます。

## 最新のレポートを表示 {#view-latest-report}

* **ヘルスアセスメント** ページで、「**最新レポート**」セクションの以下の情報を確認します。

   * 最新の実行の結果。
   * 実行日時。
   * 合計発行数。
   * 重大な問題のハイライト。
   * アクション：すべてのイシューの **[詳細を表示](#view-report-details)** または **[PDFをダウンロード](#download-pdf-report)**。

  ![ 選択した環境の新しいレポートの生成後の最新の評価ページ ](/help/implementing/cloud-manager/reports/assets/ha-latest-report-page.png)

### 最新のレポートの詳細を表示 {#view-report-details}

* **ヘルスアセスメント** ページで、**最新レポート** タイトルの右側にある ![ 省略記号アイコンまたは詳細アイコン ](https://spectrum.adobe.com/static/icons/ui_18/More.svg) をクリックし、**詳細を表示** または **ダウンロード** をクリックします。

  「**詳細を表示**」オプションには、次の情報が表示されます。

   * 問題の包括的なリスト。
   * 結果と問題の説明を表示できます。
   * 可能性のある修正を含むドキュメントを表示できる。

     ![ イシューの説明と結果 ](/help/implementing/cloud-manager/reports/assets/ha-issue-descriptions-and-findings.png)

   * 「**ダウンロード**」オプションを使用すると、PDFで個々のイシューレポートをダウンロードできます。

     ![ 個々のイシューレポートのPDFをダウンロードする ](/help/implementing/cloud-manager/reports/assets/ha-details-page-doc-links.png)


### レポート全体のPDFをダウンロード {#download-pdf-report}

* レポートページの右上隅付近にある「**ダウンロード**」をクリックします。

  そのレポートで検出されたすべての問題に対する PDF を含む ZIP ファイルが生成されます。

  ![ レポートで見つかったすべての問題のPDFをダウンロード ](/help/implementing/cloud-manager/reports/assets/ha-download-pdf.png)


## 過去のレポートの確認 {#review-past-reports}

**ヘルスアセスメント** ページで、**過去のレポート** の節を確認して、以下の情報を確認します。

* 以前のレポートの詳細を表示します。
* 各実行日を表示します。
* 任意のレポートのPDFをダウンロードします。
* 日付、問題数、環境で並べ替えます。

![ 過去のレポートの確認 ](/help/implementing/cloud-manager/reports/assets/ha-past-reports.png)

* 「**過去のレポート**」見出しの右側にある ![ 山形記号のドロップダウンまたはドロップダウンメニューから別の環境を選択 ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) をクリックすると、過去のレポートが日付順に並べ替えられます。
* レポートの右端にある ![ 省略記号アイコンまたは詳細アイコン ](https://spectrum.adobe.com/static/icons/ui_18/More.svg) をクリックし、「**詳細を表示**」または **ダウンロード** をクリックします。


## 正常性評価パターン {#ha-patterns}

AEM as a Cloud Serviceでヘルスアセスメントによって検出されるアンチパターンと問題の完全なリストを以下に示します。 この表は、項目をコンテンツ分析、コード分析、Cloud Service Optimizer アンチパターンの 3 つのタイプに分類し、それぞれに説明を提供します。

| パターン名 | カテゴリ | タイプ | 説明 | 影響 | 自動修正？ |
| --- | --- | --- | --- | --- | --- |
| ユーザーへの直接の追加を含むカスタム AEM グループ | セキュリティ | コンテンツ分析 | ユーザーが、IMS グループをメンバーとして追加するのではなく、AEM グループに直接追加された。 | 権限管理とセキュリティガバナンスは複雑になる場合があります。 [IMS のサポート ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/ims-support) | いいえ |
| ページに JCR コンテンツノードがありません | リポジトリ構造 | コンテンツ分析 | ページに `jcr:content` ノードがありません。 | Experience Manager as a Cloud Serviceの機能制限。 [ パターン検出 – ACV](https://experienceleague.adobe.com/ja/docs/experience-manager-pattern-detection/table-of-contents/acv) | いいえ |
| ページに Sling リソースタイプがありません | リポジトリ構造 | コンテンツ分析 | ページに `sling:resourceType` がありません。 | Experience Manager as a Cloud Serviceの機能制限。 [ パターン検出 – ACV](https://experienceleague.adobe.com/ja/docs/experience-manager-pattern-detection/table-of-contents/acv) | いいえ |
| ノード数が過剰なページ | パフォーマンス | コンテンツ分析 | ページの構造には、多数のノードが含まれます。 | ページの読み込み時間が遅く、ユーザーエクスペリエンスが低下する。 [ パターン検出 – PCX](https://experienceleague.adobe.com/ja/docs/experience-manager-pattern-detection/table-of-contents/pcx) | いいえ |
| 実行中のワークフローインスタンスが多すぎる | パフォーマンス | コンテンツ分析 | 実行されているワークフローインスタンスが多すぎます。 | 全体的なシステムパフォーマンスの低下。 [ メンテナンスタスク ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/operations/maintenance) | いいえ |
| パージされていない完了したワークフローインスタンス | パフォーマンス | コンテンツ分析 | 完了した古いワークフローインスタンスはパージされません。 | システム効率の低下とストレージコストの増加。 [ メンテナンスタスク ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/operations/maintenance) | いいえ |
| コンテンツフラグメントの使用状況の統計 | 統計 | コンテンツ分析 | 使用中のコンテンツフラグメント数をトラッキングします。 | 該当なし | 該当なし |
| コンテンツフラグメントモデルの使用状況統計 | 統計 | コンテンツ分析 | 使用中のコンテンツフラグメントモデルの数をトラッキングします。 | 該当なし | 該当なし |
| MSM の多数のブループリント | 統計 | コンテンツ分析 | ブループリントの数をトラッキングします。 | これにより、管理がより複雑になり、コンテンツガバナンスがより困難になる可能性があります。 | 該当なし |
| ブループリントごとの MSM ページ | 統計 | コンテンツ分析 | ブループリントごとのページ数をトラッキングします。 | これにより、管理がより複雑になり、コンテンツガバナンスがより困難になる可能性があります。 | 該当なし |
| MSM の過剰なライブコピー | 統計 | コンテンツ分析 | ライブコピー数をトラッキングします。 | ロールアウト中にパフォーマンスの問題が発生し、コンテンツの同期が複雑になる可能性があります。 | 該当なし |
| ブループリントごとの MSM 過剰なライブコピー | 統計 | コンテンツ分析 | ブループリントごとにライブコピー数をトラッキングします。 | ロールアウト中にパフォーマンスの問題が発生し、コンテンツの同期が複雑になる可能性があります。 | 該当なし |
| Assets数 | 統計 | コンテンツ分析 | アセット数をトラッキングします。 | 該当なし | 該当なし |
| サイト数 | 統計 | コンテンツ分析 | サイト数をトラッキングします。 | 該当なし | 該当なし |
| Forms数 | 統計 | コンテンツ分析 | フォーム数をトラッキングします。 | 該当なし | 該当なし |
| フォームフラグメント | 統計 | コンテンツ分析 | フォームフラグメントの数をトラッキングします。 | 該当なし | 該当なし |
| インタラクション通信 | 統計 | コンテンツ分析 | フォーム通信インタラクションの回数をトラッキングします。 | 該当なし | 該当なし |
| FDM | 統計 | コンテンツ分析 | フォームデータモデルの数をトラッキングします。 | 該当なし | 該当なし |
| 古い依存関係 | 依存関係 | コード分析 | 顧客リポジトリ内の古い依存関係をハイライト表示します。 | 新しいAEM バージョンとの非互換性。セキュリティの脆弱性が生じる可能性があります。 | いいえ |
| AEM SDKのバージョンの不一致 | 依存関係 | コード分析 | Cloud Manager環境のバージョンと比較して（n-2）より古いバージョン。 | Cloud Managerでビルドエラーが発生したり、ローカル開発環境で問題が発生したりする可能性があります。 | いいえ |
| 古い Mockito Core 依存関係 | 依存関係 | コード分析 | 4.x.x より前のバージョンは、AEM as a Cloud Serviceでは古いと見なされます。 | Cloud Managerでビルドエラーが発生したり、ローカル開発環境で問題が発生したりする可能性があります。 | いいえ |
| サポートされていない注釈 | 依存関係 | コード分析 | お客様のCloud Manager リポジトリでサポートされていない注釈。 | 潜在的なアプリケーション障害とパフォーマンスの低下。 | いいえ |
| Sling モデルの@Inject Annotation | 依存関係 | コード分析 | `@Inject` 注釈を非推奨（廃止予定）。 | インジェクション解決のオーバーヘッドにより、アプリケーションのパフォーマンスが低下しました。 | いいえ |
| アウトバウンド HTTP リクエスト | パフォーマンス | Cloud Service Optimizer アンチパターン | リクエストコンテキストでの問題のある使用方法、タイムアウトが大きい、接続が閉じられていない。 | 全体的なシステムパフォーマンスの低下と考えられる停止。 | はい |
| 処理に時間のかかるクエリ | パフォーマンス | Cloud Service Optimizer アンチパターン | 顧客コードの低速クエリ。 | システムパフォーマンスが低下し、タイムアウトの可能性がある。 | はい |

### カテゴリ {#ha-patterns-categories}

| カテゴリ | 説明 |
| --- | --- |
| セキュリティ | セキュリティ対策、ユーザー管理およびアクセス制御に関連するパターン。 |
| パフォーマンス | アプリケーションとシステムのパフォーマンスに影響を与えるパターン。 |
| リポジトリ構造 | JCR リポジトリの組織および構造に関連するパターン。 |
| 依存関係 | コードの依存関係およびバージョン管理に関連するパターン。 |
| 統計 | 使用統計と指標を表すパターン。 |



