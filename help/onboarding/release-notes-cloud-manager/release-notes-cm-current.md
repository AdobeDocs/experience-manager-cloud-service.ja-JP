---
title: Cloud Serviceリリース2020.10.0としてのAEMのCloud Managerのリリースノート
description: Cloud Serviceリリース2020.10.0としてのAEMのCloud Managerのリリースノート
translation-type: tm+mt
source-git-commit: d992646fd89a4e502d74533f5fa2bbe994a9ab97
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 48%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.10.0 {#release-notes}

このページでは、AEMのCloud ManagerのリリースノートをCloud Service2020.10.0として概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2020.10.0のリリース日は2020年10月1日です。

## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* Cloud Managerビルドコンテナで、Java 8またはJava 11を使用したプロジェクトのコンパイルがサポートされるようになりました。 Java 11のサポートは、Mavenツールチェーンシステムによって提供されます。

* 環境ごとの環境変数の数が 200 に増えました。

* 概要ページの環境カードには、最大3環境のリストが表示されます。 「すべてを **表示** 」ボタンを選択して環境の概要ページに移動し、環境の完全なリストを含む表を表示できます。
詳しくは、「 [環境の](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 表示」を参照してください。


### バグ修正 {#bug-fixes-cloud-manager}

* 環境が完全に作成される前に、Cloud Manager から開発者コンソールへのリンクが正しくアクティブになっていませんでした。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示していませんでした。

* 非実稼働パイプライン編集ページの「キャンセル」ボタンと「保存」ボタンが必ずしも表示されていなかった問題を修正しました。

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* 新しいプログラムを作成する際に、推奨名が既存のプログラム名と重複する場合がありました。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証が、1 つずれていました。

* 何も存在しない場合、環境ページにパブリッシュセグメントと Dispatcher セグメントが表示されることがありました。