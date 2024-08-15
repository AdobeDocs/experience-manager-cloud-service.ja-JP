---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 80edd0255b38beee93b3f9c779ae0f364500b4a5
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 81%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 17465 {#release-17465}

2024年8月14日（PT）に公開されたメンテナンスリリース 17465 の継続的な改善点を以下にまとめます。 前回のメンテナンスリリースは、リリース 17258 でした。

2024.8.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-17465}

* FORMS-15436 - Adobe Sign ステータススケジューラーの例外を適切に処理する。
* FORMS-15362 - aemds に forms-foundation の設定を追加して、ログインを有効にする。
* FORMS-15261 - SPA が Forms エディターでレンダリングされない。
* FORMS-15138 - sling commons json のアップグレードによる Double データの後方互換性の処理。
* FORMS-15113 - RUM トラッキング用にキー名を vistorId から sid に変更する。
* FORMS-15103 - フォームに添付された Assets が Edge Delivery で公開されない。
* FORMS-15082 - カスタムアダプティブフォームコンポーネントにマッピングする JSON スキーマ。
* FORMS-15002 - v1 フラグメントのテンプレートタイプ登録。
* FORMS-14845 - Forms Manager を介したコアコンポーネントベースフォームでの xdpRef のサポート。
* FORMS-14840 - Forms 事前入力サービスエラー。
* FORMS-14836 - Forms Manager UI を改善して、AF1 フラグメントテンプレートを一覧表示します。
* FORMS-14834 - AF1 でのフラグメントのテンプレートサポート。
* FORMS-14275 – 埋め込みコンテナでの「ありがとうございます」ページとお礼のメッセージの上書き。
* FORMS-13623 - V2 の自動保存時間ベースの機能を有効にする。
* FORMS-8651 - フォームプロパティページのデータモデル設定の変更に関する警告ダイアログ。
* SITES-23310 - コンテンツフラグメント REST API：コンテンツフラグメントのネストされた参照における循環依存関係を防ぐ。
* SITES-23285 - コンテンツフラグメント REST API：エンドポイントを作成して、使用可能なすべての言語をリストする。
* SITES-22857 - コンテンツフラグメント REST API：チェックボックス列挙フィールドで、複数のプロパティを false に設定することはできない。
* SITES-22813 - コンテンツフラグメント REST API：列挙フィールドの min/max プロパティを定義する。
* SITES-22031 - コンテンツフラグメント REST API：フラグメントのフォルダーに許可されたコンテンツフラグメントモデルを取得する。
* SITES-17640 - コンテンツフラグメント REST API：コンテンツフラグメント公開操作の検証。
* SITES-22677 - コンテンツフラグメント REST API：子孫参照のフラットリストを取得する
* SITES-22207 - コンテンツフラグメントの作成時にモデルが複製される。
* SITES-23093 - イベント：コンテンツフラグメントモデルイベントのペイロードにタグを追加する。
* SITES-23092 - イベント：コンテンツフラグメントイベントのペイロードにタグを追加する。
* SITES-22447 – 基本の「プロパティ」タブに、エクスペリエンスフラグメントのプロパティ継承のサポートを追加。
* SITES-12209 - cq:policy をインデックスに追加して、ポリシーエディターのパフォーマンスを向上。

### 修正された問題 {#fixed-issues-17465}

