---
title: 実稼動以外のパイプラインの編集
description: 実稼動以外のパイプラインの編集
index: true
source-git-commit: d090329c46155d77a7b132583c777c09555a03c9
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 実稼動以外のパイプラインの編集 {#edit-non-prod-pipeline}

パイプライン設定は、 **パイプラインカード** から **プログラムの概要** ページ。

>[!IMPORTANT]
>実行中のパイプラインは編集できません。

設定済みの実稼動以外のパイプラインを編集するには、次の手順に従います。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページ。

1. 実稼動以外のパイプラインを選択し、をクリックします。 **...**. クリック **編集**（下の図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. この **実稼動パイプラインを編集** ダイアログボックスが表示されます。

   1. この **設定** 「 」タブでは、 **パイプライン名**, **デプロイメントトリガー**、および **重要な指標の失敗の動作**.

      >[!NOTE]
      >詳しくは、 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. この **ソースコード** 「 」タブに、更新情報が表示されます **リポジトリ** そして **Git ブランチ**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. クリック **更新** 実稼動以外のパイプラインの編集が完了したら、

## その他の非実稼動パイプラインアクション {#additional-nonprod-actions}

### 実稼動以外のパイプラインの実行 {#run-nonprod}

パイプラインカードから実稼動パイプラインを実行できます。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページ。

1. クリック **...** から **パイプライン** カードとクリック **実行**（下の図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### 実稼動以外のパイプラインの削除 {#delete-nonprod}

パイプラインカードから実稼動パイプラインを削除できます。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページ。

1. クリック **...** から **パイプライン** カードとクリック **削除**（下の図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)
