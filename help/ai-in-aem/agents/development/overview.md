---
title: 開発エージェントの概要
description: Cloud Managerの開発エージェントがAEMの失敗したパイプラインを分析し、ログを作成してコード修正を提案し、デバッグを高速化する方法を説明します。
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Architect, Developer
source-git-commit: 3e565ba0cd53d9064a9aed20f4d6663781759b63
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# 開発エージェントの概要 {#development-agent-overview}

開発エージェントは、AEMの開発者と管理者がコードをより効率的に作成、デバッグ、デプロイおよび最適化するのに役立ちます。

現在、エージェントはパイプラインステータスを取得でき、修正を提案することで、失敗するビルドステップのトラブルシューティングに役立ちます。これにより、AEM as a Cloud Serviceのデプロイメントを開発環境、ステージング環境および実稼動環境にデバッグする際の時間を節約できます。 ビルドログと関連コードを調べて、手動で適用できる修正をお勧めします。

>[!VIDEO](https://video.tv.adobe.com/v/3478008?captions=jpn&quality=12&learn=on)

>[!IMPORTANT]
>
>AI によって生成された応答は、不正確であったり、誤解を招く可能性があります。 推奨される修正および回答を再確認してください。
>
>[Adobe Experience Cloud ジェネレーティブ AI ユーザーガイドライン &#x200B;](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) も参照してください。

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

## Cloud Managerから開発エージェントにアクセスする {#how-to-access-the-agent}

Development Agent には、Cloud ManagerやExperience Hubなどのユーザーインターフェイスにある AI Assistant を使用してアクセスします。

**Cloud Managerから Development Agent にアクセスするには：**

1. 開始するには、[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) をクリックしてホームページを開きます。

   ![Adobe Experience Cloudのホームページ &#x200B;](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. 左側のレールの「**サービス**」見出しの下の「**Cloud Manager**」をクリックします。

   ![&#x200B; 「コンテンツ作成者」プリセットを表示するドロップダウンリストが選択されている &#x200B;](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >表示されるウィジェット、ツールおよびアーティファクトは、ユーザーのペルソナ、使用権限およびAEM デプロイメントタイプ（AEM as a Cloud ServiceまたはManaged Services 6.5/6.5 LTS）によって異なります。

1. 左側のパネルの **プログラム** で、「概要アイコン **![概要 &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) をクリック** ます。

1. **プログラムの概要** ページの **パイプライン** カードで、パイプラインをクリックします。

   ![&#x200B; 選択したパイプライン &#x200B;](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-select.png)

1. **ビルドとコードスキャン** ページで、失敗したパイプラインを確認します。

   ![&#x200B; ビルドページとコードスキャンページに表示されるパイプラインエラー &#x200B;](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-failure.png)

1. AEM ユーザーインターフェイス（Cloud Manager ページまたはAEM環境のオーサーインスタンス）の右上隅付近にある「**AI アシスタント**」アイコンをクリックします。

   ![&#x200B; ツールバーの AI アシスタントアイコン &#x200B;](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   [AEMの AI アシスタント &#x200B;](/help/implementing/cloud-manager/ai-assistant-in-aem.md) も参照してください。

1. 下部の **AI アシスタント** パネルのテキストボックスに、質問またはプロンプトを入力し、`Enter` キーを押すか、![&#x200B; 送信アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg) をクリックします。

   例：
   *「eda-org-01-no-access」プログラムで、「no-access」パイプラインのエラーを分析してトラブルシューティングします。*

   プロンプトで次の応答が返されます。

   ![AI アシスタントのプロンプトと結果の応答 &#x200B;](/help/ai-in-aem/agents/development/assets/dev-agent-prompt-response.png)


## 権限 {#permissions}

開発エージェントのパイプライントラブルシューティング ジョブには、Cloud Manager – 開発者ロールまたはCloud Manager - プログラムマネージャーロールが必要です。



## サンプルプロンプト {#sample-prompts}

| プロンプト | 結果 |
| --- | --- |
| *プログラムのメインプログラムの失敗したパイプラインをリストします。* | 結果はさまざまですが、このプロンプトでは、失敗したパイプラインのテーブルと、分析する特定のパイプラインを参照するためのフォローアップの提案が出力されます。 |
| *「開発パイプライン」という失敗したパイプラインを分析* | このプロンプトにより、失敗したパイプラインの分析と修正の提案が表示されます。 |

## 範囲外の機能 {#out-of-scope-features}

パイプラインのトラブルシューティングは、フルスタックパイプラインのビルドステップで機能します。 その他のパイプラインタイプおよび手順の場合は、ログをダウンロードして調べることで、エラーをデバッグできます。

[&#x200B; ログへのアクセスとダウンロード &#x200B;](/help/implementing/cloud-manager/manage-logs.md) を参照してください。

パイプラインのトラブルシューティングは、BYOGIT （Bring Your Own Git）を使用したプログラムではサポートされていません。

