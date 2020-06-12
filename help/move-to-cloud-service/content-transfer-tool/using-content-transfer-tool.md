---
title: コンテンツ転送ツールの使用
description: コンテンツ転送ツールの使用
translation-type: tm+mt
source-git-commit: 0ab2631dc5ae67a50522b3a6b29d1cb4c674d193
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 86%

---


# コンテンツ転送ツールの使用 {#using-content-transfer-tool}

## コンテンツ転送ツール使用時の重要な考慮事項 {#pre-reqs}

コンテンツ転送ツールを実行する際には、次の重要事項を考慮してください。

* コンテンツ転送ツールに必要なシステム構成は、AEM 6.3 以降と Java 8 です。使用している AEM のバージョンがこれより古い場合、コンテンツ転送ツールを使用するには、コンテンツリポジトリを AEM 6.5 にアップグレードする必要があります。

* If you are using a *Sandbox Environment*, ensure that your environment is upgraded to June 10 2020 Release or later. *実稼働環境*&#x200B;を使用している場合、環境は自動的に更新されます。

* コンテンツ転送ツールを使用するには、ソースインスタンスの管理者ユーザーで、コンテンツの転送先のクラウドサービスインスタンスのAEM管理者グループに属している必要があります。 権限のないユーザーは、コンテンツ転送ツールを使用するアクセストークンを取得できません。

* 抽出段階では、コンテンツ転送ツールはアクティブな AEM ソースインスタンスで実行されます。

* オーサーの&#x200B;*インジェスト段階*&#x200B;では、オーサーのデプロイメント全体がスケールダウンされます。つまり、オーサー AEM インスタンスは、インジェストプロセス全体で使用できなくなります。

* コンテンツ転送ツールで一度にサポートできるリポジトリサイズの推奨上限は20 GBです。

## 入手方法 {#availability}

コンテンツ転送ツールは、Software Distribution Portalからzipファイル(Content Transfer Tool v1.0.0)としてダウンロードできます。 パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。

