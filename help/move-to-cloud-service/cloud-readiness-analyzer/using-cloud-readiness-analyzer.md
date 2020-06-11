---
title: Cloud Readiness Analyzerの使用
description: Cloud Readiness Analyzerの使用
translation-type: tm+mt
source-git-commit: 47773a56f8bb24342281068a8c4d03d6edfb9277
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---


# Cloud Readiness Analyzerの使用 {#using-cloud-readiness-analyzer}

## Cloud Readiness Analyzerを使用する際の重要な考慮事項 {#imp-considerations}

Cloud Readiness Analyzer(CRA)の実行中の重要な考慮事項を理解するには、次の節に従ってください。

* CRAは、バージョン6.1以降を使用するソースAEMインスタンスでサポートされます
* CRAは任意の環境( *Stage* 環境)で実行できます。

   >[!NOTE]
   >検出率を高め、ビジネスクリティカルインスタンスの遅延を回避するため、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの実稼動環境にできる限り近いソース作成者ステージング環境でCRAを実行することをお勧めします。 または、 *公開* 環境のコピーで実行することもできます。

## 入手方法 {#availability}

Cloud Readiness Analyzerは、Software Distribution Portalからzipファイルとしてダウンロードできます。 パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。

>[!NOTE]
>Software Distribution Portal *保留中のCloud Readiness AnalyzerからCloud Readiness Analyzerをダウンロードします*。

## Cloud Readiness Analyzerの実行 {#running-tool}

Cloud Readiness Analyzerの実行方法を学ぶには、次のセクションに従います。

1. Select the Adobe Experience Manager and navigate to tools -> **Operations** -> **Cloud Readiness Analyzer**.

### 結果の表示 {#viewing-the-results}

>[!IMPORTANT]
>Cloud Readiness Analyzerから生成されるレポートは、パターンディテクターに基づいています。 詳しくは、「 [パターンディテクター](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) 」を参照してください。

Cloud Readiness Analyzerの出力を表示するには、2つの方法があります。

1. **整理レポートの使用**

   >[!NOTE]
   >整理されたレポートは、AEMバージョン6.3以降で利用できます。

   または、

1. **CRAの出力の表示**

   次の手順に従って、Cloud Readiness Analyzerの出力を表示します。

   >[!NOTE]
   >次の手順は、AEMバージョン6.1以降に適用されます。

   1. を使用して **AEM Web Console** (AEM Web Console)に移動 `https://serveraddress:serverport/system/console/configMgr`します。

   1. Select **Status - Pattern Detector** as shown in the figure below.

#### AEM 6.1インスタンスでのレポートの表示 {#aem-instances-report}

AEM 6.1のCSVレポートをダウンロードできます。これは保留中です。

#### レポートの重要度レベルについて {#importance-levels}

次の表に、様々なPattern DetectorとCloud Readiness Analyzerの重要度レベルの意味を示します。

| 重要度レベル | 説明 |
|--- |--- |
| 情報/0 | この検索結果は、情報を提供する目的で提供されます。 |
| アドバイザリ/1 | この結果、アップグレードに関する問題が発生する可能性があります。 さらに調査を行うことをお勧めします。 |
| メジャー/2 | この結果、アップグレードに関する問題に対処する必要がある可能性があります。 |
| 重大/3 | この結果、アップグレードの問題が発生する可能性が高く、機能やパフォーマンスの低下を防ぐために対処する必要があります。 |