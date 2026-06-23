---
title: ステージ専用パイプラインと実稼動専用パイプラインの分割
description: 専用パイプラインを使用してステージングデプロイメントと実稼動デプロイメントを分割する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
hidefromtoc: false
index: true
exl-id: 7d76a87c-122c-4c4d-8071-957bef4c9cf1
source-git-commit: 1eb2a3fede53e01f07f511ae24de5ac1f11b8821
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 60%

---

# ステージ専用パイプラインと実稼動専用パイプラインの分割 {#stage-prod-only}

<!--
 REMOVED AS PER CQDOC-23086 ON OCTOBER 3, 2025:
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#staging-production-only-pipelines"
-->

専用パイプラインを使用してステージングデプロイメントと実稼動デプロイメントを分割できます。

## 概要 {#overview}

ステージング環境と本番環境は緊密に結び付いています。 デフォルトでは、それらに対するデプロイメントは単一のパイプラインにリンクされます。 デプロイメントパイプラインは、そのプログラムのステージング環境と実稼動環境の両方にデプロイされます。 このカップリングは通常は適していますが、欠点が生じる特定のユースケースがあります。

* ステージングにデプロイする場合は、パイプラインの&#x200B;**製品への昇格** ステップを拒否します。 ただし、実行はキャンセルとしてマークされます。
* ステージング環境の最新コードを実稼動環境にデプロイする場合は、コードが変更されていなくても、ステージングデプロイメントを含むパイプライン全体を再デプロイする必要があります。
* デプロイメント中は環境を更新できません。 実稼動環境に昇格する前に、ステージング環境で数日間テストを待っている場合、実稼動環境は使用できなくなり、更新できません。 このシナリオは、[環境変数](/help/implementing/cloud-manager/environment-variables.md)の更新など、依存しないタスクを防ぎます。

ステージのみのパイプラインとプロダクトのみのパイプラインは、専用のデプロイメントオプションを提供することで、これらのユースケースに対するソリューションを提供します。

* **ステージング専用デプロイメントパイプライン：**&#x200B;ステージング環境にのみデプロイされ、デプロイメントとテストが完了すると実行が終了します。 ステージング専用パイプラインは、標準の結合されたフルスタック実稼動パイプラインと同じように動作しますが、実稼動環境のデプロイメント手順（承認、スケジュール、デプロイ）はありません。
* **実稼動専用デプロイメントパイプライン：**&#x200B;最新の成功したステージ実行を選択して、実稼動環境にのみデプロイします。 その後、アーティファクトを本番環境にデプロイします。 製品専用パイプラインは、ビルド フェーズを省略して、ステージのデプロイメント アーティファクトを再利用します。

フルスタック実稼動パイプラインの進行中は、ステージング専用パイプラインと実稼動専用パイプラインは実行されません。その逆も同様です。 ステージング専用パイプラインとフルスタック実稼動パイプラインの両方に **Git の変更時**&#x200B;トリガーが設定され、同じブランチとリポジトリを指している場合、ステージング専用パイプラインのみが自動的に開始されます。 実稼働専用パイプラインは、リポジトリに直接リンクされていないため、**`On Git Changes`**&#x200B;をトリガーしません。

実稼働専用パイプラインは、**Git変更時**&#x200B;のトリガーのリポジトリに直接リンクされていないため、手動でトリガーされます。

これらの専用パイプラインは、より柔軟な運用を提供しますが、運用と推奨事項について次の点に注意してください。

>[!NOTE]
>
>実稼動専用パイプラインは、常にステージング専用パイプラインからのアーティファクトを利用します。 このプロセスは、標準結合生産パイプラインがその間にステージに別のバージョンをデプロイした場合でも当てはまります。
>
>* このシナリオでは、意図しないコードロールバックが発生します。
>* Adobeでは、実稼動のみのパイプラインとステージのみのパイプラインの使用を開始したら、標準的な結合実稼動パイプラインの使用を停止することをお勧めします。
>* 引き続き標準の結合パイプラインとステージング専用パイプライン／実稼動専用パイプラインの両方を実行することにした場合は、コードのロールバックを回避するためにアーティファクトの再利用を念頭に置いてください。

## パイプラインの作成 {#pipeline-creation}

実稼動専用およびステージ専用のパイプラインは、[実稼動用パイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)と[実稼動以外のパイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)が結合された標準のパイプラインと同様に作成されます。 詳しくは、これらの資料を参照してください。