>[!NOTE]
>Software Distribution PortalからContent Transfer Toolをダウンロードし [ます](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。

## コンテンツ転送ツールの実行 {#running-tool}

この節では、コンテンツ転送ツールを使用してコンテンツを AEM as a Cloud Service（オーサー／パブリッシュ）に移行する方法について説明します。

1. Adobe Experience Manager を選択し、ツール／**操作**／**コンテンツ転送**&#x200B;に移動します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. 「**移行セットを作成**」をクリックして、新しい移行セットを作成します。**コンテンツ移行セットの詳細**&#x200B;が表示されます。

   >[!NOTE]
   >コンテンツ転送画面には、既存の移行セットとその現在のステータスが表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. **コンテンツ移行セットの詳細**&#x200B;画面のフィールドに、以下のように値を入力します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **名前**：移行セットの名前を入力します。
      >[!NOTE]
      >移行セット名には特殊文字を使用できません。

   1. **クラウドサービス設定**：移行先の AEM as a Cloud Service オーサーの URL を入力します。

      >[!NOTE]
      >コンテンツ転送をおこなう際は、一度に最大 4 つの移行セットを作成し維持管理できます。
      >さらに、特定の環境（*ステージング*、*開発*、*実稼働*&#x200B;のいずれか）ごとに個別に移行セットを作成する必要があります。

   1. **アクセストークン**：アクセストークンを入力します。

      >[!NOTE]
      >オーサーインスタンスからアクセストークンを取得するには、`/libs/granite/migration/token.json` を参照します。アクセストークンは、クラウドサービスの作成者インスタンスから取得されます。

   1. **パラメーター**：移行セットを作成するには、次のパラメータを選択します。

      1. **バージョンを含める**：必要に応じて選択します。

      1. **含めるパス**：パスブラウザーを使用して、移行する必要があるパスを選択します。

         >[!IMPORTANT]
         >移行セットの作成時には、次のパスは制限されます。
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. **コンテンツ移行セットの詳細**&#x200B;画面のすべてのフィールドに値を入力したら、「**保存**」をクリックします。

1. 移行セットが&#x200B;*概要*&#x200B;ページに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   既存のすべての移行セットが、現在のステータスなどのステータス情報と共に&#x200B;*概要*&#x200B;ページに表示されます。

   * *赤い雲*&#x200B;は、抽出プロセスを完了できないことを示しています。
   * *緑の雲*&#x200B;は、抽出プロセスを完了できることを示しています。
   * *黄色のアイコン*&#x200B;は、その既存の移行セットが同じインスタンス内の他のユーザーによって作成されたことを示しています。

1. 概要ページで移行セットを選択し、「**プロパティ**」をクリックして、移行セットのプロパティを表示または編集します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### コンテンツ転送の抽出プロセス {#extraction-process}

コンテンツ転送ツールで移行セットを抽出するには、次の手順に従います。

1. *概要*&#x200B;ページで移行セットを選択し、「**抽出**」をクリックして抽出を開始します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. **移行セットの抽出**&#x200B;ダイアログボックスが表示されるので、「**抽出**」をクリックして抽出段階を完了します。

   >[!NOTE]
   >抽出段階では、ステージングコンテナを上書きするオプションがあります。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. 「**抽出**」フィールドに、進行中の抽出プロセスを表す&#x200B;**実行中**&#x200B;ステータスが表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   抽出が完了すると、移行セットのステータスが&#x200B;**完了**&#x200B;に更新され、*緑で塗りつぶされた*&#x200B;雲のアイコンが「**情報**」フィールドに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >更新されたステータスを表示するには、ページの表示を更新する必要があります。
   >抽出フェーズが開始されると、60秒後に書き込みロックが作成され、解放され *ます*。 したがって、抽出が停止した場合は、ロックが解除されるまで1分待ってから、抽出を再開する必要があります。

#### 追加抽出 {#top-up-extraction-process}

コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁におこなって、Cloud Service での運用を開始する前におこなう最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

抽出プロセスが完了したら、追加抽出方式を使用して差分コンテンツを転送できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、追加抽出の実行対象となる移行セットを選択します。

1. 「**抽出**」をクリックして、追加抽出を開始します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. **移行セットの抽出**&#x200B;ダイアログボックスが表示されます。

   >[!IMPORTANT]
   >「**抽出時にステージングコンテナを上書き**」オプションを無効にしてください。
   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### コンテンツ転送のインジェストプロセス {#ingestion-process}

コンテンツ転送ツールで移行セットを取り込むには、次の手順に従います。

1. *概要*&#x200B;ページで移行セットを選択し、「**取り込み**」をクリックしてインジェストを開始します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. **移行セットのインジェスト**&#x200B;ダイアログボックスが表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   デモのために、「**コンテンツをオーサーインスタンスに取り込み**」オプションは無効になっています。コンテンツをオーサーとパブリッシュに同時に取り込むことができます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   「**取り込み**」をクリックして、インジェスト段階を完了します。

1. インジェストが完了すると、「**オーサーインジェスト**」フィールドのステータスが&#x200B;**完了**&#x200B;に更新され、緑で塗りつぶされた雲のアイコンが「**情報**」フィールドに表示されます。
   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > 更新されたステータスを表示するには、ページの表示を更新する必要があります。

#### 追加インジェスト {#top-up-ingestion-process}

コンテンツ転送ツールには、*差分コンテンツ追加*&#x200B;をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁におこなって、Cloud Service での運用を開始する前におこなう最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

インジェストプロセスが完了したら、追加インジェスト方式を使用して差分コンテンツを転送できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、追加インジェストの実行対象となる移行セットを選択します。

1. 「**取り込み**」をクリックして、追加インジェストを開始します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. **移行セットのインジェスト**&#x200B;ダイアログボックスが表示されます。

   >[!NOTE]
   >前回のインジェストアクティビティで追加された既存のコンテンツを削除しないように、「*ワイプ*」オプションを無効にしてください。
   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### 移行セットのログの表示 {#viewing-logs-migration-set}

既存の移行セットのログを&#x200B;*概要*&#x200B;ページから表示できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、ログを表示する移行セットを選択し、アクションバーの「**ログを表示**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. **ログ**&#x200B;ダイアログボックスが表示されます。「**抽出ログ**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
または、

   *概要*&#x200B;画面から移行セットのログを直接表示することもできます。移行セットを選択し、「**抽出**」フィールド内のステータスをクリックします。下図の場合は、「**完了**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. ユーザーインターフェイスを使用せずにログの末尾を表示するには、ソースAEM環境にSSHで接続し、末尾を表示 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`します。

### 移行セットの削除 {#deleting-migration-set}

*概要*ページで移行セットを削除できます。
それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、削除する移行セットを選択し、アクションバーの「**削除**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. **移行セットを削除**&#x200B;ダイアログボックスの「**削除**」をクリックして、削除を確定します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## トラブルシューティング {#troubleshooting}

### 不明な BLOB ID {#missing-blobs}

以下に示すように、不明な BLOB ID が報告された場合は、既存のリポジトリで整合性チェックを実行し、不明な BLOB を復元する必要があります。
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

以下のコマンドを実行します。

>[!NOTE]
> `--verbose` フラグが必要なのは、BLOB の参照元ノードのパスを報告するためです。

**AEM 6.5（Oak 1.8 以前）のリポジトリの場合**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Oak 1.10 以降のリポジトリの場合**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

詳しくは、[Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)（Oak 実行可能 Jar）を参照してください。

整合性チェックのために上記で指定された *OUT_DIR* に作成されたファイルを調べて、不明なバイナリのパスや必要なアクション（バックアップからの復元、パスの削除、インデックスの再作成など）を確認できます。

### UI の動作 {#ui-behavior}

コンテンツ転送ツールのユーザーインターフェイス（UI）に次のような動作が見られることがあります。

* ユーザーが、オーサー URL（開発／ステージング／実稼動）の移行セットを作成し、抽出とインジェストを正常に実行します。

* 次に、同じオーサー URL の新しい移行セットを作成し、その新しい移行セットに対して抽出とインジェストを実行します。UI の表示では、最初の移行セットのインジェスト状態が&#x200B;**失敗**&#x200B;に変わり、使用可能なログがないことになります。

* それでも、最初の移行セットのインジェストが失敗したわけではありません。この動作が見られるのは、新しいインジェストジョブが開始されると、前回のインジェストジョブが削除されるからです。したがって、最初の移行セットのステータス変更は無視してください。

* コンテンツ転送ツールUIのアイコンが、このガイドに示すスクリーンショットとは異なるように表示される場合や、ソースAEMインスタンスのバージョンによっては表示されない場合があります。


