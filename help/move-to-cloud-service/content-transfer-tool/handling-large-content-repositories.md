---
title: 大きなコンテンツリポジトリの処理
description: この節では、大規模なコンテンツリポジトリの処理について説明します
source-git-commit: c19878b41970f4cd34083395ab11cf82c1db667e
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---


# 大きなコンテンツリポジトリの処理 {#handling-large-content-repositories}

## 概要 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="大きなコンテンツリポジトリの処理"
>abstract="コンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮して、コンテンツをCloud ServiceとしてAEMに移動するために、CTTはオプションのプリコピー手順としてAzCopyを利用できます。 この前段階が設定されたら、抽出段階で、AzCopyはAmazon S3またはAzure Blob Storageから移行セットBLOBストアにBLOBをコピーします。 取り込み段階では、AzCopyは、移行セットBLOBストアから宛先AEMにCloud ServiceBLOBストアとしてBLOBをコピーします。"
>additional-url="https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10" text="AzCopyの概要"

コンテンツ転送ツール(CTT)で大量のBLOBをコピーするには、複数日かかる場合があります。
コンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮して、コンテンツをCloud ServiceとしてAEMに移動するために、CTTでは、オプションのプリコピー手順として[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)を利用できます。 このプリコピー手順は、ソースAEMインスタンスがAmazon S3またはAzure Blob Storageデータストアを使用するように設定されている場合に使用できます。  この前段階が設定されたら、抽出段階で、AzCopyはAmazon S3またはAzure Blob Storageから移行セットBLOBストアにBLOBをコピーします。 取り込み段階では、AzCopyは、移行セットBLOBストアから宛先AEMにCloud ServiceBLOBストアとしてBLOBをコピーします。

>[!NOTE]
> この機能は、CTT 1.5.4リリースで導入されました。

## 始める前に考慮すべき重要事項 {#important-considerations}

開始する前に、次の重要事項を考慮してください。

