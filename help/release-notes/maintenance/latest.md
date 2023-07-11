---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e1183791f543d17f98cb6c9ca0c513c8936ef477
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 47%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 12585 {#release-12585}

2023 年 7 月 11 日に公開されたメンテナンスリリース12585の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 12549 からのアップデートです。

2023.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-12585}

- 一般的な RDE の安定性の向上 (SKYOPS-61133、SKYOPS-55281、SKYOPS-61216および SKYOPS-61401)
- DXML-12327:AEMガイド：ネイティブ言語公開での言語変数のサポートPDF
- DXML-11518:AEMガイド：ネイティブメタデータ公開でのメタPDFのサポートの強化
- DXML-10093:AEMガイド：外部データソースへの接続と DITA トピックへのデータの挿入のサポート
- DXML-10699:AEMガイド：翻訳での XLIFF 形式のサポート
- DXML-10141:AEMガイド：PDF（ネイティブおよび DITA-OT）、HTMLおよびカスタムプリセットタイプにマイクロサービスベースの公開を使用するオプション

### 修正された問題 {#fixed-issues-12585}

- AEMガイド：ネイティブPDFの様々な機能強化と安定性の修正
- SKYOPS-53130:RDE での AC ツールのサポートの改善
- SKYOPS-57146:AEM起動時の Sling デッドロックの修正

### 既知の問題 {#known-issues-12585}

なし。

### 組み込みテクノロジー {#embedded-tech-12585}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
