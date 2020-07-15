---
title: Adobe Experience Manager as a Cloud Service 2020.7.0 のリリースノート
description: Experience Manager 2020.7.0 のリリースノート
translation-type: tm+mt
source-git-commit: 22a025b49444e08d014e0459443751b5a3cfc7bf
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 34%

---


# AEM as a Cloud Service 2020.7.0 のリリースノート {#release-notes}

Experience Manager as a Cloud Service 2020.7.0 の一般的なリリースノートの概要を次に説明します。

## Cloud Manager の新機能 {#cloud-manager}

AEM as a Cloud Service リリース 2020.7.0 の Cloud Manager の新機能と更新点について説明します。

### リリース日 {#release-date}

[!UICONTROL Cloud Manager] バージョン 2020.7.0 のリリース日は 2020 年 7 月 09 日です。

### 新機能 {#what-is-new-cloud-manager}

* 環境ページのデザインが変更されました。

* 冬眠状態の環境が、冬眠状態の場合に、Cloud Managerで個別のステータスが表示されるようになりました。

* 環境ごとの環境変数の数が200に増えました。

* Cloud Manager ビルドコンテナで、Java 8 と Java 11 の両方がサポートされるようになりました。

### バグ修正 {#bug-fixes-cm}

* 環境が完全に作成される前に、Cloud ManagerからDeveloper Consoleへのリンクが正しくアクティブになっていませんでした。

* Cloud Managerから直接Developer Consoleへのリンクに、Sandboxプログラムの環境を非休止/休止にするオプションが表示されませんでした。

* The **Cancel** and **Save** options on the Non-Production Pipeline edit page were not always visible.

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* 新しいプログラムを作成する際に、推奨された名前が既存のプログラム名の重複を返す場合があります。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証で、1つずつエラーが発生しました。

* 何も存在しない場合、環境ページに発行セグメントとディスパッチャーセグメントが表示されることがありました。

## Cloud Readiness Analyzerの新機能 {#cloud-readiness-analyzer}

Cloud Readiness Analyzerの新機能と更新点について学ぶには、このセクションに従ってください。

### バグ修正 {#cra-bug-fixes}

* 以前のバージョンのCRAをAdobe Experience Manager(AEM) 6.1で実行できませんでした。管理者グループのユーザーに対する明示的なサポートが追加されました。

   詳しくは、「AEM 6.1へのCRAの [インストール](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) 」を参照してください。

* サマリレポートに表示される有効期限のタイムスタンプが正しくありませんでした。

* CRAは重複のカスタムコンポーネントを検出していました。

* AEM 6.1では、完全な検査を完了する前に、コンテンツ検査が終了していました。 例外処理が追加され、インスペクタは完全な検査が完了するまでスキップして続行できるようになりました。

