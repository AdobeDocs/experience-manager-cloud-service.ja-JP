---
title: AEM as a Cloud Service Release 2022.7.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.7.0 の移行ツールのリリースノート
feature: Release Information
exl-id: bc8f1a80-867e-423a-9c03-4a53b1ebc57c
source-git-commit: a878afbfc3531ae1779ca16851bbda43cbc20b90
workflow-type: ht
source-wordcount: '430'
ht-degree: 100%

---

# AEM as a Cloud Service Release 2022.7.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.7.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.30 のリリース日は 2022年7月27日です。

### 新機能 {#what-is-new-bpa}

* BPA は、`/oak:index/lucene` および `/oak:index/damAssetLucene` を除く合計 Lucene インデックスである、移行可能な Lucene インデックスの合計サイズを検出して報告できるようになりました。
* カスタム i18n 辞書の使用を検出してレポートするための新しいパターンが BPA に追加されました。Translator.html は AEM as a Cloud Service では使用できず、Cloud Manager CI/CD パイプラインを介して Git からカスタム i18n 辞書をデプロイする必要があります。

### バグの修正 {#bug-fixes-bpa}

* BPA は、コンテンツフラグメントの元のレンディションが見つからないことをレポートしていました。コンテンツフラグメントにはレンディションがないので、コンテンツフラグメントではこのチェックがスキップされるようになりました。
* ACS Commons の調査結果をフィルタリングするオプションが BPA UI にありませんでした。この問題が修正されました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v2.0.12 のリリース日は 2022年7月19日です。

### 新機能 {#what-is-new-ctt}

* LDAP を介してログインしたユーザーは、CTT でチェックサイズとユーザーマッピング機能を実行できるようになりました。
* 抽出中の SSL/TLS 接続の問題のデバッグに役立つように、ユーザーは SSL ログを有効にできるようになりました。
* ソース接続の問題のデバッグに役立つように、Azure への接続に失敗した場合にサブドメイン名がログに表示されるようになりました。
* 事前コピー中の問題のデバッグに役立つように、事前コピーが失敗した場合に AzCopy ログが抽出ログに追加されるようになりました。
* チェックサイズの結果が古くならないようにするため、前のチェックサイズが完了した後でのみ、ユーザーはチェックサイズを再実行できるようになります。

### バグの修正 {#bug-fixes-ctt}

* 移行セットを削除して再作成すると、以前の抽出ログが表示されていました。この問題が修正されました。
* 「進行状況の表示」アクションボタンが、停止ステータスの移行セットで使用できませんでした。この問題が修正されました。
* 「削除」アクションボタンが、期限切れの抽出キーの移行セットで使用できませんでした。 この問題が修正されました。
* 複数の UI のバグを修正しました。

## Cloud Acceleration Manager {#cam-release}

### リリース日 {#release-date-cam}

Cloud Acceleration Manager のリリース日は 2022年7月15日です。

### 新機能 {#what-is-new-cam}

* Cloud Acceleration Manager で、自動取得に失敗した場合に取り込みを開始できるように、移行トークンを手動で取得できるようになりました。 顧客が CAM をブロックする IP 許可リストを設定している場合や、管理者以外のユーザーが取り込みを開始しようとすると、自動取り込みが失敗する場合があります。 詳しくは、[トラブルシューティング](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting)を参照してください。
* 移行の複雑さページの長い表が、使いやすく折りたたみ可能になりました。
