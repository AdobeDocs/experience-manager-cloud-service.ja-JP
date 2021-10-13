---
title: コンテンツ転送ツールでのソースからのコンテンツの抽出
description: コンテンツ転送ツールでのソースからのコンテンツの抽出
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 69%

---


# コンテンツ転送ツールでのソースからのコンテンツの抽出 {#extracting-content}

## コンテンツ転送ツールでの抽出プロセス {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="コンテンツの抽出"
>abstract="抽出とは、ソース AEM インスタンスから、移行セットと呼ばれる一時領域にコンテンツを抽出することです。移行セットは、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#top-up-extraction-process" text="追加抽出"

コンテンツ転送ツールで移行セットを抽出するには、次の手順に従います。
>[!NOTE]
>Amazon S3 または Azure Data Store をデータストアのタイプとして使用する場合は、オプションのプリコピー手順を実行して、抽出段階を大幅に高速化できます。 そのためには、抽出を実行する前に `azcopy.config` ファイルを設定する必要があります。 詳しくは、[ 大きなコンテンツリポジトリの処理 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) を参照してください。

1. *概要*&#x200B;ページで移行セットを選択し、「**抽出**」をクリックして抽出を開始します。**移行セットの抽出**&#x200B;ダイアログボックスが表示されるので、「**抽出**」をクリックして抽出段階を完了します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >抽出段階では、ステージングコンテナを上書きするオプションがあります。


1. 「**抽出**」フィールドに「**実行中**」ステータスが表示され、抽出が進行中であることを示します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   抽出が完了すると、移行セットのステータスが&#x200B;**完了**&#x200B;に更新され、*緑で塗りつぶされた*&#x200B;雲のアイコンが「**情報**」フィールドに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >UI には自動リロード機能があり、30 秒ごとに概要ページをリロードします。
   >抽出フェーズが開始されると、書き込みロックが作成され、*60 秒*&#x200B;後に解放されます。したがって、抽出が停止した場合は、ロックが解除されるまで 1 分待ってから、抽出を再開する必要があります。

## 追加抽出 {#top-up-extraction-process}

コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。
>また、追加抽出を実行する際に、最初の抽出を実行した時点からに、既存のコンテンツのコンテンツ構造を変更しないことが重要です。 最初の抽出以降に構造が変更されたコンテンツに対しては、追加は実行できません。 移行プロセス中は、必ずこの制限をおこなってください。

抽出プロセスが完了したら、追加抽出方式を使用して差分コンテンツを転送できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、追加抽出の実行対象となる移行セットを選択します。「**抽出**」をクリックして、追加抽出を開始します。**移行セットの抽出**&#x200B;ダイアログボックスが表示されます。

   >[!IMPORTANT]
   >
   >「**抽出時にステージングコンテナを上書き**」オプションを無効にしてください。
   >
   >![画像](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)
