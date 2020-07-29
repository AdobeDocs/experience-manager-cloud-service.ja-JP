---
title: Adobe Experience Manager as a Cloud Service 2020.7.0 のリリースノート
description: Experience Manager 2020.7.0 のリリースノート
translation-type: tm+mt
source-git-commit: 9e27ff9510fda5ed238a25b2d63d1d9a3099a8b5
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 100%

---


# AEM as a Cloud Service 2020.7.0 のリリースノート {#release-notes}

Experience Manager as a Cloud Service 2020.7.0 の一般的なリリースノートの概要を次に説明します。

## Cloud Manager の新機能 {#cloud-manager}

AEM as a Cloud Service リリース 2020.7.0 の Cloud Manager の新機能と更新点について説明します。

### リリース日 {#release-date}

[!UICONTROL Cloud Manager] バージョン 2020.7.0 のリリース日は 2020 年 7 月 09 日です。

### 新機能 {#what-is-new-cloud-manager}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* 環境ごとの環境変数の数が 200 に増えました。

* Cloud Manager のパイプラインで、カスタマーセットの変数とシークレットがサポートされるようになりました。
詳細は、「 [パイプライン変数](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables)」を参照してください。

### バグ修正 {#bug-fixes-cm}

* 環境が完全に作成される前に、Cloud Manager から開発者コンソールへのリンクが正しくアクティブになっていませんでした。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示していませんでした。

* 非実稼動パイプライン編集ページの「**キャンセル**」および「**保存**」のオプションが常に表示されていませんでした。

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* 新しいプログラムを作成する際に、推奨名が既存のプログラム名と重複する場合がありました。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証が、1 つずれていました。

* 何も存在しない場合、環境ページに発行セグメントとディスパッチャーセグメントが表示されることがありました。

### 既知の問題 {#known-issues}

* コードカバレッジの計算方法の変更により、Jacoco プラグインの&#x200B;_最小_&#x200B;バージョンは 0.7.5.201505241946（2015 年 5 月リリース）になりました。古いバージョンを明示的に参照している場合は、コード品質プロセスでエラーメッセージが表示されます。

## Cloud Readiness Analyzer の新機能 {#cloud-readiness-analyzer}

Cloud Readiness Analyzer リリース v1.0.2 の新機能と更新点については、このセクションを参照してください。

### バグ修正 {#cra-bug-fixes}

* 以前のバージョンの CRA を Adobe Experience Manager（AEM）6.1 で実行できませんでした。管理者グループのユーザーに対する明示的なサポートが追加されました。

   詳しくは、[AEM 6.1 への CRA のインストール](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61)を参照してください。

* 概要レポートに表示される有効期限のタイムスタンプが正しくありませんでした。

* CRA は重複するカスタムコンポーネントを検出していました。

* AEM 6.1 では、完全な検査を完了する前に、コンテンツ検査が終了していました。例外処理が追加されたので、スキップして、検査が完了するまで続行できるようになりました。