* ソースAEMのバージョンは6.3 ～ 6.5である必要があります
* ソースAEMデータストアがAmazon S3またはAzure Blob Storageを使用するように設定されている。 詳しくは、[AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en)でのノードストアとデータストアの設定を参照してください。
* 抽出時にデータストア全体がコピーされます。 Amazon S3とAzure Blob Storageの両方からのデータ転送に関連するコストがあるので、転送コストはストレージコンテナ内のデータの総量(AEMで参照されているかどうかに関係なく)に対して相対的になります。 詳しくは、[Amazon S3](https://aws.amazon.com/s3/pricing/)および[Azure Blob Storage](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)を参照してください。
* 各移行セットはデータストア全体をコピーするので、1つの移行セットのみを使用する必要があります。
* ソースAEMインスタンスを実行するインスタンス（またはVM）に[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)をインストールするには、アクセス権が必要です。
* ソースAmazon S3バケットのアクセスキーと秘密鍵のペア、またはソースAzure Blob StorageコンテナのSAS URIが必要です（読み取り専用アクセスで問題ありません）。
* データストアのガベージコレクションは、ソース上で過去7日以内に実行されました。 詳しくは、[データストアのガベージコレクション](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection)を参照してください。
* ソース・インスタンス上のデータの大部分が移行に含まれます。

## AzCopyを事前コピーステップとして使用する設定 {#setting-up-pre-copy-step}

この節では、コンテンツ転送ツールを使用してAzCopyを事前コピー手順として使用し、コンテンツをCloud ServiceとしてAEMに移行する方法を説明します。

### 0.データストア内のすべてのコンテンツの合計サイズを決定 {#determine-total-size}

#### Azure Blobストレージデータストア {#azure-blob-storage}

Azureポータルのコンテナプロパティページで、「**サイズを計算**」ボタンを使用して、コンテナ内のすべてのコンテンツのサイズを決定します。 次に例を示します。

![画像](/help/move-to-cloud-service/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3 データストア {#amazon-data}

コンテナの「指標」タブを使用して、コンテナ内のすべてのコンテンツのサイズを指定できます。 次に例を示します。


![画像](/help/move-to-cloud-service/content-transfer-tool/assets/amazon-s3-data-store.png)

### 1. AzCopyをインストールする {#install-azcopy}

[](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) AzCopyは、この機能を有効にするためにソースインスタンス上で使用できる必要がある、Microsoftが提供するコマンドラインツールです。

要するに、[AzCopyのドキュメントページ](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)からLinux x86-64バイナリをダウンロードし、/usr/binのような場所にアンタールしたいと思うでしょう。 後の手順でバイナリへの完全パスが必要になるので、バイナリを配置した場所をメモしておきます。

### 2. AzCopyサポートを備えたコンテンツ転送ツール(CTT)リリースをインストールする {#install-ctt-azcopy-support}

AzCopyのサポートは、CTT 1.5.4リリースに含まれています。 CTTの最新リリースは、[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aemcloud.html)ポータルからダウンロードできます。

### 3. azcopy.configファイルを設定する {#configure-azcopy-config-file}

ソースAEMインスタンスのcrx-quickstart/cloud-migrationで、 azcopy.configという新しいファイルを作成します。

この設定ファイルの内容は、ソースAEMインスタンスがAzureとAmazon S3のどちらのデータストアを使用しているかによって異なります。

#### Azure Blobストレージデータストア {#azure-blob-storage-data}

azcopy.configファイルには、次のプロパティを含める必要があります（インスタンスに対して正しいazCopyPathとazureSasを使用するようにしてください）。

>[!NOTE]
>
> BLOBストレージコンテナへの書き込みアクセスを許可しない場合は、読み取りおよびリストの権限のみを持つ新しいSAS URIを生成できます。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3 データストア {#amazon-sdata-store}

azcopy.configファイルには、次のプロパティを含める必要があります（インスタンスに対して正しい値を使用してください）。

>[!NOTE]
>
> インスタンスでIAMロールを使用してAEMがS3にアクセスできるようにする場合は、S3バケットに対してListBucketとGetObjectのアクションが有効なポリシーとユーザーを作成する必要があります。 設定が完了したら、このユーザーのアクセスキーと秘密鍵を使用します。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

### 4. AzCopyを使用した抽出 {#extracting-azcopy}

上記の設定ファイルを配置すると、AzCopyのプリコピーフェーズは、後続の抽出のすべての一部として実行されます。 このファイルの実行を防ぐには、このファイルの名前を変更するか、削除します。

1. CTT UIから抽出を開始します。 詳しくは、 [コンテンツ転送ツールの実行](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)および[抽出プロセス](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process)を参照してください。
1. 抽出ログに次の行が印刷されていることを確認します。

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

おめでとうございます。このログエントリは、設定が有効と見なされ、AzCopyは現在、ソースコンテナから移行コンテナにすべてのBLOBをコピーしていることを意味します。

AzCopyのログエントリは抽出ログに表示され、先頭にc.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy pre-copy]が付きます。

>[!CAUTION]
>
> 抽出の最初の数分は、問題の兆候について、抽出ログを詳細に確認します。 例えば、ソースAzureコンテナが見つからない場合にログに記録される内容を次に示します。


```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

AzCopyに問題が発生した場合、抽出は即座に失敗し、抽出ログには失敗に関する詳細が含まれます。

エラーの前にコピーされたBLOBは、後続の実行時にAzCopyによって自動的にスキップされ、再度コピーする必要はありません。

### 5. AzCopyでの取り込み {#ingesting-azcopy}

コンテンツ転送ツール1.5.4のリリースに伴い、AzCopyのサポートがオーサーインジェストに追加されました。

>[!NOTE]
>最初にオーサーの取り込みを単独で実行することをお勧めします。 これにより、後で実行する際に、パブリッシュの取り込みが高速化されます。

取り込み中にAzCopyを利用するには、少なくともバージョン2021.6.5561のCloud ServiceバージョンとしてAEMを使用する必要があります。

CTT UIからのオーサーの取り込みを開始します。 詳しくは、 [インジェストプロセス](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process)を参照してください。
AzCopyのログエントリがインジェストログに表示されます。 次のようになります。

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
INFO: azcopy: A newer version 10.11.0 is available to download
 
 
Job 419d98da-fc05-2a45-70cc-797fee632031 has started
Log file is located at: /root/.azcopy/419d98da-fc05-2a45-70cc-797fee632031.log
 
 
0.0 %, 0 Done, 0 Failed, 886 Pending, 0 Skipped, 886 Total,
 
 
Job 419d98da-fc05-2a45-70cc-797fee632031 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 886
Number of Folder Property Transfers: 0
Total Number of Transfers: 886
Number of Transfers Completed: 17
Number of Transfers Failed: 0
Number of Transfers Skipped: 869
TotalBytesTransferred: 248350
Final Job Status: CompletedWithSkipped
 
*************** Completed AzCopy pre-copy phase ***************
```
