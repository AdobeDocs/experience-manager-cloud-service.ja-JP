---
title: Target へのコンテンツの取り込み
description: Target へのコンテンツの取り込み
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 319a9bc2aa6d82d0fb322cd1f2ca37e95c33e97d
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 85%

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
>オプションの事前コピー手順を実行して、取り込み段階を大幅に高速化できます。事前コピーステップは、1回目の完全抽出と取り込みに最も効果的です。詳しくは、[AzCopy を使用した取得](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy)を参照してください。

1. Cloud Acceleration Manager に移動します。プロジェクトカードをクリックし、コンテンツ転送カードをクリックします。**取り込みジョブ**&#x200B;に移動し、「**新しい取り込み**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)


1. 取り込みチェックリストを確認し、すべての手順が完了していることを確認します。 これらは、取り込みを正常におこなうために必要な手順です。 次の手順に進むことができます： **次へ** 手順は、チェックリストが完了した場合にのみ実行します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 新しい取り込みを作成するために必要な情報を入力します。

   * 抽出した移行セットをソースとして選択します。
   * 移行先の環境を選択します。移行セットのコンテンツは、ここに取り込まれます。階層を選択します（オーサー／パブリッシュ）。

   >[!NOTE]
   >
   >ソースがオーサーの場合は、ターゲットのオーサー層に取り込むことをお勧めします。同様に、ソースがパブリッシュの場合は、ターゲットもパブリッシュにする必要があります。

   >[!NOTE]
   >
   >ターゲット層が `Author`に設定すると、オーサーインスタンスは取り込み中にシャットダウンされ、ユーザー（作成者やメンテナンスを実行しているすべてのユーザーなど）は使用できなくなります。 これは、システムを保護し、失われたり取り込みの競合を引き起こしたりする可能性のある変更を防ぐためです。 チームがこの事実を認識していることを確認してください。 また、オーサーの取り込み中に環境が休止状態で表示されることに注意してください。

   >[!NOTE]
   >
   >オプションの事前コピー手順を実行して、取り込み段階を大幅に高速化できます。詳しくは、[AzCopy を使用した取得](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy)を参照してください。
   > 
   >事前コピーを使用した取得を（S3 または Azure データストアに対して）使用する場合は、最初にオーサーの取得を単独で実行することをお勧めします。これにより、後で実行する際に、パブリッシュの取り込みが高速化されます。

   >[!IMPORTANT]
   >
   >宛先環境への取り込みを開始するには、宛先 Cloud Service オーサーサービスで、自身もローカルの **AEM 管理者**&#x200B;グループに属している必要があります。取り込みを開始できない場合、詳しくは、[取り込みを開始できない](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion)を参照してください。

   >[!IMPORTANT]
   >
   >取り込み前の&#x200B;**ワイプ**&#x200B;設定が有効になっている場合は、既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。これは、**administrators** グループに追加された管理者ユーザーにも当てはまります。取り込みを開始するには、管理者グループに再度追加される必要があります。

1. 「**取り込み**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. その後、取り込みジョブリストビューで取り込み段階を監視できます。 また、インジェストのアクションメニューを使用して、インジェストの進行に応じてログを表示できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 取り込みが完了したら、画面の右上隅にある「i」ボタンをクリックして、取り込みジョブに関する詳細情報を取得できます。

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

## 追加取り込み {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup" title="Top Up Ingestion"
>abstract="追加取り込み機能を使用すると、前回のコンテンツ転送アクティビティ以降に変更されたコンテンツが移行されます。取り込みが完了したら、ログを調べて、エラーや警告がないか確認します。エラーが発生した場合は、報告された問題を解決するかアドビカスタマーケアに連絡して、すぐに対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=ja" text="ログの表示"

コンテンツ転送ツールには、*差分コンテンツ追加*&#x200B;をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初の完全取り込みに事前コピーステップを使用した場合は、後続の追加取り込みに対しては、プロセス全体にかかる時間が増える可能性があるので、（追加移行セットのサイズが 200 GB 未満の場合）事前コピーをスキップできます。

取り込みプロセスの完了後、差分コンテンツを取り込むには、[追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)を実行してから、追加取り込みを使用します。

それには、新しい取り込みジョブを作成し、取り込み段階では&#x200B;**ワイプ**&#x200B;設定を必ず無効にします（下図を参照）。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## トラブルシューティング {#troubleshooting}

### CAM が移行トークンを取得できない {#cam-unable-to-retrieve-the-migration-token}

移行トークンの自動取得は、ターゲットの Cloud Service 環境における [Cloud Manager を介した IP 許可リストの設定](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)など、さまざまな理由で失敗する場合があります。このようなシナリオでは、取り込みを開始しようとすると、次のダイアログが表示されます。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

ダイアログの「トークンを取得」リンクをクリックして、移行トークンを手動で取得する必要があります。 これにより、トークンを表示する別のタブが開きます。 その後、トークンをコピーし、**移行トークン入力**&#x200B;フィールドにペーストします。 これで、取り込みを開始できるようになります。

>[!NOTE]
>
>トークンは、宛先 Cloud Service オーサーサービスのローカル **AEM 管理者**&#x200B;グループに属するユーザーが使用することができます。

### 取り込みを開始できない {#unable-to-start-ingestion}

宛先 Cloud Service オーサーサービスのローカル **AEM 管理者** グループに属している場合にのみ、宛先環境への取り込みを開始することができます。AEM 管理者グループに属していない場合は、取り込みを開始しようとすると、次に示すようなエラーが表示されます。管理者に問い合わせてローカルの **AEM 管理者**&#x200B;に追加するよう依頼するか、トークン自体を依頼してから&#x200B;**移行トークン入力**&#x200B;フィールドにペーストすることができます。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

## 次の手順 {#whats-next}

コンテンツの Target への取り込みが完了したら、各手順のログ（抽出および取り込み）を表示し、エラーを探すことができます。 詳しくは、[移行セットのログの表示](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=ja)を参照してください。
