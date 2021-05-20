---
title: AEM as a Cloud Service Release 2021.4.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.4.0 Cloud Manager のリリースノート
feature: リリース情報
source-git-commit: e2d4bb7649fad3ee172c6f049ecfdedc71417ee2
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 18%

---


# Adobe Experience Manager as a Cloud Service 2021.4.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.4.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as aCloud Service2021.4.0のCloud Managerのリリース日は2021年4月8日です。
次回のリリースは2021年5月6日に予定されています。

### 新機能 {#what-is-new-april}

* プログラムの追加と編集ワークフローのUIが更新され、より直感的になりました。

* 必要な権限を持つユーザーが、UIを使用してコマースエンドポイントを送信できるようになりました。

* 環境変数を、オーサーまたはパブリッシュのいずれかの特定のサービスに対してスコープできるようになりました。 AEMのバージョン`2021.03.5104.20210328T185548Z`以降が必要です。

* パイプラインが設定されていない場合でも、「 **Gitを管理** 」ボタンがパイプラインカードに表示されます。

* Cloud Managerで使用されるAEMプロジェクトのアーキタイプのバージョンが、バージョン27に更新されました。

* Cloud Managerで作成されたAdobe I/O開発者コンソールのプロジェクトは、意図せず編集または削除できなくなりました。

* ユーザーが新しい環境を追加すると、環境を作成した後は別の地域に移動できないという通知が表示されます。

* 環境変数を、オーサーまたはパブリッシュのいずれかの特定のサービスに対してスコープできるようになりました。 AEMバージョン2021.03.5104.20210328T185548Z以降が必要です。

* 環境が削除されたときにパイプラインを開始する際に発生するエラーメッセージがわかりやすくなりました。

* Eclipseプロジェクトで提供されるOSGiバンドルがルール`CQBP-84--dependencies`から除外されるようになりました。

### バグ修正 {#bug-fixes-cm-april}

* パイプラインのエクスペリエンス監査ページを編集する際に、スラッシュ`( / )`で始まる入力パスによって、ステップが保留中ステータスのままにならなくなりました。

* 新しい実稼動パイプラインが作成された際に、ユーザーがコンテンツ監査の上書きを追加しなかった場合、デフォルトのホームページは監査されませんでした。

* `CloudServiceIncompatibleWorkflowProcess`の問題は、ダウンロード可能な問題のCSVファイルで間違った重大度を持っていました。

* `Runmode`チェックが、非フォルダーノードで偽陽性を生成していました。