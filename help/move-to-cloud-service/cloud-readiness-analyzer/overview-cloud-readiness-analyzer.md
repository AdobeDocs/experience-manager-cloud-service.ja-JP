---
title: Cloud Readiness Analyzerの概要
description: Cloud Readiness Analyzerの概要
translation-type: tm+mt
source-git-commit: f0e69dba5d670d141c82e762069f4831c2527dbe
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 概要 {#overview-cloud-readiness-analyzer}

Cloud Readiness Analyzerを使用すると、既存のAdobe Experience Manager(AEM)デプロイメントからクラウドサービスとしてAEMに移行する準備を評価するプロセスを迅速に実行できます。

このツールにより、潜在的なリファクタリングの領域を識別するレポートが生成されます。これは、AEMへのトランジション遍歴の最初の手順で、クラウドサービスとしての役割を果たします。

## Cloud Readiness Analyzerの概要レポート {#summary-report}

Cloud Readiness Analyzerの概要レポートは、アップグレードの準備状況の概要を把握するために使用します。 このレポートは、カテゴリ内の結果で構成されます。これらの結果は、AEMをクラウドサービスとしてデプロイする前に対処する必要がある問題の内容です。

サマリレポートには次のカテゴリが含まれます。

* リファクタリングが必要なアプリケーション機能
* サポートされている場所に移動する必要があるリポジトリアイテム
* 旧式のユーザーインターフェイスダイアログと、最新化が必要なコンポーネント
* デプロイと設定に関する問題
* 新しい機能に置き換えられた、またはAEMでクラウドサービスとしてサポートされていないAEM 6.xの機能

カテゴリに関する追加情報、およびこれらのカテゴリに関連する考えられる示唆とソリューションは、サマリレポート内のリンクを通して提供されます。

>[!NOTE]
>Cloud Readiness Analyzerレポートは、手動で収集して評価する必要のあるトランジションを提供することで、クラウドサービスとしてAEMに情報を提供するのに必要な時間とコストの見積もりプロセスを高速化します。

サマリレポートはAEMユーザーインターフェイスからもダウンロードできます。 保留中の詳細については、「CSV形式での結果の **表示** 」を参照してください。