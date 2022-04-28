---
title: AEM as a Cloud Service Release 2022.3.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.3.0 の移行ツールのリリースノート
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 27%

---

# AEM as a Cloud Service Release 2022.3.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.3.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.26 のリリース日は 2022 年 3 月 16 日です。

### 新機能 {#what-is-new-bpa}

* 未処理のアセットを検出する機能。 未処理のアセットが検出された場合は、コンテンツの取り込み中に問題が発生するのを避けるために、これらのアセットを処理済みに設定するか、コンテンツの転送中に移行セットから削除する必要があります。
* コンテンツに 1,000 個を超えるバニティー URL があるかどうかを検出する機能。 バニティー URL の数を多く指定することは、Dispatcher およびパブリッシュサーバーに負荷がかかるので、ベストプラクティスではありません。
* Oak インデックスの定義に関連する問題を特定し、AEM as a Cloud Serviceとの非互換性を検出する機能。
* Externalizer 設定の使用方法を検出し、レポートする機能。 AEMas a Cloud Serviceの Externalizer 設定は Cloud Manager で設定されるので、互換性を維持するには、既存の Externalizer 設定をリファクタリングする必要があります。

### バグの修正 {#bug-fixes-bpa}

* 一部のシナリオでは、FormsSelectiveFeaturesAnalysis がアサーションエラーをスローしたため、BPA が実行に失敗しました。 この問題が修正されました。
* BPA は、WRK パターンに関連する結果を CRITICAL ではなく MAJOR として報告していました。 この問題が修正されました。
* BPA は、ui.apps の OAK インデックス定義に関連する結果を誤って「重大」としてレポートしていました。 この問題が修正されました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.9.0 のリリース日は 2022 年 2 月 28 日です。

### 新機能 {#what-is-new-ctt}

* サイズガードレールを確認 — コンテンツ転送ツールのサイズを確認機能を使用すると、失敗したコンテンツ転送を減らすことができます。  [ サイズの確認 ] 機能を使用すると、1) に十分なディスク容量があるかどうかを `crx-quickstart` 抽出前のサブディレクトリ、2) 移行セットのサイズを推定し、サポートされているかどうかを確認します。 これらのチェックの一方または両方に違反した場合、CTT UI に警告が表示されます。 このガードレールを使用すると、コンテンツ転送の失敗を回避し、Adobeカスタマーケアと移行オプションについて事前に話し合うことができます。 参照： [移行セットのサイズとディスク容量の決定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) を参照してください。
