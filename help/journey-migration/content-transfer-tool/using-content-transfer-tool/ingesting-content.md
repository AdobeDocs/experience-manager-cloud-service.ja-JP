---
title: コンテンツの取り込みCloud Service
description: Cloud Acceleration Manager を使用して、移行セットから宛先Cloud Serviceインスタンスにコンテンツを取り込む方法を説明します。
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: b674b3d8cd89675ed30c1611edec2281f0f1cb05
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 40%

---

# コンテンツの取り込みCloud Service {#ingesting-content}

## Cloud Acceleration Manager での取得プロセス {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="コンテンツの取得"
>abstract="取得とは、移行セットから宛先の Cloud Service インスタンスにコンテンツを取得することを指します。コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=ja#top-up-extraction-process" text="追加抽出"

Cloud Acceleration Manager を使用して移行セットを取り込むには、次の手順に従います。

1. Cloud Acceleration Manager に移動します。プロジェクトカードをクリックし、コンテンツ転送カードをクリックします。**取り込みジョブ**&#x200B;に移動し、「**新しい取り込み**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 取り込みチェックリストをレビューし、すべての手順が完了していることを確認します。 これらの手順は、取り込みを正常に行うために必要です。チェックリストが完了した場合のみ、**次**&#x200B;の手順に進みます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 取り込みを作成するために必要な情報を入力します。

   * **移行セット：** 抽出したデータをソースとして含む移行セットを選択します。
      * 移行セットは、無操作状態が長時間続くと有効期限が切れるので、抽出が実行された後は、比較的早く取り込みが行われることが期待されます。詳しくは、[移行セットの有効期限](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)を確認してください。

   >[!TIP]
   > 抽出が実行中の場合は、ダイアログに抽出が示されます。 抽出が正常に完了すると、取り込みが自動的に開始されます。 抽出が失敗または停止した場合、取り込みジョブは取り消されます。

   * **宛先：** 宛先環境を選択します。 この環境では、移行セットのコンテンツが取り込まれます。
      * 取り込みは、Rapid Development Environment(RDE) の宛先をサポートしていないので、ユーザーがアクセスできる場合でも、目的の宛先として表示されません。
      * 移行セットは複数の宛先に同時に取り込むことができますが、宛先は、一度に 1 つの取り込みを実行または待機しているターゲットにすることができます。

   * **層：** 層を選択します。 （オーサー／パブリッシュ）。
      * ソースが `Author`を使用する場合は、 `Author` ターゲット上の層。 同様に、ソースが `Publish`の場合、ターゲットは `Publish` 同様に。

   >[!NOTE]
   > ターゲット層が `Author` の場合、オーサーインスタンスは取り込み期間中にシャットダウンされ、ユーザー（作成者やメンテナンスを実行中のユーザーなど）が使用できなくなります。これは、システムを保護し、取り込みの競合を引き起こす可能性のある変更を防ぐためです。 チームがこの事実を認識していることを確認してください。また、オーサーの取り込み中は環境が休止状態と表示されることに注意してください。

   * **ワイプ：** を選択します。 `Wipe` 値
      * The **ワイプ** 「 」オプションは、インジェストの開始点を設定します。 次の場合 **ワイプ** を有効にすると、そのすべてのコンテンツを含む宛先が、Cloud Manager で指定されたAEMのバージョンにリセットされます。 有効にしない場合、宛先は現在のコンテンツを出発点として維持します。
      * このオプションは、 **NOT** は、コンテンツの取り込みの実行方法に影響します。 取り込みでは常にコンテンツ置換戦略を使用し、 _not_ コンテンツ結合戦略で、両方で **ワイプ** および **ワイプしない** 場合、移行セットを取り込むと、宛先上の同じパスにあるコンテンツが上書きされます。 例えば、移行セットに `/content/page1` と宛先には既に次が含まれています： `/content/page1/product1`を含めない場合、取り込みによって `page1` パスとそのサブページ ( `product1`をクリックし、移行セット内のコンテンツに置き換えます。 つまり、 **ワイプしない** 管理する必要のあるコンテンツを含む宛先への取り込み。

   >[!IMPORTANT]
   > 設定が **ワイプ** を有効にすると、ターゲットリポジトリインスタンスに対するユーザー権限を含む、既存のCloud Service全体がリセットされます。 このリセットは、管理者ユーザーが **管理者** 取り込みを開始するには、グループに追加し、そのユーザーを administrators グループに再度追加する必要があります。

   * **プリコピー：** を選択します。 `Pre-copy` 値
      * オプションのプリコピー手順を実行して、取り込みを大幅に高速化できます。 詳しくは、[AzCopy で取り込む](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy)を参照してください。
      * 事前コピーを使用した取り込みを使用する場合（S3 または Azure データストアの場合）、を実行することをお勧めします `Author` 最初に単独で取り込みます。 これにより、 `Publish` 取り込み。後で実行する場合に実行します。

   >[!IMPORTANT]
   > 宛先環境への取り込みを開始するには、宛先 Cloud Service オーサーサービスで、自身もローカルの **AEM 管理者**&#x200B;グループに属している必要があります。取り込みを開始できない場合、詳しくは、[取り込みを開始できない](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion)を参照してください。

1. 「**取り込み**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. その後、取り込みジョブリストビューから取り込みを監視し、取り込みのアクションメニューを使用して、取り込みの進行に応じて期間とログを表示できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 取り込みジョブについて詳しくは、行の「**(i)**」ボタンをクリックします。 「**…**」、「**期間を表示**」の順にクリックすると、取り込みの各手順の実行中または完了時の期間を確認できます。また、抽出した情報は、取り込まれている内容を理解するためにも表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## 追加取り込み {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="追加取り込み"
>abstract="追加機能を使用して、前回のコンテンツ転送アクティビティ以降に変更されたコンテンツを移動します。 取り込みが完了したら、ログでエラーや警告がないかを確認します。 エラーが発生した場合は、報告された問題を解決するかアドビカスタマーケアに連絡して、すぐに対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=ja" text="ログの表示"

コンテンツ転送ツールには、 *トップアップ* 移行セットの これにより、移行セットを変更して、前の抽出以降に変更されたコンテンツのみを含めることができ、再度すべてのコンテンツを抽出する必要がなくなります。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初の取り込みにコピー前の手順を使用した場合、後続の追加取り込みに対してコピー前の手順をスキップできます（追加の移行セットのサイズが 200 GB 未満の場合）。 これは、プロセス全体に時間がかかる可能性があるからです。

一部の取り込みが完了した後に差分コンテンツを取り込むには、 [追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)次に、 **ワイプ** オプション **無効**. 必ず **ワイプ** 上記の説明を参照して、宛先に既に存在するコンテンツが失われないようにします。

取り込みジョブを作成して、次の点を確認します。 **ワイプ** は、次に示すように、取り込み中は無効になります。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## トラブルシューティング {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="コンテンツ取り込みのトラブルシューティング"
>abstract="取り込みログとドキュメントを参照して、取り込みが失敗する一般的な理由と問題を修正する方法を見つけてください。 修正後は、取り込みを再度実行できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=ja" text="コンテンツ転送の検証"

### CAM が移行トークンを取得できない {#cam-unable-to-retrieve-the-migration-token}

移行トークンの自動取得は、ターゲットの Cloud Service 環境における [Cloud Manager を介した IP 許可リストの設定](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)など、様々な理由で失敗する場合があります。このようなシナリオでは、取り込みを開始しようとすると、次のダイアログボックスが表示されます。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

ダイアログボックスの「トークンを取得」リンクをクリックして、移行トークンを手動で取得します。別のタブが開き、トークンが表示されます。その後、トークンをコピーし、**移行トークン入力**&#x200B;フィールドにペーストします。 これで、取り込みを開始できるようになります。

>[!NOTE]
>
>トークンは、宛先 Cloud Service オーサーサービスのローカル **AEM 管理者**&#x200B;グループに属するユーザーが使用することができます。

### 取り込みを開始できない {#unable-to-start-ingestion}

宛先環境への取り込みを開始するには、宛先 Cloud Service オーサーサービスで、自身もローカルの **AEM 管理者**&#x200B;グループに属している必要があります。AEM 管理者グループに属していない場合は、取り込みを開始しようとすると、次に示すようなエラーが表示されます。管理者に問い合わせてローカルの **AEM 管理者**&#x200B;に追加するよう依頼するか、トークン自体を依頼してから&#x200B;**移行トークン入力**&#x200B;フィールドにペーストすることができます。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 移行サービスに接続できません {#unable-to-reach-migration-service}

取り込みがリクエストされると、次のようなメッセージがユーザーに表示される場合があります。「宛先環境の移行サービスにアクセスできません。その場合は、後でもう一度試すか、アドビサポートにお問い合わせください。」

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

このメッセージは、Cloud Acceleration Manager がターゲット環境の移行サービスにアクセスして取り込みを開始できなかったことを示します。この状況は、様々な理由で発生する可能性があります。

>[!NOTE]
> 
> 「移行トークン」フィールドが表示されるのは、そのトークンの取得が実際には許可されていない場合があるためです。手動で指定できるようにすることで、ユーザーは追加のヘルプなしで、すばやく取り込みを開始できます。 トークンが指定されているにもかかわらず、メッセージが表示される場合、問題はトークンの取得ではありません。

* AEM as a Cloud Service は環境の状態を維持し、様々な通常の理由で移行サービスの再起動が必要になる場合があります。そのサービスが再起動中の場合はサービスにアクセスできませんが、最終的には利用できるようになります。
* インスタンス上で別のプロセスが実行されている可能性があります。例えば、 [AEMバージョンの更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=ja) 更新を適用中です。システムがビジー状態で、移行サービスが定期的に使用できない可能性があります。 その後、取り込みの開始を再試行できます。
* Cloud Manager を使用して [IP 許可リストが適用されている](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)場合、Cloud Acceleration Manager が移行サービスに到達するのをブロックします。アドレスが動的なので、取り込み用に IP アドレスを追加することはできません。現在、唯一の解決策は、取り込みとインデックス作成プロセス中に IP許可リストに加えるを無効にすることです。
* 調査を要する他の理由がある場合があります。 取り込みまたはインデックス作成が引き続き失敗する場合は、Adobeカスタマーケアにお問い合わせください。

### AEMバージョンの更新と取り込み {#aem-version-updates-and-ingestions}

[AEMバージョンの更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=ja) は、最新のAEM as a Cloud Serviceバージョンを使用して最新の状態に保つために、環境に自動的に適用されます。 取り込みの実行時に更新がトリガーされると、環境の破損を含む予期しない結果が生じる可能性があります。

「AEM Version Updates」が宛先プログラムでオンボーディングされている場合、取り込みプロセスは、キューを開始する前に無効にしようとします。 取り込みが完了すると、バージョンアップデータの状態が、取り込みが開始する前の状態に戻ります。

>[!NOTE]
>
> 「AEMバージョンの更新」を無効にするために、サポートチケットをログに記録する必要はなくなりました。

「AEM Version Updates」がアクティブな場合（つまり、更新が実行中か、実行待ちのキューに入っている場合）、取り込みは開始されず、ユーザーインターフェイスに次のメッセージが表示されます。 更新が完了したら、取り込みを開始できます。 Cloud Manager を使用して、プログラムのパイプラインの現在の状態を確認できます。

>[!NOTE]
>
> 「AEM Version Updates」は、環境のパイプラインで実行され、パイプラインがクリアされるまで待ちます。 更新が予想より長い時間キューに入れられている場合は、カスタムワークフローでパイプラインが意図せずロックされていないことを確認します。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### 一意性制約違反による追加取り込み失敗 {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

[追加取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)エラーの一般的な原因は、ノード ID の競合です。このエラーを識別するには、Cloud Acceleration Manager UI を使用して取り込みログをダウンロードし、次のようなエントリを探します。

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Uniqueness constraint violated property [jcr:uuid] having value a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

AEM の各ノードには、一意の UUID が必要です。このエラーは、取り込まれるノードが、宛先インスタンス上の別のパスに存在する uuid と同じ uuid を持つことを示します。
この状況は、抽出と後続の[追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)の間でノードがソース上で移動された場合に発生する可能性があります。
また、宛先のノードが取り込みとそれ以降の追加取り込みの間に移動した場合にも発生する可能性があります。

この競合は手動で解決する必要があります。コンテンツを参照する他のコンテンツに留意し、2 つのノードのうち、削除する必要があるノードをコンテンツに精通したユーザーが決定する必要があります。解決策として、問題のあるノードがなくても、追加抽出を再度行う必要が生じる場合があります。

### 参照されているノードを削除できないことが原因で追加取り込みに失敗しました {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

の別の一般的な原因 [追加取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) failure は、宛先インスタンス上の特定のノードに対するバージョンの競合です。 このエラーを識別するには、Cloud Acceleration Manager UI を使用して取り込みログをダウンロードし、次のようなエントリを探します。

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity0001：参照されているノードを削除できません： 8a2289f4-b904-4bd0-8410-15e41e0976a8

この問題は、取り込みとそれ以降の間に宛先のノードが変更された場合に発生する可能性があります **ワイプしない** 取り込み（新しいバージョンが作成される） 「バージョンを含める」を有効にして移行セットを抽出した場合、宛先にバージョン履歴や他のコンテンツで参照される最新のバージョンが含まれているので、競合が発生する可能性があります。 取り込みプロセスは、参照されているので、問題のあるバージョンノードを削除できません。

ソリューションでは、問題のあるノードがなくても、追加抽出を再び実行する必要が生じる場合があります。 または、問題のあるノードの小さな移行セットを作成し、「インクルードバージョン」を無効にします。

ベストプラクティスは、 **ワイプしない** 取り込みは、バージョンを含む移行セットを使用して実行する必要があります。移行ジャーニーが完了するまで、宛先のコンテンツをできる限り小さく変更することが重要です。 そうしないと、これらの競合が発生する可能性があります。

### ノードプロパティ値が大きいため取り込みに失敗しました {#ingestion-failure-due-to-large-node-property-values}

MongoDB に保存されるノードプロパティの値は 16 MB を超えることはできません。ノード値がサポートされているサイズを超えると、取り込みは失敗し、ログには `BSONObjectTooLarge` エラーが発生し、最大数を超えたノードを指定してください。 これは MongoDB の制限です。

詳しくは、 `Node property value in MongoDB` 注意 [コンテンツ転送ツールの前提条件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md) すべての大きなノードを見つけるのに役立つ Oak ツールへのリンクと詳細情報。 サイズの大きいすべてのノードを修正したら、抽出と取り込みを再度実行します。

### 取り込みの取り消し {#ingestion-rescinded}

実行中の抽出で作成されたインジェスト。ソース移行セットは、抽出が成功するまで待ち、その時点で正常に開始します。 抽出が失敗または停止した場合、取り込みとそのインデックス作成ジョブは開始されませんが、取り消されます。 この場合は、抽出をチェックして失敗した理由を判断し、問題を修正して、再度抽出を開始します。 固定抽出を実行した後で、新しい取り込みをスケジュールできます。

## 次の手順 {#whats-next}

取り込みが成功すると、AEMのインデックス作成が自動的に開始されます。 詳しくは、 [コンテンツ移行後のインデックス作成](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) を参照してください。

コンテンツのCloud Serviceへの取り込みが完了したら、各ステップのログ（抽出および取り込み）を表示し、エラーを探すことができます。 詳しくは、[移行セットのログの表示](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md)を参照してください。
