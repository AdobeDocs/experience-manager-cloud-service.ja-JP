---
title: AEM as a Cloud Service Release 2022.3.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.3.0 の移行ツールのリリースノート
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---

# AEM as a Cloud Service Release 2022.3.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.3.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.26 のリリース日は 2022 年 3 月 16 日です。

### 新機能 {#what-is-new-bpa}

* 未処理のアセットを検出できるようになりました。未処理のアセットが検出された場合は、コンテンツの取り込み中に問題が発生するのを避けるために、これらのアセットを処理済みに設定するか、コンテンツ転送時に移行セットから削除する必要があります。
* コンテンツに 1,000 個を超えるバニティー URL があるかどうかを検出できるようになりました。多数のバニティー URL を使用すると、Dispatcher およびパブリッシュサーバーに負荷がかかるので、ベストプラクティスではありません。
* Oak インデックスの定義に関連する問題を特定し、AEM as a Cloud Service との非互換性を検出できるようになりました。
* Externalizer 設定の使用を検出してレポートできるようになりました。AEM as a Cloud Service では Externalizer 設定は Cloud Manager で設定されるので、互換性を保つには、既存の Externalizer 設定をリファクタリングする必要があります。

### バグの修正 {#bug-fixes-bpa}

* 一部のシナリオでは、FormsSelectiveFeaturesAnalysis がアサーションエラーをスローするので BPA を実行できませんでした。この問題が修正されました。
* BPA が、WRK パターンに関連する分析結果を「致命的」ではなく「重大」として報告していました。この問題が修正されました。
* BPA が、ui.apps の OAK インデックス定義に関連する分析結果を誤って「致命的」として報告していました。この問題が修正されました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.9.0 のリリース日は 2022 年 2 月 28 日です。

### 新機能 {#what-is-new-ctt}

* サイズ確認ガードレール - コンテンツ転送ツールのサイズ確認機能は、コンテンツ転送の失敗を減らすうえで役に立ちます。サイズ確認機能を使用すると、1) `crx-quickstart` サブディレクトリに十分な空きディスク容量があるかどうかを抽出前に判断でき、2) 移行セットのサイズを推定し、それが対応可能かどうかを確認できます。これらのチェックのどちらか一方または両方に違反した場合、CTT UI に警告が表示されます。このガードレールを使用すると、コンテンツ転送の失敗を回避し、アドビカスタマーケアと一緒に移行オプションについて事前に検討することができます。詳しくは、[移行セットのサイズとディスク空き容量の決定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja#migration-set-size)を参照してください。
