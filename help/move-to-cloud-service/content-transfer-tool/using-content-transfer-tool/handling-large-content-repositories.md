---
title: 大きなコンテンツリポジトリの処理
description: この節では、大きなコンテンツリポジトリの処理について説明します
exl-id: 2eca7fa6-fb34-4b08-b3ec-4e9211e94275
source-git-commit: bdcc5cfc229fd5b1fd1f70e37c7231ed3f727e72
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 1%

---

# 大きなコンテンツリポジトリの処理 {#handling-large-content-repositories}

## 概要 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="大きなコンテンツリポジトリの処理"
>abstract="コンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮してコンテンツをAEM as a Cloud Serviceに移動するため、CTT は AzCopy をオプションの事前コピー手順として利用できます。 この前段階が設定されると、抽出段階で、AzCopy はAmazon S3 または Azure Blob Storage から移行セット BLOB ストアに BLOB をコピーします。 取り込み段階では、AzCopy は、移行セット BLOB ストアから宛先AEM as a Cloud Service BLOB ストアに BLOB をコピーします。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step" text="AzCopy を事前コピーステップとして使用する"

コンテンツ転送ツール (CTT) で大量の BLOB をコピーするには、複数日かかる場合があります。
コンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮してコンテンツをAEM as a Cloud Serviceに移動するために、CTT はオプションのプリコピー手順として [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) を利用できます。 この事前コピー手順は、ソースAEMインスタンスがAmazon S3 または Azure BLOB ストレージデータストアを使用するように設定されている場合に使用できます。  この前段階が設定されると、抽出段階で、AzCopy はAmazon S3 または Azure Blob Storage から移行セット BLOB ストアに BLOB をコピーします。 取り込み段階では、AzCopy は、移行セット BLOB ストアから宛先AEM as a Cloud Service BLOB ストアに BLOB をコピーします。

>[!NOTE]
> この機能は CTT 1.5.4 リリースで導入されました。

## 開始前の重要な考慮事項 {#important-considerations}

開始する前に、次の重要事項を考慮してください。

