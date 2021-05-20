---
title: AEM as a Cloud Service Release 2021.3.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.3.0 Cloud Manager のリリースノート
feature: リリース情報
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 84a97f09402602df33c8f0494feed57fdb510add
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 16%

---

# Adobe Experience Manager as a Cloud Service 2021.3.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.3.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as aCloud Service2021.3.0のCloud Managerのリリース日は2021年3月11日です。

## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* [IP許可リスト](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL証明書](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)および[カスタムドメイン名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)の既存の環境のお客様には、既存の設定に関するメッセージが表示され、UIを介して自己提供できます。

* 必要な権限を持つユーザーがプログラムを編集でき、セルフサービス方式で次の操作を実行できるようになりました。
   * Assetsを使用する既存のプログラムにSitesソリューションを追加する（またはその逆）。
   * SitesとAssetsの両方を含む既存のプログラムからSitesまたはAssetsを削除します。
   * 2つ目の未使用のソリューション権利を既存のプログラムまたは新しいプログラムに追加します。

* **パイプライン** 実行画面とアクティビティ画面の両方にAEM Push Updatelabelが表示されるようになりました。

* 環境が休止状態になっていて、AEMの更新も使用可能な場合は、**Hevernated**&#x200B;ステータスが&#x200B;**Update available**&#x200B;よりも優先されます。

* ユーザーは、統合シェルのユーザープロファイルアイコン（右上）に移動した後、「Cloud Managerの役割を表示」オプションを選択することで、Cloud Managerの役割を表示できるようになりました。

* ラベル&#x200B;**承認の申請**&#x200B;が&#x200B;**実稼動の承認**&#x200B;に変更され、より明確になりました。

* 実稼動パイプラインの実行画面で、**Version**&#x200B;ラベルが&#x200B;**Gitタグ**&#x200B;にリラベルされました。

* 重要な指標が定義されたしきい値を満たさない場合の動作を定義するラベルが、実際の動作を反映するように再ラベル付けされました。**直ちにキャンセル**&#x200B;および&#x200B;**直ちに承認**&#x200B;します。

* クラスおよびメソッドの廃止リストは、AEMCloud ServiceSDKのバージョン`2021.3.4997.20210303T022849Z-210225`に基づいて更新されました。

* Cloud Managerの実稼動パイプラインに、[カスタムUIテスト](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)機能が含まれるようになりました。

### バグ修正 {#bug-fixes}

* AEMのプッシュアップグレード中に、パッケージのバージョン管理がスキップされることがありました。

* 他のパッケージにパッケージが埋め込まれた場合に、品質の問題が正しく検出されない場合がありました。

* 難しい状況では、プログラムの追加ダイアログを開いたときに生成されるデフォルトのプログラム名が、既存のプログラム名と重複している可能性があります。

* 場合によっては、ユーザーがパイプラインの開始直後にパイプライン実行ページから離れると、実際に実行が開始するにもかかわらず、アクションが失敗したことを示すエラーメッセージが表示されます。

* 顧客のビルドで無効なパッケージが生成された場合、ビルド手順が不必要に再開されました。

* 場合によっては、その設定がデプロイされていない場合で許可リストも、IPの横に緑色の「アクティブ」ステータスが表示されることがあります。

* 「エクスペリエンス監査」ステップで既存のすべての実稼働パイプラインが自動的に有効になります。
