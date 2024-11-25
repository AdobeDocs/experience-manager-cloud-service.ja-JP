---
title: AEM as a Cloud Service リリース 2024.05.0 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2024.05.0 の移行ツールのリリースノート
feature: Release Information
role: Admin
exl-id: f50a74fa-ad7d-4837-b0a1-9945c32af02f
source-git-commit: 3b2ed44b438fe8587a9b9603ddfacc41111fb903
workflow-type: ht
source-wordcount: '208'
ht-degree: 100%

---

# AEM as a Cloud Service リリース 2024.05.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2024.05.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.50 のリリース日は 2024年5月です。

### 新機能 {#what-is-new-bpa}

* ベストプラクティスアナライザー（BPA）では、BPA で生成されたレポートを Cloud Acceleration Manager（CAM）に直接自動アップロードできるようになりました。ユーザーはレポートを手動でダウンロードして CAM にアップロードする必要がなくなります。詳しくは、[ベストプラクティスアナライザーの使用](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)を参照してください。

### バグ修正 {#bug-fixes-bpa}

* ベストプラクティスアナライザーにより、16MBを超えるすべてのノードが検出されるようになりました
* NCC 結果が散発的に発生する競合状態が修正されました。

## Cloud Acceleration Manager {#cam-release}

### 新機能 {#what-is-new-cam}

* Cloud Acceleration Manager（CAM）では、BPA で生成されたレポートを CAM に直接自動アップロードできるようになりました。詳しくは、[Cloud Acceleration Manager の準備フェーズ - ベストプラクティス分析カードの使用](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)を参照してください。

* Cloud Acceleration Manager では、ノード数、データストアのサイズなどの要素に基づいて、取り込み時間の推定が提供されるようになりました。詳しくは、[コンテンツの Cloud Service への取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照してください。
