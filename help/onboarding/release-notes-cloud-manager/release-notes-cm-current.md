---
title: Cloud Serviceリリース2020.11.0としてのAEMのCloud Managerのリリースノート
description: Cloud Serviceリリース2020.11.0としてのAEMのCloud Managerのリリースノート
translation-type: tm+mt
source-git-commit: 65752c7c51538de27aa2b21695e8eb6c6695a5f5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 4%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.11.0 {#release-notes}

このページでは、AEMのCloud ManagerのリリースノートをCloud Service2020.11.0として概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2020.11.0のリリース日は2020年11月12日です。

## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* 環境カードおよび環境の概要ページの環境メニューオプションから、新しいメニューオプション **** 「ローカルにログイン」を使用できるようになりました。

* Cloud Managerの「 **Learn** 」タブが更新され、UIの新しい画像が表示されるようになりました

### バグ修正 {#bug-fixes-cloud-manager}

* ビルドの実行前に行われた依存関係の読み込みには、Mavenプラグインのダウンロードが必要です。
* Cloud Managerのフッターから言語を選択するリンクが、正しい場所に移動するようになりました。
* コードのスキャン中に、SonarQubeプロセスが開始しないことがあります。 これは自動検出され、再起動が試行されます。
* 既存のすべての実稼働パイプラインは、「エクスペリエンス監査」の手順で自動的に有効になります。