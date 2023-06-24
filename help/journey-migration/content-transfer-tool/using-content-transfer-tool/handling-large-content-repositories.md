---
title: 大規模なコンテンツリポジトリーの処理
description: この節では、大規模なコンテンツリポジトリーの処理について説明します
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 49%

---

# 大規模なコンテンツリポジトリーの処理 {#handling-large-content-repositories}

## 概要 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="大規模なコンテンツリポジトリーの処理"
>abstract="コンテンツ転送アクティビティの抽出と取り込み段階を大幅に高速化してコンテンツをAEMas a Cloud Serviceに移動するために、コンテンツ転送ツール (CTT) は AzCopy をオプションのプリコピー手順として使用できます。 この前段階が設定されたら、AzCopy は、抽出段階で Amazon S3 または Azure Blob Storage から移行セット BLOB ストアに BLOB をコピーします。取り込み段階では、AzCopy は、移行セットの BLOB ストアから宛先の AEM as a Cloud Service BLOB ストアに BLOB をコピーします。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html#setting-up-pre-copy-step" text="AzCopy をコピー前手順として使用する"

コンテンツ転送ツール (CTT) で多数の BLOB をコピーするには、複数日かかる場合があります。
コンテンツ転送アクティビティの抽出段階と取り込み段階を早めてコンテンツをAEMas a Cloud Serviceの環境に移動するには、CTT で次を使用します。 [AzCopy](https://learn.microsoft.com/ja-jp/azure/storage/common/storage-use-azcopy-v10) を追加します。 この事前コピー手順を使用できるのは、ソース AEM インスタンスが Amazon S3、Azure Blob Storage データストアまたはファイルデータストアを使用するように設定されている場合です。  事前コピー手順は、最初の完全な抽出および取り込みに最も効果的です。 ただし、後続のトップアップに対して事前コピーを使用することは、プロセス全体に時間がかかる可能性があるので推奨されません（トップアップのサイズが 200GB 未満の場合）。この事前手順が設定されたら、AzCopy は、抽出段階で Amazon S3、Azure Blob Storage またはファイルデータストアから移行セット BLOB ストアに BLOB をコピーします。取り込み段階では、AzCopy は、移行セットの BLOB ストアから宛先の AEM as a Cloud Service BLOB ストアに BLOB をコピーします。

## 開始する前に考慮すべき重要事項 {#important-considerations}

開始する前に、次の重要事項を確認してください。

* CTT のバージョン 2.0.16 以降では、バンドルのインストール時にプレコピーの設定が自動的におこなわれます。 また、移行セットのサイズが 200 GB を超える場合、抽出プロセスは自動的にプリコピー機能を使用します。 azcopy.config ファイルは、crx-quickstart/cloud-migration/ ディレクトリに作成されます。CTT バージョン 2.0.16 以降を使用している場合は、プレコピー設定を手動で行う必要はありません。

* ソースAEMのバージョンは 6.3 ～ 6.5 である必要があります。

* ソース AEM のデータストアが Amazon S3 または Azure Blob Storage を使用するように設定されている。詳しくは、[AEM 6 でのノードストアとデータストアの設定を参照してください](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=ja)。

* 各移行セットはデータストア全体をコピーするので、1 つの移行セットのみを使用する必要があります。

* をインストールするには、にアクセスする必要があります [AzCopy](https://learn.microsoft.com/ja-jp/azure/storage/common/storage-use-azcopy-v10) （または VM）上のソースAEMインスタンスを実行している場合 )

* データストアのガベージコレクションは、ソース上で過去 7 日以内に実行されました。 詳しくは、[データストアのガベージコレクション](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=ja#data-store-garbage-collection)を参照してください。

### ソース AEM インスタンスが Amazon S3 または Azure Blob Storage データストアを使用するように設定されている場合の追加の考慮事項 {#additional-considerations-amazons3-azure}

* Amazon S3 および Azure Blob Storage からのデータ転送に関連するコストが発生します。 転送コストは、既存のストレージコンテナ内のデータの総量 (AEMで参照されているかどうかに関わらず ) に対する相対的な値です。 詳しくは、[Amazon S3](https://aws.amazon.com/s3/pricing/) および [Azure Blob Storage](https://azure.microsoft.com/ja-jp/pricing/details/bandwidth/) を参照してください。

* 既存のソースAmazon S3 バケットのアクセスキーと秘密鍵のペア、または既存のソース Azure Blob Storage コンテナの SAS URI が必要です（読み取り専用アクセスは問題ありません）。

### ソース AEM インスタンスがファイルデータストアを使用するように設定されている場合の追加の考慮事項 {#additional-considerations-aem-instance-filedatastore}

* ローカルシステムには、ソースデータストアの 1/256 サイズよりも厳密に大きい空き領域が必要です。例えば、データストアのサイズが 3 TB の場合、11.72 GB を超える空き領域が `crx-quickstart/cloud-migration` AzCopy が動作するソース上のフォルダ。 少なくとも、ソースシステムには 1 GB の空き領域が必要です。空き容量は `df -h` コマンドを使用し、Windows インスタンスでは dir コマンドを使用します。

* AzCopy を有効にして抽出を実行するたびに、ファイルデータストア全体が統合され、クラウド移行コンテナにコピーされます。移行セットがデータストアのサイズより小さい場合、AzCopy 抽出は最適なアプローチではありません。

* AzCopy を使用して既存のデータストアをコピーした後は、差分抽出または追加抽出に対しては AzCopy を無効にします。

## AzCopy をコピー前手順として使用する設定 {#setting-up-pre-copy-step}

>[!NOTE]
>CTT のバージョン 2.0.16 以降では、バンドルのインストール時にプレコピーの設定が自動的におこなわれます。 また、移行セットのサイズが 200 GB を超える場合、抽出プロセスは自動的にプリコピー機能を使用します。 azcopy.config ファイルは、crx-quickstart/cloud-migration/ ディレクトリに作成されます。ファイルの設定を手動で更新する場合は、以下の節を確認してください。

このセクションでは、コンテンツ転送ツールを使用してコンテンツをAEMas a Cloud Serviceに移行するための AzCopy を事前コピーステップとして使用する設定方法を学ぶことができます。

### 0. データストア内のすべてのコンテンツの合計サイズを算出する {#determine-total-size}

データストアの合計サイズを決定することが重要なのは、次の 2 つの理由によります。

* ソース AEM がファイルデータストアを使用するように設定されている場合、ローカルシステムには、ソースデータストアの 1/256 サイズより厳密に大きい空き領域が必要です。

#### Azure Blob ストレージデータストア {#azure-blob-storage}

Azure portal の既存のコンテナープロパティページから、「**サイズを計算**」ボタンを使用して、コンテナ内のすべてのコンテンツのサイズを決定します。次に例を示します。

![画像](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3 データストア {#amazon-data}

コンテナの「指標」タブを使用して、コンテナ内のすべてのコンテンツのサイズを算出できます。次に例を示します。


![画像](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### ファイルデータストア {#file-data-store-determine-size}

* Mac、UNIX®システムの場合は、データストアディレクトリで du コマンドを実行してサイズを取得します。
  `du -sh [path to datastore on the instance]`。例えば、データストアが `/mnt/author/crx-quickstart/repository/datastore`を指定した場合、次のコマンドを使用してサイズを取得できます。 `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* Windows の場合は、データストアディレクトリで dir コマンドを使用してサイズを取得します。
  `dir /a/s [location of datastore]`。

### 1. AzCopy をインストールする {#install-azcopy}

[AzCopy](https://learn.microsoft.com/ja-jp/azure/storage/common/storage-use-azcopy-v10) は、Microsoft®が提供するコマンドラインツールで、この機能を有効にするにはソースインスタンスで使用できる必要があります。

つまり、Linux® x86-64 バイナリを [AzCopy ドキュメントページ](https://learn.microsoft.com/ja-jp/azure/storage/common/storage-use-azcopy-v10) /usr/bin などの場所に展開します。

>[!IMPORTANT]
>後の手順でバイナリへの完全パスが必要になるので、バイナリの配置場所をメモしておきます。

### 2. AzCopy をサポートするコンテンツ転送ツール（CTT）リリースをインストールする {#install-ctt-azcopy-support}

>[!IMPORTANT]
>最新のリリースバージョンの CTT を使用する必要があります。

Amazon S3、Azure Blob Storage、ファイルデータストアの AzCopy のサポートは、最新の CTT リリースに含まれています。
CTT の最新リリースは、[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)ポータルからダウンロードできます。
サポートされているのはバージョン 2.0.0 以降のみであり、最新バージョンを使用することをお勧めします。

### 3. azcopy.config ファイルを設定する {#configure-azcopy-config-file}

ソースAEMインスタンス上で、 `crx-quickstart/cloud-migration`を作成し、 `azcopy.config`.

>[!NOTE]
>この設定ファイルの内容は、ソースAEMインスタンスが Azure とAmazon S3 のどちらのデータストアを使用しているかによって異なります。

#### Azure Blob ストレージデータストア {#azure-blob-storage-data}

Azcopy.config ファイルには、次のプロパティを含める必要があります（インスタンスに対して正しい azCopyPath と azureSas を使用してください）。

>[!NOTE]
>
> 既存の BLOB ストレージコンテナへの書き込みアクセスを許可しない場合は、読み取りとリストの権限のみを持つ新しい SAS URI を生成することができます。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3 データストア {#amazon-sdata-store}

azcopy.config ファイルには、次のプロパティを含める必要があります（インスタンスに対して正しい値を使用してください）。

>[!NOTE]
>
> インスタンスで IAM ロールを使用してAEMが S3 にアクセスできるようにする場合は、ListBucket と GetObject アクションを S3 バケットに対して有効にしたポリシーとユーザーを作成する必要があります。 設定が完了したら、このユーザーのアクセスキーと秘密鍵を使用します。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### ファイルデータストア {#file-data-store-azcopy-config}

お使いの `azcopy.config` ファイルには、azCopyPath プロパティと、ファイルデータストアの場所を指すオプションの repository.home プロパティが記述されている必要があります。インスタンスに正しい値を使用します。
ファイルデータストア

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

azCopyPath プロパティには、ソースAEMインスタンスに azCopy コマンドラインツールがインストールされている場所のフルパスを含める必要があります。 azCopyPath プロパティが見つからない場合、BLOB の事前コピー手順は実行されません。

If `repository.home` プロパティが azcopy.config から見つからず、その後デフォルトのデータストアの場所が見つかりません `/mnt/crx/author/crx-quickstart/repository/datastore` は、プリコピーの実行に使用されます。

### 4. AzCopy を使用して抽出する {#extracting-azcopy}

上記の設定ファイルを配置すると、AzCopy の事前コピーフェーズは、後続の抽出の一部として実行されます。 AzCopy を実行しないようにするには、ファイル名を変更するか、削除します。

>[!NOTE]
>AzCopy が正しく設定されていない場合は、次のメッセージがログに表示されます。
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`。

1. CTT UI から抽出を開始します。詳しくは、[コンテンツ転送ツールの基本を学ぶ](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)と[抽出プロセス](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)を参照してください。

1. 抽出ログに次の行が印刷されていることを確認します。

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

おめでとうございます。このログエントリは、設定が有効と見なされ、AzCopy がソースコンテナから移行コンテナにすべての BLOB をコピーすることを意味します。

AzCopy のログエントリは抽出ログに表示され、先頭に c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy — が付きます。 [AzCopy プリコピー]

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

AzCopy に問題がある場合、抽出は直ちに失敗し、抽出ログには失敗に関する詳細が含まれます。

エラーの前にコピーされた BLOB は、その後の実行時に AzCopy によって自動的にスキップされ、再度コピーする必要はありません。

#### ファイルデータストアの場合 {#file-data-store-extract}

AzCopy がソースファイルデータストアに対して実行されている場合は、次のようなメッセージがログに表示され、フォルダーが処理中であることを示します。
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. AzCopy で取り込む {#ingesting-azcopy}

Cloud Acceleration Manager（CAM）からターゲットにコンテンツを取り込む方法に関する一般的な情報については、[ターゲットへのコンテンツの取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照してください。これには、「新規取り込み」ダイアログで AzCopy（事前コピー）を使用する方法、または使用しない方法が含まれます。 

取り込み中に AzCopy を利用するには、Adobeで、少なくともバージョン 2021.6.5561 のAEMas a Cloud Serviceバージョンを使用している必要があります。

Cloud Acceleration Manager の「取り込みジョブ」リストと取り込みのログを参照して、進行状況を確認できます。 成功した AzCopy タスクに関連するログエントリは、次のように表示されます（いくつかの違いを許可）。 ログを時々確認することで、早い段階で問題を警告し、問題の迅速な解決策を見つけることができます。

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

## 次のステップ {#whats-next}

コンテンツをAEM as a Cloud Serviceに移動するためのコンテンツ転送アクティビティの抽出段階および取り込み段階を高速化する、大きなコンテンツリポジトリの処理について学習しました。 これで、コンテンツ転送ツールを使用した抽出プロセスを学習する準備が整いました。 詳しくは、 [コンテンツ転送ツールでのソースからのコンテンツの抽出](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) そのため、コンテンツ転送ツールから移行セットを抽出する方法を学ぶことができます。
