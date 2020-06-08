---
title: コンテンツ転送ツールの使用
description: コンテンツ転送ツールの使用
translation-type: tm+mt
source-git-commit: 7a0fa12198c69791caf7e44bfbfe7d71e389a984
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 3%

---


# コンテンツ転送ツールの使用 {#using-content-transfer-tool}

## コンテンツ転送ツールを使用する際の重要な考慮事項 {#pre-reqs}

次の節に従って、コンテンツ転送ツールの実行時の重要な考慮事項を理解してください。

* コンテンツ転送ツールの最小システム要件は、AEM 6.3以降およびJAVA 8です。 AEMより前のバージョンを使用している場合は、コンテンツ転送ツールを使用するには、コンテンツリポジトリをAEM 6.5にアップグレードする必要があります。

* Sandbox *環境を使用している場合は*、環境が2020年5月29日以降のリリースにアップグレードされていることを確認してください。 実 *稼働環境を使用している場合*、実稼働環境は自動的に更新されます。

* コンテンツ転送ツールを使用するには、ソースインスタンスの管理者ユーザーで、コンテンツの転送先のクラウドサービスインスタンスの管理グループに属している必要があります。 権限のないユーザーは、コンテンツ転送ツールを使用するアクセストークンを取得できません。

* 抽出段階では、コンテンツ転送ツールはアクティブなAEMソースインスタンスで実行されます。

* 作成者の *取り込みフェーズ* (Ingestion Phase)では、作成者のデプロイメント全体が縮小されます。 つまり、作成者のAEMは、取り込みプロセス全体で使用できなくなります。

## 利用可能場所 {#availability}

コンテンツ転送ツールは、ソフトウェア配布ポータルからzipファイルとしてダウンロードできます。 Package Managerを使用して、ソースAdobe Experience Manager(AEM)インスタンスにパッケージをインストールできます。

>[!NOTE]
>Adobe Experience Cloud [からContent Transfer Toolをダウンロードします](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。

## コンテンツ転送ツールの実行 {#running-tool}

この節では、コンテンツ転送ツールを使用して、コンテンツをクラウドサービス（作成者/発行）としてAEMに移行する方法について説明します。

1. Adobe Experience Managerを選択し、ツール/ **操作** / **コンテンツ転送**&#x200B;に移動します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. [移行セットの **作成** ]をクリックして、新しい移行セットを作成します。 「 **コンテンツ移行セットの詳細** 」が表示されます。

   >[!NOTE]
   >この画面で、既存の移行セットを現在のステータスで表示します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. 以下に示すように、「 **コンテンツ移行の詳細設定** 」画面のフィールドに値を入力します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **名前**: 移行セットの名前を入力します。
      >[!NOTE]
      >移行セット名には特殊文字を使用できません。

   1. **クラウドサービスの設定**: リンク先のAEMを「クラウドサービス作成者のURL」として入力します。

      >[!NOTE]
      >コンテンツ転送アクティビティ中に、一度に最大4つの移行セットを作成し、維持できます。
      >また、特定の環境( *Stage*、 *Development*、 *Production*)ごとに個別に移行を作成する必要があります。

   1. **アクセストークン**: アクセストークンを入力します。

      >[!NOTE]
      >に移動して、オーサーインスタンスからアクセストークンを取得でき `/libs/granite/migration/token.json`ます。 アクセストークンは、クラウドサービスの作成者インスタンスから取得されます。

   1. **パラメータ**: 次のパラメータを選択して、移行セットを作成します。

      1. **Include Version**: 必要に応じて選択します。

      1. **含めるパス**: パスブラウザーを使用して、移行するパスを選択します。

         >[!IMPORTANT]
         >移行セットの作成時に、次のパスが制限されます。
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. 「 **保存** 」をクリックすると、 **コンテンツ移行セットの詳細** 」画面のすべてのフィールドに値が入力されます。

1. 移行セットは、 *概要* ページで表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   この画面に表示される既存の移行セットはすべて、現在のステータスとステータス情報と共に *概要* ページに表示されます。

   * *赤い雲は* 、抽出プロセスを完了できないことを示します。
   * *緑の雲は* 、抽出プロセスを完了できることを示します。
   * *黄色のアイコンは* 、既存の移行セットを作成せず、特定の移行セットが同じインスタンス内の他のユーザーによって作成されたことを示します。

1. 「概要」ページから移行セットを選択し、「 **プロパティ** 」をクリックして表示を行うか、移行セットのプロパティを編集します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### コンテンツ転送の抽出プロセス {#extraction-process}

次の手順に従って、コンテンツ転送ツールから移行セットを抽出します。

1. [ *概要* ]ページから移行セットを選択し、[開始抽出 **の抽出** ]をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. [ **マイグレーションセット抽出** ]ダイアログボックスが表示され、[ **抽出** ]をクリックして抽出段階を完了します。

   >[!NOTE]
   >抽出段階でステージングコンテナを上書きするオプションがあります。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. 「 **抽出** 」フィールドに、進行中の抽出プロセスの **** 実行中ステータスが表示されるようになりました。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   抽出が完了すると、移行セットのステータスが **FINISHED** に更新され、 *INFO* フィールドの下に緑色の **** 塗りつぶしのアイコンが表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >更新されたステータスを表示するには、ページを更新する必要があります。
   >抽出フェーズが開始されると、60秒後に書き込みロックが作成され、解放され *ます*。 したがって、抽出が停止した場合は、ロックが解除されるまで1分待ってから、抽出を再開する必要があります。

#### トップアップ抽出 {#top-up-extraction-process}

コンテンツ転送ツールには、差分コンテンツのトップアップをサポートする機能があり、以前のコンテンツ転送アクティビティ以降に行われた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後、Cloud Serviceでの運用を開始する前に、頻繁に差分コンテンツのトップアップを行い、最終的な差分コンテンツ転送のためのコンテンツのフリーズ期間を短縮することをお勧めします。

抽出プロセスが完了すると、トップアップ抽出方式を使用して差分コンテンツを転送できます。 その場合は、次の手順に従います。

1. 「 *概要* 」ページに移動し、トップアップ抽出を実行する移行セットを選択します。

1. 「 **抽出** 」をクリックして、トップアップ抽出を開始します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. [ **マイグレーションセット抽出** ]ダイアログボックスが表示されます。

   >[!IMPORTANT]
   >「抽出中にステージングコンテナを **上書きする** 」オプションを無効にする必要があります。
   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### コンテンツ転送でのインジェストプロセス {#ingestion-process}

次の手順に従って、コンテンツ転送ツールから移行セットを取り込みます。

1. [ *概要* ]ページから移行セットを選択し、[開始抽出に **取り込む** ]をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. [ **マイグレーションセットの取り込み** ]ダイアログボックスが表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   デモ目的では、「コンテンツをオーサーインスタンスに **取り込む** 」オプションは無効になっています。 コンテンツを「作成者」に取り込むと同時に、「公開」に取り込むことができます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   [ **インジェスト** ]をクリックして、インジェストフェーズを完了します。

1. 取り込みが完了すると、「 **作成者取り込み** 」フィールドのステータスが **「完了」に更新され、** 情報 ****の下に緑色の塗りつぶしアイコンが表示されます。
   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > 更新されたステータスを表示するには、ページを更新する必要があります。

#### トップアップインジェスト {#top-up-ingestion-process}

コンテンツ転送ツールには、前のコンテンツ転送アクティビティ以降に行われた変更のみを転送できる、差分コンテンツ *のトップアップ* をサポートする機能があります。

>[!NOTE]
>最初のコンテンツ転送の後、Cloud Serviceでの運用を開始する前に、頻繁に差分コンテンツのトップアップを行い、最終的な差分コンテンツ転送のためのコンテンツのフリーズ期間を短縮することをお勧めします。

取り込み処理が完了したら、トップアップ取り込み方法を使用して、デルタコンテンツを使用できます。 その場合は、次の手順に従います。

1. 「 *概要* 」ページに移動し、トップアップインジェストを実行する移行セットを選択します。

1. 「 **取り込み** 」をクリックして、トップアップ抽出を開始します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. [ **移行セットの取り込み** ]ダイアログボックスが表示されます。

   >[!NOTE]
   >既存のコンテンツを以前のインジェストアクティビティから削除しないように、 *ワイプ* (Wipe)オプションを無効にする必要があります。
   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### 移行セットのログの表示 {#viewing-logs-migration-set}

既存の移行セットの表示ログは、 *概要* ページから実行できます。
その場合は、次の手順に従います。

1. 「 *概要* 」ページに移動し、削除する移行セットを選択し、アクションバーの「 **表示ログ** 」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. [ **ログ** ]ダイアログボックスが表示されます。 「 **抽出ログ** 」をクリックして、新しいタブでログを表示します。

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)Or、

   [ *概要* ]画面から、移行セットの表示ログを作成することもできます。 移行セットを選択し、「 **抽出** 」フィールドの下のステータスをクリックします。 この場合、「 **FINISHED** 」をクリックして表示ログを新しいタブで開きます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