1. **パイプライン**&#x200B;ウィンドウで、「**パイプラインを追加**」をクリックします。

   * [ステージ専用パイプラインを作成](#stage-only)するには、「**実稼動以外のパイプラインを追加**」を選択します。
   * [実稼動専用パイプラインを作成](#prod-only)するには、「**実稼動専用パイプラインを追加**」を選択します。

![実稼動専用パイプライン／ステージング専用パイプラインの作成](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-stage-pipeline.png)

>[!NOTE]
>
>対応するパイプラインが既に存在する場合、特定のオプションがグレー表示されます。
>
>* ステージング専用パイプラインがまだ存在しない場合、「**実稼動専用パイプラインを追加**」は使用できません。
>* 標準の結合パイプラインが既に存在する場合、「**実稼動パイプラインを追加**」は使用できません。
>* プログラムごとに、1つの実稼動専用パイプラインと1つのステージ専用パイプラインのみが許可されます。

### ステージ専用パイプラインの作成 {#stage-only}

1. **実稼動以外のパイプラインを追加** ダイアログボックスの「**設定**」タブで、パイプラインの「**デプロイメントパイプライン**」フィールドを選択します。
1. 「実稼動以外のパイプライン名」フィールドに、フリーテキスト名を入力します。
1. 目的のデプロイメントオプションを選択し、「**続行**」をクリックします。

   ![実稼動以外のパイプラインを追加ダイアログボックスの「設定」タブ](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-1.png)

1. 「**ソースコード**」タブで、「**フルスタックコード**」を選択します。 このオプションは、AEM アプリケーション全体（バックエンド、Dispatcher／web 層設定、リポジトリ内のフロントエンドモジュール）のビルドとデプロイを行います。

1. **適格なデプロイメント環境**&#x200B;ドロップダウンリストで、パイプラインのデプロイメント環境として&#x200B;**ステージ**&#x200B;環境を選択します。 ステージを選択すると、ステージ環境専用のパイプラインが作成されます（実稼動プロモーションは別のパイプラインを介して行われます）。

1. それぞれのドロップダウンリストで&#x200B;**リポジトリ**&#x200B;と **Git 分岐**&#x200B;を選択し、「**続行**」をクリックします。

   ![実稼動以外のパイプラインを追加ダイアログボックスの「ソースコード」タブ](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-2.png)

1. 「**エクスペリエンス監査**」タブで、指定されたサイト URLは、Cloud Managerがページ品質を監査する公開URLです。

1. 「**ページパス**」フィールドで監査するページを指定し、**![追加アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)ページを追加** をクリックします。

   エクスペリエンス監査は、パフォーマンス、アクセシビリティ、プログレッシブ web アプリ、ベストプラクティス、SEO、その他の品質チェックのために追加した各パスを分析します。 ![クロスサイズ 400 アイコン](https://spectrum.adobe.com/static/icons/ui_18/CrossSize400.svg) をクリックすると、複数のパスを追加および削除できます。

   ![実稼動以外のパイプラインを追加ダイアログボックスの「エクスペリエンス監査」タブ](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-3.png)

1. 「**保存**」をクリックします。


### 実稼動専用パイプラインの作成 {#prod-only}

1. **実稼動専用パイプラインを追加** ダイアログボックスの「**パイプライン名**」テキストフィールドに、パイプラインのフリーテキスト名を入力します。
1. 「**パイプライン名**」フィールドに、目的の名前を入力します。
1. **実稼動デプロイメントオプション**&#x200B;で、「**実稼動へのデプロイ前に一時停止**」を選択します。

   このオプションを選択すると、実稼動手順の直前に手動承認ゲートが挿入されます。 パイプラインは停止し、承認者（デプロイメントマネージャーやビジネスオーナーなど）が実稼動デプロイを承認またはキャンセルするのを待ちます。

   変更管理または直前の確認に使用します。

1. 「**保存**」をクリックして、これらのオプションを含む実稼動専用パイプラインを作成します。

   ![実稼動専用パイプラインの作成](/help/implementing/cloud-manager/configuring-pipelines/assets/add-production-only-pipeline.png)

## ステージ専用パイプラインと実稼動専用パイプラインの実行 {#running}

新しいパイプラインは、[他のパイプラインと同様に](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)開始できます。 また、ステージ専用パイプラインの実行詳細から実稼動専用パイプラインを直接トリガーすることもできます。

<!--
 * Stage-only and prod-only pipelines offer a new [emergency mode](#emergency-mode) to skip testing.
Prod-only pipeline run can be triggered directly from the execution details of a [stage-only pipeline](#stage-only-run).


### Emergency Mode {#emergency-mode}

When starting production-only and staging-online pipelines, you are prompted to confirm the start and how it starts.

* **Normal Mode** is a standard run and includes stage testing steps.
* **Emergency Mode** skips stage testing steps.

![Emergency Mode](/help/assets/configure-pipelines/emergency-mode.png)
-->

### ステージ専用パイプラインの実行 {#stage-only-run}

実行詳細では、テスト手順の後に「**ビルドを昇格**」ボタンが表示されます。 これをクリックすると、この実行のステージアーティファクトを実稼動環境にデプロイする実稼動専用パイプラインがトリガーされます。 ボタンは、最新のステージのみの実行が成功した場合にのみ表示されます。

![ステージング専用パイプラインの実行](/help/implementing/cloud-manager/configuring-pipelines/assets/stage-only-pipelines-run.png)

「**ビルドを昇格**」をクリックすると、関連する実稼動専用パイプラインの実行を確認するためのダイアログボックスが開きます。 開始するには、**実行**&#x200B;をクリックします。

![ビルドを昇格 - パイプラインを実行ダイアログボックス](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-run.png)

存在しない場合は、設定ダイアログボックスに作成を求めるプロンプトが表示されます。

![ビルドを昇格 - 有効なパイプラインがありませんダイアログボックス](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-no-valid-pipeline.png)


### 実稼動専用パイプラインの実行 {#prod-only-run}

**実稼動専用**&#x200B;パイプラインの場合、Cloud Manager には実稼動環境にデプロイされているソースアーティファクトが表示されます。 ソース実行の&#x200B;**アーティファクトの準備**&#x200B;ステップを確認し、それを開いて詳細とログを表示します。


![アーティファクトの詳細](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-only-pipelines-run.png)
