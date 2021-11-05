---
title: AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: null
source-git-commit: c6c1d3bef85afda0ff86ec073d0ac91ad532c93b
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 20%

---

# Adobe Experience Manager as a Cloud Service 2021.10.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.10.0の Cloud Manager のリリース日は 2021 年 10 月 14 日です。


### 新機能 {#what-is-new}

* 今後の変更に備えて、既存のデプロイメントパイプラインが参照され、ユーザーインターフェイスで次のようにラベル付けされるようになりました。 **フルスタック** パイプライン。

* パイプラインカードが更新され、実稼働と非実稼働の両方のパイプラインを表示する単一の統合面が表示されるようになりました。ユーザーは、各パイプラインに関連付けられたアクションメニューから直接「実行/一時停止/再開」を選択できます。

* デプロイメントマネージャーの役割を持つユーザーが、UI を介してセルフサービス方式で実稼動パイプラインを削除できるようになりました。

* パイプラインエクスペリエンスの追加と編集が更新され、使い慣れた最新のモデルを使用できるようになりました。

* Cloud Manager のユーザーは、 **フィードバック** ボタンをクリックします。

* 年別の SLA グラフを Cloud Manager のユーザーインターフェイスからダウンロードできるようになりました。

* コード品質と非実稼動パイプラインの実行で、ビルド手順中により効率的な浅いクローン作成プロセスを使用するようになり、特に大規模な Git リポジトリを持つお客様のビルド時間が短縮されます。

* IP許可リストの追加ウィザードで、許可されている最大数に達した場合に、ユーザーに許可リストを送信するようになりました。

* Cloud Manager API ドキュメントに、ログインしたユーザーがブラウザーで API を試すことができる、インタラクティブなプレイグラウンドが含まれるようになりました。 詳しくは、 [Cloud Manager API プレイグラウンド](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) を参照してください。

* 「移動先」の下の選択オプションが無効になっている場合は、プログラムカードのツールチップがわかりやすくなります。 「実稼動環境が存在しません」と表示されるようになりました。

### バグ修正 {#bug-fixes}

* まれに、Adobe・スタッフがお客様の環境をリストアする場合、環境が完全に稼働する前にリストアが完了したと見なされました。

* 環境の作成中におこなわれた一部の内部リクエストが再試行されませんでした。

* ドメイン名の検証後にデプロイメントの失敗エラーが発生した場合、エラーメッセージが修正され、お客様にAdobe担当者への連絡をリクエストするようになりました。

