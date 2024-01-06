---
title: パイプラインの管理
description: 既存のパイプラインの管理方法（編集、実行、削除を含む）を説明します。
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 97%

---


# パイプラインの管理 {#managing-pipelines}

既存のパイプラインの管理方法（編集、実行、削除を含む）を説明します。

## パイプラインカード {#pipeline-card}

Cloud Manager の&#x200B;**プログラムの概要**&#x200B;ページにある&#x200B;**パイプライン**&#x200B;カードには、すべてのパイプラインとその現在のステータスの概要が表示されます。

![Cloud Manager のパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

各パイプラインの横にある省略記号ボタンをクリックすると、次の操作を実行できます。

* [パイプラインを実行](#running-pipelines)
* [パイプラインを編集](#editing-pipelines)
* [パイプラインを削除](#deleting-pipelines)
* [詳細を表示](#view-details)

パイプラインのリストの下部には、一般的なオプションがあります。

* **追加** - [新しい実稼動パイプラインを追加](configuring-production-pipelines.md)するか、[新しい実稼動以外のパイプラインを追加](configuring-non-production-pipelines.md)します。
* **すべて表示** - ユーザーをパイプライン画面に移動して、すべてのパイプラインをより詳細なテーブルに表示します
* **リポジトリ情報にアクセス** - Cloud Manager の Git リポジトリへのアクセスに必要な情報を表示します
* **詳細情報** - CI／CD パイプラインのドキュメントリソースに移動します。

## パイプラインウィンドウ {#pipelines}

**パイプライン**&#x200B;ウィンドウには、選択したプログラムのすべてのパイプラインの完全なリストが表示されます。これは、[パイプラインカード](#pipeline-card)で使用可能な情報よりも包括的な情報を表示するので便利です。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページで、「**パイプライン**」タブを選択して、**パイプライン**&#x200B;ウィンドウに切り替えます。

1. ここには、プログラムのすべてのパイプラインのリストが表示され、でのように、パイプライン実行を開始および停止できます。 **パイプラインカード**.

パイプラインが実行中の場合、**ステータス**&#x200B;列にポインタを合わせると、実行に関する詳細が表示されます。

![パイプライン実行の詳細](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

「**詳細を表示**」をタップまたはクリックすると、[パイプライン実行の詳細](#view-details)が表示されます。

## アクティビティウィンドウ {#activity}

**アクティビティ**&#x200B;ウィンドウには、選択したプログラムのすべてのパイプライン実行の完全なリストが表示されます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページで、「**アクティビティ**」タブを選択して、**アクティビティ**&#x200B;ウィンドウに切り替えます。

1. ここでは、現在および過去の実行を含む、プログラムのすべてのパイプライン実行のリストを確認できます。

パイプラインが実行中の場合、**ステータス**&#x200B;列にポインタを合わせると、実行に関する詳細が表示されます。

![パイプライン実行の詳細](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

「**詳細を表示**」をタップまたはクリックすると、[パイプライン実行の詳細](#view-details)が表示されます。

## パイプラインの実行 {#running-pipelines}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、実行するパイプラインの横にある省略記号ボタンをクリックして、メニューから「**実行**」を選択します。

1. パイプラインの実行が開始され、「**ステータス**」列に示されます。

実行の詳細を確認するには、省略記号ボタンをもう一度クリックし、「**[詳細を表示](#view-details)**」を選択します。

パイプラインのタイプによっては、省略記号ボタンをもう一度クリックして「**キャンセル**」を選択すると、実行をキャンセルできる場合があります。

## パイプラインの編集 {#editing-pipelines}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、編集するパイプラインの横にある省略記号ボタンをクリックして、メニューから「**編集**」を選択します。

1. 「**実稼動パイプラインを編集**」または「**実稼動以外のパイプラインを編集**」ダイアログボックスが表示され、パイプラインの作成時に入力したのと同じ詳細を編集できます。

   * パイプラインで使用できるフィールドと設定オプションについて詳しくは、次のページを参照してください。
      * [実稼動パイプラインの設定](configuring-production-pipelines.md)
      * [実稼動以外のパイプラインの設定](configuring-non-production-pipelines.md)

1. パイプラインの編集が完了したら、「**更新**」をクリックします。

>[!NOTE]
>
>実行中のパイプラインは編集できません。

## パイプラインの削除 {#deleting-pipelines}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、実行するパイプラインの横にある省略記号ボタンをクリックして、メニューから「**削除**」を選択します。

>[!NOTE]
>
>実行中のパイプラインは削除できません。

## パイプラインの詳細を表示 {#view-details}

パイプラインの詳細を表示して、最後の実行のステータスとログを確認できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、実行するパイプラインの横にある省略記号ボタンをクリックして、メニューから「**詳細を表示**」を選択します。

1. 実行中のパイプラインの詳細ページに移動します。

![パイプラインの詳細](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

ここから、診断の目的で、パイプラインの様々なステップのステータスを確認し、ビルドログを取得できます。コードデプロイメントと実行されているテストについて詳しくは、[コードのデプロイ](/help/implementing/cloud-manager/deploy-code.md)ドキュメントを参照してください。

パイプライン実行のすべての手順が表示され、まだ開始されていない手順はグレーアウトされます。完了した手順には、期間が表示されます。

パイプラインの手順が完了すると、概要が表示されます。

![手順の概要](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

「**詳細を表示**」リンクを選択すると、「**期間**」セクションが表示されます。これには、そのプログラムの過去のトレンドに基づくパイプラインの平均期間が含まれます。

![期間](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

>[!NOTE]
>
>実行中または少なくとも 1 回実行されたパイプラインの詳細のみ表示できます。

## パイプラインをキャンセル {#cancel}

パイプラインが検証またはイメージのビルドフェーズにある場合は、パイプライン実行を安全にキャンセルできます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. プログラムの概要ページで、**パイプライン**&#x200B;カードでキャンセルするパイプラインの省略記号ボタンをクリックします。

   ![パイプラインのキャンセル](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. **キャンセル**&#x200B;を選択します。

または、パイプラインの詳細ページからパイプラインをキャンセルすることもできます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから「**パイプライン**」タブに移動し、キャンセルするパイプラインを選択します。

1. 実行中のパイプラインの詳細ページに移動します。

   ![パイプラインの詳細をキャンセル](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. **キャンセル**&#x200B;を選択します。
