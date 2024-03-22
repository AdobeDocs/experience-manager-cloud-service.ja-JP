---
title: コンテンツの Cloud Service への取り込み
description: Cloud Acceleration Manager を使用して、移行セットから移行先の Cloud Service インスタンスにコンテンツを取り込む方法について説明します。
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: de05abac3620b254343196a283cef198f434cfca
workflow-type: tm+mt
source-wordcount: '2752'
ht-degree: 87%

---

# コンテンツの Cloud Service への取り込み {#ingesting-content}

## Cloud Acceleration Manager での取得プロセス {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="コンテンツの取り込み"
>abstract="取得とは、移行セットから宛先の Cloud Service インスタンスにコンテンツを取得することを指します。コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=ja#top-up-extraction-process" text="追加抽出"

Cloud Acceleration Manager を使用して移行セットを取り込むには、次の手順に従います。

1. Cloud Acceleration Manager に移動します。プロジェクトカードをクリックし、コンテンツ転送カードをクリックします。**取り込みジョブ**&#x200B;に移動し、「**新しい取り込み**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 取り込みチェックリストをレビューし、すべての手順が完了していることを確認します。 これらの手順は、取り込みを正常に行うために必要です。チェックリストが完了した場合のみ、**次**&#x200B;の手順に進みます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 取り込みを作成するために必要な情報を入力します。

   * **移行セット：**&#x200B;抽出したデータをソースとして含む移行セットを選択します。
      * 移行セットは、無操作状態が長時間続くと有効期限が切れるので、抽出が実行された後は、比較的早く取り込みが行われることが期待されます。詳しくは、[移行セットの有効期限](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)を確認してください。

   >[!TIP]
   > 抽出が実行中の場合は、ダイアログにその旨が示されます。抽出が正常に完了すると、取り込みが自動的に開始されます。抽出が失敗または停止した場合、取り込みジョブは取り消されます。

   * **移行先：**&#x200B;移行先の環境を選択します。この環境では、移行セットのコンテンツが取り込まれます。
      * 取り込みでは、迅速な開発環境（RDE）やプレビューが出力先としてサポートされておらず、ユーザーがアクセスできる場合でも出力先の選択肢として表示されません。
      * 移行セットは複数の宛先に同時に取り込むことができますが、宛先は一度に 1 つの実行中または待機中の取り込みのターゲットになります。

   * **層：** 層を選択します。（オーサー／パブリッシュ）。
      * ソースが `Author` の場合は、ターゲットの `Author` 層に取り込むことをお勧めします。同様に、ソースが `Publish` の場合は、ターゲットも `Publish` にする必要があります。

   >[!NOTE]
   > ターゲット層が `Author` の場合、オーサーインスタンスは取り込み期間中にシャットダウンされ、ユーザー（作成者やメンテナンスを実行中のユーザーなど）が使用できなくなります。これは、システムを保護し、失われたり取り込みの競合を引き起こしたりする可能性のある変更を防ぐためです。チームがこの事実を認識していることを確認してください。また、オーサーの取り込み中は環境が休止状態と表示されることに注意してください。

   * **ワイプ：**`Wipe` 値を選択します。
      * 「**ワイプ**」オプションは、取り込みにおける宛先の開始点となります。**ワイプ**&#x200B;を有効にすると、そのすべてのコンテンツを含む宛先が、Cloud Manager で指定された AEM のバージョンにリセットされます。有効にしない場合、宛先は現在の内容を開始点として維持します。
      * このオプションは、コンテンツの取り込みの実行方法には影響&#x200B;**しません**。取り込みでは内容を結合する戦略&#x200B;_ではなく_、常に内容を置換する戦略を使用します。これにより、**ワイプあり**&#x200B;と&#x200B;**ワイプなし**&#x200B;のいずれの場合でも、移行セットを取り込むと、宛先の同じパスにある内容が上書きされます。例えば、移行セットに `/content/page1` が含まれ、移行先には既に `/content/page1/product1` が含まれている場合、取り込みを行うと `page1` パスとそのサブページ（`product1` など）が削除され、移行セット内の内容に置き換えられます。そのため、維持する必要がある内容を含む宛先に対して&#x200B;**ワイプなし**&#x200B;の取り込みを実行する場合は、慎重に計画する必要があります。

   >[!IMPORTANT]
   > 取り込みに対して&#x200B;**ワイプ**&#x200B;設定を有効にすると、ターゲットの Cloud Service インスタンスに対するユーザーの権限を含む、既存のリポジトリ全体がリセットされます。このリセットは、**管理者**&#x200B;グループに追加されている管理者ユーザーにも当てはまります。管理者グループに再度追加されない限り、こうしたユーザーが取り込みを開始することはできません。

   * **事前コピー：** `Pre-copy` 値を選択します。
      * オプションのプレコピー手順を実行すると、取り込みを大幅に高速化できます。詳しくは、[AzCopy で取り込む](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy)を参照してください。
      * 事前コピーによる取り込みを（S3 または Azure データストアに対して）使用する場合は、最初に `Author` 取り込みを単独で実行することをお勧めします。これにより、後で実行する際に、`Publish` 取り込みが高速化されます。

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
>abstract="前回のコンテンツ転送アクティビティ以降に変更されたコンテンツを移動するには、追加取り込み機能を使用します。取り込みが完了したら、エラーや警告がないかログを確認します。エラーが発生した場合は、報告された問題を解決するかアドビカスタマーケアに連絡して、すぐに対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=ja" text="ログの表示"

