---
title: コンテンツ転送ツールの使用
description: コンテンツ転送ツールの使用
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 04494e116fcdd38622ae2d4434d7cf8e4034d5aa
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 75%

---

# コンテンツ転送ツールの使用 {#using-content-transfer-tool}

## コンテンツ転送の抽出プロセス {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="コンテンツの抽出"
>abstract="抽出とは、ソース AEM インスタンスから、移行セットと呼ばれる一時領域にコンテンツを抽出することです。移行セットは、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="追加抽出"

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

### 追加抽出 {#top-up-extraction-process}

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

## コンテンツ転送のインジェストプロセス {#ingestion-process}

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

   さらに、「**カスタマーケア**」をクリックしてチケットを発行します（上図を参照）。詳しくは、[コンテンツ転送ツール使用時の重要な考慮事項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#pre-reqs)も参照してください。

1. 取り込みが完了すると、ステータスが **FINISHED** に更新されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

### 追加インジェスト {#top-up-ingestion-process}

コンテンツ転送ツールには、*差分コンテンツ追加*&#x200B;をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁におこなって、Cloud Service での運用を開始する前におこなう最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

インジェストプロセスが完了したら、追加インジェスト方式を使用して差分コンテンツを転送できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、追加取得の実行対象となる移行セットを選択します。「**取得**」をクリックして、追加取得を開始します。**移行セットのインジェスト**&#x200B;ダイアログボックスが表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >以前の取得アクティビティから既存のコンテンツを削除しないようにするには、「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションを無効にする必要があります。さらに、「**カスタマーケア**」をクリックしてチケットを発行します（上図を参照）。


### 移行セットのログの表示 {#viewing-logs-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="ログの表示"
>abstract="取得の抽出が完了したら、エラーや警告がないかログを確認します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="トラブルシューティング"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="アドビサポートのご案内"

各ステップ（抽出と取り込み）が完了したら、ログを確認してエラーを探します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。

既存の移行セットのログを&#x200B;*概要*&#x200B;ページから表示できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、ログを表示する移行セットを選択し、アクションバーの「**ログを表示**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. **ログ**&#x200B;ダイアログボックスが表示されます。「**抽出ログ**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
または、

   *概要*&#x200B;画面から移行セットのログを直接表示することもできます。移行セットを選択し、「**抽出**」フィールド内のステータスをクリックします。下図の場合は、「**完了**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. ユーザーインターフェイスを使用せずにログの末尾を表示するには、ソース AEM 環境に SSH で接続し、`crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`で tail コマンドを実行します。

### 移行セットの削除 {#deleting-migration-set}

*概要*ページで移行セットを削除できます。
それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、削除する移行セットを選択し、アクションバーの「**削除**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. **移行セットを削除**&#x200B;ダイアログボックスの「**削除**」をクリックして、削除を確定します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)


## パブリッシュインスタンスでのコンテンツ転送ツールの実行 {#running-ctt-on-publish}

コンテンツをパブリッシュインスタンスに移動する際に、CTT をソースパブリッシュインスタンスにインストールして、コンテンツをターゲットのパブリッシュインスタンスに移動することをお勧めします。 次に説明する推奨アプローチに従います。

* オーサーインスタンスで使用したのと同じバージョンの CTT を使用します。

* 移行する必要があるのは、1 つのパブリッシュノードだけです。 抽出を開始する前に、ロードバランサーから削除する必要があります。

* 移行セットを作成する場合は、オーサー AEMaCS 環境の URL を使用します。

* パブリッシュへの取り込み時に、パブリッシュ層は（オーサーとは異なり）スケールダウンされません。 予防策として、次のようなユーザーによる書き込み操作は避けてください。

   * AEMaCS オーサーからその環境のパブリッシュへのコンテンツの配布
   * パブリッシュインスタンス間のユーザー同期


## トラブルシューティング {#troubleshooting}

### 不明な BLOB ID {#missing-blobs}

以下に示すように、不明な BLOB ID が報告された場合は、既存のリポジトリーで整合性チェックを実行し、不明な BLOB を復元する必要があります。
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

以下のコマンドを実行します。

>[!NOTE]
>
>`--verbose` フラグが必要なのは、BLOB の参照元ノードのパスを報告するためです。

**AEM 6.5（Oak 1.8 以前）のリポジトリーの場合**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Oak 1.10 以降のリポジトリーの場合**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

詳しくは、[Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)（Oak 実行可能 Jar）を参照してください。

整合性チェックのために上記で指定された *OUT_DIR* に作成されたファイルを調べて、不明なバイナリのパスや必要なアクション（バックアップからの復元、パスの削除、インデックスの再作成など）を確認できます。


### UI の動作 {#ui-behavior}

コンテンツ転送ツールのユーザーインターフェイス（UI）に次のような動作が見られることがあります。

* コンテンツ転送ツール UI のアイコンが、このガイドに示すスクリーンショットとは異なって表示される場合や、ソース AEM インスタンスのバージョンによっては表示されない場合があります。
