---
title: AEM as a Cloud Service Release 2022.5.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.5.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: f84327096951772e1bed8656334841e1292d6bcf
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# AEM as a Cloud Service Release 2022.5.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.5.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.30 のリリース日は 2022年6月1日です。

### 新機能 {#what-is-new-bpa}

* CoralUI およびクラシックダイアログウィジェットを使用したカスタムダイアログウィジェットの使用状況を検出し、レポートする機能。カスタムのクラシックダイアログウィジェットを ExtJS から CoralUI に変換することをお勧めします。カスタム Coral ダイアログウィジェットを CoralUI3 に更新する必要があります。
* Assets Share Commons の使用状況とバージョンを検出し、レポートする機能。Asset Share Commons 1.x は AEM as a Cloud Service ではサポートされていないので、2.x にアップグレードする必要があります。
* バージョンのノード数を検出し、レポートする機能。
* カスタムレプリケーションエージェントまたは変更された標準のレプリケーションエージェントを検出してレポートする機能。

### バグの修正 {#bug-fixes-bpa}

* BPA が報告していた、NCC（非互換変更）、UMI（アップグレードの誤構成問題）、PCX（ページの複雑さ）の結果は誤検出でした。これらは修正されました。
* BPA は、任意のノード名の長さが 150 バイトを超えた場合にエラーを報告していました。ノードの親パスが 350 バイト以上の場合にのみ、エラーを検出するように修正されました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v2.0.10 のリリース日は 2022 年 6 月 2 日です。

### 新機能 {#what-is-new-ctt}

* コンテンツ転送ツール（CTT）は、Cloud Acceleration Manager と連携してコンテンツ転送プロセス全体を合理化するように進化しました。CTT は、コンテンツ抽出の実行に重点を置くようになりました。CTT 取り込みサービスが Cloud Acceleration Manager に統合されました。この変化によって得られるメリットは次のとおりです。
   * セルフサービス方式で、移行セットを 1 回抽出し、同時に複数の環境に取り込めます。
   * 読み込み状態、ガードレール、エラー処理が改善され、ユーザーエクスペリエンスが向上しました。
   * 取り込みログは永続化され、常にトラブルシューティングに使用できます。

## Cloud Acceleration Manager {#cam-release}

### リリース日 {#release-date-cam}

Cloud Acceleration Manager のリリース日は 2022年6月2日（PT）です。

### 新機能 {#what-is-new-cam}

* Cloud Acceleration Manager では、コンテンツ転送を開始および管理して、お客様の AEM インスタンス（オンプレミスまたは Adobe Managed Services）から AEM as a Cloud Service に移行する機能を、移行プロジェクトの一環として提供するようになりました。詳しくは、[コンテンツ移行カードの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=ja#content-transfer)を参照してください。
