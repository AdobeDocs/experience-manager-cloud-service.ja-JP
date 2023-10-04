---
title: コンテンツの取り込みCloud Service
description: Cloud Acceleration Manager を使用して、移行セットから宛先Cloud Serviceインスタンスにコンテンツを取り込む方法を説明します。
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: a6d19de48f114982942b0b8a6f6cbdc38b0d4dfa
workflow-type: tm+mt
source-wordcount: '2191'
ht-degree: 28%

---

# コンテンツの取り込みCloud Service {#ingesting-content}

## Cloud Acceleration Manager での取り込みプロセス {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="コンテンツの取得"
>abstract="取得とは、移行セットから宛先の Cloud Service インスタンスにコンテンツを取得することを指します。コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=ja#top-up-extraction-process" text="追加抽出"

Cloud Acceleration Manager を使用して移行セットを取り込むには、次の手順に従います。

1. Cloud Acceleration Manager に移動します。プロジェクトカードをクリックし、「コンテンツ転送」カードをクリックします。 に移動します。 **取り込みジョブ** をクリックします。 **新しい取り込み**

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
   > オプションのプリコピー手順を実行すると、取り込みを大幅に高速化できます。 詳しくは、 [AzCopy での取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) を参照してください。
   > 事前コピーを使用した取得を（S3 または Azure データストアに対して）使用する場合は、最初にオーサーの取得を単独で実行することをお勧めします。これにより、後で実行された場合に、パブリッシュの取り込みが高速化されます。
   > 取り込みは、Rapid Development Environment(RDE) の宛先をサポートしておらず、ユーザーがアクセスできる場合でも、目的の宛先として表示されません。

   >[!IMPORTANT]
   > 宛先環境への取り込みは、ローカルの **AEM管理者** グループを作成します。 取り込みを開始できない場合は、 [取り込みを開始できません](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) を参照してください。

   * を選択します。 `Wipe` 値
      * The **ワイプ** 「 」オプションは、インジェストの開始点を設定します。 次の場合 **ワイプ** を有効にすると、そのすべてのコンテンツを含む宛先が、Cloud Manager で指定されたAEMのバージョンにリセットされます。 有効にしない場合、宛先は現在のコンテンツを出発点として維持します。
      * このオプションは **NOT** は、コンテンツの取り込みの実行方法に影響します。 取り込みでは常にコンテンツ置換戦略を使用し、 _not_ コンテンツ結合戦略で、両方で **ワイプ** および **ワイプしない** 場合、移行セットを取り込むと、宛先上の同じパスにあるコンテンツが上書きされます。 例えば、移行セットに `/content/page1` と宛先には既に次が含まれています： `/content/page1/product1`を含めない場合、取り込みにより、 `page1` パスとそのサブページ ( `product1`をクリックし、移行セット内のコンテンツに置き換えます。 つまり、 **ワイプしない** 管理する必要のあるコンテンツを含む宛先への取り込み。

   >[!IMPORTANT]
   > 設定が **ワイプ** を有効にすると、ターゲットリポジトリインスタンスに対するユーザー権限を含む、既存のCloud Service全体がリセットされます。 このリセットは、管理者ユーザーが **管理者** 取り込みを開始するには、グループに追加し、そのユーザーを administrators グループに再度追加する必要があります。

1. クリック **取り込み**.

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. その後、取り込みジョブリストビューから取り込みを監視し、取り込みのアクションメニューを使用して、取り込みの進行に応じて期間とログを表示できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 次をクリック： **一** ボタンをクリックして、取り込みジョブの詳細を確認してください。 取り込みの各手順の実行中または完了時の期間は、「 **...**&#x200B;をクリックし、 **期間を表示**. また、抽出した情報は、取り込まれている内容を実現するためにも示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## 追加取り込み {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="追加取り込み"
>abstract="前回のコンテンツ転送アクティビティ以降に変更されたコンテンツを移動するには、追加取り込み機能を使用します。取り込みが完了したら、ログを調べて、エラーや警告がないか確認します。エラーが発生した場合は、報告された問題を解決するかアドビカスタマーケアに連絡して、すぐに対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=ja" text="ログの表示"

コンテンツ転送ツールには、 *トップアップ* 移行セットの これにより、移行セットを変更して、前の抽出以降に変更されたコンテンツのみを含めることができ、再度すべてのコンテンツを抽出する必要がなくなります。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初の取り込みにコピー前の手順を使用した場合、後続の追加取り込みに対してコピー前の手順をスキップできます（追加の移行セットのサイズが 200 GB 未満の場合）。 これは、プロセス全体に時間がかかる可能性があるからです。

一部の取り込みが完了した後に差分コンテンツを取り込むには、 [追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)次に、 **ワイプ** オプション **無効**. 必ず **ワイプ** 上記の説明を参照して、宛先に既に存在するコンテンツが失われないようにします。

取り込みジョブを作成して、次の点を確認します。 **ワイプ** は、次に示すように、取り込み中は無効になります。

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

取り込みがリクエストされると、「宛先環境の移行サービスに到達できません。 その場合は、後でやり直すか、Adobeサポートにお問い合わせください。」

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

このメッセージは、Cloud Acceleration Manager が、ターゲット環境の移行サービスに到達して取り込みを開始できなかったことを示します。 この状況は、様々な理由で発生する可能性があります。

>[!NOTE]
> 
> 「移行トークン」フィールドが表示されるのは、そのトークンの取得が実際には許可されていない場合があるためです。手動で指定できるようにすることで、ユーザーは追加のヘルプなしで、すばやく取り込みを開始できます。 トークンが指定され、メッセージが表示される場合は、トークンの取得に問題はありませんでした。

* AEM as a Cloud Serviceは環境の状態を維持し、通常の様々な理由で移行サービスを再起動する必要が生じる場合があります。 そのサービスが再起動中の場合は、そのサービスには到達できませんが、最終的に使用可能になります。
* 別のプロセスがインスタンス上で実行されている可能性があります。 例えば、 [AEMバージョンの更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=ja) 更新を適用中です。システムがビジー状態で、移行サービスが定期的に使用できない可能性があります。 その後、取り込みの開始を再試行できます。
* 次の場合、 [IP許可リストに加えるが適用されました](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) Cloud Manager を通じて、 Cloud Acceleration Manager が移行サービスに到達するのをブロックします。 アドレスが動的なので、取り込み用に IP アドレスを追加できません。 現在、唯一の解決策は、取り込みの実行中に IP 許可リストを無効にすることです。
* 調査を要する他の理由がある場合があります。 それでも取り込みに失敗する場合は、Adobeカスタマーケアにお問い合わせください。

### AEMバージョンの更新と取り込み

[AEMバージョンの更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=ja) は、最新のAEM as a Cloud Serviceバージョンを使用して最新の状態に保つために、環境に自動的に適用されます。 取り込みの実行時に更新がトリガーされると、環境の破損を含む予期しない結果が生じる可能性があります。

「AEM Version Updates」が宛先プログラムでオンボーディングされている場合、取り込みプロセスは、キューを開始する前に無効にしようとします。 取り込みが完了すると、バージョンアップデータの状態が、取り込みが開始される前の状態に戻ります。

>[!NOTE]
>
> 「AEMバージョンの更新」を無効にするために、サポートチケットをログに記録する必要はなくなりました。

「AEM Version Updates」がアクティブな場合（更新が実行中、または実行待ちのキューに入れられている場合）、取り込みは開始されず、ユーザーインターフェイスに次のメッセージが表示されます。 更新が完了したら、取り込みを開始できます。 Cloud Manager を使用して、プログラムのパイプラインの現在の状態を確認できます。

>[!NOTE]
>
> 「AEM Version Updates」は、環境のパイプラインで実行され、パイプラインがクリアされるまで待ちます。 更新が予想より長い時間キューに入れられている場合は、カスタムワークフローでパイプラインが意図せずロックされていないことを確認します。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### 追加取り込みエラー 一意性制約違反による

[追加取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)エラーの一般的な原因は、ノード ID の競合です。このエラーを識別するには、Cloud Acceleration Manager UI を使用して取り込みログをダウンロードし、次のようなエントリを探します。

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Uniqueness constraint violated property [jcr:uuid] having value a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

AEM の各ノードには、一意の UUID が必要です。このエラーは、取り込まれるノードが、宛先インスタンス上の別のパスに存在する uuid と同じ uuid を持つことを示します。
この状況は、抽出とそれ以降の間にソース上でノードが移動した場合に発生する可能性があります [追加抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
また、宛先のノードが取り込みとそれ以降の追加取り込みの間に移動した場合にも発生する可能性があります。

この競合は手動で解決する必要があります。コンテンツを参照する他のコンテンツに留意し、2 つのノードのうち、削除する必要があるノードをコンテンツに精通したユーザーが決定する必要があります。解決策として、問題のあるノードがなくても、追加抽出を再度行う必要が生じる場合があります。

### 参照されているノードを削除できないことが原因で追加取り込みに失敗しました

の別の一般的な原因 [追加取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) failure は、宛先インスタンス上の特定のノードに対するバージョンの競合です。 このエラーを識別するには、Cloud Acceleration Manager UI を使用して取り込みログをダウンロードし、次のようなエントリを探します。
>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity0001：参照されているノードを削除できません： 8a2289f4-b904-4bd0-8410-15e41e0976a8

この問題は、取り込みとそれ以降の間に宛先のノードが変更された場合に発生する可能性があります **ワイプしない** 取り込み（新しいバージョンが作成される） 「バージョンを含める」を有効にして移行セットを抽出した場合、宛先にバージョン履歴や他のコンテンツで参照される最新のバージョンが含まれているので、競合が発生する可能性があります。 取り込みプロセスは、参照されているので、問題のあるバージョンノードを削除できません。

解決策として、問題のあるノードがなくても、追加抽出を再度行う必要が生じる場合があります。または、問題のあるノードの小さな移行セットを作成し、「インクルードバージョン」を無効にします。

ベストプラクティスは、 **ワイプしない** 取り込みは、バージョンを含む移行セット（「include versions」=true で抽出）を使用して実行する必要があります。移行ジャーニーが完了するまで、宛先のコンテンツをできる限り小さく変更する必要があります。 そうしないと、これらの競合が発生する可能性があります。


## 次の手順 {#whats-next}

取り込みが成功すると、AEMのインデックス作成が自動的に開始されます。 詳しくは、 [コンテンツ移行後のインデックス作成](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) を参照してください。

コンテンツのCloud Serviceへの取り込みが完了したら、各ステップのログ（抽出および取り込み）を表示し、エラーを探すことができます。 詳しくは、[移行セットのログの表示](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md)を参照してください。
