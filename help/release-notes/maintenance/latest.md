---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 7ae30d2053a17c2855c66b265c831ea27d19d535
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 13%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 21331 {#21331}

2025年6月24日（PT）に公開された、メンテナンスリリース 21331 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 21193 でした。

2025.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-21331}

* CQ-4356522:`WorkflowResourceStatusProvider` の最適化。
* FORMS-16458：フォントプロパティを選択するための UI （書体）。
* FORMS-17707:AEP コネクタがAEP platform ステージで機能しない。
* FORMS-19125:AF エディターで自動フラグメントマッピングをサポート。
* FORMS-19336:AF エディターの Data Source ツリーに追加された検索。
* FORMS-19417：階層表示でのラジオボタンのサポート。
* FORMS-19603：ルールエディターでマスターページとデザインページの両方をサポートします。
* SITES-10575:「MSM Blueprint Bloomfilter Loader」は、100000 行を超える読み込みを試みます。
* SITES-14542：ライブコピーソースページの名前変更または移動は、以前に公開されていた場合に備えて、名前変更または移動が行われたライブコピーページの公開でトリガーが発生する場合があります。
* SITES-19754：ユニバーサルエディターを使用したEdge Delivery：統合で問題が発生した場合に、人間が読み取れるエラーメッセージを追加します。
* SITES-23499：ユニバーサルエディターを使用したEdge Delivery：ブロックオプションに使用する複数のフィールドのサポートを追加。
* SITES-23518：ユニバーサルエディターを使用したEdge Delivery:Edge Delivery固有のアセットレンディションのサポートを追加。
* SITES-25913：コンテンツフラグメント Rest API：公開ワークフローを開始する前に、リソースのタイムボックス検証を行います。
* SITES-25976:MSM ロールアウト後にエクスペリエンスフラグメント内のリンクが適応しない。
* SITES-26271：コンテンツフラグメント Rest API:GET バリエーションエンドポイントの BFS トラバーサルに切り替えます。
* SITES-27486：ユニバーサルエディター – AEM統合。
* SITES-27775：公開中に最適化された参照検索（メタデータの遅延読み込み）。
* SITES-27782：ユニバーサルエディターを使用したEdge Delivery：特定のパブリッシャー/サブスクライバー実装を追加して、コンテンツをEdge Deliveryに公開する（アーリーアクセス）。
* SITES-27792：ユニバーサルエディターを使用したEdge Delivery：専用のEdge Delivery サービス設定テンプレートを追加する。
* SITES-28683:MSM LiveRelationship 検索で詳細ステータスをスキップできるようにします。
* SITES-29930：コンテンツフラグメント Rest API：コンテンツフラグメント公開ワークフローの指標を追加します。
* SITES-29986：コンテンツフラグメント Rest API:CF モデルの技術的な命名をサポートします。
* SITES-30088：コンテンツフラグメント Rest API:CF 公開 – filterReferencesByStatus が空の場合、参照の取得をスキップします。
* SITES-30328：ユニバーサルエディターを使用したEdge Delivery:Sidekickからのプレビューのサポートを追加。
* SITES-30445：コンテンツフラグメント Rest API:CF モデル UI スキーマ：折りたたみ可能なの初期状態を制御するオプションを追加します。
* SITES-30604：コンテンツフラグメント Rest API：新しい UI でのモデルメタデータスキーマの採用をサポートします。
* SITES-30885：永続クエリでの JSON 処理を最適化しました。
* SITES-30886：コンテンツフラグメント Rest API：ワークフローメタデータに保存されたフラグメント UUID に基づく、コンテンツフラグメントエンドポイント用のGET ワークフロー。
* SITES-31005：ロールアウトジョブ UI を強化して進行状況を表示します。
* SITES-31020: ライブコピージョブ UI の作成を強化して進行状況を表示します。
* SITES-31472：ローンチが大量の場合、ローンチを削除するとリポジトリが一時停止する可能性があります。
* SITES-31677：カスタムワークスペースは、Target へのAEM コンテンツフラグメントの書き出しをサポートします。
* SITES-31782：コンテンツフラグメント Rest API：ローカルアセットの説明を追加します。
* SITES-32175：ライブコピーの作成と MSM ページロールアウトの両方で中間コミットを許可します。
* SITES-5358：コンテンツフラグメント Rest API:CF を子と共にコピーします。

