---
title: Adobe Experience Manager as a Cloud Service 2020.5.0 のリリースノート
description: Experience Manager 2020.5.0 のリリースノート
translation-type: tm+mt
source-git-commit: 94a732f56929ad4af23855152e258f82ad61ee2c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 29%

---


# AEM as a Cloud Service 2020.5.0 のリリースノート {#release-notes}

Experience Manager as a Cloud Service 2020.5.0 の一般的なリリースノートの概要を次に説明します。

## Cloud Manager {#cloud-manager}

AEM as a Cloud Service リリース 2020.5.0 の Cloud Manager の新機能と更新点について説明します。

### 最新情報 {#what-is-new}

* クラウドサービスへの移行を計画する際に発生する可能性のある問題を特定するために、6つのコード品質ルールが追加されました。
* 互換性に関連する問題の数をまとめるための新しい指標 *「* クラウドサービスの互換性」が追加されました。
* 作成に失敗した環境は、作成に失敗した後、既に削除されていない限り、約24時間後に自動的に削除されるようになりました。
* アクティビティページとパイプライン実行リストAPIのパフォーマンスが向上しました。
* コード品質ログに、例外の完全なスタックトレースが含まれるようになりました。

### バグ修正  {#bug-fixes}

* 実稼働パイプラインの実行中に、誤解を招くカードが概要ページに表示されていました。
* DontImplementOrExtendProviderTypesPomCheck ** コードの品質ルールでNullポインタの例外が発生する場合があります。
* 概要ページの一部のドキュメントリンクが正しく機能しませんでした。
* Safariで、環境を作成ダイアログが正しくレンダリングされませんでした。
* 概要ページの一部のカードで、エンティティ名が正しく表示されませんでした。
* 場合によっては、ビルドイメージで顧客パッケージを正常にダウンロードできないことがあります。

