---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2e90e40a0fe439653987a23792a4c1ec612aafd6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 63%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 21570 {#21570}

2025年7月15日（PT）に公開された、メンテナンスリリース 21570 の継続的な改善点を以下にまとめます。 前回のメンテナンスリリースは、リリース 21484 でした。

>[!NOTE]
>
>[ リリース 21484](/help/release-notes/maintenance/2025/2025-7-0.md#21484) はプライベートになり、リリース 21570 に置き換えられました。

2025.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-21570}

* Apache Httpd 2.4.63 への移行

### 修正された問題 {#fixed-issues-21570}

* SKYOPS-112722 - バニティ URL の解決に失敗する問題を修正しました

### 既知の問題 {#known-issues-21570}

* 関連するAEM SDKは、異なるリリース ID （21575）を持ち、ソフトウェア配布ポータルから利用できます。
* Apache HTTP サーバーバージョン 2.4.63 では、URL 内の疑問符（`mod_rewrite`）の処理方法に `?` いて互換性のない変更が導入されました。 この変更は、セキュリティリスクと見なされた `UnsafeAllow3F` フラグの使用を防ぐために実装されました。 これは、URL パターンでの疑問符の検出に依存する `RewriteRule` ディレクティブに影響します。

### 廃止された機能と API {#deprecated-21570}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-21570}

なし

### 組み込みテクノロジー {#embedded-tech-21570}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
