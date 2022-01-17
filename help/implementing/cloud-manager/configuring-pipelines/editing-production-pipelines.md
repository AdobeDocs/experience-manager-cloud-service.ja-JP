---
title: 実稼動パイプラインの編集
description: 実稼動パイプラインの編集
index: true
source-git-commit: d090329c46155d77a7b132583c777c09555a03c9
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 96%

---


# 実稼動パイプラインの編集 {#edit-prod-pipeline}

**プログラムの概要**&#x200B;ページでパイプライン設定を編集できます。

>[!IMPORTANT]
>実行中のパイプラインは編集できません。

設定済みのパイプラインを編集するには、次の手順に従います。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動します。

1. **パイプライン**&#x200B;カードの「**...**」をクリックし、「**編集**」をクリックします（下図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. **実稼動パイプラインを編集**&#x200B;ダイアログボックスが表示されます。

   1. 「**設定**」タブでは、「**パイプライン名**」、「**デプロイメントトリガー**」および「**重要な指標のエラー動作**」を更新できます。

      >[!NOTE]
      >Cloud Manager でリポジトリーを追加および管理する方法については、[リポジトリーの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)を参照してください。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. 「**ソース**」タブでは、「**実稼動へのデプロイ前に一時停止**」と「**スケジュール設定**」のチェックボックスオプションが「**実稼動デプロイメントオプション**」に用意されています。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. 「**エクスペリエンス監査**」オプションを使用すると、新しいページを更新または追加できます。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. パイプラインの編集が完了したら、「**更新**」をクリックします。

## 実稼動パイプラインに対するその他のアクション {#additional-prod-actions}

### 実稼動パイプラインの実行 {#run-prod}

パイプラインカードから実稼動パイプラインを実行できます。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動します。

1. **パイプライン**&#x200B;カードの「**...**」をクリックし、「**実行**」をクリックします（下図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

### 実稼動パイプラインの削除 {#delete-prod}

パイプラインカードから実稼動パイプラインを削除できます。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動します。

1. **パイプライン**&#x200B;カードの「**...**」をクリックし、「**削除**」をクリックします（下図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >デプロイメントマネージャーの役割を持つユーザーが、パイプラインカードの「**削除**」オプションを使用して、セルフサービスｓで実稼動パイプラインを削除できるようになりました。