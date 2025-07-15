---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 5d00bed4008c70e81f3a70d219ddc411ec8bdc59
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 94%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 21484 {#21484}

2025年7月10日（PT）に公開された、メンテナンスリリース 21484 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 21331 でした。

2025.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-21484}

なし。

### 修正された問題 {#fixed-issues-21484}

なし。

#### AEM ガイド {#guides-21484}

* GUIDES-29781：Source ビューの要素内に XML コメントが追加されると、ビューを切り替えるとコメントの前後のスペースが失われます。
* GUIDES-29078：ブラウザーの更新後にオーサービューでトピックを開くと、以前にファイルプロパティパネルで適用したタグが保持されず、特に多数のタグを選択できる場合に、新しいタグを追加すると既存のタグが上書きされます。
* GUIDES-28214：AEM ワークフローを使用してレビュータスクを作成しようとしても、レビュー用ノードが作成されないため、作成が常に失敗します。
* GUIDES-28104：`chunk=to-content` 属性を使用して DITA マップを公開すると、新しい AEM Sites の出力で JCR ノードが重複して作成され、AEM Sites 内に冗長なコンテンツ構造が発生します。
* GUIDES-29065、GUIDES-28793：大規模なコレクションを操作する際に、読み込み時間の長期化や断続的なタイムアウトなどのパフォーマンス問題が発生します。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-21484}

* ソフトウェア配布ポータルで使用可能になったSDKに、ローカルで動作する問題があります。 ローカルテストには、引き続き以前のSDKを使用してください。

### 廃止された機能と API {#deprecated-21484}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-21484}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 5 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-21484}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
