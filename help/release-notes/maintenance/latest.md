---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1a1eeb3b9aec839677baadf9bea67993a22f9519
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 44%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 22943 {#22943}

2025年10月14日（PT）に公開された、メンテナンスリリース 22943 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 22758 でした。

2025.10.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-22943}

* ASSETS-57809:damAssetLucene-13 のインデックス定義を更新。
* ASSETS-36521: DM 再アップロードワークフローを改善し、一貫性のある後処理を確保しました。
* ASSETS-56400：透明度を持つアセット用に新しい OOTB ズーム PNG レンディションを追加しました。
* ASSETS-55326:HTTP イベントを通じて、AI メタデータフォルダー設定ビューを有効にしました。
* ASSETS-56905：プロキシを介した Indesign への接続をサポートします。
* ASSETS-48286:GenStudioの Algolia に CAI プロパティを追加します。
* ASSETS-48653：前処理フェーズで非表示の透かしを適用します。
* ASSETS-55874:scene7 から DMWithOpenapi に画像プリセットを移行。
* SITES-30452:/content/definition エンドポイントでの ASO のコンテンツ API の改善。

### 修正された問題 {#fixed-issues-22943}

* ASSETS-56301：選択的なメタデータの書き出しを修正し、CSV に PredictedTags を含めるようにしました。
* ASSETS-55543：非同期処理ロジックをリファクタリングし、再利用可能なバンドルにしました。
* ASSETS-54789:DM ACL が有効な場合に、ACLPermissionsValidator で NPE が修正されました。
* ASSETS-55888:UI レンディションパネルに表示されるマルウェアのレンディションを修正。
* GRANITE-62236：スマートコレクションの保存済み検索でのキーワードのローカライズの問題を修正しました。
* GRANITE-61875：コンテンツフラグメントやアセットのダウンロードを保存できない、「無効な式の評価」ホットフィックスの問題を修正しました。
* SITES-24074：キーボードタブナビゲーション中にフォーカスを受け取る、非表示のモバイルナビゲーションを修正しました。
* SITES-33611：大口市場におけるライブコピーの概要の問題を修正しました。

#### AEM ガイド {#guides-22943}

* GUIDES-31421：複数の DITA マップまたはトピックが開いていて、トピックの 1 つが閉じている場合、開いているすべてのタブを表示する **>>** ボタンが、タブバーの残りの開いているタブと重なります。
* GUIDES-33229: PDF を生成する際、プロパティ名にピリオドが含まれている場合、DITAVAL ファイルのフィルタールールは無視されます。
* GUIDES-33720：翻訳 UI の画面をズームすると、「翻訳用に送信」ボタンが省略記号の下に移動し、アセットが選択されていなくても有効になります。
* GUIDES-33590：レビュー担当者がレビュータスクを完了するか、コメントを入力せずにレビュータスクを更新すると、送信された通知メールには最新の以前のコメントが表示されます。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 廃止された機能と API {#deprecated-22943}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-22943}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 14 個の脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 変更通知

* このリリースには、次の新しい製品インデックスバージョンが含まれています。
* **damAssetLucene-13**

### 組み込みテクノロジー {#embedded-tech-22943}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.30.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
