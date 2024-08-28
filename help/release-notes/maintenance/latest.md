---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: eb01b6982578ad1300163c2fd536e844afc815fa
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 52%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 17569 {#release-17569}

2024年8月27日（PT）に公開されたメンテナンスリリース 17569 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 17465 でした。

2024.9.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-17569}

* CQ-4353778：翻訳プロセスイベント。
* CQ-4354583:Adobeパイプラインを使用して翻訳プロセスイベントを送信します。
* CQ-4356479:Adobeコードでのみ/adobe サーブレットコンテキストの使用を許可します。
* CQ-4358226：翻訳キーワードを保存機能が、特定の文字列形式で機能しない。
* CQ-4358270:AEM翻訳キット：8 月 8 日（PT）。
* CQ-4358310:oak-compat-query-spi-1.2 をクイックスタートに追加します。
* GRANITE-49833：イベント送信者とプロキシのバッチ処理のサポート。
* GRANITE-52053:Commons コレクションの使用を削除 3:Platform その他。
* GRANITE-52492:PIT リストアの場合の弾性非同期のキャッチアップ。
* GRANITE-53099:Apache Felix Http Jetty 5.1.24 を更新します。
* GRANITE-53125:CloudEvent に分類を追加する。
* GRANITE-53328：スタッシングログの改善を含めて、Filevault を 3.8.0-T20240726111512-3cc11d50 に更新します。
* GRANITE-53453: commons-lang を 3.15.0 に更新します。
* GRANITE-53478:Filevault をバージョン 3.8.0 に更新します。
* GRANITE-53505:QS を commons-collections-3.2.2-adobe-2 に更新します。
* GRANITE-53528:Platform アーティファクトのバージョンを更新します。
* GRANITE-53547:Apache Commons Lang 2 の使用を避ける代替 API を提供する。
* GRANITE-53575:CS で BSAFE 6.2.5 を使用します。
* GRANITE-53608:Oakを最新の公開リリース（1.68.0）に更新します。
* SITES-23583:Sites エバーグリーンテストが Java 17 で失敗する。
* SKYOPS-79535: rum スクリプト v2 に更新します。
* SKYOPS-79816:FACT ツールでのサービスユーザーマッピング用の Sling 機能アナライザータスクを有効にします。
* SKYOPS-81179:AEMは、バンドルの切り替えのテストをビルドします。
* SKYOPS-81866:Java 21 と互換性がないことがわかっているバンドルの警告を報告します。
* SKYOPS-82660:Sling API を 2.27.6 に更新します。
* SKYOPS-82961:Sling ResourceResolver 1.12.0-T20240723153354-a0270a0 を更新しました。
* SKYOPS-83356:AEMのデプロイメントで使用される JVM バージョンを追跡するためのグローバルダッシュボードを作成します。
* SKYOPS-83436:Java Runtime 21 ロールアウトで、アダプティブフォームAEM Formsの作成が中断される。
* SKYOPS-84272: AEM ランチャーの起動時に使用される Java バージョンを記録します。

### 修正された問題 {#fixed-issues-17569}

* CMGR-60225:AEM リリース 17486 へのアップデートの検証中に、AEM Sites CS のお客様でパイプライン実行エラーが検出されました。
* GRANITE-45919:「ユーザー設定の編集」の「国/地域」リストに禁輸対象の国が表示される。
* GRANITE-51715：ピッカーで、テキストフィールドに選択範囲が入力されない場合がある。
* GRANITE-53290:XSS チェックで URL を解析する際に、プロトコルを正しく確認してください。
* GRANITE-53576:OSGi 設定のサービスランキングの定義が正しくありません。
* SKYOPS-82129:Sling モデルでの Memoryleak。

### 既知の問題 {#known-issues-17569}

* ASSETS-40875 - AssetDeleteHandler クラスが、アセット削除イベントをリッスンし、削除イベントのタイプ（PRE_DELETE または POST_DELETE）に基づいて特定のアクションを実行する。特定のシナリオでは、POST_DELETE タイプのイベントによって NullPointerException が発生します。
* FORMS-14340 - FormsAndDocumentOmniSearchHandler および CloudStorageSubmitActionInserter のインスタンス化中にエラーが発生する。これらは無害なログステートメントです。
* FORMS-15818 - コンポーネント記述子エントリ「OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml」のステートメントがサーバーログで見つからない。これらは無害なログステートメントです。
* SITES-23662 - 公開をトリガーするユーザーがサーバーログの JCR ログステートメントから抽出できない。これは開発中の機能で、断続的で無害な「OSGi イベントのバッチで有効なユーザー ID が見つかりません」というエラーがログに記録される可能性があります。

### 変更通知 {#change-notice-17569}

* 2024年9月以降、AEM as a Cloud Service では、Sling Model Exporter フレームワークを介したリソースリゾルバーのシリアル化が無効になります。 詳しくは、[ドキュメント](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)を参照してください。

### 廃止された機能と API {#deprecated-17569}

現在 `com.day.cq.wcm.api` を更新中で、現在のリリースでは、いくつかのメソッドとクラスを `@Deprecated` としてマークしています。これらは今後のリリースでは削除される予定なので、いずれかを使用している場合は、推奨される代替手段に切り替えます。

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-17569}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 4 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-17569}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.26.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
