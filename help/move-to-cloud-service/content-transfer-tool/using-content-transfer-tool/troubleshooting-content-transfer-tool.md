---
title: コンテンツ転送ツールのトラブルシューティング
description: コンテンツ転送ツールのトラブルシューティング
source-git-commit: 27e68cd282414da4cc23c3ba276b0fb3c330d49c
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 93%

---


# コンテンツ転送ツールのトラブルシューティング {#troubleshoot-content-transfer-tool}


## 不明な BLOB ID {#missing-blobs}

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


## UI の動作 {#ui-behavior}

コンテンツ転送ツールのユーザーインターフェイス（UI）に次のような動作が見られることがあります。

* コンテンツ転送ツール UI のアイコンが、このガイドに示すスクリーンショットとは異なって表示される場合や、ソース AEM インスタンスのバージョンによっては表示されない場合があります。
