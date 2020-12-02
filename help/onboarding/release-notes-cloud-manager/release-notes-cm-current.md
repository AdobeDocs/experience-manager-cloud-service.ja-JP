---
title: Cloud Serviceリリース2020.11.0としてのAEMのCloud Managerのリリースノート
description: Cloud Serviceリリース2020.11.0としてのAEMのCloud Managerのリリースノート
translation-type: tm+mt
source-git-commit: 727dfd1d16a80620fba6db00289021ee5efae0fc
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 36%

---


# Cloud Service2020.11.0 {#release-notes}としてのAdobe Experience ManagerのCloud Managerのリリースノート

このページでは、AEMのCloud ManagerのリリースノートをCloud Service2020.11.0として概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2020.11.0のリリース日は2020年11月12日です。

## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* 新しいメニューオプション&#x200B;**ローカルログイン**が、環境カードおよび環境の概要ページの環境メニューオプションから利用できるようになりました。
詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md##login-locally)を参照してください。

* Cloud Managerの「**学習**」タブが更新され、UIの新しい画像が表示されました。

### バグ修正 {#bug-fixes-cloud-manager}

* ビルドの実行に先立っておこなわれる依存関係の読み込みには、Maven プラグインのダウンロードが必要でした。
* 言語を選択するための Cloud Manager フッターからのリンクが、正しい場所を指すようになりました。
* コードスキャン時に SonarQube プロセスが起動しないことがあります。これが自動検出され、再起動が試行されるようになりました。
* 既存のすべての実稼働パイプラインは、「エクスペリエンス監査」の手順で自動的に有効になります。