---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 30b5d5838087a35a457939cdbaa13c5735df144e
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 53%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 19823 {#19823}

2025年3月4日（PT）に公開された、メンテナンスリリース 19823 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 19687 でした。

2025.3.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-19823}

* ASSETS-46491：アセット処理のステータス変更に関する OSGI イベントハンドラー。
* ASSETS-45613：アセットが削除または移動されると、非公開イベントを送信します。
* ASSETS-45131:Content Hubでのカスタムタグプロパティのサポート。

### 修正された問題 {#fixed-issues-19823}

* ASSETS-20433：パスワードで保護された PDF に Dynamic Media の取り込みに関する問題。
* ASSETS-24675：画像処理オプションがスウォッチのみの画像プロファイルに表示されない。
* ASSETS-41257：アセットのバージョン比較で、間違った縦横比でアセットをレンダリングする。 タイムラインに誤った順序で表示されるアセットのバージョン。
* ASSETS-44894:Assets ビューのブックマークをクリックできない場合があります。
* ASSETS-45015：スマート切り抜きアセットハンドルが見つからない場合、スマート切り抜きの幅と高さがゼロに設定される。
* ASSETS-45192：パルスリクエストの頻度を減らします。
* ASSETS-45724：アップロードジョブが割り当てられていない場合は、DM アップロードを再試行します。
* ASSETS-46425:Adobe Stock統合の検索の問題。
* ASSETS-27400：フォルダープレビュージェネレーターが、オリジナルを開こうとする可能性があります。
* CQ-4358722:Java 11 と Java 17 で異なるロケールコードを処理します。
* SITES-29369：アセットのアクティベーション/非アクティベーションでトリガーされたページの公開/非公開イベント。
* SITES-24074：統合シェルの下でキーボードアクセシビリティを修正。
* SITES-28058:Assets フォルダーのタイトルがライブコピーに引き継がれない。

### 既知の問題 {#known-issues-19823}

なし。

### 廃止された機能と API {#deprecated-19823}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-19823}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 6 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-19823}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
