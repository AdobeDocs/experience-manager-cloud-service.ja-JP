---
title: Target へのコンテンツの取り込み
description: Target へのコンテンツの取り込み
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 48%

---

# Target へのコンテンツの取り込み {#ingesting-content}

## コンテンツ転送ツールの取り込みプロセス {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="コンテンツの取得"
>abstract="取得とは、移行セットからターゲット Cloud Service インスタンスにコンテンツを取り込むことです。コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja" text="追加インジェスト"

コンテンツ転送ツールで移行セットを取り込むには、次の手順に従います。

>[!NOTE]
>この取り込みのサポートチケットを忘れずにログに記録しましたか？[コンテンツ転送ツールを使用する前の重要な考慮事項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=ja#important-considerations)を参照して、取り込みを成功させるためのその他の考慮事項を確認してください。

1. Cloud Acceleration Manager に移動します。プロジェクトカードをクリックし、「コンテンツ転送」カードをクリックします。 に移動します。 **取り込みジョブ** をクリックし、 **新しい取り込み**

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 取り込みチェックリストを確認し、すべての手順が完了していることを確認します。 これらの手順は、取り込みを正常におこなうために必要です。 次に進みます。 **次へ** 手順は、チェックリストが完了した場合にのみ実行します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 取り込みを作成するために必要な情報を指定します。

   * 抽出したデータをソースとして含む移行セットを選択します。
      * 移行セットは、無操作状態が長時間続くと有効期限が切れるので、抽出が実行された後は、比較的早く取り込みが行われることが期待されます。詳しくは、[移行セットの有効期限](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)を確認してください。
   * 移行先の環境を選択します。この環境では、移行セットのコンテンツが取り込まれます。 階層を選択します（オーサー／パブリッシュ）。迅速な開発環境はサポートされていません。

   >[!NOTE]
   >コンテンツの取り込みには、次の注意事項が適用されます。
   > ソースがオーサーの場合は、ターゲットのオーサー層に取り込むことをお勧めします。同様に、ソースがパブリッシュの場合は、ターゲットもパブリッシュにする必要があります。
   > ターゲット層が `Author`に設定されていない場合、オーサーインスタンスは取り込み中にシャットダウンされ、ユーザー（作成者やメンテナンスを実行しているすべてのユーザーなど）は使用できなくなります。 これは、システムを保護し、失われたり取り込みの競合が発生したりする可能性のある変更を防ぐためです。 チームがこの事実を認識していることを確認します。 また、オーサーの取り込み中に環境が休止状態であるように見えます。
   > オプションの事前コピー手順を実行して、取り込み段階を大幅に高速化できます。詳しくは、 [AzCopy での取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) を参照してください。
   > 事前コピーを使用した取得を（S3 または Azure データストアに対して）使用する場合は、最初にオーサーの取得を単独で実行することをお勧めします。これにより、後で実行された場合に、パブリッシュの取り込みが高速化されます。
   > 取り込みは、Rapid Development Environment(RDE) の宛先をサポートしておらず、ユーザーがアクセスできる場合でも、目的の宛先として表示されません。

   >[!IMPORTANT]
   > コンテンツの取り込みには、次の重要な注意事項が適用されます。
   > 宛先環境への取り込みは、ローカルの **AEM管理者** グループを作成します。 取り込みを開始できない場合は、 [取り込みを開始できません](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) を参照してください。
   > 設定が **ワイプ** は取り込み前に有効になり、既存のリポジトリ全体が削除され、コンテンツを取り込むためのリポジトリが作成されます。 このワークフローは、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定をリセットします。このリセットは、管理者ユーザーが **管理者** グループ化します。 取り込みを開始するには、管理者グループに読み上げる必要があります。

1. クリック **取り込み**.

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. その後、取り込みジョブリスト表示で取り込み段階を監視できます。 また、取り込みのアクションメニューを使用し、取り込みの進行に伴ってログを表示できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 次をクリック： **一** ボタンをクリックして、取り込みジョブの詳細を確認してください。 取り込みの各手順の実行中または完了中に、「 **...**&#x200B;をクリックし、 **期間を表示**. また、抽出した情報は、取り込まれている内容を実現するためにも示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

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
   
   Also, see [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## 追加取り込み {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="追加取り込み"
>abstract="前回のコンテンツ転送アクティビティ以降に変更されたコンテンツを移動するには、追加取り込み機能を使用します。取り込みが完了したら、ログを調べて、エラーや警告がないか確認します。エラーが発生した場合は、報告された問題を解決するかアドビカスタマーケアに連絡して、すぐに対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=ja" text="ログの表示"

コンテンツ転送ツールには、*差分コンテンツ追加*&#x200B;をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初のフル取り込みにコピー前の手順を使用した場合、後続の追加取り込みに対してコピー前の手順をスキップできます（追加の移行セットのサイズが 200 GB 未満の場合）。 これは、プロセス全体に時間がかかる可能性があるからです。

取り込みプロセスが完了したら、差分コンテンツを取り込むには、 [追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)をクリックし、追加インジェスト方法を使用します。

取り込みジョブを作成して、次の点を確認します。 **ワイプ** は、次に示すように、取得段階では無効になっています。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## トラブルシューティング {#troubleshooting}

### CAM が移行トークンを取得できない {#cam-unable-to-retrieve-the-migration-token}

移行トークンの自動取得は、ターゲットの Cloud Service 環境における [Cloud Manager を介した IP 許可リストの設定](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)など、様々な理由で失敗する場合があります。このようなシナリオでは、取り込みを開始しようとすると、次のダイアログボックスが表示されます。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

ダイアログボックスの「トークンを取得」リンクをクリックして、移行トークンを手動で取得します。 別のタブが開き、トークンが表示されます。 その後、トークンをコピーし、**移行トークン入力**&#x200B;フィールドにペーストします。 これで、取り込みを開始できるようになります。

>[!NOTE]
>
>トークンは、ローカルのに属するユーザーが使用できます **AEM管理者** グループを作成します。

### 取り込みを開始できない {#unable-to-start-ingestion}

宛先環境への取り込みは、ローカルの **AEM管理者** グループを作成します。 AEM administrators グループに属していない場合は、取り込みを開始しようとすると、次のようなエラーが表示されます。 管理者に問い合わせてローカルの **AEM 管理者**&#x200B;に追加するよう依頼するか、トークン自体を依頼してから&#x200B;**移行トークン入力**&#x200B;フィールドにペーストすることができます。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 移行サービスに接続できません {#unable-to-reach-migration-service}

取り込みが要求されると、次のようなメッセージがユーザーに表示される場合があります。「宛先環境の移行サービスに到達できません。 その場合は、後でやり直すか、Adobeサポートにお問い合わせください。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

このメッセージは、Cloud Acceleration Manager が、ターゲット環境の移行サービスに到達して取り込みを開始できなかったことを示します。 この状況は、様々な理由で発生する可能性があります。

>[!NOTE]
> 
> 「移行トークン」フィールドが表示されるのは、そのトークンの取得が実際には許可されていない場合があるためです。手動で指定できるようにすることで、ユーザーは追加のヘルプなしで、すばやく取り込みを開始できます。 トークンが指定され、メッセージが表示される場合は、トークンの取得に問題はありませんでした。

* AEM as a Cloud Serviceは環境の状態を維持し、通常の様々な理由で移行サービスを再起動する必要が生じる場合があります。 そのサービスが再起動中の場合は、そのサービスには到達できませんが、最終的に使用可能になります。
* 別のプロセスがインスタンス上で実行されている可能性があります。 例えば、Release Orchestrator が更新を適用している場合、システムがビジー状態で、移行サービスが定期的に使用できない可能性があります。 これと、ステージインスタンスまたは実稼動インスタンスが破損する可能性が、取り込み中に更新を一時停止することを強くお勧めする理由です。
* 次の場合、 [IP許可リストが適用されました](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) Cloud Manager を通じて、 Cloud Acceleration Manager が移行サービスに到達するのをブロックします。 アドレスが動的なので、取り込み用に IP アドレスを追加できません。 現在、唯一の解決策は、取り込みの実行中に IP 許可リストを無効にすることです。
* 調査を要する他の理由がある場合があります。 それでも取り込みに失敗する場合は、Adobeカスタマーケアにお問い合わせください。

### リリースオーケストレーターによる自動更新は引き続き有効です

リリースオーケストレーターは、更新を自動的に適用することで、環境を自動的に最新の状態に保ちます。取り込みの実行時に更新がトリガーされると、環境の破損を含む予期しない結果が生じる可能性があります。 取り込みを開始する前にカスタマーサポートチケットをログに記録する適切な理由（上記の「注意」を参照）。これにより、Release Orchestrator を一時的に無効にするようにスケジュールできます。

取り込みの開始時に Release Orchestrator が実行中である場合は、ユーザーインターフェイスにこのメッセージが表示されます。 フィールドをチェックしてもう一度ボタンを押すことにより、リスクを受け入れて続行することを選択できます。

>[!NOTE]
>
> Release Orchestrator は現在開発環境にデプロイされているので、これらの環境での一時停止更新もおこなう必要があります。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### 追加取り込みエラー

[追加取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)エラーの一般的な原因は、ノード ID の競合です。このエラーを識別するには、Cloud Acceleration Manager UI を使用して取り込みログをダウンロードし、次のようなエントリを探します。

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Uniqueness constraint violated property [jcr:uuid] having value a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

AEM の各ノードには、一意の UUID が必要です。このエラーは、取り込まれるノードが、ターゲットインスタンス上の別のパスに存在する uuid と同じ uuid を持つことを示します。
この状況は、抽出とそれ以降の抽出の間にソース上でノードが移動した場合に発生する可能性があります [追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
また、ターゲット上のノードが取り込みと後続の追加取り込みの間に移動した場合にも発生する可能性があります。

この競合は手動で解決する必要があります。コンテンツを参照する他のコンテンツに留意し、2 つのノードのうち、削除する必要があるノードをコンテンツに精通したユーザーが決定する必要があります。解決策として、問題のあるノードがなくても、追加抽出を再度行う必要が生じる場合があります。

## 次の手順 {#whats-next}

Target へのコンテンツの取り込みが完了したら、各ステップ（抽出と取り込み）のログを表示し、エラーを探すことができます。詳しくは、[移行セットのログの表示](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=ja)を参照してください。
