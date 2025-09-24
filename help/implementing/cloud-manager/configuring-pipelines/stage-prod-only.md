---
title: ステージング専用パイプラインと実稼動専用パイプラインの分割
description: 専用パイプラインを使用してステージングデプロイメントと実稼動デプロイメントを分割する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#staging-production-only-pipelines"
hide: true
hidefromtoc: true
index: false
exl-id: 7d76a87c-122c-4c4d-8071-957bef4c9cf1
source-git-commit: 51318172b826eb81dff86b3e8dfb6f2ded648c4c
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 48%

---

# ステージのみのパイプラインと実稼動のみのパイプラインの分割 {#stage-prod-only}

専用パイプラインを使用してステージングデプロイメントと実稼動デプロイメントを分割できます。

## 概要 {#overview}

ステージング環境と実稼動環境は緊密に結び付いています。デフォルトでは、それらに対するデプロイメントは単一のパイプラインにリンクされます。これは、そのプログラムのステージング環境と実稼動環境の両方にデプロイされるデプロイメントパイプラインです。この結合は通常は適切ですが、デメリットが存在する特定のユースケースがあります。

* ステージング専用環境にデプロイする場合は、パイプラインの&#x200B;**実稼動環境に昇格**&#x200B;手順を拒否します。ただし、実行はキャンセルとしてマークされます。
* ステージング環境の最新コードを実稼動環境にデプロイする場合は、コードが変更されていなくても、ステージングデプロイメントを含むパイプライン全体を再デプロイする必要があります。
* デプロイメント中は環境を更新できません。実稼動環境に昇格する前にステージング環境で数日間一時停止してテストする場合、実稼動環境はロックされたままになり、更新できません。このシナリオにより、[環境変数](/help/implementing/cloud-manager/environment-variables.md)の更新などの非依存タスクが不可能になります。

ステージング専用パイプラインと実稼動専用パイプラインは、専用のデプロイメントオプションを提供することで、これらのユースケースに対するソリューションを提供します。

* **ステージング専用デプロイメントパイプライン：**&#x200B;ステージング環境にのみデプロイされ、デプロイメントとテストが完了すると実行が終了します。ステージング専用パイプラインは、標準の結合されたフルスタック実稼動パイプラインと同じように動作しますが、実稼動環境のデプロイメント手順（承認、スケジュール、デプロイ）はありません。
* **実稼動専用デプロイメントパイプライン：** 成功した最新のステージ実行を選択して、実稼動環境にのみデプロイします。 次に、そのアーティファクトを実稼動環境にデプロイします。実稼動専用パイプラインは、ステージデプロイメントアーティファクトを再利用し、ビルドフェーズをバイパスします。

フルスタック実稼動パイプラインの進行中は、ステージング専用パイプラインと実稼動専用パイプラインは実行されません。その逆も同様です。ステージング専用パイプラインとフルスタック実稼動パイプラインの両方に **Git の変更時**&#x200B;トリガーが設定され、同じブランチとリポジトリを指している場合、ステージング専用パイプラインのみが自動的に開始されます。実稼動専用パイプラインはリポジトリに直接リンクされていないので、**`On Git Changes`** には開始されません。

実稼動専用パイプラインは、**Git の変更時**&#x200B;のリポジトリに直接リンクされていないので、手動でトリガーされます。

これらの専用パイプラインはより柔軟性に優れていますが、次の操作の詳細と推奨事項に注意する必要があります。

>[!NOTE]
>
>実稼動専用パイプラインは、常にステージング専用パイプラインからのアーティファクトを利用します。このプロセスは、標準の結合された実稼動パイプラインがその間にステージング環境に他のものをデプロイした場合でも当てはまります。
>
>* このようなシナリオにより、不要なコードのロールバックが発生する可能性があります。
>* アドビでは、実稼動専用パイプラインとステージング専用パイプラインの使用を開始したら、結合された標準の実稼動パイプラインの使用を停止することをお勧めします。
>* 引き続き標準の結合パイプラインとステージング専用パイプライン／実稼動専用パイプラインの両方を実行することにした場合は、コードのロールバックを回避するためにアーティファクトの再利用を念頭に置いてください。

## パイプラインの作成 {#pipeline-creation}

実稼動専用パイプラインとステージング専用パイプラインは、標準の[実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)と[実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)の結合と同様の方法で作成されます。詳しくは、これらの資料を参照してください。

