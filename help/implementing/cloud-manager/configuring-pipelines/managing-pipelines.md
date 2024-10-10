---
title: パイプラインの管理
description: 既存のパイプラインの管理方法（編集、実行、削除を含む）を説明します。
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f7a8e823f058115f11241f0864517432a7dea5ab
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 34%

---


# パイプラインの管理 {#managing-pipelines}

既存のパイプラインの管理方法（編集、実行、削除を含む）を説明します。

## パイプラインカード {#pipeline-card}

Cloud Manager の&#x200B;**プログラムの概要**&#x200B;ページにある&#x200B;**パイプライン**&#x200B;カードには、すべてのパイプラインとその現在のステータスの概要が表示されます。

![Cloud Manager のパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

各パイプラインの横にある ![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックすると、次の操作を実行できます。

* [パイプラインを実行](#running-pipelines)
* [パイプラインのキャンセル](#cancel)
* [パイプラインの編集](#editing-pipelines)
* [パイプラインの削除](#deleting-pipelines)
* [パイプラインの前回の実行詳細の表示](#view-details)

パイプラインのリストの下部には、次の一般的なオプションがあります。

* **追加** -[ 新しい実稼動パイプラインを追加 ](configuring-production-pipelines.md) または [ 新しい実稼動以外のパイプラインを追加 ](configuring-non-production-pipelines.md)
* **すべて表示** - ユーザーをパイプライン画面に移動して、すべてのパイプラインをより詳細なテーブルに表示します
* **リポジトリ情報にアクセス** - Cloud Manager の Git リポジトリへのアクセスに必要な情報を表示します
* **詳細情報** - CI／CD パイプラインのドキュメントリソースに移動します。

## パイプラインページ {#pipelines}

**パイプライン** ページには、選択したプログラムのすべてのパイプラインの完全なリストが表示されます。 この情報は、[ パイプラインカード ](#pipeline-card) で使用可能な情報よりも包括的な情報を提供するので便利です。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要** ページで、「![ パイプライン」タブ – ワークフローアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) 「**パイプライン**」タブをクリックします。

1. **パイプライン** ページには、プログラムのすべてのパイプラインのリストが表示され、**パイプライン** カードと同じようにパイプラインの実行を開始および停止できます。

パイプラインが実行中の場合は、![ ステータス ](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) 列の **情報 – 中アイコン** をクリックすると、実行の詳細を示すポップアップが表示されます。 ポップアップ内で、「詳細を表示 **をクリックして** パイプライン実行の詳細 [ を表示し ](#view-details) す。

![パイプライン実行の詳細](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)


パイプラインの横にある ![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、パイプラインの状態に適した追加のアクション（[ 編集 ](#editing-pipelines) または [ 実行のキャンセル ](#cancel) を実行することもできます。

![パイプラインアクション](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

## アクティビティページ {#activity}

**アクティビティ** ページには、選択したプログラムのすべてのパイプライン実行の完全なリストと、その他の重要なプログラムイベントが表示されます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要** ページのサイドメニューで、![ ベルアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg)**アクティビティ** をクリックします。

1. **アクティビティ** ページには、現在および過去の実行を含む、プログラムのすべてのパイプライン実行のリストが表示されます。

パイプラインが実行中の場合は、![ ステータス ](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) 列の **情報 – 中アイコン** をクリックすると、実行に関する情報を示すポップアップが表示されます。

![パイプライン実行の詳細](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

パイプライン実行を表す行をクリックして、[ パイプライン実行の詳細 ](#view-details) を表示します。

![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、詳細の表示やログのダウンロードなど、パイプライン実行に関する追加のアクションを実行すると、[ パイプラインの詳細ページ ](#view-details) に移動できます。

![パイプライン実行アクション](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## パイプラインを実行 {#running-pipelines}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動します。

1. 実行するパイプラインの横にある ![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューから、![ ファイル名を指定して実行 – 再生アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PlayCircle_18_N.svg)**ファイル名を指定して実行** をクリックします。

   パイプラインの実行が開始され、「**ステータス**」列に進行状況が表示されます。

実行の詳細を確認するには、もう一度 ![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックし、「**[詳細を表示](#view-details)** をクリックします。

パイプラインのタイプによっては、![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) を再度クリックして「キャンセル **をクリックすると、実行をキャンセルできる場合があ** ます。

## パイプラインの編集 {#editing-pipelines}

実行されていないパイプラインは編集できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動します。

1. 編集するパイプラインの横にある ![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューから、「**編集**」をクリックします。

1. **実稼動パイプラインを編集** または **実稼動以外のパイプラインを編集** ダイアログボックスで、パイプラインの作成時に入力したのと同じ詳細を編集します。

   パイプラインで使用できるフィールドと設定オプションについて詳しくは、次のページを参照してください。
   * [実稼動パイプラインの設定](configuring-production-pipelines.md)
   * [実稼動以外のパイプラインの設定](configuring-non-production-pipelines.md)

1. 完了したら、「**更新**」をクリックします。

>[!NOTE]
>
>Web 階層設定パイプラインは、プライベートリポジトリではサポートされていません。詳細と制限事項の一覧については、[Cloud Managerのプライベート GitHub リポジトリーを追加する ](/help/implementing/cloud-manager/managing-code/private-repositories.md) を参照してください。

## パイプラインの削除 {#deleting-pipelines}

実行中でないパイプラインは削除できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動します。

1. 実行するパイプラインの横にある ![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューから、「**削除**」をクリックします。


## パイプラインの前回の実行詳細の表示 {#view-details}

パイプラインの詳細を確認して、最新の実行のステータスとログを表示できます。 ただし、詳細にアクセスできるのは、パイプラインが現在実行中か、少なくとも 1 回実行されている場合のみです。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動します。

1. ドロップダウンメニューから、実行するパイプラインの横にある ![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューから、「**最後の実行を表示**」をクリックします。

   実行中のパイプラインの詳細ページに移動します。

   ![パイプラインの詳細](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

   ここから、診断の目的で、パイプラインの様々なステップのステータスを確認し、ビルドログを取得できます。コードのデプロイメントとテストの実行について詳しくは、[ コードのデプロイ ](/help/implementing/cloud-manager/deploy-code.md) を参照してください。

   パイプライン実行のすべての手順が表示され、まだ開始されていない手順はグレーアウトされます。完了した手順には、期間が表示されます。

   パイプラインステップが完了すると、概要が表示されます。

   ![手順の概要](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

1. 「**詳細を表示**」をクリックして「**期間**」セクションを展開すると、プログラムの履歴トレンドに基づいてパイプラインの平均期間を確認できます。

   ![期間](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

1. 問題のフラグが設定された **コードスキャン** 手順がパイプラインに含まれている場合は、「**詳細をダウンロード**」をクリックして、成功しなかった [ コード品質テスト ](/help/implementing/cloud-manager/code-quality-testing.md) のリストにアクセスします。

   ![コード品質の問題](assets/managing-pipelines-code-quality-issues.png)

   CSV ファイルには「プロジェクトファイルの場所 **列が含まれ** おり、プロジェクトに関連する問題のあるコードへのパスを示しています。 これに対し、「**ファイルの場所**」列には、Maven で生成されたパスが反映されます。

   ![プロジェクトコードスキャン問題の詳細](assets/managing-pipelines-code-quality-details.png)

## パイプラインのキャンセル {#cancel}

検証またはビルド画像フェーズのパイプライン実行は安全にキャンセルできます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. プログラムの概要ページで、キャンセルするパイプラインの ![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) を **パイプライン** カードでクリックします。

   ![ パイプラインのキャンセル ](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. **キャンセル** をクリックします。

または、パイプラインの詳細ページでパイプラインをキャンセルできます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. ![ プログラムの概要 **ページから「** パイプライン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) タブ – ワークフローアイコン **** パイプライン タブに移動し、キャンセルするパイプラインを選択します。

   実行中のパイプラインの詳細ページに移動します。

   ![パイプラインの詳細をキャンセル](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. **キャンセル** をクリックします。