* ソースAEMのバージョンは 6.3 ～ 6.5 である必要があります
* ソースAEMデータストアがAmazon S3 または Azure Blob Storage を使用するように設定されている。 詳しくは、[AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en) でのノードストアとデータストアの設定を参照してください。
* 抽出時に、データストア全体がコピーされます。 Amazon S3 と Azure Blob Storage の両方からのデータ転送に関連するコストがあるので、転送コストはストレージコンテナ内のデータの総量 (AEMで参照されているかどうかに関わらず ) に対して相対的になります。 詳しくは、[Amazon S3](https://aws.amazon.com/s3/pricing/) および [Azure Blob Storage](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) を参照してください。
* 各移行セットはデータストア全体をコピーするので、1 つの移行セットのみを使用する必要があります。
* ソースAEMインスタンスを実行しているインスタンス（または VM）に [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) をインストールするには、アクセスする必要があります。
* ソースAmazon S3 バケットのアクセスキーと秘密鍵のペア、またはソース Azure Blob Storage コンテナの SAS URI が必要です（読み取り専用アクセスが正常です）。
* データストアのガベージコレクションは、ソース上で過去 7 日以内に実行されました。 詳しくは、[ データストアのガベージコレクション ](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection) を参照してください。
* 移行元インスタンスのデータの大部分は、移行に含まれます。

## AzCopy をコピー前のステップとして使用する設定 {#setting-up-pre-copy-step}

このセクションでは、コンテンツ転送ツールを使用して AzCopy を事前コピー手順として使用し、コンテンツをAEM as a Cloud Serviceに移行する方法を説明します。

### 0.データストア内のすべてのコンテンツの合計サイズを決定 {#determine-total-size}

#### Azure Blob ストレージデータストア {#azure-blob-storage}

Azure ポータルのコンテナプロパティページで、「**サイズを計算**」ボタンを使用して、コンテナ内のすべてのコンテンツのサイズを決定します。 例えば、次の操作が可能です。

![画像](/help/move-to-cloud-service/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3 データストア {#amazon-data}

コンテナの「指標」タブを使用して、コンテナ内のすべてのコンテンツのサイズを指定できます。 例えば、次の操作が可能です。


![画像](/help/move-to-cloud-service/content-transfer-tool/assets/amazon-s3-data-store.png)

### 1. AzCopy をインストールする {#install-azcopy}

[](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) AzCopy は、Microsoftが提供するコマンドラインツールで、この機能を有効にするには、ソースインスタンスで使用できる必要があります。

要するに、[AzCopy docs ページ ](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) から Linux x86-64 バイナリをダウンロードし、/usr/bin のような場所にアンタールしたいと思うでしょう。 後の手順でバイナリへの完全パスが必要になるので、バイナリの配置場所をメモしておきます。

### 2. AzCopy サポートを備えたコンテンツ転送ツール (CTT) リリースをインストールする {#install-ctt-azcopy-support}

AzCopy のサポートは、CTT 1.5.4 リリースに含まれています。 CTT の最新リリースは、[ ソフトウェア配布 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) ポータルからダウンロードできます。

### 3. azcopy.config ファイルを設定する {#configure-azcopy-config-file}

ソースAEMインスタンスの crx-quickstart/cloud-migration で、 azcopy.config という新しいファイルを作成します。

この設定ファイルの内容は、ソースAEMインスタンスが Azure とAmazon S3 のどちらのデータストアを使用しているかによって異なります。

#### Azure Blob ストレージデータストア {#azure-blob-storage-data}

azcopy.config ファイルには、次のプロパティを含める必要があります（インスタンスに対して正しい azCopyPath と azureSas を使用してください）。

>[!NOTE]
>
> BLOB ストレージコンテナへの書き込みアクセスを許可しない場合は、読み取りとリストのアクセス権のみを持つ新しい SAS URI を生成できます。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3 データストア {#amazon-sdata-store}

azcopy.config ファイルには、次のプロパティを含める必要があります（インスタンスに対して正しい値を使用してください）。

>[!NOTE]
>
> インスタンスで IAM ロールを使用してAEMが S3 にアクセスできるようにする場合は、S3 バケットに対して ListBucket および GetObject アクションを有効にしたポリシーおよびユーザーを作成する必要があります。 設定が完了したら、このユーザーのアクセスキーと秘密鍵を使用します。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

### 4. AzCopy を使用した抽出 {#extracting-azcopy}

上記の構成ファイルを配置すると、AzCopy の事前コピーフェーズは、後続の抽出のすべての一部として実行されます。 このファイルの実行を防ぐには、このファイルの名前を変更するか、削除します。

1. CTT UI からの抽出を開始します。 詳しくは、[ コンテンツ転送ツールの実行 ](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool) および [ 抽出プロセス ](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) を参照してください。
1. 抽出ログに次の行が印刷されていることを確認します。

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

おめでとうございます。このログエントリは、設定が有効と見なされ、現在 AzCopy がソースコンテナから移行コンテナにすべての BLOB をコピーしていることを意味します。

AzCopy のログエントリは抽出ログに表示され、先頭に c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy pre-copy] が付きます

>[!CAUTION]
>
> 抽出の最初の数分間は、問題の兆候について、抽出ログを詳細に確認します。 例えば、ソース Azure コンテナが見つからない場合にログに記録される内容を次に示します。

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

AzCopy に問題が発生した場合、抽出は直ちに失敗し、抽出ログには失敗の詳細が記録されます。

エラーの前にコピーされた BLOB は、後続の実行時に AzCopy によって自動的にスキップされ、再度コピーする必要はありません。

### 5. AzCopy での取り込み {#ingesting-azcopy}

コンテンツ転送ツール 1.5.4 のリリースに伴い、AzCopy のサポートがオーサーの取り込みに追加されました。

>[!NOTE]
>最初にオーサーの取り込みを単独で実行することをお勧めします。 これにより、後で実行した場合に、パブリッシュの取り込みが高速化されます。

取り込み中に AzCopy を利用するには、少なくともバージョン 2021.6.5561 のAEMas a Cloud Serviceバージョンを使用する必要があります。

CTT UI からのオーサーの取り込みを開始します。 詳しくは、[ インジェストプロセス ](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) を参照してください。
AzCopy のログエントリがインジェストログに表示されます。 次のようになります。

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
