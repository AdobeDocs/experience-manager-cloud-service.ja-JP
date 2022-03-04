---
title: Target へのコンテンツの取り込み
description: Target へのコンテンツの取り込み
source-git-commit: 80e148aa5533963bcd6354e2117a4619bcf5b27f
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 97%

---


# Target へのコンテンツの取り込み {#ingesting-content}

## コンテンツ転送ツールの取り込みプロセス {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="コンテンツの取得"
>abstract="取得とは、移行セットからターゲット Cloud Service インスタンスにコンテンツを取り込むことです。コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#top-up-ingestion-process" text="追加インジェスト"

コンテンツ転送ツールで移行セットを取り込むには、次の手順に従います。
>[!NOTE]
>オプションのプリコピー手順を実行して、取り込み段階を大幅に高速化できます。 詳しくは、[AzCopy を使用した取得](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja#ingesting-azcopy)を参照してください。

1. **コンテンツ転送**&#x200B;ページで移行セットを選択し、「**取得**」をクリックして取り込みを開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. **移行セットのインジェスト**&#x200B;ダイアログボックスが表示されます。コンテンツは、オーサーインスタンスかパブリッシュインスタンスのどちらかに一度に取り込むことができます。コンテンツの取り込み先のインスタンスを選択します。「**取得**」をクリックして、取得段階を完了します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >事前コピーを使用した取得を（S3 または Azure データストアに対して）使用する場合は、最初にオーサーの取得を単独で実行することをお勧めします。これにより、後でパブリッシュの取得を実行するときに、処理が迅速化されます。

   >[!IMPORTANT]
   >「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションが有効な場合は、既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。これは、**administrators** グループに追加された管理者ユーザーにも当てはまります。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   さらに、「**カスタマーケア**」をクリックしてチケットを発行します（下図を参照）。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   詳しくは、[コンテンツ転送ツール使用時の重要な考慮事項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=ja#important-considerations)も参照してください。

1. 取り込みが完了すると、「**オーサーインジェスト**」フィールドのステータスが&#x200B;**完了**&#x200B;に更新されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## 追加インジェスト {#top-up-ingestion-process}

コンテンツ転送ツールには、*差分コンテンツ追加*&#x200B;をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

インジェストプロセスが完了したら、追加インジェスト方式を使用して差分コンテンツを転送できます。それには、次の手順に従います。

1. **コンテンツ転送**&#x200B;ウィザードに移動し、追加取り込みの実行対象となる移行セットを選択します。「**取り込み**」をクリックして、追加インジェストを開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. **移行セットのインジェスト**&#x200B;ダイアログボックスが表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >以前の取得アクティビティから既存のコンテンツを削除しないようにするには、「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションを無効にする必要があります。さらに、「**カスタマーケア**」をクリックしてチケットを発行します（上図を参照）。

## 次のステップ {#whats-next}

コンテンツ転送ツールで Target にコンテンツを取り込む方法を理解したら、各ステップ（抽出と取り込み）の完了時にログを表示し、エラーを探すことができます。詳しくは、[移行セットのログの表示](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=ja)を参照してください。
