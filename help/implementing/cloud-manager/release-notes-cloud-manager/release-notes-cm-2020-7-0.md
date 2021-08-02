---
title: AEM as a Cloud Service Release 2020.7.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2020.7.0 Cloud Manager のリリースノート
feature: リリース情報
exl-id: b5ac4dd4-18c6-4867-b2df-53711555007f
source-git-commit: 596a7a41dac617e2fb57ba2e4891a2b4dce31fad
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2020.7.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2020.7.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2020.7.0 Cloud Manager のリリース日は 2020 年 7 月 9 日です。

## 新機能 {#whats-new-cloud-manager}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* 環境ごとの環境変数の数が 200 に増えました。

* Cloud Manager のパイプラインで、顧客が設定した変数とシークレットがサポートされるようになりました。


   詳細は、「パイプライン変数」を参照してください。

* 認証バウンドのプライベート Maven リポジトリーがサポートされるようになりました。

* Cloud Manager ビルドコンテナで、Java 8 と Java 11 の両方がサポートされるようになりました。詳細は、「Java 11 サポートの使用」を参照してください。

### バグ修正 {#bug-fixes-cm}

* 環境が完全に作成される前に、Cloud Manager から開発者コンソールへのリンクが正しくアクティブになっていませんでした。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示していませんでした。

* 非実稼動パイプライン編集ページの「**キャンセル**」および「**保存**」のオプションが常に表示されていませんでした。

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* 新しいプログラムを作成する際に、推奨名が既存のプログラム名と重複する場合がありました。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証が、1 つずれていました。

* 何も存在しない場合、環境ページにパブリッシュセグメントと Dispatcher セグメントが表示されることがありました。

### 既知の問題 {#known-issues}

* コードカバレッジの計算方法が変更されたことで、Jacoco プラグインの&#x200B;*最小*&#x200B;バージョンが 0.7.5.201505241946（2015 年 5 月リリース）になりました。古いバージョンを明示的に参照している場合は、コード品質プロセスでエラーメッセージが表示されます。
