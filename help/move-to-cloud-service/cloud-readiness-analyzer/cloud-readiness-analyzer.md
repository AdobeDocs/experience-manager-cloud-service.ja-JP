---
title: クラウドサービスへの移行の複雑さの評価
description: クラウドサービスへの移行の複雑さの評価
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Cloud Readiness Analyzer {#accesing-complexity}

## 概要 {#overview}

Cloud Readiness Analyzer(CRA)を使用すると、次のパターンを検出することで、既存のAEMインスタンスがクラウドサービスに移行する準備ができているかどうかを確認できます。

* クラウドサービスで現在サポートされていないAEM 6.xの機能を使用する

* クラウドサービスへの移行の影響を受ける特定のルールに違反する

>[!NOTE]
>CRAの出力は、クラウドサービスへの移行に必要な開発作業の評価を高速化します。

## Cloud Readiness Analyzerのセットアップ {#setting-up-cra}

CRAは、XX以上のAEMソースバージョンで動作するパッケージとしてリリースされ、クラウドサービスへの移行を検討しています。

このツールは、ソフトウェア配布ポータルで入手でき、Package Managerを使用してインストールできます。

### Cloud Readiness Analyzerの使用 {#using-cra}

>[!NOTE]
> CRAは、ローカル開発インスタンスを含む、任意の環境で実行できます。

>[重要]
>ただし、検出率を高め、ビジネスクリティカルなインスタンスの遅延を回避するために、ユーザーアプリケーション、コンテンツおよび設定の領域で実稼働環境にできる限り近いステージング環境で実行することをお勧めします

### Cloud Readiness Analyzerでの出力の表示 {#viewing-output-cra}


1. を使用して **Adobe Experience Manager Web Console Configuration** ( `https://serveraddress:serverport/system/console/configMgr`Adobe Experience Manager Web Console Configuration)に移動し、AEM Webコンソールに移動します。

1. 次の画像に示すように、「ステータス — Cloud Readiness Analyzer」を選択します。

1. また、リアクティブなテキストベースまたは通常のJSONインターフェイスを使用して出力を表示することもできます。

>[!NOTE]
> これらの方法の詳細については、 [パターン検出](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) (Pattern Detector)を参照してください。 CRAを使用する準備が整ったら、このセクションを追加する必要があります。

## クラウドの準備に関する次の手順 {#the-next-steps}

クラウドサービスの準備状況に関する詳細を取得するには、CRAの出力を評価する必要があります。

次の手順に従って、ファイルを返送します。

1. AEM Webコンソールに移動し、次の画像のようにxxファイルをダウンロードします。

1. DayCareチケットを開き、次の方法でアドビにファイルを送信します。
   1. Daycareで、 **Cloud Readiness Analyzerの出力という名前のサポートチケットのログ**
   1. 出力ファイルのチケットへの添付

