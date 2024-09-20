---
title: AEM as a Cloud Service リリース 2024.09 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2024.09.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 0c16f264826a46907afc33c91a021e7696f5b7a8
workflow-type: ht
source-wordcount: '230'
ht-degree: 100%

---

# AEM as a Cloud Service リリース 2024.09.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2024.09.0 の移行ツールのリリースノートの概要を説明しています。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツトランスファーツール v3.0.20 のリリース日は 2024年8月28日（PT）です。

### 新機能 {#what-is-new-ctt}

* このリリースではユーザーが取り込まれなくなるので、ユーザーマッピングオプション機能は削除されました。
* 抽出および取り込み時のプリンシパルの移行を無効または有効にする OSGI 設定オプションが追加されました（デフォルト設定では有効になっています）

### バグ修正 {#bug-fixes-ctt}

* azcopy 設定で秘密鍵の保護を解除する際のエラーを防ぐために、CTT を改善しました
* 検証フェーズで AzCopy ログをコピーする際に、CTT がエラーを適切に処理するようになりました
* 抽出プロセス中に作成された azcopy ログディレクトリの変更

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.52 のリリース日は 2024年9月4日（PT）です。

### 新機能 {#what-is-new-bpa}

* AEM で JCR ベースのイベントを検出する新しいパターンが導入されました

### バグ修正 {#bug-fixes-bpa}

* 誤検出を修正しました
* Dispatcher からリダイレクトされた応答を処理する際の堅牢性が向上しました
* /apps/wcm/core/resources/languages/ 下のすべての言語について、NCC 検索がレポートされない点を修正しました
* ノードの複数プロパティに値がないかどうかを検出するチェックを追加しました

