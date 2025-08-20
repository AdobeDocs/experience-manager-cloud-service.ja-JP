---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 90e92cfb15a6dfe5a8a474996f52c8a0c689f5e6
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 39%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 21994 {#21994}

2025年8月19日（PT）に公開されたメンテナンスリリース 21994 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 21772 でした。

2025.8.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 新機能  {#new-features-21994}

なし。

### 機能強化 {#enhancements-21994}

* GRANITE-53488:deleteconf.json エンドポイントのエラー処理を改善。
* GRANITE-59968: REPLICATION_FORCE_READY_MILLIES を設定できます。
* GRANITE-60183:Apache commons-fileupload 1.6.0。
* GRANITE-60306:Apache commons-lang を 3.18.0 に変更。
* GRANITE-60637:Apache commons-codec を 1.19.0 に。
* GRANITE-60645:Apache commons-ui 2.20.0。
* GRANITE-60663:Apache commons-text 1.14.0。
* GRANITE-60714:Mongo Java ドライバー 5.2。
* GRANITE-60778:Filevault 4.0.0
* GRANITE-60823:Jackrabbit 2.22.2。
* GRANITE-60967:clientlib のコンパイル時間を追跡するための指標を作成します。
* SKYOPS-105469: Autofix API で acsredirectMgr のサポートを追加しました。
* SKYOPS-113929：レプリケーション準備完了チェック用の指標を追加。
* SKYOPS-84821:Sling エンジン 2.16.6。
* SKYOPS-114322: クロージャ コンパイラの言語をレベルから `ECMASCRIPT_2018` にアップしました。

### 修正された問題 {#fixed-issues-21994}

* GRANITE-60167:Skyline の非同期インデックス更新で CSV データがサポートされていません。
* GRANITE-60532：値の切り替えの変更は取得されません。
* SITES-34277：ページの翻訳ワークフローにおけるブロッキングエラーを修正。
* SKYOPS-105471: aso Autofix の dambaseredirect 修正をサポートします。
* SKYOPS-109532：機能を追加すると、削除されたリンクがコメントビハインドとしてトグルで表示される。

#### AEM ガイド {#guides-21994}

* GUIDES-26688: PDFのネイティブテンプレートに含まれる CSS ファイルとページレイアウトファイルのファイルロック動作に一貫性がなく、ファイルがロックされている場合でも編集が可能です。
* GUIDES-30900：多数のアセットを含むフォルダーをAssets UI からコピーすると、API のタイムアウトが発生する。 操作はバックエンドで引き続き実行され、しばらくすると完了しますが、成功または失敗のメッセージや通知は UI に表示されません。
* GUIDES-29090: ネイティブ PDF出力で、インデックスのリスト（LOI）がアルファベット順以外の順序で表示され、ネストされたインデックス用語が正しくグループ化されず、インデックスを移動するのが難しくなります。
* GUIDES-11227: Assets UI から DITA マップをコピーすると、関連付けられたベースラインも新しいマップにコピーされます。
* GUIDES-31506：最近のファイル ウィジェットにリストされているファイルの 1 つが、ソーステンプレートにサムネールが含まれていないテンプレートに基づいている場合、ホームページが空白になります。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-21994}

* Apache HTTPD バージョン 2.4.65 では、セキュリティ修正の一部として実装された新しい制限により、特定の設定に影響を与える可能性がある変更が導入されました。 これらの修正により、Content-Type ヘッダーの変更に使用される `RequestHeader set`、`edit`、`edit_r` などのディレクティブがリクエストヘッダーに正しく制限されるようになり、脆弱性に対処しています。 この変更により、特に静的コンテンツに対する応答ヘッダーへの意図しない変更を防ぎます。

### 廃止された機能と API {#deprecated-21994}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-21994}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 2 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-21994}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