* CQ-4358028 - サムネールがアップロードされている場合に、プロジェクトを作成できなかった。
* CQ-4357891 - 書き出された XLIFF のシーケンスの問題。
* CQ-4357059 – 翻訳ジョブが完了するまでに時間がかかり、AEMaaCS で 503 タイムアウトが発生する。
* FORMS-15320 - メールの送信がコアコンポーネントベースのフォームで機能しない。
* FORMS-15272 - AEM Forms - チェックボックスグループで 1 つの値のみが送信される。
* FORMS-15269 - メンテナンスリリース 16461 以降、製品関連の問題が発生する。
* FORMS-15174 - JsonSchemaParser が有効な問題。
* FORMS-15095 – 複数行のテキストボックスを、AEM Forms 内に含まれるパネルよりも拡大できる。
* FORMS-15057 - 送信数が 999 件より多い場合に、FDM SharePoint リストが添付ファイルエラーをスローする。
* FORMS-15011 - コアエディターで、フォームを開く際にコンソールエラーが発生する。
* FORMS-14809 – 共有された一時ディレクトリ内で SDK フォルダーが自動的に作成されない。
* FORMS-14327 - Forms サービス API：データを抽出：非インタラクティブ PDF を入力で指定すると応答コード 500 が返される。
* FORMS-7475 - アダプティブフォームの作成ページで並べ替えが機能しない。
* FORMS-3309 - フォームの送信時に複数のオプションが選択されている場合、生成された DoR では 1 つのオプションのみが表示される。
* SITES-23646 - フィールドに一意の値が含まれている場合、OpenAPI で作成されたモデルの GraphQL モデルエンドポイントが失敗する。
* SITES-23637 - コンテンツフラグメント REST API：OpenAPI で列挙に正しい値タイプが使用されない。
* SITES-23573 - コンテンツフラグメント REST API：ライブ関係は、uuid による GET コンテンツフラグメントでは考慮されない。
* SITES-23535 - コンテンツフラグメント REST API：コンテンツフラグメントモデルの列挙型複数フィールドに空の値がある。
* SITES-23534 - コンテンツフラグメント REST API：コンテンツフラグメント検証 ClassCastException。
* SITES-23524 – 複数フィールドの列挙フィールドをサポートするように GraphQL BFF モデルエンドポイントを適応させる。
* SITES-23467 - コンテンツフラグメント REST API：カーソルの問題が原因で検索モデルが失敗する。
* SITES-23327 - タイムラインイベント処理の説明中に AuditLogTimelineEventProvider で ArrayIndexOutOfBoundsException が発生する。
* SITES-23277 - コンテンツフラグメント REST API：コンテンツフラグメントフィールドのライブ関係チェックは、ライブコピーに対してのみ行う必要がある。
* SITES-23232 – 新しい CF エディター UI でカスタム検証が機能しない。
* SITES-23090 - コンテンツフラグメント REST API：ロックされたコンテンツフラグメントのタイトルを更新できない。
* SITES-22981 - ネスト深度がローンチを昇格しても公開されない。
* SITES-22870 - PathAttributesHandler.processSrcAttr ArrayIndexOutOfBoundsException。
* SITES-22814 - コンテンツフラグメント REST API：チェックボックス列挙フラグメントフィールドの値は、モデルで定義されたキーで並べ替える必要がある。
* SITES-22716 - OOTB コンポーネントのライブ使用状況リストに関する問題。
* SITES-22457 - 深度がローンチを昇格してもソースコンテンツが更新されない。
* SITES-22449 - AEM P20 のアップグレード後に、コンテンツフラグメントで変更を保存できない。
* SITES-22279 - コンテンツフラグメント REST API：コンテンツフラグメントに列挙タイプの一意の属性がない。
* SITES-22203 - コンテンツフラグメント REST API：同じ状況に対して同じ応答を返すように、管理 API を調整する。
* SITES-21973 - コンテンツフラグメント REST API：モデルに列挙タイプの一意の属性がない。
* SITES-20364 - 302 リダイレクトが URL のセレクターでは機能しない。
* SITES-21198 - VersionPreviewServlet：クリーンアップがすべてのクラスターノードで同時に実行され、結合の競合とブロックのコミットが発生する。

### 既知の問題 {#known-issues-17465}

* ASSETS-40875 - AssetDeleteHandler クラスは、アセット削除DELETEをリッスンし、削除DELETE（PRE_event または Asset_event）のタイプに基づいて特定のPOSTを実行します。 状況によっては、event_event 型のPOSTDELETEが NullPointerException を引き起こします。
* FORMS-14340 - FormsAndDocumentOmniSearchHandler および CloudStorageSubmitActionInserter のインスタンス化でエラーが発生しました。 これらは無害なログステートメントです。
* FORMS-15818 - コンポーネント記述子エントリ「OSGI-INF/com.adobe.aemfd.docmanager.impl。*.xml&#39;がサーバーログに見つかりません。 これらは無害なログステートメントです。
* 
   * SITES-23662 - サーバーログの JCR ログステートメントからパブリッシュをトリガーするユーザーを抽出できない。 これは、開発中の機能で、断続的で無害な「OSGI イベントのバッチで有効なユーザー ID が見つかりません」エラーがログに発生する可能性があります。

### 変更通知 {#change-notice-17465}

* 2024年9月以降、AEM as a Cloud Service では、Sling Model Exporter フレームワークを介したリソースリゾルバーのシリアル化が無効になります。 詳しくは、[ドキュメント](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)を参照してください。

### 廃止された機能と API {#deprecated-17465}

アドビは現在 `com.day.cq.wcm.api` を更新中で、現在のリリースでは、いくつかのメソッドとクラスを `@Deprecated` としてマークしています。 これらは今後のリリースで削除される予定です。使用している場合は、推奨される代替手段に切り替えることを検討してください。

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティの修正 {#security-17465}

AEM as a Cloud Serviceは、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースは、特定された 7 つの脆弱性に対処し、堅牢なシステム保護への取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-17465}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.25.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
