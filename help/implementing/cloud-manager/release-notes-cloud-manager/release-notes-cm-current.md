---
title: AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 3b1ff5f1715cd18228a9b7e5c57b0f3d84ee0eb0
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 21%

---

# Adobe Experience Manager as a Cloud Service 2021.10.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.10.0の Cloud Manager のリリース日は 2021 年 10 月 14 日です。
次回のリリースは 2021 年 11 月 4 日に予定されています。

### 新機能 {#what-is-new}

* 今後の変更に備えて、既存のデプロイメントパイプラインが **フルスタック** パイプラインとして参照およびラベル付けされるようになりました。

* パイプラインカードが更新され、実稼動パイプラインと非実稼動パイプラインの両方を表示する単一の統合面が表示され、各パイプラインに関連付けられたアクションメニューから直接「実行/一時停止/再開」を選択できます。

* デプロイメントマネージャーの役割を持つユーザーが、UI を使用して、セルフサービス方式で実稼動パイプラインを削除できるようになりました。

* パイプラインエクスペリエンスの追加と編集が更新され、使い慣れた最新のモデルを使用できるようになりました。

* Cloud Manager のユーザーは、ランディングページの右上にある **フィードバック** ボタンを使用して、ユーザーインターフェイスから直接フィードバックを送信できるようになりました。

* 年別の SLA グラフを Cloud Manager のユーザーインターフェイスからダウンロードできるようになりました。

* コード品質と非実稼動パイプラインの実行で、ビルド手順中により効率的な浅いクローン作成プロセスを使用できるようになり、特に大きな Git リポジトリを持つお客様のビルド時間が短縮されます。

* 「IP許可リストの追加」ウィザードで、許可されている IP許可リストの最大数に達した場合に、ユーザーに通知が表示されるようになりました。

* Cloud Manager API ドキュメントに、ログインしたユーザーがブラウザーで API を試すことができる、インタラクティブなプレイグラウンドが含まれるようになりました。 [Cloud Manager API プレイグラウンド ](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) を参照してください。

* 「移動先」の選択オプションが無効になっている場合は、プログラムカードのツールチップがわかりやすくなります。 「実稼動環境が存在しません」と表示されるようになりました。

### バグ修正 {#bug-fixes}

* まれに、Adobe・スタッフがお客様の環境をリストアする場合、環境が完全に稼働する前にリストアが完了したと見なされました。

* 環境の作成中におこなわれた一部の内部要求が再試行されていませんでした。

