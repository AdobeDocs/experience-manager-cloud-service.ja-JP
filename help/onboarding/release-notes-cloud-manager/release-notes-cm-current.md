---
title: AEM as a Cloud Service Release 2021.4.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.4.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
translation-type: tm+mt
source-git-commit: 69694f2067c53667803d38bbf7bc752f3b3afac6
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 18%

---

# Adobe Experience Manager as a Cloud Service 2021.4.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.4.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2021.4.0のリリース日は2021年4月8日です。
次回のリリースは2021年5月6日に予定されています。

### 新機能 {#what-is-new-april}

* UIが更新され、プログラムワークフロー追加と編集がより直感的になりました。

* 必要な権限を持つユーザーが、UIを介してコマースエンドポイントを送信できるようになりました。

* 環境変数は、作成者または発行の特定のサービスに対してスコープできるようになりました。 AEMバージョン`2021.03.5104.20210328T185548Z`以上が必要です。

* パイプラインが設定されていない場合でも、**Gitを管理**&#x200B;ボタンがパイプラインカードに表示されます。

* Cloud Managerで使用されるAEMプロジェクトのアーキタイプのバージョンが、バージョン27に更新されました。

* Cloud Managerで作成されたAdobe I/Oデベロッパーコンソールのプロジェクトを誤って編集または削除できなくなりました。

* ユーザが新しい環境を追加すると、環境が作成された後は、別の領域に移動できないという通知が表示されます。

* 環境変数は、作成者または発行の特定のサービスに対してスコープできるようになりました。 AEMバージョン2021.03.5104.20210328T185548Z以上が必要です。

* 環境が削除されたときにパイプラインを開始したときのエラーメッセージが明確になりました。

* Eclipseプロジェクトで提供されるOSGiバンドルは、ルール`CQBP-84--dependencies`から除外されるようになりました。

### バグ修正 {#bug-fixes-cm-april}

* パイプラインのエクスペリエンス監査ページを編集する際に、スラッシュ`( / )`で始まる入力パスによって、ステップが保留状態のままになることはなくなりました。

* 新しい実稼動パイプラインが作成された場合、コンテンツ監査の上書きがユーザーによって追加されない場合、デフォルトのホームページは監査されませんでした。

* `CloudServiceIncompatibleWorkflowProcess`の問題は、ダウンロード可能な雑誌号CSVファイル内で誤った重大度になっていました。

* `Runmode`チェックは、非フォルダーノードで偽陽性を生み出していました。