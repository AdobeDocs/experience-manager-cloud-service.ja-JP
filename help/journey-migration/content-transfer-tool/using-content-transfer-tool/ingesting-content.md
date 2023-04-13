---
title: Target へのコンテンツの取り込み
description: Target へのコンテンツの取り込み
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: cab182a7998be6a569cf16e4000184f7235082da
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 88%

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
>この取り込みのサポートチケットを忘れずにログに記録しましたか？[コンテンツ転送ツールを使用する前の重要な考慮事項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=ja#important-considerations)を参照して、取り込みを成功させるためのその他の考慮事項を確認してください。

1. Cloud Acceleration Manager に移動します。プロジェクトカードをクリックし、コンテンツ転送カードをクリックします。**取り込みジョブ**&#x200B;に移動し、「**新しい取り込み**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 取り込みチェックリストをレビューし、すべての手順が完了していることを確認します。 これらは、取り込みを正常に行うために必要な手順です。 チェックリストが完了した場合にのみ、**次**&#x200B;の手順に進むことができます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 新しい取り込みを作成するために必要な情報を入力します。

   * 抽出したデータをソースとして含む移行セットを選択します。
      * 移行セットは、無操作状態が長時間続くと有効期限が切れるので、抽出が実行された後は取り込みが比較的早くおこなわれます。 レビュー [移行セットの有効期限](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 」を参照してください。
   * 移行先の環境を選択します。移行セットのコンテンツは、ここに取り込まれます。階層を選択します（オーサー／パブリッシュ）。迅速な開発環境はサポートされていません。

   >[!NOTE]
   >コンテンツの取り込みには、次の注意事項が適用されます。
   > ソースがオーサーの場合は、ターゲットのオーサー層に取り込むことをお勧めします。同様に、ソースがパブリッシュの場合は、ターゲットもパブリッシュにする必要があります。
   > ターゲット層が `Author` の場合、オーサーインスタンスは取り込み期間中にシャットダウンされ、ユーザー（作成者やメンテナンスを実行中のユーザーなど）が使用できなくなります。 これは、システムを保護し、変更を防ぐことを目的としています。変更は、失われたり取り込みの競合を引き起こしたりする可能性があるためです。チームがこの事実を認識していることを確認してください。 また、オーサーの取り込み中は環境が休止状態と表示されることに注意してください。
   > オプションの事前コピー手順を実行して、取り込み段階を大幅に高速化できます。詳しくは、[AzCopy を使用した取得](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy)を参照してください。
   > 事前コピーを使用した取得を（S3 または Azure データストアに対して）使用する場合は、最初にオーサーの取得を単独で実行することをお勧めします。これにより、後で実行する際に、パブリッシュの取り込みが高速化されます。
   > 取り込みは、Rapid Development Environment(RDE) の宛先をサポートしていません。 ユーザーがアクセス権を持っている場合でも、これらは選択可能な宛先として表示されません。

   >[!IMPORTANT]
   > コンテンツの取り込みには、次の重要な注意事項が適用されます。
   > ローカルの **AEM管理者** グループを作成します。 取り込みを開始できない場合、詳しくは、[取り込みを開始できない](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion)を参照してください。
   > 取り込み前の&#x200B;**ワイプ**&#x200B;設定が有効になっている場合は、既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。これは、**administrators** グループに追加された管理者ユーザーにも当てはまります。取り込みを開始するには、管理者グループに再度追加される必要があります。

1. 「**取り込み**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. その後、取り込みジョブリスト表示で取り込み段階を監視できます。 また、取り込みのアクションメニューを使用し、取り込みの進行に伴ってログを表示できます。

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
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## 追加取り込み {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="追加取り込み"
>abstract="追加取り込み機能を使用すると、前回のコンテンツ転送アクティビティ以降に変更されたコンテンツが移行されます。取り込みが完了したら、ログを調べて、エラーや警告がないか確認します。エラーが発生した場合は、報告された問題を解決するかアドビカスタマーケアに連絡して、すぐに対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html" text="ログの表示"

コンテンツ転送ツールには、*差分コンテンツ追加*&#x200B;をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初の完全取り込みに事前コピーステップを使用した場合は、後続の追加取り込みに対しては、プロセス全体にかかる時間が増える可能性があるので、（追加移行セットのサイズが 200 GB 未満の場合）事前コピーをスキップできます。

取り込みプロセスの完了後、差分コンテンツを取り込むには、[追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)を実行してから、追加取り込みを使用します。

それには、新しい取り込みジョブを作成し、取り込み段階では&#x200B;**ワイプ**&#x200B;設定を必ず無効にします（下図を参照）。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## トラブルシューティング {#troubleshooting}

### CAM が移行トークンを取得できない {#cam-unable-to-retrieve-the-migration-token}

移行トークンの自動取得は、ターゲットの Cloud Service 環境における [Cloud Manager を介した IP 許可リストの設定](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)など、様々な理由で失敗する場合があります。このようなシナリオでは、取り込みを開始しようとすると、次のダイアログが表示されます。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

ダイアログの「トークンを取得」リンクをクリックして、移行トークンを手動で取得する必要があります。 これにより、トークンを表示する別のタブが開きます。 その後、トークンをコピーし、**移行トークン入力**&#x200B;フィールドにペーストします。 これで、取り込みを開始できるようになります。

>[!NOTE]
>
>トークンは、宛先 Cloud Service オーサーサービスのローカル **AEM 管理者**&#x200B;グループに属するユーザーが使用することができます。

### 取り込みを開始できない {#unable-to-start-ingestion}

ローカルの **AEM管理者** グループを作成します。 AEM 管理者グループに属していない場合は、取り込みを開始しようとすると、次に示すようなエラーが表示されます。管理者に問い合わせてローカルの **AEM 管理者**&#x200B;に追加するよう依頼するか、トークン自体を依頼してから&#x200B;**移行トークン入力**&#x200B;フィールドにペーストすることができます。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 移行サービスに接続できません {#unable-to-reach-migration-service}

取り込みが要求されると、次のようなメッセージがユーザーに表示される場合があります。「現在、宛先環境の移行サービスにアクセスできません。再試行するか、アドビサポートにお問い合わせください。」

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

つまり、Cloud Acceleration Manager が、ターゲット環境の移行サービスにアクセスして取り込みを開始できなかったことを示しています。 これは、様々な理由で発生する可能性があります。

>[!NOTE]
> 
> 「移行トークン」フィールドが表示されるのは、そのトークンの取得が実際には許可されていない場合があるためです。手動で指定できるようにすることで、ユーザーは追加のヘルプなしで、すばやく取り込みを開始できます。 トークンが指定され、メッセージがそれでも表示される場合は、問題はトークンの取得ではありませんでした。

* AEM as a Cloud Service は環境の状態を維持し、通常の理由で移行サービスの再起動が必要になる場合があります。そのサービスが再起動中の場合はサービスにアクセスできませんが、すぐに利用できるようになります。
* インスタンス上で別のプロセスが実行されている可能性があります。 例えば、リリースオーケストレーターが更新を適用している場合、システムがビジー状態になり、移行サービスが定期的に利用できなくなる可能性があります。これと、ステージインスタンスまたは実稼動インスタンスが破損する可能性があるため、取り込み中に更新を一時停止することを強くお勧めします。
* Cloud Manager を使用して [IP 許可リストが適用されている](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)場合、Cloud Acceleration Manager が移行サービスに到達するのをブロックします。 アドレスが非常に動的なので、取り込み用に IP アドレスを追加することはできません。現在、唯一の解決策は、取り込みの実行中に IP 許可リストを無効にすることです。
* 調査を要する他の理由がある場合があります。 それでも取り込みに失敗する場合は、アドビカスタマーケアにお問い合わせください。

### リリースオーケストレーターによる自動更新は引き続き有効です

リリースオーケストレーターは、更新を自動的に適用することで、環境を自動的に最新の状態に保ちます。取り込みの実行中に更新がトリガーされると、環境の破損など、予期しない結果が生じる可能性があります。これは、取り込みを開始する前にサポートチケットをログに記録する必要がある理由の 1 つです（上記の「メモ」を参照）。これにより、リリースオーケストレーターの一時的な無効化をスケジュールできます。

取り込みの開始時にリリースオーケストレーターがまだ実行されている場合、UI にこのメッセージが表示されます。フィールドをチェックしてもう一度ボタンを押すことにより、リスクを受け入れて続行することを選択できます。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### 追加取り込みエラー

[追加取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)エラーの一般的な原因は、ノード ID の競合です。このエラーを識別するには、Cloud Acceleration Manager UI を使用して取り込みログをダウンロードし、次のようなエントリを探します。

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Uniqueness constraint violated property [jcr:uuid] having value a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

AEM の各ノードには、一意の UUID が必要です。このエラーは、取り込まれているノードが、ターゲットインスタンスの別のパスに既に存在するノードと同じ uuid を持っていることを示します。
これは、抽出と後続の[追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)の間でノードがソース上で移動された場合に発生する可能性があります。
また、ターゲット上のノードが取り込みと後続の追加取り込みの間に移動した場合にも発生する可能性があります。

この競合は手動で解決する必要があります。コンテンツを参照する他のコンテンツに留意し、2 つのノードのうち、削除する必要があるノードをコンテンツに精通したユーザーが決定する必要があります。解決策として、問題のあるノードがなくても、追加抽出を再度行う必要が生じる場合があります。

## 次の手順 {#whats-next}

Target へのコンテンツの取り込みが完了したら、各ステップ（抽出と取り込み）のログを表示し、エラーを探すことができます。詳しくは、[移行セットのログの表示](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html)を参照してください。
