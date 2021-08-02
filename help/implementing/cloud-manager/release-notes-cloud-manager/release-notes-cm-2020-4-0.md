---
title: AEM as a Cloud Service リリース 2020.4.0 の Cloud Manager のリリースノート
description: AEM as a Cloud Service リリース 2020.4.0 の Cloud Manager のリリースノート
feature: リリース情報
exl-id: 15665fb5-9444-416b-938a-45c31fdce5cf
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2020.4.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2020.4.0 の Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2020.4.0 の Cloud Manager のリリース日は 2020 年 4 月 9 日です。

## 新機能 {#whats-new-cloud-manager}

* 発行者の URL が、Cloud Manager UI の環境ページから利用できるようになりました。
* ナビゲーションが変更され、Cloud Manager の概要ページでユーザーがプログラムの編集、切り替え、追加が可能になりました。
* ユーザーが Cloud Manager ランディングページのプログラムカードからプログラムを編集できるように変更しました。
* 関連付けられた環境に対して、新しいパイプラインステータス「**パイプライン実行中**」が表示されます。
* パイプライン実行ページをわかりやすく改善しました。これには、パイプライン名（非実稼動パイプラインのみ）とタイプの表示、およびパイプラインのステータスが「処理中」、「キャンセル」、「失敗」のいずれであるかを示すバッジが含まれます。
* ユーザーエクスペリエンスを向上させ、「プログラム／環境」ボタンが無効になる理由を理解しやすくするためのツールヒント。
* 失敗した環境は、UI と API を使用して削除できるようになりました。
* git パスワードの生成に使用されるプロセスは、基盤となるサービス層の問題に対してより柔軟に対処できるようになりました。

### バグ修正 {#bug-fixes-cloud-manager}

* パイプライン実行の詳細ページのステージ環境へのリンクが、正しい場所に一貫してナビゲーションしていなかった。
* 環境作成プロセス内の個々のステップが、必要な時間より早くタイムアウトし、プロセスが失敗する。
* アーティファクトのメタデータをダウンロードする際のデッドロックを回避するため、ビルドコンテナで使用される Maven の設定を更新。
* 場合によっては、イメージのビルド手順で顧客パッケージを正常にダウンロードできない。
* 発生頻度の低い状況によっては、環境の削除が妨げられる場合がある。
* Experience Cloud の通知が一貫して受信されなかった。
