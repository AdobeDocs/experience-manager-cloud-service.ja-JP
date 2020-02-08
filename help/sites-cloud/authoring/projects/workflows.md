---
title: プロジェクトワークフローの操作
description: すぐに使用可能な様々なプロジェクトワークフローが用意されています。
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# プロジェクトワークフローの操作 {#working-with-project-workflows}

すぐに使用可能なプロジェクトワークフローには、次のものがあります。

* **プロジェクト承認ワークフロー** — このワークフローでは、ユーザーにコンテンツを割り当て、確認してから承認できます。
* **リクエストの開始** — 開始をリクエストするワークフロー。
* **リクエストランディングページ** — このワークフローはランディングページをリクエストします。
* **電子メールをリクエスト** - 電子メールをリクエストするワークフローです。
* **DAM 言語コピー作成／翻訳および DAM 言語コピーを作成** - アセットおよびフォルダー用に翻訳されたバイナリ、メタデータ、タグを作成します。

選択するプロジェクトテンプレートに応じて、以下の特定のワークフローが使用可能です。

|  | **シンプルなプロジェクト** | **メディアプロジェクト** | **翻訳プロジェクト** |
|---|:-:|:-:|:-:|
| コピーをリクエスト |  | x |  |
| 撮影した製品写真 |  | x |  |
| プロジェクト承認 | x |  |  |
| ローンチをリクエスト | x |  |  |
| ランディングページをリクエスト | x |  |  |
| 電子メールをリクエスト | x |  |  |
| DAM Create Language Copy&amp;ast; |  |  | x |
| DAM Create and Translate Language Copy&amp;ast; |  |  | x |

>[!NOTE]
>
>&amp;ast; These workflows are not started from the **Workflow** tile in Projects. アセットの言語コピーの作成を参照してください。
<!--
>&ast; These workflows are not started from the **Workflow** tile in Projects. See [Creating Language Copies for Assets.](/help/sites-administering/tc-manage.md)
-->

ワークフローを開始および完了する手順は、どのワークフローを選択した場合も同じです。手順が変わるだけです。

ワークフローは、プロジェクト内で直接開始します（DAM 言語コピーを作成または DAM 言語コピー作成／翻訳を除く）。プロジェクト内の未処理のタスクに関する情報は、**タスク**&#x200B;タイルに表示されます。完了する必要があるタスクに関する通知は、ユーザーアイコンの横に表示されます。

AEMでのワークフローの操作について詳しくは、次を参照してください。

* [ワークフローへの参加](/help/sites-cloud/authoring/workflows/participating.md)
* [ページへのワークフローの適用](/help/sites-cloud/authoring/workflows/applying.md)
* ワークフローの設定 <!--* [Configuring workflows](/help/sites-administering/workflows.md)-->

このセクションでは、プロジェクトに使用可能なワークフローについて説明します。

## コピーをリクエストワークフロー {#request-copy-workflow}

このワークフローでは、ユーザーの原稿をリクエストし、承認することができます。コピーをリクエストワークフローを開始するには：

1. メディアプロジェクトで&#x200B;**ワークフロー**&#x200B;タイルの「**+**」記号を選択し、「**コピーをリクエストワークフロー**」を選択します。
1. 原稿のタイトルと、リクエストするものの簡単な概要を入力します。必要に応じて、ターゲットの単語数、タスクの優先度および期限を入力します。

   ![コピーワークフローの要求](/help/sites-cloud/authoring/assets/projects-request-copy.png)

1. 「**作成**」をクリックします。ワークフローが開始されます。タスクが&#x200B;**タスク**&#x200B;タイルに表示されます。

   ![リクエストのコピーが追加されました](/help/sites-cloud/authoring/assets/projects-request-copy-add.png)

## プロジェクト承認ワークフロー {#project-approval-workflow}

プロジェクト承認ワークフローでは、コンテンツをユーザーに割り当て、レビューし、コンテンツを承認します。

1. In your Simple project, select the **`+`** sign in the **Workflows** tile and select **Project Approval Workflow**.
1. タイトルを入力し、チームリストから割り当て先を選択します。必要に応じて、説明、コンテンツのパス、タスクの優先度および期限を入力します。

   ![承認の要求](/help/sites-cloud/authoring/assets/projects-approval.png)

1. 「**作成**」をクリックします。ワークフローが開始されます。タスクが&#x200B;**タスク**&#x200B;タイルに表示されます。

   ![要求の承認が追加されました](/help/sites-cloud/authoring/assets/projects-approval-add.png)

## ローンチをリクエストワークフロー {#request-launch-workflow}

このワークフローでは、ローンチをリクエストできます。

1. シンプルなプロジェクトで&#x200B;**ワークフロー**&#x200B;タイルの「**+**」記号を選択し、「**ローンチをリクエストワークフロー**」を選択します。
1. ローンチのタイトルを入力し、ローンチのソースパスを指定します。必要に応じて、説明とライブ日付も追加できます。希望するローンチの動作に応じて「ソースページのライブデータを継承」または「サブページを除外」を選択します。

   ![リクエストの開始](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. 「**作成**」をクリックします。ワークフローが開始されます。**ワークフローが「ワークフロー」リ**&#x200B;ストに表示されます&#x200B;**(「楕円」をクリ**&#x200B;ックします…」をクリックし **て** 、このリストにアクセスします。

## アセットの言語コピー作成（および翻訳）ワークフロー {#create-and-translate-language-copy-workflow-for-assets}

The **Create Language Copy** and the **Create and Translate Language Copy** workflows are covered in detail in creating language copies for assets.
