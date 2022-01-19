---
title: AEM as a Cloud Serviceリリース2021.12.0の移行ツールのリリースノート
description: AEM as a Cloud Serviceリリース2021.12.0の移行ツールのリリースノート
feature: Release Information
source-git-commit: 2788db9338da5499b4a9e72ce196e4ae9857b5d5
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 19%

---


# AEM as a Cloud Serviceリリース2021.12.0の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2021.12.0の移行ツールのリリースノートの概要を説明します。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.22 のリリース日は 2021 年 12 月 1 日です。

### 新機能 {#what-is-new-bpa}

* 使用する ACS コモンのバージョンを検出し、レポートする機能。
* 1 つのグループ内のユーザーとサブグループの数を検出し、レポートする機能。
* 16MB を超える MongoDB のノードプロパティ値を検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa}

* 偽陰性を減らすために、基盤コンポーネントの検出を改善しました。
* AEM Formsのお客様向けに、に関する BPA メッセージ `EMAIL_PDF_SUBMIT_ACTION` AEM as a Cloud Serviceで使用できない問題を修正しました。


## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.7.10 のリリース日は 2021 年 12 月 8 日です。

### 新機能 {#what-is-new-ctt}

* コンテンツ転送ツールのインジェスト段階に切り替えが追加され、ユーザーが無効にできるようになりました [プリコピー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja) 取り込み中に 最適な取り込み速度を得るには、小さな移行セットの場合、または最後の取り込み以降に追加された BLOB が少ない場合、取り込み中のプリコピーを無効にする必要があります。
* ユーザーマッピングが更新され、2,000 人のユーザーを一度に取得できる改善された User Management API を使用するようになり、パフォーマンスが大幅に向上しました。
