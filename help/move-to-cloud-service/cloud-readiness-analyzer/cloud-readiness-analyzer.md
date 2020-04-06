---
title: クラウドサービスへの移行の複雑さの評価
description: クラウドサービスへの移行の複雑さの評価
translation-type: tm+mt
source-git-commit: 83f7a1d57fae92e6ce15e4d9d6e00682d4596d05

---


# クラウドサービスへの移行の複雑さの評価 {#accesing-complexity}

## 概要 {#overview}

Cloud Readiness Analyzer(CRA)を使用すると、次のパターンを検出することで、既存のAEMインスタンスがクラウドサービスに移行する準備ができているかを確認できます。

* クラウドサービスで現在サポートされていないAEM 6.x機能の使用

* クラウドサービスへの移行の影響を受ける特定のルールに違反する

>[!NOTE]
>CRAの出力は、クラウドサービスへの移行に必要な開発作業の評価を高速化します。

## Cloud Readiness Analyzerの設定 {#setting-up-cra}

CRAは、XX以降のAEMソースバージョンで動作するパッケージとしてリリースされ、クラウドサービスへの移行を検討しています。

Software Distribution Portalで入手でき、Package Managerを使用してインストールできます。

### Cloud Readiness Analyzerの使用 {#using-cra}

>[!NOTE]
> CRAは、ローカル開発インスタンスを含む、どの環境でも実行できます。

>[重要]
>ただし、検出率を高め、ビジネスクリティカルなインスタンスの遅延を回避するために、ユーザーアプリケーション、コンテンツ、設定の領域で実稼働環境にできる限り近いステージング環境で実行することをお勧めします

### Cloud Readiness Analyzerでの出力の表示 {#viewing-output-cra}


1. を使用して、 **Adobe Experience Manager Web Console Configurationに移動し、AEM Web Consoleに移動します**`https://serveraddress:serverport/system/console/configMgr`。

1. 次の画像に示すように、「Status - Cloud Readiness Analyzer」を選択します。

1. また、リアクティブなテキストベースの表示や、通常のJSONインターフェイスを使用して出力を生成することもできます。

>[!NOTE]
> これらの方法の [詳細については](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) 、『パターンディテクター』を参照してください)。 CRAを使用する準備が整ったら、このセクションを追加する必要があります。

## クラウドの準備に関する次の手順 {#the-next-steps}

クラウドサービスの準備状況に関する詳細を入手するには、CRAの出力をアドビが評価する必要があります。

次の手順に従って、ファイルを返送します。

1. AEM Web Consoleに移動し、次の画像に示すようにxxファイルをダウンロードします。

1. DayCareチケットを開き、次の方法でアドビにファイルを送信します。
   1. Daycareでのサポートチケットのログ( **Cloud Readiness Analyzer Output)**
   1. 出力ファイルのチケットへの添付

