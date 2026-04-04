---
title: 開発エージェントの概要
description: AEMのDevelopment Agentが、Cloud Managerで失敗したパイプラインを分析し、コード修正を提案してデバッグを高速化するためのログをビルドする方法を説明します。
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Developer
exl-id: 2194556f-aac2-4cdd-8f7f-00c92c8c4424
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---


# 開発エージェントの概要 {#development-agent-overview}

[Brand Experience Agentの一部として、](/help/ai-in-aem/agents/brand-experience/overview.md)開発エージェントは、AEMの開発者および管理者がより効率的にコードを作成、デバッグ、デプロイ、および最適化できるよう支援します。

エージェントは、パイプラインのステータスを取得し、修正を提案することで、失敗したビルドステップのトラブルシューティングを支援します。これにより、AEM as a Cloud Service デプロイメントを開発環境、ステージ環境、実稼動環境にデバッグする際の時間を節約できます。 ビルドログと関連コードを調べて、手動で適用できる修正を推奨します。

>[!VIDEO](https://video.tv.adobe.com/v/3478006?quality=12&learn=on)

>[!IMPORTANT]
>
>AIによる回答は、不正確または誤解を招く可能性があります。 修正案と回答案を再確認しましょう。
>
>[Adobe Experience Cloud生成AI ユーザーガイドライン &#x200B;](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)も参照してください。

>[!NOTE]
>
>パイプラインのトラブルシューティングはフルスタックパイプライン（デプロイメントとコード品質）に限定されますが、**Web階層設定パイプライン**&#x200B;のサポートはベータ版で利用できるようになりました。 アクセスをリクエストするには、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)に電子メールを送信してください。 AEMのAgentsへの既存のアクセスが必要です。

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

このエージェントにアクセスするには、[&#x200B; リリースノート &#x200B;](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)を参照して、ベータプログラムへの登録方法に関する手順を確認してください。開発エージェントへの関心を必ず示してください。 また、開発エージェント固有のフィードバックを[aem-devagent@adobe.comに電子メールで送信することもできます。](mailto:aem-devagent@adobe.com)

[&#x200B; チュートリアル &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/ai/agents/development-agent-troubleshoot-ci-cd-pipeline)に従って、開発エージェントを使用してパイプラインのエラーをトラブルシューティングする方法を学習します。

## Cloud ManagerからDevelopment Agentにアクセスします {#how-to-access-the-agent}

Development Agentには、Cloud ManagerやExperience HubなどのユーザーインターフェイスにあるAI アシスタントを通じてアクセスします。

1. 開始するには、[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)をクリックしてホームページを開きます。

   ![Adobe Experience Cloud ホームページ &#x200B;](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. 左側のパネルの「**サービス**」見出しの下にある「**Cloud Manager**」をクリックします。

   ![&#x200B; コンテンツ作成者プリセットを表示するドロップダウンリストが選択されています](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >表示されるウィジェット、ツール、アーティファクトは、ユーザーペルソナ、使用権限、AEM デプロイメントタイプ（AEM as a Cloud ServiceまたはManaged Services 6.5/6.5 LTS）によって異なります。

1. 左側のパネルの&#x200B;**プログラム**&#x200B;で、**![概要アイコン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg)概要**&#x200B;をクリックします。

1. **プログラムの概要** ページの&#x200B;**パイプライン** カードで、パイプラインをクリックします。

   ![選択したパイプライン &#x200B;](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-select.png)

1. **ビルドおよびコードスキャン** ページで、失敗したパイプラインに注意してください。

   ビルドおよびコードスキャンページ ![に表示される](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-failure.png) パイプラインの失敗

1. AEM ユーザーインターフェイスの右上隅付近（Cloud Manager ページまたはAEM環境のオーサーインスタンス）で、**AI アシスタント** アイコンをクリックします。

   ![&#x200B; ツールバーのAI アシスタント アイコン &#x200B;](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   AEMの[AI アシスタント &#x200B;](/help/implementing/cloud-manager/ai-assistant-in-aem.md)も参照してください。

1. 下部付近の&#x200B;**AI アシスタント** パネルのテキストボックスに、質問またはプロンプトを入力し、`Enter`を押すか、![送信アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)をクリックします。

   例：
   *「eda-org-01-no-access」プログラムで、「no-access」パイプラインのエラーを分析し、トラブルシューティングを行います。*

   プロンプトの結果、次の応答が返されます。

   ![AI アシスタント プロンプトと結果の応答](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-prompt-response.png)

## 権限 {#permissions}

Development Agentには、Cloud Manager - Developer ロールまたはCloud Manager - Program Manager ロールが必要です。

## サンプルプロンプト {#sample-prompts}

| プロンプト | 結果 |
| --- | --- |
| *失敗したパイプラインのトラブルシューティング* | パイプラインが失敗した理由の分析を実行します。どのパイプラインが参照されているのかわからない場合は、ユーザーに追加の質問が送信されます。 |
| *プログラムのメイン プログラムに失敗したパイプラインを一覧表示します。* | 結果は異なる場合がありますが、このプロンプトは、分析する特定のパイプラインを参照するためのフォローアップの提案とともに、失敗したパイプラインのテーブルを出力します。 |
| *失敗した「開発パイプライン」というパイプラインを分析します。* | このプロンプトを入力すると、失敗したパイプラインの分析が表示され、修正する候補が表示されます。 複数のエラーがある場合は、ユーザーに追加の質問が表示されます。 |
| *パイプライン実行のトラブルシューティング 1234567* | 正確なパイプライン実行idを指定することで、パイプライン分析が実行されます。 |

## 範囲外の機能 {#out-of-scope-features}

パイプラインのトラブルシューティングは、フルスタックのデプロイメントおよびコード品質パイプラインの「ビルドと単体テスト」ステップと「コードスキャン」ステップで実行します。 その他のパイプラインタイプやステップについては、ログをダウンロードして調べることでエラーをデバッグします。

詳細については、[&#x200B; アクセスおよびログのダウンロード &#x200B;](/help/implementing/cloud-manager/manage-logs.md)を参照してください。
