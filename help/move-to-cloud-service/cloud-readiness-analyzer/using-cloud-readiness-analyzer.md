---
title: Cloud Readiness Analyzerの使用
description: Cloud Readiness Analyzerの使用
translation-type: tm+mt
source-git-commit: 1739f81d4894f3e04cc4119f344a3bea5bd042d8
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 3%

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

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Cloud Readiness Analyzerをクリックすると ****、レポートを生成するツール開始が発生し、数分後にはAEMインスタンスでサマリレポートが使用できるようになります。

   >[!NOTE]
   >完全なレポートを表示するには、ページを下にスクロールする必要があります。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### サマリレポートでの結果の表示 {#viewing-the-results}

>[!IMPORTANT]
>Cloud Readiness Analyzerから生成されるレポートは、パターンディテクターに基づいています。 詳しくは、「 [パターンディテクター](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) 」を参照してください。

ページを下にスクロールして完全なサマリレポートを表示すると、レポート内で強調表示されている各カテゴリの次の情報を確認できます。

1. **重要度レベル**

   次の表に、様々なPattern DetectorとCloud Readiness Analyzerの重要度レベルの意味を示します。

   | 重要度レベル | 説明 |
   |--- |--- |
   | 情報/0 | この検索結果は、情報を提供する目的で提供されます。 |
   | アドバイザリ/1 | この結果、アップグレードに関する問題が発生する可能性があります。 さらに調査を行うことをお勧めします。 |
   | メジャー/2 | この結果、アップグレードに関する問題に対処する必要がある可能性があります。 |
   | 重大/3 | この結果、アップグレードの問題が発生する可能性が高く、機能やパフォーマンスの低下を防ぐために対処する必要があります。 |

1. **説明**：説明は、レポートされたカテゴリに関する情報を提供します。

1. **ドキュメントURL**&#x200B;ドキュメントURLを使用すると、関連するタイプの技術ドキュメントを表示できます。

1. **メッセージ** 1つのメッセージ内の検索結果の説明。

### CSV形式での結果の表示 {#viewing-the-results-csv}

サマリレポートはAEMユーザーインターフェイスで利用できます。 フルレポートは、リファクタリングプロセス中に役立つコンマ区切り値(CSV)形式でダウンロードできます。

サマリレポートのCSV形式を生成するには、次の手順に従います。

1. 
   1. Select the Adobe Experience Manager and navigate to tools -> **Operations** -> **Cloud Readiness Analyzer**.

1. レポートが使用可能になったら、 **CSVをクリックして** 、以下の図に示すように、カンマ区切り値(CSV)形式の完全なサマリレポートをダウンロードします。

![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)


#### AEM 6.1インスタンスでのレポートの表示 {#aem-instances-report}

次の手順に従って、Adobe Experience Manager (AEM) 6.1用のCSVレポートをダウンロードします。

1.Navigate to **Adobe Experience Manager Web Console
Configuration** using `https://serveraddress:serverport/system/console/configMgr`.

1. 次の図に示すように、「 **Status** 」タブを選択し、ドロップダウンリストから「 **Pattern Detector** 」を検索します。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. サマリレポートはzipフォルダーまたはJSON形式でダウンロードできます。


