---
title: 大規模なコンテンツリポジトリーの処理
description: この節では、大規模なコンテンツリポジトリーの処理について説明します
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 66%

---

# 大規模なコンテンツリポジトリーの処理 {#handling-large-content-repositories}

## 概要 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="大規模なコンテンツリポジトリーの処理"
>abstract="コンテンツを AEM as a Cloud Service に移動するコンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮するために、CTT は、オプションのコピー前手順として AzCopy を活用できます。この前段階が設定されたら、AzCopy は、抽出段階で Amazon S3 または Azure Blob Storage から移行セット BLOB ストアに BLOB をコピーします。取り込み段階では、AzCopy は、移行セットの BLOB ストアから宛先の AEM as a Cloud Service BLOB ストアに BLOB をコピーします。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja#setting-up-pre-copy-step" text="AzCopy をコピー前手順として使用する"

コンテンツ転送ツール（CTT）で大量の BLOB をコピーするには、数日かかる場合があります。
コンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮して、コンテンツを AEM as a Cloud Service に移動するために、CTT では、オプションのコピー前手順として [AzCopy](https://docs.microsoft.com/ja-jp/azure/storage/common/storage-use-azcopy-v10) を活用できます。このプリコピー手順は、ソースAEMインスタンスがAmazon S3、Azure Blob ストレージデータストア、またはファイルデータストアを使用するように設定されている場合に使用できます。 この前の手順が設定されると、抽出段階で、AzCopy はAmazon S3、Azure Blob ストレージ、またはファイルデータストアから移行セット blob ストアに BLOB をコピーします。 取り込み段階では、AzCopy は、移行セットの BLOB ストアから宛先の AEM as a Cloud Service BLOB ストアに BLOB をコピーします。

>[!NOTE]
> この機能は、CTT 1.5.4 リリースで導入されました。

## 開始する前に考慮すべき重要事項 {#important-considerations}

開始する前に、次の重要事項を確認してください。

* ソース AEM のバージョンは 6.3 ～ 6.5 である必要がある。

* ソース AEM のデータストアが Amazon S3 または Azure Blob Storage を使用するように設定されている。詳しくは、[AEM 6 でのノードストアとデータストアの設定を参照してください](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=ja)。

* 各移行セットはデータストア全体をコピーするので、1 つの移行セットのみを使用する必要がある。

* ソース AEM インスタンスを実行するインスタンス（または VM）に [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) をインストールするには、アクセス権が必要である。

* データストアのガベージコレクションが、ソース上で過去 7 日以内に実行されている。詳しくは、[データストアのガベージコレクション](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=ja#data-store-garbage-collection)を参照してください。


### ソースAEMインスタンスがAmazon S3 または Azure Blob ストレージデータストアを使用するように設定されている場合の追加の考慮事項 {#additional-considerations-amazons3-azure}

* Amazon S3 と Azure Blob Storage の両方からのデータ転送に関連するコストがあるので、転送コストはストレージコンテナ内のデータの総量（AEM で参照されているかどうかに関係なく）に対して相対的になります。詳しくは、[Amazon S3](https://aws.amazon.com/s3/pricing/) および [Azure Blob Storage](https://azure.microsoft.com/ja-jp/pricing/details/bandwidth/) を参照してください。

* ソース Amazon S3 バケットのアクセスキーと秘密鍵のペア、またはソース Azure Blob Storage コンテナの SAS URI が必要である（読み取り専用アクセスで問題ありません）。

### ソースAEMインスタンスがファイルデータストアを使用するように設定されている場合のその他の考慮事項 {#additional-considerations-aem-instance-filedatastore}

* ローカルシステムの空き領域は、ソースデータストアの1/256サイズよりも厳密に大きい必要があります。 例えば、データストアのサイズが 3 TB の場合、11.72 GB を超える空き領域が `crx-quickstart/cloud-migration` AzCopy が動作するソース上のフォルダ。 少なくとも、ソースシステムの空き容量は 1 GB である必要があります。 空き容量は `df -h` コマンドは Linux インスタンスで、dir コマンドは Windows インスタンスで実行します。

* AzCopy を有効にして抽出を実行するたびに、ファイルデータストア全体が統合され、クラウド移行コンテナにコピーされます。 移行セットがデータストアのサイズより大幅に小さい場合、AzCopy 抽出は最適なアプローチではありません。

* AzCopy を使用してデータストアをコピーした後は、差分抽出または追加抽出で無効にします。

## AzCopy をコピー前手順として使用する設定 {#setting-up-pre-copy-step}

この節では、コンテンツ転送ツールを使用して AzCopy をコピー前手順として使用し、コンテンツを AEM as a Cloud Service に移行する方法を説明します。

### 0. データストア内のすべてのコンテンツの合計サイズを算出する {#determine-total-size}

次の 2 つの理由により、データストアの合計サイズを決定することが重要です。

* ソースAEMがファイルデータストアを使用するように設定されている場合、ローカルシステムの空き領域は、ソースデータストアの1/256サイズを厳密に超えている必要があります。

* データストアの合計サイズを把握することで、抽出と取り込みにかかる時間を見積もるのに役立ちます。 以下を使用： [コンテンツ転送ツール計算ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en#content-transfer) in [Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/introduction-cam/overview-cam.html?lang=en) をクリックして、抽出および取り込み時間を予測します。

#### Azure Blob ストレージデータストア {#azure-blob-storage}

Azure ポータルのコンテナプロパティページで、「**サイズを計算**」ボタンを使用して、コンテナ内のすべてのコンテンツのサイズを算出します。次に例を示します。

![画像](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3 データストア {#amazon-data}

コンテナの「指標」タブを使用して、コンテナ内のすべてのコンテンツのサイズを算出できます。次に例を示します。


![画像](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### ファイルデータストア {#file-data-store-determine-size}

* mac の場合、UNIX システムの場合、データストアディレクトリで du コマンドを実行してサイズを取得します。
   `du -sh [path to datastore on the instance]`。例えば、データストアが `/mnt/author/crx-quickstart/repository/datastore`を指定しない場合、次のコマンドを使用してサイズを取得できます。 `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* Windows の場合、データストアディレクトリの dir コマンドを使用してサイズを取得します。
   `dir /a/s [location of datastore]`

### 1. AzCopy をインストールする {#install-azcopy}

[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) は、Microsoft が提供するコマンドラインツールであり、この機能を有効にするには、ソースインスタンス上で利用可能である必要があります。

つまり、[AzCopy のドキュメントページ](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)から Linux x86-64 バイナリをダウンロードし、/usr/bin のような場所に un-tar する必要があります。

>[!IMPORTANT]
>後の手順でバイナリへのフルパスが必要になるので、バイナリを配置した場所をメモしておきます。

### 2. AzCopy をサポートするコンテンツ転送ツール（CTT）リリースをインストールする {#install-ctt-azcopy-support}

CTT 1.5.4 リリースには、Amazon S3 と Azure Blob Storage の AzCopy のサポートが含まれています。
ファイルデータストアのサポートは、CTT 1.7.2 リリースに含まれています CTT の最新リリースは、 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) ポータル。


### 3. Azcopy.config ファイルを設定する {#configure-azcopy-config-file}

ソースAEMインスタンス上で、 `crx-quickstart/cloud-migration`、という名前の新しいファイルを作成します。 `azcopy.config`.

>[!NOTE]
>この設定ファイルの内容は、ソースAEMインスタンスが Azure とAmazon S3 のどちらのデータストアを使用しているかによって異なります。

#### Azure Blob ストレージデータストア {#azure-blob-storage-data}

Azcopy.config ファイルには、次のプロパティを含める必要があります（インスタンスに対して正しい azCopyPath と azureSas を使用してください）。

>[!NOTE]
>
> BLOB ストレージコンテナへの書き込みアクセスを許可しない場合は、Read  と List の権限のみを持つ新しい SAS URI を生成できます。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3 データストア {#amazon-sdata-store}

azcopy.config ファイルには、次のプロパティを含める必要があります（インスタンスに対して正しい値を使用してください）。

>[!NOTE]
>
> インスタンスで IAM の役割を使用して AEM が S3 にアクセスできるようにする場合は、S3 バケットに対して ListBucket と GetObject のアクションを有効にしたポリシーとユーザーを作成する必要があります。設定が完了したら、このユーザーのアクセスキーと秘密鍵を使用します。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### ファイルデータストア {#file-data-store-azcopy-config}

お使いの `azcopy.config` ファイルには、azcopyPath プロパティと、ファイルデータストアの場所を指すオプションの repository.home プロパティを含める必要があります。 インスタンスに正しい値を使用します。
ファイルデータストア

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

azcopyPath プロパティには、ソースAEMインスタンスに azCopy コマンドラインツールがインストールされている場所のフルパスを含める必要があります。 azCopyPath プロパティが見つからない場合、BLOB の事前コピー手順は実行されません。

If `repository.home` プロパティが azcopy.config から見つからず、その後デフォルトのデータストアの場所が見つかりません `/mnt/crx/author/crx-quickstart/repository/datastore` は、プリコピーの実行に使用されます。

### 4. AzCopy を使用して抽出する {#extracting-azcopy}

上記の設定ファイルを配置すると、AzCopy のコピー前段階は、移行の抽出の一部として実行されます。AzCopy を実行しないようにするには、ファイル名を変更するか、削除します。

>[!NOTE]
>AzCopy が正しく設定されていない場合は、次のメッセージがログに表示されます。
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`。

1. CTT UI から抽出を開始します。詳しくは、[コンテンツ転送ツールの基本を学ぶ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja)と[抽出プロセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=ja)を参照してください。

1. 抽出ログに次の行が出力されていることを確認します。

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

おめでとうございます。このログエントリは、設定が有効と見なされ、AzCopy がソースコンテナから移行コンテナにすべての BLOB をコピー中であることを意味します。

AzCopy のログエントリは抽出ログに表示され、先頭に c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy pre-copy ]が付きます。

>[!CAUTION]
>
> 抽出の最初の数分は、問題の兆候がないか抽出ログを注意して確認します。例として、ソース Azure コンテナが見つからない場合にログに記録される内容を次に示します。

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

AzCopy に問題が発生した場合、抽出は直ちに失敗し、抽出ログには失敗の詳細が記録されます。

エラーの発生前にコピーされた BLOB は、その後の実行で AzCopy によって自動的にスキップされ、再度コピーされることはありません。

#### ファイルデータストアの場合 {#file-data-store-extract}

AzCopy がソースファイル dataStore に対して実行されている場合は、次のようなメッセージがログに表示され、フォルダが処理されていることを示します。
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. AzCopy で取り込む {#ingesting-azcopy}

コンテンツ転送ツール 1.5.4 のリリースでは、AzCopy のサポートがオーサーの取り込みに追加されました。

>[!NOTE]
>最初にオーサーの取り込みを単独で実行することをお勧めします。これにより、後で実行する際に、パブリッシュの取り込みが高速化されます。

取り込み中に AzCopy を利用するには、少なくともバージョン 2021.6.5561 の AEM as a Cloud Service バージョンを使用する必要があります。

オーサーの取り込みを CTT UI から開始します。詳しくは、[取り込みプロセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=ja)を参照してください。AzCopy のログエントリが取り込みログに表示されます。次のようになります。

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

## AzCopy を無効にしています {#disable-azcopy}

AzCopy を無効にするには、 `azcopy.config` ファイル。

例えば、azcopy の抽出を無効にするには、次のオプションを使用します。 `mv /mnt/crx/author/crx-quickstart/cloud-migration/azcopy.config /mnt/crx/author/crx-quickstart/cloud-migration/noazcopy.config`.

## 次のステップ {#whats-next}

コンテンツを AEM as a Cloud Service に移行するコンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮するための大規模コンテンツリポジトリー処理を理解したら、コンテンツ転送ツールでの抽出プロセスを学ぶ準備が整いました。コンテンツ転送ツールで移行セットを抽出する方法について詳しくは、[ソースからのコンテンツの抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)を参照してください。
