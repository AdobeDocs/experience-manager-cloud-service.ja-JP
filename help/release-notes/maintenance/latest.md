---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 8ee3da55024c0f5246f6c194bc07172b4b71823a
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 53%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 22758 {#22758}

2025年10月1日（PT）に公開された、メンテナンスリリース 22758 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 22450 でした。

2025.10.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-22758}

* ASSETS-56227:adobe-countdown-timer 修飾子の名前を変更します。
* CNTBF-493: content-backflow バンドルのバージョンを 2.0.28 にバンプします。
* CQ-4361110:Granite 翻訳。
* CQ-4361112：最新のAEM翻訳。
* GRANITE-56026：権限 API ステータスコード応答を改善しました。
* GRANITE-61015：公開 `org.apache.commons.io.channels` 書き出されたリストにパッケージを追加しました。
* GRANITE-61167:Felix ログを最新の OSGI 仕様に更新。
* GRANITE-61167:Felix の依存関係を更新する。
* GRANITE-61169：保護された文字列のチェックを改善する。
* GRANITE-61622:Sling の依存関係を更新する。
* GRANITE-61663：クイックスタートに `com.adobe.granite.repository.indexdefs-1.0.2` を追加します。
* GRANITE-61811：クイックスタートに `com.adobe.granite.repository-2.0.0` を追加します。
* SITES-32014：外部イベントをリッスンして、サービス登録を更新します。
* SITES-34277：ページの翻訳ワークフローでのブロックエラーを修正。
* SKYOPS-108706: アップグレードされたリリースでは、バンドルが最新バージョンに切り替わります（etag キャッシュ）。
* SKYOPS-114210: aem.pss.service バンドルの最新バージョンに更新しています。
* SKYOPS-116171：Sling ResourceResolver 1.12.12 にアップデート。
* SKYOPS-119811:dispatcher-publish 2.0.258 をリリースしました。

### 修正された問題 {#fixed-issues-22758}

* GRANITE-61875:「無効な式の評価」のトリガーを修正しました – 作成者がコンテンツフラグメントを保存できず、アセットをダウンロードできません。
* SITES-22059:PDF ビューアコンポーネントでの JS エラーを修正しました。 コアコンポーネントサイト/PDF ビューアの「ファイルプレビューを使用できません」文字列がローカライズされていません。
* GRANITE-59704：編集モードが失敗する原因となる htmllibmanager.debug を修正しました。
* GRANITE-61042:FELIX-6796 （ServiceTracker NPE 修正）をAEM Felix web コンソールバンドルに統合します。
* GRANITE-61165:Workspace.copy （）が RepositoryException をスローしている。
* GRANITE-61875: ui.commons を 5.10.50 に更新します。

### 既知の問題 {#known-issues-22758}

なし。

### 廃止された機能と API {#deprecated-22758}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-22758}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 13 個の脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-22758}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.30.1 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
