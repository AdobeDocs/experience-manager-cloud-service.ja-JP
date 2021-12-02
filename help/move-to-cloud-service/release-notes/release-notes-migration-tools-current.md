---
title: AEM as a Cloud Serviceリリース2021.12.0の移行ツールのリリースノート
description: AEM as a Cloud Serviceリリース2021.12.0の移行ツールのリリースノート
feature: Release Information
source-git-commit: 587258a831fb5cd3b3a23d1f891db8c2254a8d6b
workflow-type: tm+mt
source-wordcount: '163'
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
