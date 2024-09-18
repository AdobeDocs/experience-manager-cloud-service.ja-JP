---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9323464610b804ff407f5eedf404ab2cca93a8da
workflow-type: ht
source-wordcount: '572'
ht-degree: 100%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 17689 {#release-17689}

2024年9月10日（PT）に公開されたメンテナンスリリース 17689 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 17569 でした。

2024.9.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-17689}

* ASSETS-41404：DRM の改善をサポートするための変更。
* ASSETS-41621：非同期アセットコピージョブの更新。
* ASSETS-32166：非同期アセット移動ジョブの更新。
* ASSETS-41429：DM OpenAPI での画像プリセットのサポート。
* ASSETS-38968：コンテンツフラグメント参照の表示域の改善。
* ASSETS-41787、ASSETS-41183：アセットの一括操作フレームワークの改善。
* GRANITE-52917：コンテンツのコピーパッケージのインストール時間を改善するための最適化。
* SCRNS-3980：アセットがスケジュールされていないサブシーケンスを持つプレーヤーでのグレー画面の検出。

### 修正された問題 {#fixed-issues-17689}

* ASSETS-40875：疑わしい NPE がAssetDeleteHandler によってログに記録される。
* ASSETS-42422：単一のアセットの移動時に非同期ジョブのトリガーが回避される。
* ASSETS-41234：統合シェル - 検索バーが開いているときにグローバルナビゲーションを開くと、機能しない可能性がある。
* ASSETS-42256：統合シェル - 環境を示すタグ／バッジが断続的にしか機能しない。
* ASSETS-41271：移動操作中にアセットの再公開が不必要に防がれる。
* ASSETS-38894：ウォッチドッグの処理によって、再試行が制限される。
* ASSETS-40815：リンク共有 UI での PPT ファイルの表示に、プレビュー PDF レンディションが使用される。
* ASSETS-37123：リンク共有ダイアログでアセットのプレビューが読み込まれない。
* CQ-4358156：削除するタグのバックリンクが更新される。
* SCRNS-4495：異なるユーザーグループで「貼り付け」ボタンが正しく機能しない問題が修正された。
* SCRNS-4512：AEMaaCS 画面からデバイスに関連するコンポーネントが削除された。
* SCRNS-4466：チャネルダッシュボード上で、マニフェストの表示、オフラインコンテンツの生成、マニフェストキャッシュの更新、パネルの表示が非表示になった。
* SCRNS-4513：リスト表示の検索結果ページに列ヘッダーが追加された。

### 既知の問題 {#known-issues-17689}

* FORMS-14340：FormsAndDocumentOmniSearchHandler および CloudStorageSubmitActionInserter のインスタンス化中にエラーが発生する。これらは無害なログステートメントです。
* FORMS-15818：コンポーネント記述子エントリ「OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml」のステートメントがサーバーログで見つからない。これらは無害なログステートメントです。
* SITES-23662：公開をトリガーするユーザーを、サーバーログの JCR ログステートメントから抽出できない。これは開発中の機能で、断続的で無害な「OSGi イベントのバッチで有効なユーザー ID が見つかりません」というエラーがログに記録される可能性があります。

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
