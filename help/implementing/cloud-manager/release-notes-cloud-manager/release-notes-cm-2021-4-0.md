---
title: AEM as a Cloud Service Release 2021.4.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.4.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: a11ebe0e-2872-4fde-acc0-5babc6b01e1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.4.0 の Cloud Manager のリリースノート {#release-notes}

ここでは、AEM as a Cloud Service Release 2021.4.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.4.0 Cloud Manager のリリース日は 2021 年 4 月 8 日です。次回のリリースは 2021年5月6日（PT）に予定されています。

### 新機能 {#what-is-new-april}

* プログラムの追加と編集ワークフローの UI がアップデートされ、より直感的になりました。

* 必要な権限を持つユーザーが、UI を使用してコマースエンドポイントを送信できるようになりました。

* 環境変数を、オーサーまたはパブリッシュのいずれかの特定のサービスに対して適用できるようになりました。AEM バージョン `2021.03.5104.20210328T185548Z` 以降が必要です。

* パイプラインが設定されていない場合でも、「**Git を管理**」ボタンがパイプラインカードに表示されます。

* Cloud Manager で使用される AEM プロジェクトのアーキタイプのバージョンが 27 にアップデートされました。

* Cloud Manager で作成された Adobe I/O デベロッパーコンソールのプロジェクトは、意図せずに編集または削除できなくなりました。

* 新しい環境を追加すると、作成された環境は別の地域に移動できないという通知が表示されます。

* 環境変数を、オーサーまたはパブリッシュのいずれかの特定のサービスに対して適用できるようになりました。AEM バージョン 2021.03.5104.20210328T185548Z 以降が必要です。

* 環境が削除されたときにパイプラインを開始する際に表示されるエラーメッセージがわかりやすくなりました。

* Eclipse プロジェクトで提供される OSGi バンドルがルール `CQBP-84--dependencies` から除外されるようになりました。

### バグ修正 {#bug-fixes-cm-april}

* パイプラインのエクスペリエンス監査ページを編集する際に、スラッシュ `( / )` で始まる入力パスによってこの手順が保留中ステータスのままになることがなくなりました。

* 新しい実稼動パイプラインが作成された際に、ユーザーがコンテンツ監査の上書きを追加しなかった場合、デフォルトのホームページは監査されませんでした。

* `CloudServiceIncompatibleWorkflowProcess` の問題は、ダウンロード可能な問題の CSV ファイルで間違った重大度を持っていました。

* `Runmode` チェックが、フォルダー以外のノードで偽陽性を生成していました。
