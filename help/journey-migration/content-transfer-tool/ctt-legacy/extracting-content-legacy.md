---
title: ソースからのコンテンツの抽出（レガシー）
description: ソースからのコンテンツの抽出
hide: true
hidefromtoc: true
exl-id: 9f43356c-ba51-48bc-97f5-f1f5db81e7f3
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 69%

---

# ソースからのコンテンツの抽出（レガシー） {#extracting-content}

## コンテンツ転送ツールの抽出プロセス {#extraction-process}

コンテンツ転送ツールで移行セットを抽出するには、次の手順に従います。
>[!NOTE]
>Amazon S3 または Azure データストアをデータストアのタイプとして使用する場合は、オプションの事前コピーステップを実行して、抽出段階を大幅に迅速化できます。そのためには、 `azcopy.config` ファイルを作成してください。 詳しくは、[大規模なコンテンツリポジトリーの処理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)を参照してください。

>[!IMPORTANT]
>ソースからコンテンツを抽出する前に、ユーザーマッピングツールを実行する必要があります。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en)を参照してください。

1. **コンテンツ転送**&#x200B;ウィザードで移行セットを選択し、「**抽出**」をクリックして抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. **移行セットの抽出**&#x200B;ダイアログボックスが表示されるので、「**抽出**」をクリックして抽出段階を完了します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >オプションで、抽出段階でステージングコンテナを上書きできます。

   >[!IMPORTANT]
   >ソースからコンテンツを抽出する前に、この移行セットでユーザーマッピングが実行されていない場合は、次の図に示すように、ユーザーマッピング手順が保留中であることを示す警告が表示されます。 選択 **ユーザーをマッピング** をクリックして、[ ユーザマッピング ] ツールを実行します。
   >![画像](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. 「**抽出**」フィールドに「**実行中**」ステータスが表示され、抽出が進行中であることを示します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   抽出が完了すると、移行セットのステータスが&#x200B;**完了**&#x200B;に更新され、*緑で塗りつぶされた*&#x200B;雲のアイコンが「**情報**」フィールドに表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >UI には自動リロード機能があり、30 秒ごとに&#x200B;**コンテンツ転送**ウィザードをリロードします。
   >抽出フェーズが開始されると、書き込みロックが作成され、*60 秒*&#x200B;後に解放されます。したがって、抽出が停止した場合は、ロックが解除されるまで 1 分待ってから、抽出を再開する必要があります。

## 追加抽出 {#top-up-extraction-process}

コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。
>また、追加抽出を実行する際に、最初の抽出を実行した時点からに対して、既存のコンテンツのコンテンツ構造が変更されないようにしてください。 最初の抽出以降に構造が変更されたコンテンツでは、トップアップを実行できません。 移行プロセス中は、必ずこの制限を実施してください。

抽出プロセスが完了したら、追加抽出方式を使用して差分コンテンツを転送できます。

次の手順に従います。

1. **コンテンツ転送** ウィザードに移動し、追加抽出の実行対象となる移行セットを選択します。「**抽出**」をクリックして、追加抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. **移行セットの抽出**&#x200B;ダイアログボックスが表示されます。「**抽出**」をクリックします。

   >[!IMPORTANT]
   >「**抽出時にステージングコンテナを上書き**」オプションを無効にしてください。
   >![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## 次の手順 {#whats-next}

コンテンツ転送ツールの「ソースからのコンテンツの抽出」について学習したら、コンテンツ転送ツールの取り込みプロセスについて学ぶ準備が整いました。 コンテンツ転送ツールから移行セットを取り込む方法については、[Target へのコンテンツの取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照してください。
