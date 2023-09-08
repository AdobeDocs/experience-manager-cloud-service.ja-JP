---
title: AEM as a Cloud Service リリース 2023.07.0 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2022.07.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 1f01408223a661c0149d959b1901293dc91ed7ee
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 46%

---

# AEM as a Cloud Service リリース 2023.07.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.07.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.42 のリリース日は 2023年7月06日です。

### 新着情報 {#what-is-new-bpa}

* このリリースのベストプラクティスアナライザーには、複数のベストプラクティスパターンが追加されました。 次のものが含まれます。
   * 最小メンテナンスタスク設定の識別
   * 長時間実行されるクエリや処理の多いクエリの検出
   * 実行中または古い状態のオーサーワークフローの検出数が多い
   * OSGI Apache Sling ジョブ設定の検出
   * カスタム Guava キャッシュの検出

### バグ修正 {#bug-fixes-bpa}

* BPA が改善され、結果数が多いレポートでメモリ不足のレポート生成エラーが発生するのを防ぎました。
* BPA が改善され、AEM as a Cloud Serviceへの移行コンテンツの取り込み失敗を防ぐため、パス内のエスケープ文字を検出できるようになりました。
