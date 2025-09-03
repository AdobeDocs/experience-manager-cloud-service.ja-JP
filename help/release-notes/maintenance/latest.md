---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 33468de99a3e77539f4bdc9435324c9f52a45d9f
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 70%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 22171 {#22171}

2025年9月2日（PT）に公開されたメンテナンスリリース 22171 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 21994 でした。

2025.9.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 新機能  {#new-features-22171}

* ASSETS-53136:OpenAPI を使用した Dynamic Media でのバニティ ID のサポート。

### 機能強化 {#enhancements-22171}

なし。

### 修正された問題 {#fixed-issues-22171}

* ASSETS-52510:Unicode `U+202F` を含むファイル名の場合、重複ファイル名の検出が失敗します。
* ASSETS-53489:Assets ビュー UI からフォルダーを削除しても、含まれているすべてのアセットが未承認になるわけではありません。
* ASSETS-54821:Asset Link で「Server error」が断続的に発生する。
* ASSETS-55024:AEM Assetsの「メールでダウンロード」テンプレートの壊れた画像。
* ASSETS-55325:Dynamic Media の静的 URL で、アセットの名前変更の後、ファイル拡張子が省略される。
* ASSETS-55334: リンク共有ダイアログが、短時間点滅して消えるか、表示されません。
* ASSETS-55382：非同期アセットジョブを再起動すると、重複した出力先フォルダーが作成される。
* ASSETS-55472:「公開を管理」オプションの「既に公開済みのページのみを含める」が無視される。
* SITES-31600:Contexthub js エラーによりパーソナライゼーションが機能しない。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-22171}

なし。

### 廃止された機能と API {#deprecated-22171}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-22171}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 7 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-22171}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
