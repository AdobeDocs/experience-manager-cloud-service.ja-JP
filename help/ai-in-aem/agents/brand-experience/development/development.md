---
title: 開発エージェントの概要
description: AEMのDevelopment Agentが、Cloud Managerで失敗したパイプラインを分析し、コードの修正を提案し、デバッグを高速化するためのログを作成する方法、Cloud Manager情報の取得方法、レプリケーションエラーのヘルプ、AEM アップデートのサイレントアワーを設定して無料期間を更新する方法を説明します。
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Developer
exl-id: 2194556f-aac2-4cdd-8f7f-00c92c8c4424
source-git-commit: 0b050b161b11b9b4cd58e575d69472d3173dfe94
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 10%

---


# 開発エージェントの概要 {#development-agent-overview}

[Brand Experience Agentの一部として、](/help/ai-in-aem/agents/brand-experience/overview.md)Development Agentは、従来のAEM Java スタックの開発者および管理者が、より効率的にコードを作成、デバッグ、デプロイ、および最適化するのに役立ちます。

AI アシスタントの会話型インターフェイスを通じてアクセスできる次のジョブをサポートしています。

* Cloud Manager ジョブ：プログラムと環境のリスト、パイプラインステータスなどの読み取り専用オペレーション
* パイプラインのトラブルシューティングジョブ：失敗したパイプラインのデバッグ
* 静止時間数と無料期間の更新の管理ジョブ（制限付き可用性）：静止時間数と無料期間の更新を表示、作成、編集します
* レプリケーショントラブルシューティングジョブ（Beta）：ブロックされたキューなど、レプリケーション関連の問題をデバッグします。

