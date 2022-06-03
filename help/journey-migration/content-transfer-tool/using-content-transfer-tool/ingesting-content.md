---
title: Target へのコンテンツの取り込み
description: Target へのコンテンツの取り込み
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 05765bdaa681502b60fc5a7c943e2265c09764ec
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 40%

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
>オプションのプリコピー手順を実行して、取り込み段階を大幅に高速化できます。 事前コピー手順は、最初の完全な抽出および取り込みに最も効果的です。 詳しくは、[AzCopy を使用した取得](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy)を参照してください。

1. Cloud Acceleration Manager に移動します。 プロジェクトカードをクリックし、「コンテンツ転送」カードをクリックします。 に移動します。 **取り込みジョブ** をクリックし、 **新しい取り込み**

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 新しい取り込みを作成するために必要な情報を入力します。

   * ソースとして抽出した移行セットを選択します。
   * 宛先環境を選択します。 移行セットのコンテンツは、ここに取り込まれます。 層を選択します。 （オーサー/パブリッシュ）。

   >[!NOTE]
   >
   >ソースがオーサーの場合は、ターゲットのオーサー層に取り込むことをお勧めします。 同様に、ソースが「公開」の場合は、ターゲットも「公開」にする必要があります。

   >[!NOTE]
   >
   >オプションのプリコピー手順を実行して、取り込み段階を大幅に高速化できます。 詳しくは、[AzCopy を使用した取得](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy)を参照してください。
   > 
   >事前コピーを使用した取得を（S3 または Azure データストアに対して）使用する場合は、最初にオーサーの取得を単独で実行することをお勧めします。これにより、後で実行する際に、パブリッシュの取り込みが高速化されます。

   >[!IMPORTANT]
   >
   >ローカルの **AEM管理者** グループを作成し、Cloud Serviceを転送します。 AEM administrators グループに属していない場合は、取り込みを開始しようとすると、次に示すエラーが表示されます。
   >![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam21.png)

   >[!IMPORTANT]
   >
   >設定が **ワイプ** は取り込み前に有効になり、既存のリポジトリ全体を削除し、コンテンツを取り込むための新しいリポジトリを作成します。 つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。これは、**administrators** グループに追加された管理者ユーザーにも当てはまります。取り込みを開始するには、administrators グループに再度追加される必要があります。

1. クリック **取り込み**

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. その後、取り込みジョブリストビューで、取り込み段階を監視できます

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 取り込みが完了したら、画面の右上隅にある (i) ボタンをクリックして、取り込みジョブに関する詳細情報を取得します。

<!-- Alexandru: hiding temporarily, until it's reviewed 

1. The **Migration Set ingestion** dialog box displays. Content can be ingested to either Author instance or Publish instance at a time. Select the instance to ingest content to. Click on **Ingest** to start the ingestion phase. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >If ingesting with pre-copy is used (for S3 or Azure Data Store), it is recommended to run Author ingestion first alone. This will speed up the Publish ingestion when it is run later. 

   >[!IMPORTANT]
   >When the **Wipe existing content on Cloud instance before ingestion** option is enabled, it deletes the entire existing repository and creates a new repository to ingest content into. This means that it resets all settings including permissions on the target Cloud Service instance. This is also true for an admin user added to the **administrators** group.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Additionally, click on **Customer Care** to log a ticket, as shown in the figure below. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## 追加インジェスト {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup" title="Top Up Ingestion"
>abstract="トップアップ機能を使用して、前回のコンテンツ転送アクティビティ以降に変更されたコンテンツを移動します。 取り込みが完了したら、ログでエラーや警告を確認します。 エラーが発生した場合は、報告された問題に対処するか、Adobeカスタマーケアにお問い合わせください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="ログの表示"

コンテンツ転送ツールには、*差分コンテンツ追加*&#x200B;をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初のフル取り込みにコピー前の手順を使用した場合、プロセス全体に時間がかかる可能性があるので、後続の追加取り込みに対しては（追加の移行セットのサイズが 200GB 未満の場合）プリコピーをスキップできます。

取り込みプロセスが完了したら、差分コンテンツを取り込むには、 [追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) 次に、追加インジェスト方法を使用します。

これをおこなうには、新しい取り込みジョブを作成し、 **ワイプ** は、次に示すように、取得段階では無効になっています。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)



## 次の手順 {#whats-next}

コンテンツ転送ツールで Target にコンテンツを取り込む方法を理解したら、各ステップ（抽出と取り込み）の完了時にログを表示し、エラーを探すことができます。詳しくは、[移行セットのログの表示](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=ja)を参照してください。
