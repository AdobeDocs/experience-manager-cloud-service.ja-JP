---
title: Cloud Serviceリリース2020.7.0としてのAEMのCloud Managerのリリースノート
description: Cloud Serviceリリース2020.7.0としてのAEMのCloud Managerのリリースノート
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 78%

---


# Cloud Service2020.7.0 {#release-notes}としてのAdobe Experience ManagerのCloud Managerのリリースノート

このページでは、AEMのCloud ManagerのリリースノートをCloud Service2020.7.0として概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2020.7.0のリリース日は2020年7月20日です。

## 新機能 {#whats-new-cloud-manager}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* 環境ごとの環境変数の数が 200 に増えました。

* Cloud Manager のパイプラインで、顧客が設定した変数とシークレットがサポートされるようになりました。


   詳細は、「[パイプライン変数](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables)」を参照してください。

* 認証バウンドのプライベート Maven リポジトリーがサポートされるようになりました。

* Cloud Manager ビルドコンテナで、Java 8 と Java 11 の両方がサポートされるようになりました。詳細は、「[Java 11 サポートの使用](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)」を参照してください。

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

* コードカバレッジの計算方法の変更により、Jacoco プラグインの&#x200B;*最小*&#x200B;バージョンは 0.7.5.201505241946（2015 年 5 月リリース）になりました。古いバージョンを明示的に参照している場合は、コード品質プロセスでエラーメッセージが表示されます。