---
title: Cloud Serviceリリース2020.5.0としてのAEMのCloud Managerのリリースノート
description: Cloud Serviceリリース2020.5.0としてのAEMのCloud Managerのリリースノート
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 71%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.5.0 {#release-notes}

このページでは、AEMのCloud ManagerのリリースノートをCloud Service2020.5.0として概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2020.5.0のリリース日は2020年5月7日です。

## 新機能 {#whats-new-cloud-manager}

* Cloud Service への移行を計画する際に発生する可能性のある問題を特定できるように、6 つのコード品質ルールが追加されました。
* 互換性に関連する問題の数を集計するための新しい指標「*Cloud Service との互換性*」が追加されました。
* 作成に失敗した環境は、既に削除されていない場合、失敗の約 24 時間後に自動的に削除されるようになりました。
* アクティビティページとパイプライン実行リスト API のパフォーマンスが向上しました。
* コード品質ログに、例外の完全なスタックトレースが含まれるようになりました。

### バグ修正  {#bug-fixes}

* 実稼働パイプラインの実行中に、誤解を招くおそれのあるカードが概要ページに表示されていました。
* *DontImplementOrExtendProviderTypesPomCheck* コード品質ルールでヌルポインター例外が発生する場合がありました。
* 概要ページの一部のドキュメントリンクが正しく機能していませんでした。
* Safari で、環境を作成ダイアログが正しくレンダリングされていませんでした。
* 概要ページの一部のカードで、エンティティ名が正しく表示されていませんでした。
* 場合によっては、「イメージのビルド」で顧客パッケージを正常にダウンロードできないことがありました。