>[!NOTE]
>
> 開発者にとっても、AIを活用した次のような機能は有効です。
> * AEM コンポーネントの生成などのローカル開発シナリオ用の[IDE エージェントスキル ](/help/ai-in-aem/local-development-with-ai-tools.md#agent-skills)。
> * ローカル開発用の[ ローカル MCP サーバー](/help/ai-in-aem/local-development-with-ai-tools.md#aem-quickstart-mcp-server)、特にAEMおよびDispatcherの問題のデバッグ。
> * APIおよびAEM エージェントにアクセスするための[ リモート MCP サーバー](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)。

>[!IMPORTANT]
>
>AIによる回答は、不正確または誤解を招く可能性があります。 修正案と回答案を再確認しましょう。
>
>[Adobe Experience Cloud生成AI ユーザーガイドライン ](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)も参照してください。

開発エージェント固有のフィードバックを[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)に電子メールで送信できます。

## Cloud Manager Job {#cloud-manager-job}

お使いのAEM プログラムと環境に関する情報（以下を含む）を確認します。
* プログラムと環境の一覧表示
* 環境変数のリスト
* パイプラインの名前と現在の実行ステータスおよび手順の詳細の検索
* ダウンロード可能なログへのリンクの取得

### サンプルプロンプト {#sample-cm-job-prompts}


| プロンプト | 結果 |
| --- | --- |
| *すべてのAEM Cloud Service プログラムを一覧表示* | アクセスできるプログラムを一覧表示します。 |
| *プログラム 12345*&#x200B;の詳細を取得 | プログラムの詳細を取得します。 |
| *プログラム 12345*&#x200B;の環境を一覧表示 | プログラム内の環境を一覧表示します。 |
| *実稼動環境のログを取得* | 様々なAEM、Dispatcher、CDN ログファイルへのリンクを取得して、デバッグやその他の目的でダウンロードできるようにします。 |
| プログラム 12345 *の* リスト パイプライン | プログラム内のパイプラインのリスト。 |
| *現在のパイプライン実行のステータスは？* | パイプラインのステータスで応答します。 |
| *パイプライン実行のビルド ログ リンクを取得する12345* | 特定のパイプライン実行のパイプラインビルドログへのリンクを取得します。 |


## 休止時間数と無料期間管理ジョブの更新 {#control-updates-job}

>[!AVAILABILITY]
>
>この機能は限定的な可用性フェーズにあり、今後数週間にわたってロールアウトされる予定です。 [aem-devagent@adobe.comに電子メールを送信します。](mailto:aem-devagent@adobe.com) ただちにアクセス。

AEMのAI アシスタントを通じて、サイレントアワーおよび無料期間を直接表示、作成、編集できます。

主なメリットは、スケジュール設定のエラーが少ないことです。 リクエストを行う際に、アシスタントは可能な限り案内し、適用される制限、例えば3期間の上限、期間の間の必須1週間の間隔、スケジュールできない予定されているメンテナンス除外ウィンドウなどをフラグ付けします。

そのため、設定に失敗した後に制約を検出する代わりに、ビジネスオーナーとデプロイメントマネージャーは、同じ会話で有効なスケジュールに誘導されます。 これにより、重要なビジネスウィンドウを自動メンテナンス更新から保護し、行き違いや設定ミスを減らすことができます。

### サンプルプロンプト {#sample-updates-prompts}

| プロンプト | 結果 |
| --- | --- |
| *プログラム 12345の現在の更新スケジュールを教えてください。* | 現在のAEM更新ルールのリストが表示されます。 |
| *プログラム 12345*&#x200B;の午前9時から午後5時までのESTのAEM更新をブロック | AEMの更新が標準的な勤務時間中に適用されないようにルールを設定します。 |
| *プログラム 12345*&#x200B;の日次アップデートブロックを削除 | AEMの更新を妨げるルールを削除します。 |
| *プログラム 12345*&#x200B;の2週間で始まるAEMの更新を一時停止します | AEMの更新を防ぐルールを作成します。 |
| *プログラムは、都合の悪い時間に更新され続けています。 どのようなオプションがありますか？* | は、AEMの更新スケジュールを制御するためのルールを設定する方法に関する情報を返します。 |



## パイプラインのトラブルシューティングジョブ  {#cloud-manager-pipeline-troubleshooting}

このジョブは、パイプラインのステータスを取得し、修正を提案することで、失敗したビルドステップのトラブルシューティングを支援します。これにより、AEM as a Cloud Service デプロイメントを開発環境、ステージ環境、実稼動環境にデバッグする際の時間を節約できます。 ビルドログと関連コードを調べて、手動で適用できる修正を推奨します。

>[!VIDEO](https://video.tv.adobe.com/v/3478006?quality=12&learn=on)

>[!NOTE]
>
>パイプライントラブルシューティングは、フルスタックパイプライン（デプロイメントとコード品質）とWeb階層設定パイプラインに限定されます。

<!--
To access this agent, please refer to the [release notes](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs) for instructions on how to enroll in the beta program, being sure to indicate your interest in the  Development Agent. You can also email development agent–specific feedback to [aem-devagent@adobe.com.](mailto:aem-devagent@adobe.com)

-->

[ チュートリアル ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/agents/development-agent-troubleshoot-ci-cd-pipeline)に従って、開発エージェントを使用してパイプラインのエラーをトラブルシューティングする方法を学習します。

### Cloud ManagerからDevelopment Agentにアクセスします {#how-to-access-the-agent}

Development Agentには、Cloud ManagerやExperience HubなどのユーザーインターフェイスにあるAI アシスタントを通じてアクセスします。

1. 開始するには、[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) をクリックしてホームページを開きます。

   ![Adobe Experience Cloud のホームページ](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. 左側のパネルの「**サービス**」見出しの下にある「**Cloud Manager**」をクリックします。

   ![ コンテンツ作成者プリセットを表示するドロップダウンリストが選択されています](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >表示されるウィジェット、ツール、アーティファクトは、ユーザーペルソナ、使用権限、AEM デプロイメントタイプ（AEM as a Cloud Service または Managed Services 6.5/6.5 LTS）によって異なります。

1. 左側のパネルの&#x200B;**プログラム**&#x200B;で、**![概要アイコン ](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg)概要**&#x200B;をクリックします。

1. **プログラムの概要** ページの&#x200B;**パイプライン** カードで、パイプラインをクリックします。

   ![選択したパイプライン ](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-select.png)

1. **ビルドおよびコードスキャン** ページで、失敗したパイプラインに注意してください。

   ビルドおよびコードスキャンページ ](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-failure.png)に表示される![ パイプラインの失敗

1. AEM ユーザーインターフェイスの右上隅付近（Cloud Manager ページまたは AEM 環境のオーサーインスタンス）で、「**AI アシスタント**」アイコンをクリックします。

   ![ツールバーの AI アシスタントアイコン](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   AEMの[AI アシスタント ](/help/implementing/cloud-manager/ai-assistant-in-aem.md)も参照してください。

1. 下部付近の **AI アシスタント**&#x200B;パネルのテキストボックスに、質問またはプロンプトを入力し、`Enter` を押すか「![送信アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)」をクリックします。

   例：
   *「eda-org-01-no-access」プログラムで、「no-access」パイプラインのエラーを分析し、トラブルシューティングを行います。*

   プロンプトの結果、次の応答が返されます。

   ![AI アシスタント プロンプトと結果の応答](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-prompt-response.png)

### 権限 {#permissions}

パイプラインのトラブルシューティングジョブには、Cloud Manager – 開発者ロールまたはCloud Manager - プログラムマネージャーロールが必要です。

### サンプルプロンプト {#sample-pipeline-prompts}

| プロンプト | 結果 |
| --- | --- |
| *失敗したパイプラインのトラブルシューティング* | パイプラインが失敗した理由の分析を実行します。どのパイプラインが参照されているのかわからない場合は、ユーザーに追加の質問が送信されます。 |
| *プログラムのメイン プログラムに失敗したパイプラインを一覧表示します。* | 結果は異なる場合がありますが、このプロンプトは、分析する特定のパイプラインを参照するためのフォローアップの提案とともに、失敗したパイプラインのテーブルを出力します。 |
| *失敗した「開発パイプライン」というパイプラインを分析します。* | このプロンプトを入力すると、失敗したパイプラインの分析が表示され、修正する候補が表示されます。 複数のエラーがある場合は、ユーザーに追加の質問が表示されます。 |
| *パイプライン実行のトラブルシューティング 1234567* | 正確なパイプライン実行idを指定することで、パイプライン分析が実行されます。 |

### 範囲外の機能 {#out-of-scope-features}

パイプラインのトラブルシューティングは、フルスタックのデプロイメントおよびコード品質パイプラインの「ビルドと単体テスト」ステップと「コードスキャン」ステップで実行します。 また、[web階層設定パイプライン ](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines)もサポートしています。

その他のパイプラインタイプやステップについては、ログをダウンロードして調べることでエラーをデバッグします。 詳細については、[ アクセスおよびログのダウンロード ](/help/implementing/cloud-manager/manage-logs.md)を参照してください。



## レプリケーショントラブルシューティングジョブ（Beta） {#replication-troubleshooting-job}

ブロックされたキューなど、レプリケーションに関連する問題をデバッグします。

ベータ版プログラムへのアクセスについては、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)まで電子メールでご連絡ください。
