---
title: Adobe Experience Manager as a Cloud Service 2020.5.0 のリリースノート
description: 「[!DNL Adobe Experience Manager] as a Cloud Service 2020.5.0 のリリースノート」
exl-id: 8570d2c3-6d55-4914-94b2-f5d162e0c285
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 100%

---

# AEM as a Cloud Service 2020.5.0 のリリースノート {#release-notes}

このページでは、Experience Manager as a Cloud Service 2020.5.0 の一般的なリリースノートの概要を説明します。

## リリース日 {#release-date}

[!DNL Experience Manager] as a Cloud Service 2020.5.0 のリリース日は 2020 年 5 月 7 日です。

## AEM Sites の新機能 {#aem-sites}

AEM as a Cloud Service リリース 2020.5.0 の AEM Sites の新機能と更新点について説明します。

* ページの一括移動およびロールアウトを非同期ジョブとして処理した後に、詳細なジョブ情報が利用できるようになりました。
* ページツリーのコピー／貼り付けを行う場合、ルートページのみを貼り付けるか、ツリーのサブページも貼り付けるかを選択できるようになりました。
* Adobe Target ワークスペースに書き出された AEM エクスペリエンスフラグメントは、Target 内で一意のオファータイプおよびオファーソースとして表示されるようになりました。
* MSM - *パブリッシュ*&#x200B;トリガーを使用すると、ライブコピーソース内のコンポーネントの削除イベント、つまりライブコピーソース内で削除されたライブコピー内のコンポーネントの削除を正常にロールアウトできるようになりました。
* MSM - ライブコピーコンポーネントは、ライブコピーソースから同じコンポーネントをロールアウトした後、名前が *_msm_moved* に変更されるようになりました。


## Cloud Manager の新機能 {#cloud-manager}

AEM as a Cloud Service リリース 2020.5.0 の Cloud Manager の新機能と更新点について説明します。

### 新機能 {#what-is-new}

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
