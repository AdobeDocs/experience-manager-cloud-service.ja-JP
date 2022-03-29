---
title: AEM as a Cloud Service Release 2021.3.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.3.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 95539851590456b6b5ecbfeb0df8fc7bc7dde74b
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.3.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.3.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.3.0 の Cloud Manager のリリース日は 2021 年 3 月 11 日です。


## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* [IP 許可リスト](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL 証明書](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)、[カスタムドメイン名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)に既存のカスタムドメイン名がある環境のユーザーは、既存の設定に関するメッセージが表示され、UI を使用してセルフサービス方式で操作できるようになります。

* 必要な権限を持つユーザーがプログラムを編集して、セルフサービス方式で以下を行えるようになりました。
   * Assets を使用している既存のプログラムに Sites サイトソリューションを追加する（またはその逆）。
   * Sites と Assets の両方を使用している既存のプログラムから Sites または Assets を削除する。
   * 使用されていない 2 つ目のソリューション使用権限を既存のプログラムに追加するか、新しいプログラムとして追加する。

* パイプラインの実行画面とアクティビティ画面の両方に **AEM プッシュアップデート**&#x200B;ラベルが表示されるようになりました。

* 環境が休止状態になっている場合は、AEM アップデートが使用可能でも、**休止状態**&#x200B;ステータスが&#x200B;**アップデート利用可能**&#x200B;ステータスより優先されます。

* 統合シェルのユーザープロファイルアイコン（右上）に移動した後、「Cloud Manager の役割を表示」オプションを選択すると、Cloud Manager の役割が表示されるようになりました。

* **アプリケーションの承認**&#x200B;ラベルが&#x200B;**実稼動の承認**&#x200B;ラベルに変更され、意味がより明確になりました。

* 実稼動パイプラインの実行画面の&#x200B;**バージョン**&#x200B;ラベルが **Git タグ**&#x200B;ラベルに変更されました。

* 重要な指標が定義済みのしきい値を満たさない場合の動作を定義するラベルが、その実際の動作を反映するように変更されました（**ただちにキャンセルする**&#x200B;と&#x200B;**ただちに承認する**）。

* AEM Cloud Service SDK のバージョン `2021.3.4997.20210303T022849Z-210225` に基づいて、クラスとメソッドの廃止リストが更新されました。

* Cloud Manager の実稼働パイプラインに[カスタム UI テスト](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)機能が追加されました。

### バグ修正  {#bug-fixes}

* AEM プッシュアップグレード時に、パッケージバージョン管理がスキップされる場合がありました。

* パッケージが他のパッケージに埋め込まれている場合に、品質の問題が正しく検出されないことがありました。

* プログラムを追加ダイアログを開いたときに生成されるデフォルトのプログラム名が、既存のプログラム名と重複する場合がありました。

* パイプラインの開始直後にパイプラインの実行ページから移動すると、実際には実行が開始したにもかかわらず、アクションが失敗したという内容のエラーメッセージが表示される場合がありました。

* ユーザービルドの結果、無効なパッケージが生成された場合、ビルドステップが不必要に再開されていました。

* 該当する設定がデプロイされていない場合でも、IP 許可リストの横に緑色の「アクティブ」ステータスが表示される場合がありました。

* 「エクスペリエンス監査」ステップで既存のすべての実稼働パイプラインが自動的に有効になります。
