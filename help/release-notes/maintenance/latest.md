---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 39b2afda66e3bcb7db8ae63a2d0dcd27014ce377
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 66%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 12790 {#release-12790}

2023 年 7 月 21 日に公開されたメンテナンスリリース12790の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 12697 からのアップデートです。

2023.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-12790}

なし。

### 修正された問題 {#fixed-issues-112790}

- SLING-11974 — 非認証要求の SlingHttpServletRequest#getUserPrincipal の回帰を修正しました。 この修正により、未認証のリクエストに対してもプリンシパルが返されるようになりました。

### 既知の問題 {#known-issues-12790}

なし。

### 組み込みテクノロジー {#embedded-tech-12790}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