1. **パイプライン**&#x200B;ウィンドウで、「**パイプラインを追加**」をクリックします。

   * 「**実稼動以外のパイプラインを追加**」を選択して [ ステージ専用パイプラインを作成 ](#stage-only) します。
   * **実稼動専用パイプラインを追加** を選択して [ 実稼動専用パイプラインを作成 ](#prod-only) します。

![実稼動専用パイプライン／ステージング専用パイプラインの作成](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-stage-pipeline.png)

>[!NOTE]
>
>対応するパイプラインが既に存在する場合、特定のオプションはグレー表示される場合があります。
>
>* ステージング専用パイプラインがまだ存在しない場合、「**実稼動専用パイプラインを追加**」は使用できません。
>* 標準の結合パイプラインが既に存在する場合、「**実稼動パイプラインを追加**」は使用できません。
>* プログラム別に許可される実稼動専用パイプラインとステージング専用パイプラインは 1 つだけです。

### ステージのみのパイプラインを作成 {#stage-only}

1. **実稼動以外のパイプラインを追加** ダイアログボックスの「**設定**」タブで、パイプラインの「**デプロイメントパイプライン**」フィールドを選択します。
1. 「実稼動以外のパイプライン名」フィールドに、任意の名前を入力します。
1. 必要なデプロイメントオプションを選択し、「**続行**」をクリックします。

   ![ 実稼動以外のパイプラインを追加ダイアログボックスの「設定」タブ ](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-1.png)

1. 「**Source コード**」タブで、「**フルスタックコード**」を選択します。 このオプションは、AEM アプリケーション全体（バックエンド、Dispatcher/web 階層設定、リポジトリ内のフロントエンドモジュール）のビルドとデプロイをおこないます。

1. **適格なデプロイメント環境** ドロップダウンリストで、パイプラインのデプロイメント環境として **ステージ** 環境を選択します。 「ステージ」を選択すると、ステージ環境専用のパイプラインが作成されます（実稼動のプロモーションは別のパイプラインによって行われます）。

1. **リポジトリ** と **Git ブランチ** をそれぞれのドロップダウンリストで選択し、「**続行**」をクリックします。

   ![ 実稼動以外のパイプラインを追加ダイアログボックスの「Source コード」タブ ](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-2.png)

1. 「**エクスペリエンス監査**」タブで指定されたサイト URL は、Cloud Managerがページ品質を監査する公開済み URL です。

1. **ページパス** フィールドで、監査するページを指定し、**![追加アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) ページを追加** をクリックします。

   エクスペリエンス監査は、追加した各パスを分析して、パフォーマンス、アクセシビリティ、プログレッシブ Web アプリ、ベストプラクティス、SEO、その他の品質チェックを行います。 複数のパスを追加して削除するには、![ クロスサイズ 400 アイコン ](https://spectrum.adobe.com/static/icons/ui_18/CrossSize400.svg) をクリックします。

   ![ 実稼動以外のパイプラインを追加ダイアログボックスの「エクスペリエンス監査」タブ ](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-3.png)

1. 「**保存**」をクリックします。


### 実稼動専用パイプラインの作成 {#prod-only}

1. **実稼動のみのパイプラインを追加** ダイアログボックスで、「**パイプライン名**」テキストフィールドにパイプラインのフリーテキスト名を入力します。
1. **パイプライン名** フィールドに、必要な名前を入力します。
1. **実稼動デプロイメントオプション** で、「**実稼動へのデプロイ前に一時停止**」を選択します。

   このオプションを選択すると、実稼動手順の直前に手動承認ゲートが挿入されます。 パイプラインは停止し、承認者（デプロイメントマネージャーやビジネスオーナーなど）が実稼動デプロイを承認またはキャンセルするのを待ちます。

   変更制御または直前のチェックに使用します。

1. 「**保存**」をクリックして、これらのオプションを含む実稼動専用パイプラインを作成します。

   ![実稼動専用パイプラインの作成](/help/implementing/cloud-manager/configuring-pipelines/assets/add-production-only-pipeline.png)

## ステージング専用および実稼動専用パイプラインの実行 {#running}

新しいパイプラインは [ 他のパイプラインと同様 ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines) 開始できます。 ステージングのみのパイプラインのトリガーの詳細から直接実稼動のみのパイプラインを実行することもできます。

<!-- * Stage-only and prod-only pipelines offer a new [emergency mode](#emergency-mode) to skip testing.
Prod-only pipeline run can be triggered directly from the execution details of a [stage-only pipeline](#stage-only-run).


### Emergency Mode {#emergency-mode}

When starting production-only and staging-online pipelines, you are prompted to confirm the start and how it starts.

* **Normal Mode** is a standard run and includes stage testing steps.
* **Emergency Mode** skips stage testing steps.

![Emergency Mode](/help/assets/configure-pipelines/emergency-mode.png) -->

### ステージ専用パイプラインの実行 {#stage-only-run}

実行詳細には、テストステップの後に「ビルドを昇格 **ボタンが表示され** す。 クリックして、この実行のステージアーティファクトを実稼動環境にデプロイする実稼動専用パイプラインをトリガーにします。 このボタンは、成功した最新のステージのみ実行した場合にのみ表示されます。

![ステージング専用パイプラインの実行](/help/implementing/cloud-manager/configuring-pipelines/assets/stage-only-pipelines-run.png)

**ビルドを昇格** をクリックすると、関連する実稼動専用パイプラインの実行を確認するダイアログボックスが開きます。 「**実行**」をクリックして開始します。

![ ビルドを昇格 – パイプラインを実行ダイアログボックス ](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-run.png)

何も存在しない場合は、設定ダイアログボックスが表示され、作成するように求められます。

![ ビルドを昇格 – 有効なパイプラインがありませんダイアログボックス ](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-no-valid-pipeline.png)


### 実稼動専用パイプラインの実行 {#prod-only-run}

**実稼動専用** パイプラインの場合、Cloud Managerには実稼動環境にデプロイされたソースアーティファクトが表示されます。 ソース実行の **アーティファクトの準備** ステップを確認し、それを開いて詳細とログを表示します。


![アーティファクトの詳細](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-only-pipelines-run.png)
