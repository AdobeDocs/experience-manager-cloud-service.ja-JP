---
title: ソースからのコンテンツの抽出
description: ソースの Adobe Experience Manager (AEM) インスタンスからコンテンツを抽出し、後で Cloud Service AEM インスタンスに転送する方法を説明します。
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
feature: Migration
role: Admin
source-git-commit: d568619bd8ebb42a6914211401df680352c921ab
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 100%

---

# ソースからのコンテンツの抽出 {#extracting-content}

## コンテンツトランスファーツールの抽出プロセス {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="コンテンツの抽出"
>abstract="抽出とは、ソース Adobe Experience Manager（AEM）インスタンスから、移行セットと呼ばれる一時領域にコンテンツを抽出することです。 移行セットは、アドビが提供するクラウドストレージエリアで、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#top-up-extraction-process" text="追加抽出"


コンテンツトランスファーツールで移行セットを抽出するには、次の手順に従います。

>[!NOTE]
>Amazon S3、Azure データストア、ファイルデータストアのいずれかをデータストアのタイプとして使用する場合は、オプションの事前コピーステップを実行して、抽出段階を迅速化できます。プレコピー手順は、最初の完全な抽出と取り込みに最も効果的です。詳しくは、[大規模なコンテンツリポジトリの処理](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)を参照してください。

1. **コンテンツ転送**&#x200B;ウィザードで移行セットを選択し、「**抽出**」をクリックして抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!TIP]
   >抽出が成功した直後に取り込みを自動的に開始するようにスケジュールを設定できるようになりました。詳しくは、[ターゲットへのコンテンツの取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照してください。

   >[!IMPORTANT]
   >
   >抽出キーが有効で、有効期限に近づいていないことを確認します。有効期限が近い場合は、移行セットを選択して「プロパティ」をクリックすることで、抽出キーを更新できます。「**更新**」をクリックします。Cloud Acceleration Manager が表示されるので、そこで「**抽出キーをコピー**」をクリックできます。「**抽出キーをコピー**」をクリックするたびに、新しい抽出キーが生成され、作成日から 14 日間有効です。
   >![画像](/help/journey-migration/content-transfer-tool/assets-ctt/migrationSetDetails.png)

1. 抽出ダイアログが表示されます。「**抽出**」をクリックして、抽出段階を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/migrationSetExtraction.png)

   >[!NOTE]
   >オプションで、抽出段階でステージングコンテナを上書きできます。「**ステージングコンテナを上書き**」が無効になっている場合、コンテンツパスやインクルードバージョンの設定が変更されていない後続の移行については、抽出を高速化できます。ただし、コンテンツパスやインクルードバージョンの設定が変更されている場合は、「**ステージングコンテナを上書き**」を有効にしてください。

1. 「**抽出**」フィールドに「**実行中**」ステータスが表示され、抽出が進行中であることを示します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   「**進行状況を表示**」をクリックして、進行中の抽出の詳細を把握できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/viewProgress.png)

   また、コンテンツ転送ページにアクセスして Cloud Acceleration Manager から抽出段階の進行状況を監視することもできます。さらに、**…**／**詳細を表示**&#x200B;をクリックして詳細を確認することもできます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 抽出が完了したら、**ソース**&#x200B;および&#x200B;**パス**&#x200B;などの他の列をレビューして、入力した移行セットの詳細を確認します。**...**／**詳細を表示**&#x200B;をクリックすると、抽出の各手順の期間を含む詳細が表示されます。抽出中にこのダイアログボックスを表示して、手順の進行状況を確認します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## 追加抽出 {#top-up-extraction-process}

コンテンツトランスファーツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初の完全抽出にプレコピー手順を使用した場合、後続の追加抽出に対しては、（追加移行セットのサイズが 200 GB 未満の場合）プレコピーをスキップできます。これは、プロセス全体にかかる時間が増える可能性があるからです。
>>また、最初の抽出を実行した時点から、追加抽出を実行する時点まで、既存コンテンツのコンテンツ構造が変わらないことが不可欠です。最初の抽出以降に構造が変更されたコンテンツに対しては、追加を実行できません。移行作業中には必ず制限するようにしてください。

>[!NOTE]
>コンテンツパスをステージングコンテナに移行すると、これらのパスやそのパス内のサブパスを後続の追加移行から削除または除外できません。
>>例：初回移行：content/dam/weRetail。
>>次の追加除外の試行：content/dam/weRetail/ab。
>>このシナリオでは、データが既にステージングコンテナに移行されているので、content/dam/weRetail/ab を除外できません。

抽出プロセスが完了したら、追加抽出方式を使用して差分コンテンツを転送できます。

次の手順に従います。

1. **コンテンツ転送** ウィザードに移動し、追加抽出の実行対象となる移行セットを選択します。「**抽出**」をクリックして、追加抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. **移行セットの抽出**&#x200B;ダイアログボックスが表示されます。「**抽出**」をクリックします。

   >[!IMPORTANT]
   >「**抽出時にステージングコンテナを上書き**」オプションを無効にしてください。
   >![画像](/help/journey-migration/content-transfer-tool/assets-ctt/overwriteStagingContainer.png)


## 次の手順 {#whats-next}

コンテンツトランスファーツールでソースからのコンテンツの抽出を学んだら、次はコンテンツトランスファーツールの取り込みプロセスを学びましょう。コンテンツトランスファーツールから移行セットを取り込む方法については、[Target へのコンテンツの取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照してください。
