---
title: Cloud Readiness Analyzerの使用
description: Cloud Readiness Analyzerの使用
translation-type: tm+mt
source-git-commit: 317dd08600df9c7127cf8502341f93758ac8ce0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---


# Cloud Readiness Analyzerの使用 {#using-cloud-readiness-analyzer}

## Cloud Readiness Analyzerを使用する際の重要な考慮事項 {#imp-considerations}

Cloud Readiness Analyzer(CRA)の実行中の重要な考慮事項を理解するには、次の節に従ってください。

* CRAは、バージョン6.1以降を使用するソースAEMインスタンスでサポートされます。
* CRAは任意の環境で実行できます。 ただし、検出率を高め、ビジネスクリティカルなインスタンスの遅延を回避するため、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの実稼働環境にできる限り近いソース作成者ステージング環境で実行することをお勧めします。 または、公開環境のコピーで実行することもできます。

## 利用可能場所 {#availability}

Cloud Readiness Analyzer(CRA)は、ソフトウェア配布ポータルからzipファイルとしてダウンロードできます。 Package Managerを使用して、ソースAdobe Experience Manager(AEM)インスタンスにパッケージをインストールできます。

>[!NOTE]
>保留中からCloud Readiness Analyzer(CRA)をダウンロードします。

## Cloud Readiness Analyzerの実行 {#running-tool}

Cloud Readiness Analyzerの実行方法を学ぶには、次のセクションに従います。

1. Adobe Experience Managerを選択し、ツール/ **操作** / **Cloud Readiness Analyzerに移動します**。

### 結果の表示 {#viewing-the-results}

CRAの出力を表示するには、2つの方法があります。

1. 整理されたレポートの使用（AEMバージョン6.3以降で利用可能）レポートの重要度レベルについては、CRAドキュメント計画とステータスを参照してください。

CRAの出力を表示するには（AEMバージョン6.1以降で使用できます）:

1. に移動して、AEM Webコンソールに移動します。

1. 次の画像に示すように、「ステータス — Cloud Readiness Analyzer」を選択します。