---
title: Adobe Experience Manager as a Cloud Service 2020.7.0 のリリースノート
description: Experience Manager 2020.7.0 のリリースノート
translation-type: tm+mt
source-git-commit: 74abf1c4cc6ae449a81e3e40d073bfcb23b056e8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 51%

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