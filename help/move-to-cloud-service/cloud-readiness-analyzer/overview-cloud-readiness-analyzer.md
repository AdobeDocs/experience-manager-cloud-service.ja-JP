---
title: Cloud Readiness Analyzerの概要
description: Cloud Readiness Analyzerの概要
translation-type: tm+mt
source-git-commit: 47773a56f8bb24342281068a8c4d03d6edfb9277
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 概要 {#overview-cloud-readiness-analyzer}

Cloud Readiness Analyzerは、既存のAEMインスタンスからAEMにクラウドサービスとして移行する準備ができているかどうかを評価するのに役立ちます。

このツールは、リファクタリングが必要な領域を決定します。これは、AEMへのトランジション遍歴の最初の手順で、クラウドサービスとしての役割を果たします。

CRAは、次のようなパターンを検出し、レポートします。

* AEMでクラウドサービスとして現在サポートされていないAEM 6.xの機能を使用する

* クラウドサービスとしてのAEMへの移行の影響を受ける特定のルール、設定、使用に違反する

## Cloud Readiness Analyzerの概要レポート {#summary-report}

Cloud Readiness Analyzerは、一般的なアップグレードの準備状況を把握するために使用できる概要レポートを生成します。

レポートは、結果をカテゴリ別、およびカテゴリ内のサブタイプ別にまとめます。 カテゴリに関する追加情報、およびこれらのカテゴリに関連する考えられる示唆とソリューションは、サマリレポート内のリンクを通して提供されます。

>[!NOTE]
>Cloud Readiness Analyzerの出力は、クラウドサービスとしてAEMに移行する際に必要な時間とコストの見積もりプロセスを高速化するのに役立ちます。