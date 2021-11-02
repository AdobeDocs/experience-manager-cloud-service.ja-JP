---
title: AEM as a Cloud Serviceリリース2021.10.0の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2021.10.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: null
source-git-commit: 0058cfda65ec8f59dbe3ea1bbcc43c08c5e5fe3e
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 15%

---


# AEM as a Cloud Serviceリリース2021.10.0の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2021.10.0の移行ツールのリリースノートの概要を説明します。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## Cloud Acceleration Manager {#cam-release}

### リリース日 {#release-date-cam}

Cloud Acceleration Manager のリリース日は 2021 年 10 月 25 日です。

### 新機能 {#what-is-new-cam}

Cloud Acceleration Manager では、ユーザーがトレンドラインレポートで履歴 BPA レポートを表示できるようになりました。 このレポートを使用すると、ユーザーは進行状況をグラフで簡単に参照できます。 参照： [近似曲線の表示の使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) を参照してください。

### リリース日 {#release-date-october-cam}

Cloud Acceleration Manager のリリース日は 2021 年 10 月 4 日です。

### 新機能 {#what-is-new-cam-oct}

Cloud Acceleration Manager では、BPA レポートを印刷可能なプレビューで表示できるようになり、印刷や印刷を簡単にPDFでき、共有が容易になりました。 手順 6 および 7( [ベストプラクティス分析カードの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).


## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツール v1.6.0 のリリース日は 2021 年 10 月 4 日です。

### 新機能 {#what-is-new-ctt-oct}

* ユーザーマッピングツールが改善され、以下の機能を含むシンプルなユーザーエクスペリエンスが提供されました。 詳しくは、 [ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html).
   * ユーザーマッピングを実行する前に、User Management API への接続をテストする
   * エラーを適切にスキップし、「ユーザーマッピング」アクティビティに進みます
   * 次の場合にユーザーマッピングが失敗しなくなりました： **アクセストークン** は、24 時間後に期限切れになります。 ユーザーマッピングは、最後に停止した場所から再実行できます。

* コンテンツ転送ツールの堅牢性を高めるために、コンテンツは一度にオーサーインスタンスまたはパブリッシュインスタンスに取り込むことができます。 詳しくは、 [コンテンツ転送ツールの概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) を参照してください。

* バージョンが含まれる場合、パス `/var/audit` 監査イベントを移行するために、が自動的に含まれます。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa-latest}

ベストプラクティスアナライザー v2.1.20 のリリース日は 2021 年 10 月 5 日です。

### 新機能 {#what-is-new-bpa-oct}

* ノード名の長さを検出し、レポートする機能。

* 合計インデックスサイズを検出し、レポートする機能。

* 元のレンディションが欠落しているアセットを検出し、レポートする機能。