コンテンツ転送ツールには、移行セットの&#x200B;*追加*&#x200B;を実行することで、差分コンテンツを抽出できる機能が備わっています。これにより、再度すべてのコンテンツを抽出するのではなく、前回の抽出以降に変更されたコンテンツのみを含めるように移行セットを変更できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツの追加を頻繁に行って、Cloud Service での運用を開始する前に行う最終的な差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初の取り込みで事前コピー手順を使用した場合、後続の追加取り込みでは（追加移行セットのサイズが 200 GB 未満の場合）事前コピーをスキップできます。これは、プロセス全体に時間がかかる可能性があるためです。

一部の取り込みが完了した後に差分コンテンツを取り込むには、[追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)を実行してから、**ワイプ**&#x200B;オプションを&#x200B;**無効**&#x200B;にした取り込み方法を使用する必要があります。必ず上記の&#x200B;**ワイプ**&#x200B;の説明を参照して、宛先にある既存のコンテンツが失われないようにしてください。

最初に、取り込みジョブを作成し、以下に示すとおり、取り込み中に&#x200B;**ワイプ**&#x200B;が無効になっていることを確認します。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## トラブルシューティング {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="コンテンツ取り込みのトラブルシューティング"
>abstract="取り込みログとドキュメントを参照して、取り込みが失敗する一般的な原因に関する解決策を見つけ、問題を修正します。修正したら、取り込みを再実行できます。"
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
* インスタンス上で別のプロセスが実行されている可能性があります。例えば、[AEM バージョンの更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=ja)の適用中にシステムがビジー状態になり、移行サービスが定期的に利用できなくなる可能性があります。その場合はプロセスが完了すると、取り込みの開始を再試行できます。
* Cloud Manager を使用して [IP 許可リストが適用されている](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)場合、Cloud Acceleration Manager が移行サービスに到達するのをブロックします。アドレスが動的なので、取り込み用に IP アドレスを追加することはできません。現在、唯一の解決策は、取り込みとインデックス作成プロセス中に IP 許可リストを無効にすることです。
* 調査が必要となる理由が、他に存在する場合があります。それでも取り込みやインデックス作成に失敗する場合は、アドビカスタマーケアにお問い合わせください。

### AEM バージョンの更新と取り込み {#aem-version-updates-and-ingestions}

[AEM バージョンの更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=ja)は、最新の AEM as a Cloud Service バージョンを使用して最新の状態に保つために、環境に自動的に適用されます。取り込みの実行中に更新がトリガーされると、環境が壊れるなど、予期しない結果が生じる可能性があります。

移行先プログラムで「AEM バージョンの更新」がオンボーディングされている場合、取り込みプロセスでは、開始前にそのキューを無効にしようとします。取り込みが完了すると、バージョン更新の状態が、取り込み開始前の状態に戻ります。

>[!NOTE]
>
> 「AEM バージョンの更新」を無効にするために、サポートチケットを記録する必要はなくなりました。

「AEM バージョンの更新」がアクティブな場合（つまり、更新が実行中か、実行待ちのキューに入っている場合）は取り込みが開始されず、ユーザーインターフェイスに以下のメッセージが表示されます。更新が完了したら、取り込みを開始できます。Cloud Manager を使用して、プログラムのパイプラインの現在の状態を確認できます。

>[!NOTE]
>
> 「AEM バージョンの更新」は環境のパイプラインで実行され、パイプラインがクリアされるまで待機します。更新が予想より長い時間キューに登録されている場合は、カスタムワークフローでパイプラインが意図せずロックされていないか確認してください。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### 一意性制約違反による追加取り込みのエラー {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_uuid"
>title="一意性制約違反"
>abstract="非ワイプ取り込みエラーの一般的な原因は、ノード ID が競合していることです。 競合するノードは 1 つだけです。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html#top-up-ingestion-process" text="追加取り込み"

[追加取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)エラーの一般的な原因は、ノード ID の競合です。このエラーを識別するには、Cloud Acceleration Manager UI を使用して取り込みログをダウンロードし、次のようなエントリを探します。

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Uniqueness constraint violated property [jcr:uuid] having value a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

AEM の各ノードには、一意の UUID が必要です。このエラーは、取り込まれているノードの UUID が、移行先インスタンスの別のパスに存在するノードと同じであることを示します。この状況は、以下の 2 つの理由で発生する可能性があります。

* 抽出と後続の[追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)の間でノードがソース上で移動される
   * _留意事項_：追加抽出の場合、ソース上に存在しなくなっても、移行セットにノードが存在します。
* 移行先のノードが取り込みと後続の追加取り込みの間に移動される

