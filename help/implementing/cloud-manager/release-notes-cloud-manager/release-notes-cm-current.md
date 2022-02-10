---
title: AEM as a Cloud Service Release 2022.02.0 Cloud Manager のリリースノート
description: AEM as a Cloud Serviceリリース2022.02.0の Cloud Manager のリリースノートです。
feature: Release Information
source-git-commit: d1fe713f0c35a96cf6ba3172ea11986fd9d42fd6
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 10%

---


# Adobe Experience Manager as a Cloud Service 2022.02.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.02.0の Cloud Manager のリリースノートの概要を説明します。

>[!NOTE]
>
>参照： [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Service 2022.02.0の Cloud Manager のリリース日は 2022 年 2 月 10 日です。 次回のリリースは 2022 年 3 月 10 日に予定されています。

## 新機能 {#what-is-new}

* 新しい加速 [Web 層設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) HTTPD/Dispatcher 設定のみをデプロイするためのが導入されました。
   * AEM版である必要があります `2021.12.6151.20211217T120950Z` またはそれ以降 [dispatcher ツールの柔軟なモードのオプトイン](/help/implementing/dispatcher/disp-overview.md#validation-debug) この機能を使用するには、をクリックします。
   * この機能は、2022.02.0リリース以降の 2 週間にわたって段階的に展開されます。
* Cloud Manager のランディングページエクスペリエンスが更新され、ナビゲーションの改善、グリッド/タイル表示の切り替え、プログラムの概要をすばやく表示するためのポップオーバーが簡単に実現されました。
* 新しい失敗したしきい値 (`< D`) が [信頼性評価指標です。](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * システムの安定性に影響を与える重大な品質の問題（主に無効なインデックスとワークフロープロセスに関連）を持つお客様は、その問題が解決されるまでデプロイできません。
* の重大度 `BannedPath` [品質ルール](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) がブロッカーから重大に変更されました。
* パイプラインウィザードでは、AEM環境の更新が必要になった場合に、 [Web 層設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 関連付けられています。

## バグ修正 {#bug-fixes}

* 古い Git リポジトリのパスワードが、新しいパスワードの生成時に常に無効化されるようになりました。
* API で環境変数を更新しても、まれにパイプラインの実行に干渉しなくなりました。
