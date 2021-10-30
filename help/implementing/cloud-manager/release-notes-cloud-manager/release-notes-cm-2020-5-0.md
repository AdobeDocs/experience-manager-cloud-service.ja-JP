---
title: AEM as a Cloud Service リリース 2020.5.0 の Cloud Manager のリリースノート
description: AEM as a Cloud Service リリース 2020.5.0 の Cloud Manager のリリースノート
feature: リリース情報
exl-id: 9f534858-d18f-4224-8b94-9583a05aed95
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: ht
source-wordcount: '232'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2020.5.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2020.5.0 の Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2020.5.0 の Cloud Manager のリリース日は 2020 年 5 月 7 日です。

## 新機能 {#whats-new-cloud-manager}

* Cloud Service への移行を計画する際に発生する可能性のある問題を特定できるように、6 つのコード品質ルールが追加されました。
* 互換性に関連する問題の数を集計するための新しい指標「*Cloud Service との互換性*」が追加されました。
* 作成に失敗した環境は、既に削除されていない場合、失敗の約 24 時間後に自動的に削除されるようになりました。
* アクティビティページとパイプライン実行リスト API のパフォーマンスが向上しました。
* コード品質ログに、例外の完全なスタックトレースが含まれるようになりました。

### バグ修正  {#bug-fixes}

* 実稼動パイプラインの実行中に、誤解を招くカードが概要ページに表示されていました。
* *DontImplementOrExtendProviderTypesPomCheck* コード品質ルールでヌルポインター例外が発生する場合がありました。
* 概要ページの一部のドキュメントリンクが正しく機能していませんでした。
* Safari で、環境を作成ダイアログが正しくレンダリングされていませんでした。
* 概要ページの一部のカードで、エンティティ名が正しく表示されていませんでした。
* 場合によっては、「イメージのビルド」で顧客パッケージを正常にダウンロードできないことがありました。
