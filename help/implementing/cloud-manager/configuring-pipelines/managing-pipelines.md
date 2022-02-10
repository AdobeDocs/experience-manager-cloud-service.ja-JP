---
title: パイプラインの管理
description: 既存のパイプラインの管理方法（編集、実行、削除を含む）を説明します。
index: true
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 4%

---


# パイプラインの管理 {#managing-pipelines}

既存のパイプラインの管理方法（編集、実行、削除を含む）を説明します。

## パイプラインカード {#pipeline-card}

この **パイプライン** カード **プログラムの概要** Cloud Manager のページには、すべてのパイプラインとその現在のステータスの概要が表示されます。

![Cloud Manager のパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

各パイプラインの横にある省略記号ボタンをクリックすると、次の操作を実行できます。

* [パイプラインを実行](#running-pipelines)
* [パイプラインを編集](#editing-pipelines)
* [パイプラインの削除](#deleting-pipelines)
* [詳細を表示](#view-details)

パイプラインのリストの下部には、一般的なオプションがあります。

* **追加**  — 宛先 [新しい実稼動パイプラインを追加](configuring-production-pipelines.md) または [実稼動以外の新しいパイプラインを追加](configuring-non-production-pipelines.md)
* **すべて表示**  — ユーザーがパイプライン画面に移動し、より詳細なテーブルのすべてのパイプラインを表示します。
* **リポジトリ情報にアクセス** - Cloud Manager の Git リポジトリへのアクセスに必要な情報を表示します
* **詳細情報** - CI/CD パイプラインのドキュメントリソースに移動します。

## 実行中のパイプライン {#running-pipelines}

1. Cloud Manager( ) にログインします。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 適切な組織およびプログラムを選択します。

1. 次に移動： **パイプライン** カード **プログラムの概要** ページを開き、実行するパイプラインの横の省略記号ボタンをクリックします。 **実行** を選択します。

1. パイプラインの実行が開始され、が示します。 **ステータス** 列。

実行の詳細を確認するには、省略記号ボタンをもう一度クリックし、「 」を選択します。 **[詳細を表示します。](#view-details)**

パイプラインのタイプに応じて、省略記号ボタンをもう一度クリックし、「 」を選択すると、実行をキャンセルできます **キャンセル**.

## パイプラインの編集 {#editing-pipelines}

1. Cloud Manager( ) にログインします。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 適切な組織およびプログラムを選択します。

1. 次に移動： **パイプライン** カード **プログラムの概要** ページに移動し、編集するパイプラインの横の省略記号ボタンをクリックし、「 」を選択します。 **編集** を選択します。

1. この **実稼動パイプラインを編集** または **実稼動以外のパイプラインを編集** ダイアログボックスが表示され、パイプラインの作成時に入力したのと同じ詳細を編集できます。

   * パイプラインで使用できるすべてのフィールドと設定オプションの詳細については、次のページを参照してください。
      * [実稼動パイプラインの設定](configuring-production-pipelines.md)
      * [実稼動以外のパイプラインの設定](configuring-non-production-pipelines.md)

1. パイプラインの編集が完了したら、「**更新**」をクリックします。

>[!NOTE]
>
>実行中のパイプラインは編集できません。

## パイプラインの削除 {#deleting-pipelines}

1. Cloud Manager( ) にログインします。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 適切な組織およびプログラムを選択します。

1. 次に移動： **パイプライン** カード **プログラムの概要** ページを開き、実行するパイプラインの横の省略記号ボタンをクリックします。 **削除** を選択します。

>[!NOTE]
>
>実行中のパイプラインは削除できません。

## 詳細を表示 {#view-details}

1. Cloud Manager( ) にログインします。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 適切な組織およびプログラムを選択します。

1. 次に移動： **パイプライン** カード **プログラムの概要** ページを開き、実行するパイプラインの横の省略記号ボタンをクリックします。 **詳細を表示** を選択します。

1. 実行中のパイプラインの詳細ページに移動します。

![パイプラインの詳細](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

ここから、診断の目的で、パイプラインの様々なステップのステータスを確認し、ビルドログを取得できます。 ドキュメントを参照 [コードのデプロイ](/help/implementing/cloud-manager/deploy-code.md) を参照してください。

>[!NOTE]
>
>実行中または少なくとも 1 回実行されたパイプラインの詳細のみ表示できます。