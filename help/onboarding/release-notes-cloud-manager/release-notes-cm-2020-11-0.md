---
title: AEM as a Cloud Service リリース 2020.11.0 の Cloud Manager のリリースノート
description: AEM as a Cloud Service リリース 2020.11.0 の Cloud Manager のリリースノート
translation-type: tm+mt
source-git-commit: 79af82d1589108e7a8953e29a5d0f0169920585c
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 2020.11.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2020.11.0 の Cloud Manager リリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2020.11.0 の Cloud Manager のリリース日は 2020 年 11 月 12 日です。

## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* 新しい「**ローカルログイン**」メニューオプションが、環境カードおよび環境の概要ページの環境メニューオプションから利用できるようになりました。
詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md#login-locally)を参照してください。

* Cloud Manager の「**学習**」タブが更新され、UI に新しい画像が追加されました。

### バグ修正 {#bug-fixes-cloud-manager}

* ビルドの実行に先立っておこなわれる依存関係の読み込みには、Maven プラグインのダウンロードが必要でした。
* 言語を選択するための Cloud Manager フッターからのリンクが、正しい場所を指すようになりました。
* コードスキャン時に SonarQube プロセスが起動しないことがあります。これが自動検出され、再起動が試行されるようになりました。
* 「エクスペリエンス監査」ステップで既存のすべての実稼働パイプラインが自動的に有効になります。
