---
title: 実稼動パイプラインの編集
description: 実稼動パイプラインの編集
index: true
source-git-commit: d090329c46155d77a7b132583c777c09555a03c9
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# 実稼動パイプラインの編集 {#edit-prod-pipeline}

パイプライン設定は、 **プログラムの概要** ページ。

>[!IMPORTANT]
>実行中のパイプラインは編集できません。

設定したパイプラインを編集するには、次の手順に従います。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページ。

1. クリック **...** から **パイプライン** カードとクリック **編集**（下の図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. この **実稼動パイプラインを編集** ダイアログボックスが表示されます。

   1. この **設定** 「 」タブでは、 **パイプライン名**, **デプロイメントトリガー**、および **重要な指標の失敗動作**.

      >[!NOTE]
      >詳しくは、 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. この **ソース** 「 」タブに、チェックまたはチェック解除を行うオプションが表示されます **実稼動にデプロイする前に一時停止します** および **予定** オプション **実稼動デプロイメントオプション**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. この **エクスペリエンス監査** オプションを使用すると、新しいページを更新または追加できます。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. クリック **更新** パイプラインの編集が完了したら、

## その他の実稼動パイプラインアクション {#additional-prod-actions}

### 実稼動パイプラインの実行 {#run-prod}

パイプラインカードから実稼動パイプラインを実行できます。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページ。

1. クリック **...** から **パイプライン** カードとクリック **実行**（下の図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

### 実稼動パイプラインの削除 {#delete-prod}

パイプラインカードから実稼動パイプラインを削除できます。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページ。

1. クリック **...** から **パイプライン** カードとクリック **削除**（下の図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >デプロイメントマネージャーの役割を持つユーザーが、 **削除** オプションを使用して、パイプラインカードから取得できます。