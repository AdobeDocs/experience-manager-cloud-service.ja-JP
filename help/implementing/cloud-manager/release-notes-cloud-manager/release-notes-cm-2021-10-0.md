---
title: AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノート
feature: Release Information
source-git-commit: 14042b45b14f2c5575fc96979579bb0aaffc9a17
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 59%

---

# Adobe Experience Manager as a Cloud Service 2021.10.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.10.0の Cloud Manager のリリース日は 2021 年 10 月 14 日です。


### 新機能 {#what-is-new}

* 今後の変更に備えて、既存のデプロイメントパイプラインが参照され、ユーザーインターフェイスで次のようにラベル付けされるようになりました。 **フルスタック** パイプライン。

* パイプラインカードが更新され、実稼動パイプラインと実稼動以外のパイプラインの両方が 1 つのカードでまとめて表示されるようになりました。ユーザーは、各パイプラインに関連付けられたアクションメニューから「実行」／「一時停止」／「再開」を直接選択することができます。

* デプロイメントマネージャーの役割を持つユーザーが、UI を使用して、セルフサービス方式で実稼働パイプラインを削除できるようになりました。

* パイプラインの追加操作と編集操作が更新され、使い慣れた最新のモーダルを使用するようになりました。

* Cloud Manager のユーザーは、 **フィードバック** ボタンをクリックします。

* 年別の SLA グラフを Cloud Manager のユーザーインターフェイスからダウンロードできるようになりました。

* コード品質パイプラインと実稼動以外のパイプラインの実行で、より効率的なシャロー（shallow）クローン作成プロセスをビルドステップ中に使用するようになりました。これにより、特に大きな Git リポジトリーを使用しているお客様の場合、ビルド時間が短縮されます。

* IP許可リストの追加ウィザードで、許可されている最大数に達した場合に、ユーザーに許可リストを送信するようになりました。

* ログインしたユーザーがブラウザーで API を試すことができるインタラクティブなプレイグラウンドに関する説明が、Cloud Manager API ドキュメントに含まれるようになりました。詳しくは、[Cloud Manager API Playground](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) を参照してください。

* 「移動先」の選択オプションが無効になっている場合のプログラムカードのツールヒントがわかりやすくなりました。「実稼動環境が存在しません」と表示されるようになりました。

### バグ修正 {#bug-fixes}

* まれに、Adobe・スタッフがお客様の環境をリストアする場合、環境が完全に稼働する前にリストアが完了したと見なされました。

* 環境の作成中におこなわれた一部の内部リクエストが再試行されませんでした。

* ドメイン名の検証後にデプロイメントの失敗エラーが発生した場合、エラーメッセージが修正され、お客様にAdobe担当者への連絡をリクエストするようになりました。

