---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: b83d8736d47778ed133e0cc07207e02e581bbc69
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 37%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 24893 {#release-24893}

2026年3月17日（PT）に公開された、メンテナンスリリース 24893 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 24678 でした。

2026.3.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-24893}

* CNTBF-613：アクセス拒否の修正（JCR-101） – ノードタイプを登録できませんでした。
* GRANITE-53957:oak-blob-azure のAzure SDK V8 を V12 にアップグレードします。
* GRANITE-57035: Bouncy Castle をデフォルトのセキュリティプロバイダーとして使用します。
* GRANITE-59249:JVM にセキュリティプロバイダーを登録しないでください。
* GRANITE-61564:`/security/users.html` の設定の表示を管理者に対して開けない。
* GRANITE-64748:OIDC：設定可能な `sling.oauth-request-key` Cookie の有効期限。
* SITES-39767: リクエスト属性（CSP）を介した nonce 値のサポート。
* SKYOPS-129301: API jar javadoc コンプライアンスレベルを 17 に設定します。
* GRANITE-64962:Apache Jackrabbit Oakを 1.92.0 に更新します。
* GRANITE-64963:Apache Jackrabbit Filevault を 4.2.0 に更新します。
* GRANITE-64764:Apache Commons テキストをバージョン 1.15.0 に更新します。
* SKYOPS-131412:Apache Commons Exec を 1.6.0 に更新します。
* SKYOPS-131432:Felix SCR を 2.2.14 に更新します。
* SKYOPS-131907: Sling API 領域を 1.1.10 に更新します。
* SKYOPS-131938:GSON を 2.13.2 に更新します。
* SKYOPS-132173:Apache Commons Codec を 1.21.0 に更新します。
* SKYOPS-132182: Sling テナントを 1.1.8 に更新します。
* SKYOPS-132267:org.osgi.service.component を 1.5.1 に更新します。
* SKYOPS-132272: Sling 機能モデルを 2.0.4 に更新します。
* SKYOPS-133689:Apache httpd 2.4.66 を使用するようにDispatcherを更新します。

### 修正された問題 {#fixed-issues-24893}

* GRANITE-64443:`workflow.core` の非推奨（廃止予定）のエクスポートを削除 `log4j` ます。
* GRANITE-64543：権限制限の応答は、API コントラクトと一致する必要があります。

#### AEM ガイド {#guides-24893}

* GUIDES-38412 :Schematron `(*.sch)` ファイルを編集して「検索と置換」機能を使用すると、「検索と置換」パネルが下部の画面から部分的に消えて表示され、入力フィールドやコントロールにアクセスできなくなります。
* GUIDES-37806：異なる条件付きプリセットが設定された複数のマップで同じトピックが再利用される場合、最新のマップをSalesforceに公開すると、トピックのコンテンツが上書きされ、以前に公開されたマップのユーザーに誤ったデータが表示されます。
* GUIDES-39394：特定のバージョンの言語固有のアセットとして最初に管理されていた画像（例えば、`/en/` で）が、更新されたバージョンのグローバルフォルダーに移動されてベースラインの書き出しが実行されると、新しいベースラインはその画像の古い言語固有のバージョンを引き続き参照し、ベースラインの書き出しに失敗します。
* GUIDES-39054：動的ベースラインを作成する場合、複数の同時 API リクエストが原因でエディターが応答しなくなり、他のすべての操作が停止することがあります。
* GUIDES-37781：レビュータスクにユーザーを割り当てると、ドロップダウンに選択したプロジェクトに関連付けられているユーザーだけでなく、すべてのユーザーが一覧表示され、無効なユーザーオプションが表示される。
* GUIDES-39385：マップのレポートを開いている間、フィルターパネルの読み込みに遅延が生じます。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-24893}

なし。

### 廃止された機能と API {#deprecated-24893}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-24893}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 9 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-24893}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.92.0 | [Oak 1.92.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.92.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.66 | [Apache Httpd 2.4.66](https://apache.googlesource.com/httpd/+/refs/tags/2.4.66/CHANGES) |
| AEM コアコンポーネント | 2.30.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
