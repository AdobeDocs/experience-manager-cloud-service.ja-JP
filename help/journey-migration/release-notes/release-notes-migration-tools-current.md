---
title: AEM as a Cloud Serviceリリース 2022.2.0 の移行ツールのリリースノート
description: AEM as a Cloud Serviceリリース 2022.2.0 の移行ツールのリリースノート
feature: Release Information
source-git-commit: 8876702f1a172282fd1ff46387ade2a45e187fed
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 18%

---


# AEM as a Cloud Serviceリリース 2022.2.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.2.0 の移行ツールのリリースノートの概要を説明します。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.24 のリリース日は 2022 年 2 月 01 日です。

### 新機能 {#what-is-new-bpa}

* スマートタグを使用するアセットの数、およびスマートタグを使用しないアセットの数を検出してレポートする機能。
* 使用されているコアコンポーネントのバージョンを検出してレポートする機能。
* BPA が実行されたソース層（オーサー層またはパブリッシュ層）の種類を検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa}

* BPA サイズ設定ロジックがより高速で効率的になりました。
* BPA は、実行時に分析済みのカウントを増分しないことがありました。 この問題が修正されました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.8.6 のリリース日は 2022 年 2 月 03 日です。

### 新機能 {#what-is-new-ctt}

* コンテンツの検証 — コンテンツ転送ツールで抽出されたすべてのコンテンツがターゲットインスタンスに正常に取り込まれたかどうかを確実に判断できます。 この機能を使用するには、 `System Console` ソースAEM環境の 参照： [コンテンツ転送の検証 — はじめに](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) を参照してください。

### バグ修正 {#bug-fixes-ctt}

* ユーザーマッピングでは大文字と小文字が区別されるので、一部のユーザーがマッピングされませんでした。 この問題が修正されました。ユーザーマッピングでは、大文字と小文字が区別されなくなりました。

