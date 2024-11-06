---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: dc7f95ac98fd300a803e307ce11a51937d604a07
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 32%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 18459 {#18459}

2024年11月5日（PT）に公開された、メンテナンスリリース 18459 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 18311 でした。

2024.11.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-18459}

* CQ-4357471:AEMaaCS で i18n 辞書翻訳のサポートを追加。
* SITES-23591：コンテンツフラグメント：UUID をサポートするためのコンテンツフラグメントのアップグレード。
* SITES-25440：コンテンツフラグメント：レプリケーションステータスを表示する CFM 検索 API。
* SITES-24369：コンテンツフラグメント：OpenAPI ドキュメントの改善。
* SITES-25478：コンテンツフラグメント：外部アセット参照のバックエンドサポートを追加しました。
* SITES-26119：コンテンツフラグメント：参照タイプで外部アセット参照のサポートを追加。
* SITES-21199：ユニバーサルエディターを使用したEdge Delivery：ページから作成されたテンプレートのサポートを追加。
* SITES-20311：ユニバーサルエディターを使用したEdge Delivery:CSV をスプレッドシートに読み込むサポートを追加。
* SITES-24821：ユニバーサルエディターを使用したEdge Delivery:aem.page / aem.live をデフォルトにして、Edge Deliveryと統合します。

### 修正された問題 {#fixed-issues-18459}

* CQ-4358730：翻訳するキーが 10 個を超える場合、CQPagePreviewGenerator が失敗します。
* FORMS-14978：テーマエディターでコアコンポーネントベースのフォームのページ読み込みを有効にする。
* FORMS-16596：アクセシビリティの問題：無効なボタンが画面のReaderで認識されない。
* SITES-10575:MSM：ブループリント Bloomfilter ローダーは、100,000 行を超える読み込みを試みます。
* SITES-20755：コンテンツフラグメント：UUID の更新でのアセット参照で、サムネールが表示されない。
* SITES-26253：コンテンツフラグメント：UUID の移行：Sling ジョブトピックを汎用に変更します。
* SITES-21338：コンテンツフラグメント：referencedBy エンドポイントが正しいページ参照を返さない。
* SITES-24421：コンテンツフラグメント：「CF を編集」エンドポイントが、GET CF を使用して取得した CF に対して機能しない。
* SITES-25461：コンテンツフラグメント：CF の検索でのモデルによるフィルタリングでは、大文字と小文字を区別しない必要があります。
* SITES-25471：コンテンツフラグメント：ModelValidatorServlet のグローバルモデルの検証を修正しました。
* SITES-25795：コンテンツフラグメント：cq の日付が設定されていない場合、CF モデル API が失敗します。
* SITES-25817：コンテンツフラグメント：PromoteLaunch の強化：CF ローンチの最後のプロモーションを更新。
* SITES-26030：コンテンツフラグメント：Endpoint /referencesTree が必要なヘッダーを返さない。
* SITES-26031：コンテンツフラグメント：CFM 検索エンドポイントでレプリケーションステータスが返されない。
* SITES-26213：コンテンツフラグメント：コンテンツフラグメントを非公開にすると、公開済みの参照のみが検証されます。
* SITES-26226：コンテンツフラグメント：指定されたパスをどれも使用できない場合に、ワークフローの問題を開始します。
* SITES-26238：コンテンツフラグメント：API から返されるアセット参照は、JCR からの順序とは異なる順序を持ちます。
* SITES-25456：イベント：ページを移動する際、ページ移動イベントの他に、ページ削除イベントが生成されます。
* SITES-25658：イベント：層と sourceUrl は、ページコンテンツの状態イベントには入力されません。
* SITES-6497：ローンチ：ローンチでページを作成が機能しません。
* SITES-25393：ユニバーサルエディターを使用したEdge Delivery:1 つの段落を含む書式設定されたリッチテキストをレンダリングすると、テキストノードが失われる。
* SITES-24643：ユニバーサルエディターを使用したEdge Delivery：ページメタデータモデルで OpenGraph とtwitterメタデータ属性が機能しない。

### 既知の問題 {#known-issues-18459}

なし。

### 廃止された機能と API {#deprecated-18459}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-18459}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 21 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-18459}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