### 移行セットの削除 {#deleting-migration-set}

移行セットは *概要* ページから削除できます。
その場合は、次の手順に従います。

1. 「 *概要* 」ページに移動し、削除する移行セットを選択し、アクションバーの「 **削除** 」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. 「 **Delete** from **Delete Migration Set** 」ダイアログ・ボックスをクリックして削除を確定します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## トラブルシューティング {#troubleshooting}

### BLOB IDがありません {#missing-blobs}

以下に示すように、欠落したBLOB IDが報告された場合は、既存のリポジトリで整合性チェックを実行し、欠落したBLOBを復元する必要があります。
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

次のコマンドが実行されます

>[!NOTE]
> `--verbose` フラグは、blobが参照されているノードのパスを報告するために必要です。

**リポジトリ用AEM 6.5 （Oak 1.8以前）**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Oakが1.10を超えるリポジトリの場合**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

詳細は、 [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) を参照してください。

上記の *OUT_DIR* （整合性を確保するために指定したファイル）で作成したファイルは、バイナリが見つからないパスや、バックアップからの復元、パスの削除、再インデックスなど、適切な操作をチェックできます。

### UIの動作 {#ui-behavior}

ユーザーの場合、コンテンツ転送ツールのユーザーインターフェイス(UI)に次のような動作の変更が表示されます。

* ユーザーは、作成者URL（開発/ステージ/実稼動）の移行セットを作成し、抽出と取り込みを正常に実行します。

* 次に、同じ作成者URLに対して新しい移行セットを作成し、新しい移行セットに対して抽出と取り込みを実行します。 UIに、最初の移行セットの取り込み状態が **FAILEDに変更され** 、ログが使用できないことが示されます。

* これは、最初の移行セットの取り込みが失敗したことを意味するわけではありません。 この動作は、新しい取り込みジョブが開始されると、以前の取り込みジョブが削除されるために表示されます。 したがって、最初の移行セットの変更ステータスは無視する必要があります。

* コンテンツ転送ツールUIのアイコンが、このガイドに示すスクリーンショットとは異なるように表示される場合や、ソースAEMインスタンスのバージョンによっては表示されない場合があります。