### 修正された問題 {#fixed-issues-21331}

* CQ-4359756：翻訳ルールに、コンポーネントレベルのフィルタープロパティが含まれるようになりました。
* CQ-4359826：コンテンツフラグメント参照パネルでの一貫性のないステータスを解決します。
* CQ-4359866:LanguageUtils クラスで、依存関係を追加せずに単体テストをサポートするようになりました。
* FORMS-13990:Forms サービス API：ドキュメント生成：選択後、空のままにした場合、期待される値が 400 の場合、データフィールドに 200 が表示される。
* FORMS-14309:Forms サービス API : データ応答コードの修正を抽出します。
* FORMS-18526：条件に複数のフィールドを含むルールをコピーしても、固定フィールドが変わらない。
* FORMS-18977:DOR サービスがドキュメントのタイトルを渡していない。
* FORMS-19047:SP22 でAEM Formsにアダプティブフォームを公開すると、翻訳が欠落する。
* FORMS-19234:AEM forms で PDF のタイムライン機能を使用できない。
* FORMS-19628：自動生成された DOR で、ネストされたパネルタイトルを除外すると、ルートパネルタイトルが非表示になる。
* FORMS-19651：クリックされたボタンがバイナリ条件で使用され、その後 then ステートメントでも同じボタンが使用される場合にルールを修正します。
* FORMS-19808:FormsPortal – 遅延読み込みが有効な場合、ドラフトを取得できない。
* FORMS-19887:HTML5 プレビューでアクセスプロパティが機能しない。
* SITES-15452：一意の CF 要素をローンチ内のコピーと照合しないでください。
* SITES-24492:ARIA タブリストにアクセス可能な名前がない。
* SITES-24623：コンテンツフラグメント Rest API：同じ CF のエンドポイント間の ETag 不一致を修正しました。
* SITES-24668：ズームが 400% に増えると、参照レール機能が機能しなくなる。
* SITES-24678：参照レールのステータスメッセージがスクリーンリーダーによって読み上げられない。
* SITES-24697：画像モデルの読み込み状態がスクリーンリーダーによって読み上げられない。
* SITES-24708：ズームが 400% に増えると、フィルターレール機能が機能しなくなる。
* SITES-25235：フィルターパネルのコンテンツ読み込みメッセージがスクリーンリーダーで読み上げられない。
* SITES-25254：コンテンツを 320 px で表示すると、カルーセルモーダルに水平スクロールバーが表示される。
* SITES-25433：ユニバーサルエディターを使用したEdge Delivery：多言語サイト構造のページバージョンのレンダリングを修正しました。
* SITES-26890：キーボードの使用中、「テーブルヘッダー」範囲のキーボードフォーカスが「公開を管理」ページに表示されない。
* SITES-29075：大容量の Web サイトでライブコピーの概要が機能しない。
* SITES-29514：ユニバーサルエディターを使用したEdge Delivery：新しいサイトを作成する際に、GitHub/プロジェクト URL を必須にします。
* SITES-29691：特定のローンチに関連するケースで、ページを移動できない。
* SITES-29745：コンテンツフラグメント Rest API:BFS トラバーサルでの参照のバリエーションの水和を実装します。
* SITES-29748: レンダリング条件を修正して、CF エディター内で managepublication/quickpublish アクションを表示する。
* SITES-29789：コピーされたルートページのコンポーネントリンクの変更の問題。
* SITES-29987：コンテンツフラグメント Rest API：コンテンツフラグメントモデルの作成と編集では `previewUrlPattern` をサポートしていません。
* SITES-30140：コンテンツフラグメントの参照を作成する際のデュアルウィンドウの問題。
* SITES-30260：コンテンツフラグメント Rest API：最新の ETag を使用して CF を更新/削除する際のエラー。
* SITES-30327：コンテンツフラグメント Rest API：権限のない CF を公開すると、ペイロードリソースごとに個別のワークフローが作成される。
* SITES-30333:xmp の解析の問題を回避するために、jcr からアセットメタデータを読み取ります。
* SITES-30353:AEM コンテンツフラグメントの「src」フィールドに対するGraphQL DataFetchingExceptions。
* SITES-30377：ユニバーサルエディターを使用したEdge Delivery：組織名とサイト名を削除する
* SITES-30386：ユニバーサルエディターを使用したEdge Delivery：重複した従来の UE `cors.js` を削除する。
* SITES-30583：コンテンツフラグメント Rest API：検索と置換ツールで、すべての文字を小文字に変更する。
* SITES-30585：コンテンツフラグメント Rest API：参照を含む CFM の作成時に設定されませ `previewUrlPattern`。
* SITES-30634:RTE 画像の代替テキストと配置が一貫して機能しない。
* SITES-30660：カスタム AEM コンポーネントの ADA コンプライアンスの問題。
* SITES-30695：ユニバーサルエディターを使用したEdge Delivery: カスタムコードを妨げないように、リライターパイプラインのランキングを上げます。
* SITES-30727：実稼動オーサーエディターにコンポーネントをドラッグ&amp;ドロップできない。
* SITES-30752：永続クエリ応答を生成する際に、`If-modified-since`/`last-modified` ヘッダーを使用しないでください。
* SITES-30871:afteredit リスナーがトリガーされた後に DOM が更新される。
* SITES-30877：子ページのロールアウトステータスが正しくありません。
* SITES-30899:「後で」ロールアウト オプションを使用すると、日付を選択せずに続行できます。
* SITES-30947：ロールアウト時にブループリントに「behavior」プロパティがないことが原因で、ヌルポインター例外が発生する。
* SITES-31157：コンテンツフラグメント Rest API:patch Failes は、特定のケースで発生します。
* SITES-31272:PageManager.copy からAssets言語コピーを作成できない。
* SITES-31327：コンテンツフラグメント Rest API:GET フラグメントリクエストで ETag 検証を削除します。
* SITES-31387：ゴーストコンポーネントの継承を再度有効にすると、JavaScript エラー「ns.ui.alert は関数ではありません」。
* SITES-31455：コンテンツフラグメント Rest API：同じコンテンツフラグメントモデルのエンドポイント間の ETag 不一致を修正しました。
* SITES-31459：コンテンツフラグメント Rest API：コンテンツ参照フィールドがある場合、CF ライブコピーを編集できません。
* SITES-31467：ページエディターの contexthub.authoring-hook.js の js-errors。
* SITES-31594：コンテンツフラグメント Rest API:`extractMetadataSchemaFieldLabel` エラー。
* SITES-31621：ユニバーサルエディターを使用したEdge Delivery：ライブコピーであるスプレッドシートから空の行を削除します。
* SITES-31676：コンポーネントをオーサリングまたは削除すると、ページ下部に空白が残る。
* SITES-31822:ClassicUI のチェックボックスラベルが見つからず、エンコードされたHTML。
* SITES-31857：一重引用符が付いたフォルダーで、CF の作成が失敗する。
* SITES-31888：コンテンツフラグメントの削除が、プレビューに反映されない。
* SITES-31922：コンテンツフラグメント Rest API：ページ参照が referencedBy エンドポイントから返されない。
* SITES-31987：コンテンツフラグメントをプレビュー用に公開する際に、そのプレビュー URL を表示しない。
* SITES-32095：ライブコピーの after childdelete イベントリスナーで自動更新が失敗する。
* SITES-32237：ユニバーサルエディターを使用したEdge Delivery：空のテキストコンポーネントや形式が正しくないテキストコンポーネントのレンダリングを修正します。

### 既知の問題 {#known-issues-21331}

なし。

### 廃止された機能と API {#deprecated-21331}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-21331}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 21 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-21331}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
