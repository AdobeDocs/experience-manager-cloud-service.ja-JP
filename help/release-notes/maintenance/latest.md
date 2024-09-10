---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9323464610b804ff407f5eedf404ab2cca93a8da
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 50%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 17689 {#release-17689}

2024年9月10日（PT）に公開されたメンテナンスリリース 17689 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 17569 でした。

2024.9.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-17689}

* ASSETS-41404:DRM の改善をサポートする変更。
* ASSETS-41621：非同期アセットコピージョブを更新しました。
* ASSETS-32166：非同期のアセット移動ジョブを更新しました。
* ASSETS-41429:DM OpenAPI での画像プリセットのサポート。
* ASSETS-38968：コンテンツフラグメント参照の表示域が向上しました。
* ASSETS-41787、ASSETS-41183: Assets一括操作フレームワークの機能強化。
* GRANITE-52917：コンテンツのコピーパッケージのインストール時間を改善するための最適化。
* SCRNS-3980: アセットがスケジュールされていない後続のプレーヤーでグレーの画面を検出します。

### 修正された問題 {#fixed-issues-17689}

* ASSETS-40875:AssetDeleteHandler によってログに記録されたスプリアス NPE。
* ASSETS-42422:1 つのアセット移動に対して非同期ジョブをトリガーしないようにします。
* ASSETS-41234：検索バーが開いている場合、統合シェル – グローバルナビゲーションが機能しない可能性があります。
* ASSETS-42256：統合シェル – 環境を示すタグ/バッジが断続的にのみ機能します。
* ASSETS-41271：移動操作中にAssetsを不必要に再公開しないようにします。
* ASSETS-38894：ウォッチドッグを処理して再試行を制限します。
* ASSETS-40815：プレビューPDFレンディションを使用して、リンク共有 UI で PPT ファイルを表示します。
* ASSETS-37123：リンク共有ダイアログでアセットのプレビューを読み込めない。
* CQ-4358156：削除されるタグのバックリンクを更新します。
* SCRNS-4495：異なるユーザーグループに対して、貼り付けボタンが正しく機能しない問題を修正しました。
* SCRNS-4512: AEMaaCS 画面からデバイスに関連するコンポーネントを削除します。
* SCRNS-4466: チャネル ダッシュボードで、非表示 – マニフェストの表示、オフライン コンテンツの生成、マニフェスト キャッシュの更新、表示パネル。
* SCRNS-4513: リスト ビューで検索結果ページの列ヘッダーを追加します。

### 既知の問題 {#known-issues-17689}

* FORMS-14340:FormsAndDocumentOmniSearchHandler および CloudStorageSubmitActionInserter のインスタンス化でエラーが発生しました。 これらは無害なログステートメントです。
* FORMS-15818: コンポーネント記述子エントリ &#39;OSGI-INF/com.adobe.aemfd.docmanager.impl。*.xml&#39;がサーバーログに見つかりません。 これらは無害なログステートメントです。
* SITES-23662：公開をトリガーするユーザーを、サーバーログの JCR ログステートメントから抽出できない。 これは、開発中の機能で、断続的で無害な「OSGI イベントのバッチで有効なユーザー ID が見つかりません」エラーがログに発生する可能性があります。

### 変更通知 {#change-notice-17689}

* 2024年9月以降、AEM as a Cloud Service では、Sling Model Exporter フレームワークを介したリソースリゾルバーのシリアル化が無効になります。 詳しくは、[ドキュメント](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)を参照してください。

### 廃止された機能と API {#deprecated-17689}

現在 `com.day.cq.wcm.api` を更新中で、現在のリリースでは、いくつかのメソッドとクラスを `@Deprecated` としてマークしています。これらは今後のリリースでは削除される予定なので、いずれかを使用している場合は、推奨される代替手段に切り替えます。

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-17689}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 4 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-17689}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.26.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
