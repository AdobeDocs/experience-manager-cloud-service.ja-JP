---
title: AEM as a Cloud Service リリース 2021.10.0 における移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2021.11.0 における移行ツールのリリースノート
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 100%

---

# AEM as a Cloud Service リリース 2021.10.0 における移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2021.10.0 の移行ツールのリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、 [こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja) をクリックしてください。

## Cloud Acceleration Manager {#cam-release}

### リリース日 {#release-date-cam}

Cloud Acceleration Manager のリリース日は 2021年10月25日（PT）です。

### 新機能 {#what-is-new-cam}

Cloud Acceleration Manager のトレンドラインレポートで、履歴 BPA レポートを表示できるようになりました。このレポートを使用すると、進行状況をグラフで簡単に参照できます。詳しくは、 [トレンドラインの表示の使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=ja#trendline-view-cam) を参照してください。

### リリース日 {#release-date-october-cam}

Cloud Acceleration Manager のリリース日は 2021年10月4日です。

### 新機能 {#what-is-new-cam-oct}

Cloud Acceleration Manager では、BPA レポートを印刷可能なプレビューで表示できるようになり、印刷や PDF へのエクスポートが簡単になりました。これにより、共有が容易になりました。[ベストプラクティス分析カードの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=ja#best-practices-analysis) の手順 6 および 7 を参照してください。


## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツール v1.6.0 のリリース日は 2021年10月4日です。

### 新機能 {#what-is-new-ctt-oct}

* ユーザーマッピングツールが改善され、以下の機能が提供されるなど、ユーザーエクスペリエンスがシンプルになりました。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=ja)を参照してください。
   * ユーザーマッピングを実行する前に、User Management API への接続をテストできます
   * エラーを適切にスキップし、「ユーザーマッピング」アクティビティを続行できます
   * **アクセストークン**&#x200B;が 24 時間後に期限切れになっても、ユーザーマッピングが失敗しなくなりました。最後に停止した位置からユーザーマッピングを再実行できます。

* コンテンツ転送ツールの堅牢性を高めるために、オーサーインスタンスまたはパブリッシュインスタンスにコンテンツを一度に取り込むことができます。詳しくは、[コンテンツ転送ツールの基本を学ぶ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja)を参照してください。

* バージョンが含まれる場合は、監査イベントを移行するために、パス `/var/audit` が自動的に含まれます。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa-latest}

ベストプラクティスアナライザー v2.1.20 のリリース日は 2021年10月5日です。

### 新機能 {#what-is-new-bpa-oct}

* ノード名の長さを検出して通知できるようになりました。

* 合計インデックスサイズを検出して通知できるようになりました。

* 元のレンディションが欠落しているアセットを検出して通知できるようになりました。
