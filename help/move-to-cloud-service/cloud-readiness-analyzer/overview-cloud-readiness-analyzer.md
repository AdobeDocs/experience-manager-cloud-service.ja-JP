---
title: Cloud Readiness Analyzerの概要
description: Cloud Readiness Analyzerの概要
translation-type: tm+mt
source-git-commit: ae38a1300ef2d8f2b344313195ec904fca48d86b
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# 概要 {#overview-cloud-readiness-analyzer}

Cloud Readiness Analyzerを使用すると、既存のAdobe Experience Manager(AEM)のデプロイメントからCloud ServiceとしてAEMに移行する準備を評価するプロセスを迅速に実行できます。

このツールにより、Cloud ServiceとしてAEMに到達するトランジションの最初の手順である、リファクタリングの可能性がある領域を識別するレポートが生成されます。

## Cloud Readiness Analyzerの概要レポート {#summary-report}

Cloud Readiness Analyzerの概要レポートは、アップグレードの準備状況の概要を把握するために使用します。 このレポートは、Cloud ServiceとしてAEMへの導入を成功させる前に対処する必要のある問題のカテゴリ内の結果で構成されます。

サマリレポートには次のカテゴリが含まれます。

* リファクタリングが必要なアプリケーション機能
* サポートされている場所に移動する必要があるリポジトリアイテム
* 旧式のユーザーインターフェイスダイアログと、最新化が必要なコンポーネント
* デプロイと設定に関する問題
* 新しい機能に置き換えられた、またはCloud ServiceとしてAEMで現在サポートされていないAEM 6.xの機能

カテゴリに関する追加情報、およびこれらのカテゴリに関連する考えられる示唆とソリューションは、サマリレポート内のリンクを通して提供されます。

>[!NOTE]
>Cloud Readiness Analyzerレポートは、手動で収集して評価する必要のあるトランジションを提供することで、Cloud ServiceとしてAEMに情報を提供するのに必要な時間とコストの見積もりプロセスを高速化します。

Cloud Readiness Analyzerレポートは、AEMインスタンスからダウンロードすることもできます。 保留中の詳細については、「CSV形式での結果の **表示** 」を参照してください。