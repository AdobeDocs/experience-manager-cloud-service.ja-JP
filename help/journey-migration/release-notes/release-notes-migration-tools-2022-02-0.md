---
title: AEM as a Cloud Service Release 2022.2.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.2.0 の移行ツールのリリースノート
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 94%

---

# AEM as a Cloud Service Release 2022.2.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.2.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.24 のリリース日は 2022 年 2 月 01 日です。

### 新機能 {#what-is-new-bpa}

* スマートタグを使用するアセットと使用しないアセットの数を検出してレポートできるようになりました。
* 使用されているコアコンポーネントのバージョンを検出しレポートできるようになりました。
* BPA が実行されたソース層（オーサーまたはパブリッシュ）の種類を検出してレポートできるようになりました。

### バグの修正 {#bug-fixes-bpa}

* BPA のサイズ決定ロジックがより高速かつ効率的になりました。
* 一部のシナリオで、BPA が実行時に分析済みのカウントを増分しないことがありました。この問題が修正されました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.8.6 のリリース日は 2022 年 2 月 03 日です。

### 新機能 {#what-is-new-ctt}

* コンテンツの検証 - コンテンツ転送ツールで抽出されたすべてのコンテンツがターゲットインスタンスに正常に取り込まれたかどうかをユーザーが確実に判断できます。この機能を使用するには、 `System Console` ソースAEM環境の 詳しくは、[コンテンツ転送の検証 - はじめに](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=ja#getting-started)を参照してください。

### バグの修正 {#bug-fixes-ctt}

* ユーザーマッピングでは大文字と小文字が区別されるので、一部のユーザーがマッピングされませんでした。この問題が修正されました。ユーザーマッピングでは、大文字と小文字が区別されなくなりました。
