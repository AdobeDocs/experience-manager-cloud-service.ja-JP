---
title: AEM as a Cloud Service リリース 2023.03.0 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2023.03.0 の移行ツールのリリースノート
feature: Release Information
exl-id: cdc57cca-e10a-4b0d-b803-910ccc9350a6
role: Admin
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 96%

---

# AEM as a Cloud Service リリース 2023.03.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2023.03.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.40 のリリース日は 2023年3月3日（PT）です。

### 新機能 {#what-is-new-bpa}

* BPA は、競合するノード（同じ `jcr:uuid` を持つノード）を検出し、レポートできるようになりました。このような結果は、コンテンツを AEM as a Cloud Service に移動する際にコンテンツ取り込みに失敗する可能性があるので、重要としてフラグ付けされます。
* BPA は、イベントリスナーの使用状況を検出し、報告できるようになりました。AEM as a Cloud Service に移行する際には、このタイプのイベント処理メカニズムを Sling ジョブにリファクタリングすることをお勧めします。

### バグの修正 {#bug-fixes-bpa}

* BPA は、`grouprendercondition` に関して偽陽性をレポートしていました。この問題は修正されました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v2.0.16 のリリース日は 2023年3月8日（PT）です。

### 新機能 {#what-is-new-ctt}

* ユーザーマッピングが合理化され、コンテンツ抽出手順に統合されました。設定は必要なく、デフォルトでは、ユーザーがコンテンツの抽出を開始する際に、ユーザーマッピングが自動的に行われます。必要に応じて、ユーザーマッピングを無効にするオプションがあります。
* [AzCopy](https://learn.microsoft.com/ja-jp/azure/storage/common/storage-use-azcopy-v10) を使用したプレコピー手順がコンテンツ転送ツールと統合され、コンテンツ抽出が大幅に高速化しました。このバージョンの CTT がインストールされると、プレコピーは自動的に設定およびインストールされます。デフォルトでは、抽出が開始されると、200 GB を超える移行セットに対してプレコピーが自動的に実行されます。必要に応じて、無効にするオプションがあります。詳しくは、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja)を参照してください。
* CTT を Windows サーバーで使用できるようになりました。

### バグの修正 {#bug-fixes-ctt}

* コンテンツの抽出の回復性を向上させるために、複数のバグを修正しました。
