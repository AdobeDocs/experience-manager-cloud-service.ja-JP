---
title: Cloud Readiness Analyzer の概要
description: Cloud Readiness Analyzer の概要
translation-type: tm+mt
source-git-commit: 2064dd6c647780dc149c51b7ff166779ba0a2212
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 95%

---


# 概要 {#overview-cloud-readiness-analyzer}

Cloud Readiness Analyzer を使用すると、既存の Adobe Experience Manager（AEM）のデプロイメントから AEM as a Cloud Service への移行の準備状況を評価するプロセスを迅速に実行できます。

このツールでは、AEM as a Cloud Service への移行の最初の手順として、リファクタリングの可能性がある領域を識別するレポートを生成します。

## Cloud Readiness Analyzer レポート {#cra-report}

Cloud Readiness Analyzer レポートは、一般的なアップグレードの準備状況を理解するために使用します。このレポートは、カテゴリの中で発見された問題で構成されており、AEM as a Cloud Service のデプロイメントを成功させるにはそれらの問題を解決する必要があります。

Cloud Readiness Analyzer レポートには、次のカテゴリが含まれます。

* リファクタリングが必要なアプリケーション機能
* サポートされている場所に移動する必要があるリポジトリ項目
* 旧式のユーザーインターフェイスダイアログと、最新化が必要なコンポーネント
* デプロイと設定に関する問題
* 新しい機能に置き換えられた、または AEM as a Cloud Service で現在サポートされていない AEM 6.x の機能

カテゴリに関する追加情報、およびこれらのカテゴリに関連する示唆と解決策に関する情報は、Cloud Readiness Analyzer レポート内からリンクを介して提供されます。

>[!NOTE]
>Cloud Readiness Analyzer レポートは、手動で収集および評価する必要のある情報を提供することで、AEM as a Cloud Service の移行に必要な時間とコストの見積もりプロセスをスピードアップします。

Cloud Readiness Analyzer レポートは、AEM インスタンスからダウンロードすることもできます。詳細については、 [「Cloud Readiness Analyzerレポートの](/help/move-to-cloud-service/cloud-readiness-analyzer/using-cloud-readiness-analyzer.md#viewing-report) 表示」を参照してください。