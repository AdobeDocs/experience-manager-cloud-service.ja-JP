---
title: Cloud Readiness Analyzerの使用
description: Cloud Readiness Analyzerの使用
translation-type: tm+mt
source-git-commit: 3d818278c53f3d3b4c5b53aa5b78d06d876bf05f
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 6%

---


# Cloud Readiness Analyzerの使用 {#using-cloud-readiness-analyzer}

## Cloud Readiness Analyzerを使用する際の重要な考慮事項 {#imp-considerations}

Cloud Readiness Analyzer(CRA)の実行中の重要な考慮事項を理解するには、次の節に従ってください。

* CRAは、バージョン6.1以降を使用するソースAEMインスタンスでサポートされます。
* CRAは任意の環境で実行できます。

   >[!NOTE]
   >検出率を高め、ビジネスクリティカルインスタンスの遅延を回避するため、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの実稼動環境にできる限り近いソース作成者ステージング環境でCRAを実行することをお勧めします。 または、公開環境のコピーで実行することもできます。

## 入手方法 {#availability}

Cloud Readiness Analyzer(CRA)は、ソフトウェア配布ポータルからzipファイルとしてダウンロードできます。 パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。

>[!NOTE]
>保留中からCloud Readiness Analyzer(CRA)をダウンロードし *ます*。

## Cloud Readiness Analyzerの実行 {#running-tool}

Cloud Readiness Analyzerの実行方法を学ぶには、次のセクションに従います。

1. Select the Adobe Experience Manager and navigate to tools -> **Operations** -> **Cloud Readiness Analyzer**.

### 結果の表示 {#viewing-the-results}

CRAの出力を表示するには、2つの方法があります。

1. 整理されたレポートの使用

   >[!NOTE]
   >整理されたレポートは、AEMバージョン6.3以降で利用できます。

CRAドキュメントの計画とステータスを参照して、レポートの重要度レベルを説明します。

1. CRAの出力の表示（AEMバージョン6.1以降で使用可能）:

   1. に移動して、AEM Webコンソールに移動します。

   1. 次の画像に示すように、「ステータス — Cloud Readiness Analyzer」を選択します。

#### レポートの重要度レベルについて {#importance-levels}

次の表に、様々なPattern DetectorとCloud Readiness Analyzerの重要度レベルの意味を示します。

| 重要度レベル | 説明 |
|--- |--- |
| 情報/0 | この検索結果は、情報を提供する目的で提供されます。 |
| アドバイザリ/1 | この結果、アップグレードに関する問題が発生する可能性があります。 さらに調査を行うことをお勧めします。 |
| メジャー/2 | この結果、アップグレードに関する問題に対処する必要がある可能性があります。 |
| 重大/3 | この結果、アップグレードの問題が発生する可能性が高く、機能やパフォーマンスの低下を防ぐために対処する必要があります。 |