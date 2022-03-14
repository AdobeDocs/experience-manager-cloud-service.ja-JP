---
title: AEM as a Cloud Service Release 2021.8.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.8.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: cf1d5c4f-404a-4ced-90f2-273c710adc0f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.8.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.8.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.8.0 の Cloud Manager のリリース日は 2021年8月12日（PT）です。

### 新機能 {#what-is-new}

* Cloud Service ユーザーは、Cloud Manager でサービスレベル契約（SLA）レポートを表示できるようになりました。これは、今後数か月で段階的に利用可能になる予定です。
詳しくは、[SLA レポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html?lang=ja)を参照してください。

* IndexType および `IndexDamAssetLucene` 品質ルールのタイプと重大度が変更されました。これらはどちらも、*重大度*&#x200B;が「ブロッカー」のバグになりました。

* 新しい Oak インデックス品質ルールが導入されて、非同期設定と Tika 設定に対応するようになりました。

* プログラムごとの SSL 証明書の最大数が 50 に増えました。

* セルフサービス機能により、ユーザーが Cloud Manager UI を使用して複数のリポジトリーを作成および管理できるようになりました。

* SonarQube が Git 履歴データを不必要に読み取っていました。大規模なコードベースでは、これにより、ビルドパフォーマンスが不必要に低下することがありました。

* パイプラインごとに Maven 依存関係キャッシュを無効にする API が追加されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 29 に更新されました。

### バグ修正 {#bug-fixes}

* 最新のリリースが現在のリリースより前の場合は、更新可能ステータスは表示されるべきではありません。

* 名前が非常に長い新規組織で、初回のオンボーディングが失敗していました。

* 何らかの理由でパイプラインが 2 回トリガーされた場合、「*パイプライン実行ステータスを更新できませんでした*」エラーで、いずれかの実行が失敗します。