この競合は手動で解決する必要があります。コンテンツを参照する他のコンテンツに留意し、2 つのノードのうち、削除する必要があるノードをコンテンツに精通したユーザーが決定する必要があります。解決策として、問題のあるノードがなくても、追加抽出を再度行う必要が生じる場合があります。

### 参照されているノードを削除できないことによる追加取り込みの失敗 {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_referenced_node"
>title="参照されているノードを削除できません"
>abstract="ワイプしない取り込みエラーの一般的な原因は、宛先インスタンス上の特定のノードのバージョンの競合です。 ノードのバージョンを修正する必要があります。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html#top-up-ingestion-process" text="追加取り込み"

[追加取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)が失敗するもう一つの一般的な原因は、移行先インスタンスの特定のノードに対するバージョンの競合です。このエラーを識別するには、Cloud Acceleration Manager UI を使用して取り込みログをダウンロードし、次のようなエントリを探します。

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity0001: Unable to delete referenced node: 8a2289f4-b904-4bd0-8410-15e41e0976a8

この問題は、取り込みと、新しいバージョンが作成された後続の&#x200B;**ワイプなし**&#x200B;の取り込みの間で、移行先のノードが変更された場合に発生する可能性があります。「バージョンを含める」を有効にして移行セットを抽出した場合、移行先にはバージョン履歴やその他のコンテンツで参照されるより新しいバージョンが含まれるため、競合が発生する可能性があります。取り込みプロセスでは、問題のあるバージョンノードが参照されているため、そのノードを削除できません。

解決策として、問題のあるノードを使用せずに、追加抽出を再度行う必要が生じる場合があります。または、問題のあるノードの小さな移行セットを作成し、「インクルードバージョン」を無効にします。

バージョンを含む移行セットを使用して、**ワイプなし**&#x200B;の取り込みを実行する必要がある場合は、移行ジャーニーが完了するまで、移行先のコンテンツをできるだけ変更しないのがベストプラクティスです。そうしないと、これらの競合が発生する可能性があります。

### ノードプロパティの大きな値による取り込みエラー {#ingestion-failure-due-to-large-node-property-values}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_bson"
>title="Large Node プロパティ"
>abstract="取り込み失敗の一般的な原因は、ノードプロパティの値の最大サイズを超えていることです。 この状況を修正するには、BPA レポートに関連するものを含むドキュメントに従います。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=ja" text="移行の前提条件"

MongoDB に保存されるノードプロパティの値は 16 MB を超えることはできません。ノード値がサポートされているサイズを超えると、取り込みに失敗し、ログには `BSONObjectTooLarge` エラーが含まれ、最大値を超えたノードが指定されます。これは MongoDB の制限です。

大きなノードすべてを見つけるのに役立つ Oak ツールへのリンクと詳細情報については、[コンテンツ転送ツールの前提条件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md)の `Node property value in MongoDB` メモを参照してください。サイズの大きいすべてのノードを修正したら、抽出と取り込みを再度実行します。

### 取り込みの取り消し {#ingestion-rescinded}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_rescinded"
>title="取り込みの取り消し"
>abstract="取り込みを待機していた抽出が正常に完了しませんでした。 実行できなかったので、取り込みが取り消されました。"

ソース移行セットとして、実行中の抽出で作成された取り込みは、その取り込みが成功するまで待機し、その時点で正常に開始されます。抽出が失敗または停止した場合、取り込みおよびそのインデックス作成ジョブは開始されず、取り消されます。この場合は、抽出をチェックして失敗した理由を判断し、問題を修正して、再度抽出を開始します。固定抽出を実行した後で、新しい取り込みをスケジュールできます。

### 取り込みを再実行した後、削除されたアセットが存在しません

一般に、取り込みの間にクラウド環境データを変更することはお勧めしません。

Assets タッチ UI を使用してCloud Serviceの宛先からアセットを削除すると、ノードデータは削除されますが、画像を含むアセット BLOB は即座に削除されません。 削除のマークが付けられ、UI に表示されなくなります。ただし、ガベージコレクションが発生して BLOB が削除されるまで、データストアに残ります。

以前に移行したアセットが削除され、次の取り込みがガベージコレクターがアセットの削除を完了する前に実行される場合、同じ移行セットを取り込んでも、削除されたアセットは復元されません。 取り込みがクラウド環境でアセットを確認すると、ノードデータがなくなるので、取り込みはノードデータをクラウド環境にコピーします。 ただし、BLOB ストアをチェックすると、BLOB が存在することが確認され、BLOB をコピーするのをスキップします。 これは、タッチ UI からアセットを見ると取り込み後にメタデータが表示されるのに対し、画像は表示されないためです。 移行セットとコンテンツ取り込みは、この場合に対処するように設計されていません。 これらは、以前に移行したコンテンツを復元するのではなく、クラウド環境に新しいコンテンツを追加することを目的としています。

## 次の手順 {#whats-next}

取り込みが成功すると、AEM のインデックス作成が自動的に開始されます。詳しくは、[コンテンツ移行後のインデックス作成](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md)を参照してください。

Cloud Service へのコンテンツの取り込みが完了したら、各ステップ（抽出と取り込み）のログを表示し、エラーを探すことができます。詳しくは、[移行セットのログの表示](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md)を参照してください。
