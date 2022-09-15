---
title: AEM as a Cloud Service Release 2022.7.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.7.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 05adf79b66c36e6354fe95fe4d5f654b49980589
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 23%

---

# AEM as a Cloud Service Release 2022.7.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.7.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.30 のリリース日は 2022 年 7 月 27 日です。

### 新機能 {#what-is-new-bpa}

* BPA は、移行可能な Lucene インデックスの合計サイズ（Total Lucene Index：除く）を検出し、報告できるようになりました `/oak:index/lucene` および `/oak:index/damAssetLucene`.
* カスタム i18n 辞書の使用を検出してレポートするための新しいパターンが BPA に追加されました。 AEMas a Cloud Serviceでは Translator.html を使用できません。また、Cloud Manager CI/CD パイプラインを通じて、カスタム i18n 辞書を Git からデプロイする必要があります。

### バグ修正 {#bug-fixes-bpa}

* BPA は、コンテンツフラグメントの見つからない元のレンディションに関するレポートを作成していました。 コンテンツフラグメントにはレンディションがないので、コンテンツフラグメントではこのチェックがスキップされるようになりました。
* ACS Commons の結果をフィルターするオプションが BPA UI に見つかりませんでした。 この問題が修正されました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v2.0.12 のリリース日は 2022 年 7 月 19 日です。

### 新機能 {#what-is-new-ctt}

* LDAP を介してログインしたユーザーは、CTT でチェックサイズとユーザーマッピング機能を実行できるようになりました。
* 抽出中の SSL/TLS 接続の問題をデバッグできるように、ユーザーは SSL ログを有効にできます。
* ソース接続の問題のデバッグに役立つように、Azure への接続に失敗した場合にサブドメイン名がログに表示されるようになりました。
* 事前コピー中の問題のデバッグに役立つように、事前コピーが失敗した場合、AzCopy ログが抽出ログに追加されるようになりました。
* チェックサイズの結果が古くならないようにするため、以前のチェックサイズが完了した後でのみ、ユーザーはチェックサイズを再実行できます。

### バグ修正 {#bug-fixes-ctt}

* 移行セットを削除して再作成した後、以前の抽出ログが表示されていました。 この問題が修正されました。
* 「進行状況の表示」アクションボタンが、「停止」ステータスの移行セットで使用できなかった問題を修正しました。 この問題が修正されました。
* 抽出キーの期限切れの移行セットで、削除アクションボタンが使用できなかった問題を修正しました。 この問題が修正されました。
* 複数の UI のバグを修正しました。

## Cloud Acceleration Manager {#cam-release}

### リリース日 {#release-date-cam}

Cloud Acceleration Manager のリリース日は 2022 年 7 月 15 日です。

### 新機能 {#what-is-new-cam}

* Cloud Acceleration Manager で、自動取得に失敗した場合に取り込みを開始できるように、移行トークンを手動で取得できるようになりました。 顧客が CAM をブロックする IP 許可リストを設定している場合や、管理者以外のユーザーが取り込みを開始しようとすると、自動取り込みが失敗する場合があります。 参照： [トラブルシューティング](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) を参照してください。
* 移行の複雑さページの長いテーブルが、使いやすく折りたたみ可能になりました。
