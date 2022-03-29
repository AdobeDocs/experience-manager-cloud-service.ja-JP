---
title: AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: f8a87b00-52ce-42a6-a955-45cb14703b40
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.10.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、 [こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja) をクリックしてください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.10.0 の Cloud Manager のリリース日は 2021年10月14日（PT）です。


### 新機能 {#what-is-new}

* 今後の変更に備えて、ユーザーインターフェイスでは、既存のデプロイメントパイプラインが&#x200B;**フルスタック**&#x200B;パイプラインとして参照されラベル付けされるようになりました。

* パイプラインカードが更新され、実稼動パイプラインと実稼動以外のパイプラインの両方を 1 つのカードでまとめて表示するようになりました。ユーザーは、各パイプラインに関連付けられたアクションメニューから「実行」／「一時停止」／「再開」を直接選択することができます。

* デプロイメントマネージャーの役割を持つユーザーが、UI を使用して、セルフサービス方式で実稼働パイプラインを削除できるようになりました。

* パイプラインの追加操作と編集操作が更新され、使い慣れた最新のモーダルを使用するようになりました。

* Cloud Manager のユーザーが、ランディングページの右上にある「**フィードバック**」ボタンを使用して、ユーザーインターフェイスから直接フィードバックを送信できるようになりました。

* 年別の SLA グラフを Cloud Manager のユーザーインターフェイスからダウンロードできるようになりました。

* コード品質パイプラインと実稼動以外のパイプラインの実行で、より効率的なシャロー（浅い）クローン作成プロセスがビルドステップ中に使用されるようになりました。これにより、特に大きな Git リポジトリーを使用しているお客様の場合、ビルド時間が短縮されます。

* IP 許可リストを追加ウィザードで、設定可能な IP 許可リストの最大数に達した場合、ユーザーに通知されるようになりました。

* ログインしたユーザーがブラウザーで API を試すことができるインタラクティブなプレイグラウンドに関する説明が、Cloud Manager API ドキュメントに含まれるようになりました。詳しくは、[Cloud Manager API Playground](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) を参照してください。

* 「移動先」の選択オプションが無効になっている場合のプログラムカードのツールヒントがわかりやすくなりました。「実稼動環境が が存在しません。」と表示されるようになりました。

### バグの修正 {#bug-fixes}

* アドビスタッフがお客様の環境をリストアする場合に、環境が完全に動作可能になる前にリストアが完了したと見なされることが稀にありました。

* 環境の作成時に行われた特定の内部リクエストが再試行されていませんでした。

* ドメイン名の検証後にデプロイメント失敗エラーが発生した場合、アドビ担当者への連絡を促すようにエラーメッセージが修正されました。
