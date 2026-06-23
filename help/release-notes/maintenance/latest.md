---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a876efeed0e078fa0f8f8718484bd3f069a71cb5
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 40%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 26773 {#release-26773}

2026年6月17日（PT）に公開されたメンテナンスリリース 26773の継続的な改善の概要を以下に示します。 以前のメンテナンスリリースはリリース 26353でした。

2026.6.0機能のアクティベーションは、このメンテナンスリリースの完全な機能セットを提供します。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

>[!NOTE]
>
>リリース 26635は非公開になっています。

### 機能強化 {#enhancements-26773}

* GRANITE-67251: `cq:Searchable` mixin タイプで定義された、新しい標準インデックス `cqSiteSearch`を導入しました。 これにより、サイトインデックスに含まれるコンテンツをきめ細かく制御でき、セマンティック検索を含むAEM web サイトの本格的なサイト検索が可能になります。
* GRANITE-68099：組み込みApache Jackrabbit Oakを最新の公開リリース（2.2.0）に更新しました。
* SKYOPS-135241：不変ファームフィルターのaem プレフィックスを導入して、顧客が定義した設定と名前の競合を回避します。

### 修正された問題 {#fixed-issues-26773}

なし。

#### AEM ガイド {#guides-26773}

* GUIDES-46275: `mm`などの単位で指定した画像のサイズが正しくレンダリングされないため、指定したサイズではなく元のサイズで画像が表示されます。
* GUIDES-45800: `<keydef>`または`<topicref>`内の`<topicmeta>`内の`<keywords>`をコピー&amp;ペーストすると、不要な外部タグ内にキーワードが挿入されます。
* GUIDES-45409: マップにDITA以外のリソース（`.html`など）を指す外部`topicref`が含まれている場合、そのプレビューはAssets UIに表示されません。
* GUIDES-45254: PDF テンプレートの`.plt`および`.css` ファイルを操作する場合、**IDを生成** オプションは、これらのファイルタイプに適用されないにもかかわらず、右クリックコンテキストメニューで使用できます。
* GUIDES-45508：多数のアセットを含むマップにベースラインを適用すると、選択した言語の翻訳レポートの読み込みが遅くなり、レポートのレンダリング前にタイムアウトがリクエストされることがあります。
* GUIDES-45511: トピック名の横にあるレビューUIの左側のパネルに、**バージョン履歴** アイコンのツールヒントがありません。
* GUIDES-44942：質問バンクから挿入オプションを使用してクイズに質問を追加する場合、有効な質問IDがあるにもかかわらず、簡潔な回答の質問が表示されません。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-26773}

なし。

### 廃止された機能と API {#deprecated-26773}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-26773}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースは、10の特定された脆弱性に対処し、堅牢なシステム保護への取り組みを強化します。

### 組み込みテクノロジー {#embedded-tech-26773}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 2.2.0 | [Oak 2.2.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.2.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.67 | [Apache Httpd 2.4.67](https://apache.googlesource.com/httpd/+/refs/tags/2.4.67/CHANGES) |
| Dispatcher | 2.0.274 |  |
| AEM コアコンポーネント | 2.31.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
| Java 21 | 21.0.11 | [JDK 21.0.11](https://www.oracle.com/java/technologies/javase/21-0-11-relnotes.html) |
