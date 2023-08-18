---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: cf8b5d8b11452268b2839053c1e05cc2ec107a91
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 53%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 13173 {#release-13173}

2023 年 8 月 18 日に公開されたメンテナンスリリース13173の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 13099 からのアップデートです。

2023.8.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-13173}

なし。

### 修正された問題 {#fixed-issues-13173}

- SITES-15463：サイトテンプレート — テンプレートを公開できません。

### 既知の問題 {#known-issues-13173}

- SITES-15359：コンテンツフラグメント — バリエーション名のパターンが、 ```'_'``` を含める必要があります。
- FORMS-10444：アダプティブFormsテンプレート — テンプレートを公開できません（回避策：配布コンソールを使用）。
- CQ-4354191：ワークフロー — カスタムランチャーは、nt:unstructured ノードに存在するレプリケーションメタデータが原因で、何度もトリガーする場合があります（回避策：重複を避けるためにレプリケーションメタデータプロパティを除外するランチャーを更新）。

### 組み込みテクノロジー {#embedded-tech-13173}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
