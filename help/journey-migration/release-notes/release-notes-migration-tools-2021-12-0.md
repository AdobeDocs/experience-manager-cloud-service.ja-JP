---
title: AEM as a Cloud Service リリース 2021.12.0 における移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2021.12.0 における移行ツールのリリースノート
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 100%

---

# AEM as a Cloud Service リリース 2021.12.0 における移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2021.12.0 の移行ツールのリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、 [こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja) をクリックしてください。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.22 のリリース日は 2021年12月1日（PT）です。

### 新機能 {#what-is-new-bpa}

* 使用する ACS Commons のバージョンを検出し、レポートする機能。
* 1 つのグループ内のユーザーとサブグループの数を検出し、レポートする機能。
* 16MB を超える MongoDB のノードプロパティ値を検出し、レポートする機能。

### バグの修正 {#bug-fixes-bpa}

* 偽陰性を減らすために、基盤コンポーネントの検出を改善しました。
* AEM Forms のお客様向けに、AEM as a Cloud Service で使用できない `EMAIL_PDF_SUBMIT_ACTION` に関する BPA メッセージングを修正しました。


## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.7.10 のリリース日は 2021年12月8日（PT）です。

### 新機能 {#what-is-new-ctt}

* コンテンツ転送ツールの取り込み段階に切替スイッチが追加され、ユーザーが取り込み中に [事前コピー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja) を無効にできるようになりました。最適な取り込み速度を得るには、小さな移行セットの場合、または最後の取り込み以降に追加された BLOB が数個しかない場合は、取り込み中の事前コピーを無効にする必要があります。
* ユーザーマッピングが更新され、2,000 人のユーザーを一度に取得できる改善された User Management API を使用するようになり、パフォーマンスが大幅に向上しました。
