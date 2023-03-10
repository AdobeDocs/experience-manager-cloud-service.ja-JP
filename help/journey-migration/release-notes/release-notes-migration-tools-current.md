---
title: AEM as a Cloud Service リリース 2023.03.0 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2022.03.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: b2681113f5565e4f63c76abeaf46d5f4b1a8a8ea
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 29%

---

# AEM as a Cloud Service リリース 2023.03.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.03.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.40 のリリース日は 2023 年 3 月 03 日です。

### 新機能 {#what-is-new-bpa}

* BPA は、競合するノード（同じノードを持つノード）を検出し、レポートできるようになりました。 `jcr:uuid`. このような結果は、コンテンツをAEM as a Cloud Serviceに移動する際にコンテンツ取り込みに失敗する可能性があるので、重要としてフラグ付けされます。
* BPA は、イベントリスナーの使用状況を検出し、報告できるようになりました。 AEM as a Cloud Serviceに移行する際には、このタイプのイベント処理メカニズムを Sling ジョブにリファクタリングすることをお勧めします。

### バグの修正 {#bug-fixes-bpa}

* BPA は、次の偽陽性をレポートしていました： `grouprendercondition`. この問題が修正されました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v2.0.16 のリリース日は 2022 年 3 月 08 日です。

### 新機能 {#what-is-new-ctt}

* ユーザーマッピングが合理化され、コンテンツ抽出手順に統合されました。 設定は必要なく、デフォルトでは、ユーザーがコンテンツの抽出を開始する際に、ユーザーマッピングが自動的におこなわれます。 ユーザーは、必要に応じてユーザーマッピングを無効にするオプションがあります。 詳細情報 [こちら。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html?lang=en#user-mapping-detail)
* を使用したプリコピー手順 [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) は、コンテンツ抽出を大幅に高速化するために、コンテンツ転送ツールと統合されました。 このバージョンの CTT がインストールされると、プリコピーは自動的に設定およびインストールされます。 デフォルトでは、抽出が開始されると、200 GB を超える移行セットに対してプリコピーが自動的に実行されます。 必要に応じて、無効にするオプションがあります。 詳細情報 [こちら。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)
* CTT を Windows サーバーで使用できるようになりました。

### バグの修正 {#bug-fixes-ctt}

* コンテンツの抽出の回復性を向上させるために、複数のバグを修正しました。
