---
title: AEM as a Cloud Service Release 2021.3.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.3.0 Cloud Manager のリリースノート
translation-type: tm+mt
source-git-commit: 36e5e90785a1bc9a4f4f8d4febd462e00252a0ea
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 16%

---


# Adobe Experience Manager as a Cloud Service 2021.3.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.3.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2021.3.0のリリース日は2021年3月11日です。
次回のリリースは2021年4月8日に予定されています。

## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* [IP許可リスト](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL証明書](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)、[カスタムドメイン名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)の既存のカスタムドメイン名を設定している環境のお客様は、既存の設定に関するメッセージを表示し、UIを使用して自己提供できます。

* 必要な権限を持つユーザーは、プログラムを編集でき、セルフサービスの方法で次の操作を行うことができます。
   * アセットを追加持つ既存のプログラム（またはその逆）に対するサイトソリューション
   * サイトとアセットの両方を含む既存のプログラムからサイト（またはアセット）を削除します。
   * 2つ目追加は、使用されていないソリューションのエンタイトルメントを既存のプログラムに対して、または新しいプログラムとして使用することです。

* パイプライン実行画面とアクティビティ画面の両方に、AEM Push Update」ラベルが表示されるようになりました。

* 環境が休止状態になっているが、AEMの更新も使用可能な場合、「休止状態」のステータスは「利用可能な更新」よりも優先されます。

* 統合シェルのユーザープロファイルアイコン（右上）に移動した後、「表示Cloud Managerロール」オプションを選択すると、Cloud Managerロールを表示できるようになりました。

* ラベル「Application for Approval」が「Production Approval」にラベル変更され、より明確になりました。

* 「Version」ラベルが、実稼働パイプラインの実行画面で「Git Tag」に再ラベル付けされました。

* 重要な指標が定義したしきい値を満たさない場合の動作を定義するラベルは、実際の動作（「すぐにキャンセル」および「すぐに承認」）を反映するようにラベルが変更されました。

* AEMCloud ServiceSDKのバージョン`2021.3.4997.20210303T022849Z-210225`に基づいて、クラスとメソッドの非推奨リストが更新されました。

* Cloud Manager実稼働パイプラインに、カスタムUIテスト機能が含まれるようになりました。

### バグ修正 {#bug-fixes}

* AEMのプッシュアップグレード中に、パッケージのバージョン管理がスキップされる場合がありました。

* 他のパッケージにパッケージが埋め込まれた場合に、品質の問題が正しく検出されない場合がありました。

* 不明確な状況では、プログラムダイアログを開いたときに生成される追加デフォルトのプログラム名は、既存のプログラム名の重複の場合があります。

* 場合によっては、パイプラインの開始直後にパイプラインの実行ページから移動すると、実際に実行が開始したにもかかわらず、アクションが失敗したことを示すエラーメッセージが表示されます。

* お客様のビルドで無効なパッケージが生成された場合、ビルド手順が不必要に再開されました。

* 場合によっては、IP許可リストの横に緑色の「アクティブ」ステータスが表示される場合があります。このステータスは、その設定が展開されていない場合でも表示されます。

* 「エクスペリエンス監査」ステップで既存のすべての実稼働パイプラインが自動的に有効になります。