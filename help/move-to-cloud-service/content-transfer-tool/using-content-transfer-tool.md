---
title: コンテンツ転送ツールの使用
description: コンテンツ転送ツールの使用
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 57%

---

# コンテンツ転送ツールの使用 {#using-content-transfer-tool}

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
