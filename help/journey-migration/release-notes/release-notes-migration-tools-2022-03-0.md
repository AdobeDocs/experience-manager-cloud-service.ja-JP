---
title: AEM as a Cloud Service Release 2022.3.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.3.0 の移行ツールのリリースノート
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: ht
source-wordcount: '349'
ht-degree: 100%

---

# AEM as a Cloud Service Release 2022.3.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.3.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.26 のリリース日は 2022 年 3 月 16 日です。

### 新機能 {#what-is-new-bpa}

* 未処理のアセットを検出できるようになりました。未処理のアセットが検出された場合は、コンテンツの取り込み中に問題が発生するのを避けるために、コンテンツ転送中にこれらのアセットを処理済みに設定するか、移行セットから削除する必要があります。
* コンテンツに 1,000 個を超えるバニティー URL があるかどうかを検出できるようになりました。多数のバニティー URL を使用すると、Dispatcher およびパブリッシュサーバーに負荷がかかるので、ベストプラクティスではありません。
* Oak インデックスの定義に関連する問題を特定し、AEM as a Cloud Service との非互換性を検出できるようになりました。
* Externalizer 設定の使用を検出してレポートできるようになりました。AEM as a Cloud Service Externalizer では、Cloud Manager が設定を行います。したがって、互換性を維持するには、既存の Externalizer 設定をリファクタリングする必要があります。

### バグの修正 {#bug-fixes-bpa}

* 一部のシナリオで、FormsSelectiveFeaturesAnalysis がアサーションエラーをスローするので BPA を実行できませんでした。
* BPA が、WRK パターンに関連する分析結果を「致命的」ではなく「重大」として報告していました。
* BPA が、ui.apps の Oak インデックス定義に関連する分析結果を誤って「重大」として報告していました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.9.0 のリリース日は 2022 年 2 月 28 日です。

### 新機能 {#what-is-new-ctt}

* サイズ確認ガードレール - コンテンツ転送ツールのサイズ確認機能は、コンテンツ転送の失敗を減らすうえで役に立ちます。サイズの確認機能を使用すると、ユーザーは抽出前に `crx-quickstart` サブディレクトリに十分なディスク容量があるかどうかを判断できます。また、移行セットのサイズを推定し、サポートされているかどうかを確認できます。これらのチェックのどちらか一方または両方に違反した場合、CTT ユーザーインターフェイスに警告が表示されます。このガードレールを使用すると、コンテンツ転送の失敗を回避し、アドビのカスタマーケアと一緒に移行オプションについて事前に検討することができます。詳しくは、[移行セットのサイズとディスク空き容量の決定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja#migration-set-size)を参照してください。
