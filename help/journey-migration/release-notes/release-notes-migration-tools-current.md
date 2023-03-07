---
title: AEM as a Cloud Service リリース 2023.03.0 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2022.03.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 5815dacd2806cc7886aa0c7c5c9fd329306b3e1b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 49%

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