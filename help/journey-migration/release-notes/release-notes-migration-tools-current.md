---
title: AEM as a Cloud Service Release 2022.7.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.7.0 の移行ツールのリリースノート
feature: Release Information
source-git-commit: f84327096951772e1bed8656334841e1292d6bcf
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 28%

---

# AEM as a Cloud Service Release 2022.7.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.7.0 の移行ツールのリリースノートの概要を説明しています。

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

