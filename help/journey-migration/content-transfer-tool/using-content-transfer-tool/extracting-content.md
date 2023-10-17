---
title: ソースからのコンテンツの抽出
description: ソースAdobe Experience Manager(AEM) インスタンスからコンテンツを抽出し、後でCloud ServiceAEMインスタンスに転送する方法を説明します。
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 031ddfa2da0fc5ecc92267eae1f9dcaac394573d
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 44%

---

# ソースからのコンテンツの抽出 {#extracting-content}

## コンテンツ転送ツールの抽出プロセス {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="コンテンツの抽出"
>abstract="抽出とは、ソース Adobe Experience Manager（AEM）インスタンスから、移行セットと呼ばれる一時領域にコンテンツを抽出することです。移行セットは、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#top-up-extraction-process" text="追加抽出"


コンテンツ転送ツールで移行セットを抽出するには、次の手順に従います。

>[!NOTE]
>Amazon S3、Azure Data Store、またはファイルデータストアをデータストアのタイプとして使用する場合は、オプションのプリコピー手順を実行して、抽出段階の速度を上げることができます。 プレコピー手順は、最初の完全な抽出と取り込みに最も効果的です。詳しくは、[大規模なコンテンツリポジトリの処理](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)を参照してください。

1. 移行セットを **コンテンツ転送** ウィザードとクリック **抽出** 抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >抽出キーが有効で、有効期限に近いものでないことを確認します。 有効期限が近い場合は、移行セットを選択して「プロパティ」をクリックすることで、抽出キーを更新できます。 クリック **更新**. Cloud Acceleration Manager が表示され、ここで **抽出キーをコピー**. クリックするたびに **抽出キーをコピー**に設定すると、新しい抽出キーが生成され、作成日から 14 日間有効です。
   >![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. 抽出ダイアログが表示されます。 クリック **抽出** をクリックして、抽出段階を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14b.png)

   >[!NOTE]
   >オプションで、抽出段階でステージングコンテナを上書きできます。 次の場合 **ステージングコンテナを上書き** が無効になっている場合、コンテンツパスやインクルードバージョンの設定が変更されていない後続の移行で、抽出を高速化できます。 ただし、コンテンツパスやインクルードバージョンの設定が変更されている場合は、「**ステージングコンテナを上書き**」を有効にしてください。

1. 「**抽出**」フィールドに「**実行中**」ステータスが表示され、抽出が進行中であることを示します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   次をクリックできます。 **進行状況を表示** を使用して、進行中の抽出の詳細を把握できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   また、 Cloud Acceleration Manager からコンテンツ転送ページに移動して抽出段階の進行状況を監視し、「 **...** > **詳細を表示**.

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 抽出が完了したら、他の列 ( **ソース** および **パス** に、入力した移行セットの詳細を示します。 クリック **...** > **詳細を表示** をクリックすると、抽出の各ステップの期間を含む詳細が表示されます。 抽出中にこのダイアログボックスを表示して、手順の進行状況を確認できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## 追加抽出 {#top-up-extraction-process}

コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初の完全抽出に対してコピー前の手順を使用した場合、後続の追加抽出に対してはコピー前の手順をスキップできます（追加の移行セットのサイズが 200 GB 未満の場合）。 これは、プロセス全体にかかる時間が増える可能性があるからです。
>また、追加抽出を実行する際に、最初の抽出を実行した時点からに対して、既存のコンテンツのコンテンツ構造を変更しないことが不可欠です。 最初の抽出以降に構造が変更されたコンテンツに対しては、追加を実行できません。移行作業中には必ず制限するようにしてください。

抽出プロセスが完了したら、追加抽出方式を使用して差分コンテンツを転送できます。

次の手順に従います。

1. **コンテンツ転送** ウィザードに移動し、追加抽出の実行対象となる移行セットを選択します。「**抽出**」をクリックして、追加抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. **移行セットの抽出**&#x200B;ダイアログボックスが表示されます。クリック **抽出**.

   >[!IMPORTANT]
   >「**抽出時にステージングコンテナを上書き**」オプションを無効にしてください。
   >![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## 次の手順 {#whats-next}

コンテンツ転送ツールでソースからのコンテンツの抽出について学習したら、コンテンツ転送ツールでの取り込みプロセスについて学習する準備が整いました。 詳しくは、 [Target へのコンテンツの取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) ここでは、コンテンツ転送ツールから移行セットを取り込む方法について説明します。
