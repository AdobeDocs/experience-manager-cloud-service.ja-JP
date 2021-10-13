---
title: コンテンツ転送ツールでの Target へのコンテンツの取り込み
description: コンテンツ転送ツールでの Target へのコンテンツの取り込み
source-git-commit: 65847fc03770fe973c3bfee4a515748f7e487ab6
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 66%

---


# コンテンツ転送ツールでの Target へのコンテンツの取り込み {#ingesting-content}

## コンテンツ転送ツールのインジェストプロセス {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="コンテンツの取得"
>abstract="取得とは、移行セットからターゲット Cloud Service インスタンスにコンテンツを取り込むことです。コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="追加インジェスト"

コンテンツ転送ツールで移行セットを取り込むには、次の手順に従います。
>[!NOTE]
>Amazon S3 または Azure Data Store をデータストアのタイプとして使用する場合は、オプションのプリコピー手順を実行して、取り込み段階を大幅に高速化できます。 詳細は [AzCopy での取り込み ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) を参照してください。

1. *概要* ページで移行セットを選択し、**取り込み** をクリックして取り込みを開始します。 **移行セットのインジェスト**&#x200B;ダイアログボックスが表示されます。コンテンツは、一度にオーサーインスタンスまたはパブリッシュインスタンスに取り込むことができます。 コンテンツの取り込み先のインスタンスを選択します。 「**取得**」をクリックして、取得段階を完了します。

   >[!IMPORTANT]
   >事前コピーを使用した取り込みを（S3 または Azure データストアに対して）使用する場合は、最初にオーサーの取り込みを単独で実行することをお勧めします。 これにより、後で実行した場合に、パブリッシュの取り込みが高速化されます。

   >[!IMPORTANT]
   >「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションが有効な場合は、既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。これは、**administrators** グループに追加された管理者ユーザーにも当てはまります。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-03.png)

   さらに、「**カスタマーケア**」をクリックしてチケットを発行します（上図を参照）。詳しくは、[コンテンツ転送ツール使用時の重要な考慮事項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations)も参照してください。

1. 取り込みが完了すると、ステータスが **FINISHED** に更新されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

## 追加インジェスト {#top-up-ingestion-process}

コンテンツ転送ツールには、*差分コンテンツ追加*&#x200B;をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁におこなって、Cloud Service での運用を開始する前におこなう最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

インジェストプロセスが完了したら、追加インジェスト方式を使用して差分コンテンツを転送できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、追加取得の実行対象となる移行セットを選択します。「**取得**」をクリックして、追加取得を開始します。**移行セットのインジェスト**&#x200B;ダイアログボックスが表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >以前の取得アクティビティから既存のコンテンツを削除しないようにするには、「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションを無効にする必要があります。さらに、「**カスタマーケア**」をクリックしてチケットを発行します（上図を参照）。
