---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8d7f23ef89de97ed656157ba628fd33206b4588
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 94%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 20133 {#20133}

2025年4月1日（PT）に公開された、メンテナンスリリース 20133 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 19823 でした。

2025.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-20133}

* ASSETS-47850：AEM CS で ES が有効な場合、Scene7 設定の追加を制限。
* CQ-4359547：Git リポジトリから Guava を完全に削除。
* FORMS-17551：SharePoint リスト統合に対するレコードのドキュメント（DoR）のサポートを追加。
* FORMS-18432：OSGI レベルの変更なしで選択的な事前入力機能を有効化するために、フォーム固有（正規表現ベース）のクライアントサイド事前入力設定を実装。
* FORMS-18513：ウィザード機能とデータ処理機能を強化するために、AEP コネクタにデータツリー変換サポートを実装。
* FORMS-19068：フォームデータ統合機能を強化するために、Forms Manager API に AEP コネクタ送信アクションのサポートを追加。
* GRANITE-57717：AEM でクライアントバンドルを更新。
* SITES-10469：AdapterFactory は常に同じ PageManager インスタンスを返す必要がある。
* SITES-25130：コアコンポーネント 2.28.0 をリリース。
* SITES-25433：古いバージョンを比較する際に、完全なページレンダリングをサポート。
* SITES-25923：URL が保存されていない場合、LinkInfoStorageImpl がブロックされる可能性がある。
* SITES-26208：ワークフロー経由でコンテンツフラグメントを削除すると、新しく削除されたフラグメントを削除することによって参照リソースを更新するオプションを使用できるようになる。
* SITES-26500：ワークフロー経由でコンテンツフラグメントを移動するオプション（`move-fragments`）を追加。
* SITES-26711：ロールアウトトリガー - リンクが更新されない。
* SITES-27583：エクスペリエンスフラグメントの移動後にバージョン履歴が失われる。
* SITES-27618：ページ内のフラグメントの参照を検索すると、すべての結果が返されない。
* SITES-27781：コンテンツフラグメント参照のモデルレベルの検証を実装し、モデル制約と必要なタグに対して参照されたフラグメントを検証できるようになる。
* SITES-27784：`jcr:path` の代わりに PATH 関数を使用するように SQL クエリ生成を更新。
* SITES-28040：Adobe Target ExperienceFragmentsReplicationListener が破損している。
* SITES-28051：コンテンツフラグメントに対する現在のユーザーの権限を取得します：GET /cf/fragments/{fragmentId}/permissions。
* SITES-28190：プレビュー統合テストの設定を行う。
* SITES-28227：フラグメントへの参照としてアセットを追加する際、アセットが存在することを検証。
* SITES-28248：OSGI 設定に基づいて Sites イベントを切り替える。
* SITES-28255：3 つのすべての監査プロパティ（作成、変更、公開）から完全な名前が欠落している。
* SITES-28390：PageImpl：hasContent() を最適化。
* SITES-28404：オーサー環境でページを削除すると、プレビューサービスからページが非公開になる。
* SITES-28446：応答に表示されなかった 2 つの新しいフィールド（NumberModelField のプレースホルダーと LongTextModelField からの許可されたモデル）を追加。
* SITES-28536：コンテンツフラグメントの `RENAME` エンドポイントを作成。
* SITES-28537：ワークフロー経由でコンテンツフラグメントの名前を変更するオプション（`rename-fragments`）を追加。
* SITES-28538：作成および公開時に有効なコンテンツを維持するために、参照を再公開する必要がある。
* SITES-28549：AEM 層に基づいてドメイン ID を返す `/cf/domains` を作成。
* SITES-29026：言語と国コードを使用してコンテンツフラグメントのロケールを指定するオプションのパラメーターを追加。
* SITES-29031：フラグメントを PATCH 処理するためのロジックを改善し、パフォーマンスを向上。
* SITES-29169：移動、名前変更または削除されたリソースを参照している場合、公開済みステータスのリソースが再公開される。
* SITES-29376：公開済みリソースの削除の検証にコード切替スイッチを追加。
* SITES-29417：リクエストを含めるのではなく jcr:content ノードに転送するように `/libs/cq/Page/proxy.jsp` を更新。
* SITES-2947：公開 RASP を比較できるように、Kibana ビジュアライゼーションを作成／変更。
* SITES-29733：コンテンツフラグメントのタグによるモデル検索のパフォーマンスを向上。
* SITES-8316：コンテンツポリシー：ContentPolicyManager をキャッシュ。
* SITES-24906：ユニバーサルエディターを使用した Edge Delivery：マッピングせずに、作成者が作成したスプレッドシートをサポート（早期アクセス）。
* SITES-24907：ユニバーサルエディターを使用した Edge Delivery：MSM のユースケース向けに複数のサイトへのアセットの公開をサポート（早期アクセス）。
* SITES-27956：ユニバーサルエディターを使用した Edge Delivery：公開スループットを向上（早期アクセス）。
* SITES-27956：ユニバーサルエディターを使用した Edge Delivery：Edge Delivery Services への公開に対するエラー処理を改善（早期アクセス）。
* SITES-29602:CIF:core-cif-components-core での Guava の使用の削除。
* SITES-25785:CIF:CIFの商品参照データタイプに対する商品バリアントの選択の追加。
* SITES-26392:CIF[ 試行用 ]:PDP のCIF コアコンポーネントにおける JSON+LD。
* SITES-21278:CIF[ 試験的 ]:CIFでキャッシュをクリアする機能。

### 修正された問題 {#fixed-issues-20133}

* CQ-4358378：翻訳実行でのライセンスエラーの処理。
* CQ-4359263：ジョブの完了時に、ダイアログにメッセージが表示されない。
* CQ-4359386：AEMaaCS の翻訳プロジェクトに i18n 辞書を追加できない。
* FORMS-18068：リッチテキストフィールドを使用するラジオボタンおよびチェックボックスグループのレコードのドキュメント（DoR）で、太字テキストレンダリングの問題が発生する。
* FORMS-18189：空のクライアントライブラリに対するエラーログを防ぎ、UI でのエラー表示を改善するために、カスタム関数処理を変更。
* FORMS-18213：レコードのドキュメント（DoR）から無効なフィールドを非表示／除外する機能を実装し、ドキュメントの明確さとユーザーエクスペリエンスを改善。
* FORMS-18271：Forms テーマエディターにローカライズされていないエラーメッセージが表示され、フォーム設定やテーマのカスタマイズのユーザーエクスペリエンスに影響を与えている。
* FORMS-18304：Acrobat および LiveCycle ES4 で検証に成功した PDF/A-1b ドキュメントが、デバイス依存のカラーエラーにより、AEM 6.5 Forms で誤って非準拠としてフラグ付けされる。
* FORMS-18325：フォームデータの統合機能と処理機能を強化するために Adobe Experience Platform（AEP）クラウド設定を追加。
* FORMS-18360：Forms ドキュメント管理のチームサイトの SharePoint リストスコープ管理を強化し、データの整理とアクセス制御を改善。
* FORMS-18375：基盤コンポーネントベースのフォームで、特定の設定コンテナを選択していない場合、`conf/global` フォルダーから reCAPTCHA 設定が誤って選択される。
* FORMS-18426：リスト名に特殊文字（例：「-」）が含まれている場合、SharePoint リストのルックアップ機能でエラーが発生し、SharePoint リストとのフォーム統合に影響を与えている。
* FORMS-19028：クライアントサイドの事前入力機能によりフォームイベントの処理が中断され、フォームの読み込み時に値コミットイベントと DOMContentLoaded イベントが適切にトリガーされなくなる。
* FORMS-6950：スクリーンリーダーのアクセシビリティを向上し、WCAG 4.1.2 の名前、役割、値（レベル A）標準に準拠するために、ファイルシステムナビゲーターのツリービューコンポーネントに必要な ARIA の役割と属性を追加。
* FORMS-7016：フォームエディターのキーボードのフォーカス順序が論理ナビゲーションに従わない。
* SITES-1960：コンテンツフラグメントエディターの JSON プレビュー操作のパフォーマンスを向上。
* SITES-24308：コンテンツのサイズを 400％に変更すると、水平スクロールバーが表示される。
* SITES-24493：インタラクティブ要素に必要な役割がない。
* SITES-24669：参照パネルウィンドウスプリッタにキーボードでアクセスできない。
* SITES-26881：AEMaaCS アクセシビリティのバグ - コメント入力フィールドの横にある「3 つのドット」アイコンに対して、誤った役割が指定される。
* SITES-26956：SITES-24920 のフォローアップ：本番環境でページを移動できない。
* SITES-27707：アセット名の問題（6.5 SP22 回帰）により、コンテンツファインダーのアセットの一覧表示が失敗する。
* SITES-27757：ユニバーサルエディターを使用した Edge Delivery：helix-html-pipeline セマンティクスに従ってアイコンが書き換えられる。
* SITES-27780：SP22 のプレーンテキスト DefaultPasteMode で RTE に予期しない &lt;br> タグが表示される。
* SITES-27958：リンクチェッカーが「このセッションは閉じられました」エラーをスローする。
* SITES-28149：ターゲットへの XF 書き出し中にカスタム ExperienceFragmentLinkRewriterProvider がトリガーされない。
* SITES-28449：ワークフローウィジェット UI のバグ - 子を含めると AEM のすべての子ページが表示されない。
* SITES-28456：GraphiQL Explorer で誤った永続クエリを保存した場合、UI に通知が表示されない（フォローアップ - SITES-28313）。
* SITES-28464：フラグメントクエリを更新して、ミリ秒で書式設定された日付を使用。
* SITES-28486：新しいコンテンツフラグメントエディターでのインプレース編集で、古いエディターにリダイレクトされない。
* SITES-28570：欠落しているアセットメタデータが、コンテンツフラグメントの GraphQL によって適切に処理される。
* SITES-28580：SP22 へのアップグレード後に、クラシック画像アセットファインダーが破損する。
* SITES-28600：ローンチ - コンテンツの複製。
* SITES-28668：LaunchPromotionParameters でローンチを昇格できない。
* SITES-28820：リベース時に作成した新しいバリエーション内に、ローンチプレフィックスが 2 回追加される。
* SITES-28877：ローカル Externalizer エンドポイントを定義していない場合、UE URL サービスが例外をスローする。
* SITES-28956：タグをコンテンツフラグメントで参照している場合、タグ削除操作で警告が表示される。
* SITES-29208：参照フィールドに無効なパスが含まれている場合でも、参照とバリエーションが適切に返される。
* SITES-29363：ネストされたライブコピーコンテンツ階層に対して「ライブコピーをリセット」ボタンが機能しない。
* SITES-29369：AIO のアセットイベントの問題 | ページ公開済み／未公開イベントが誤ってトリガーされる。
* SITES-29972：削除および名前変更アクションにより、誤ったワークフローコメントが生成される場合がある。
* SITES-24631:CIF：商品フィールドの検索の問題。
* SITES-24902:CIF：製品の URL 形式が#variant_sku で期待どおりに動作しない。
* SITES-29191:CIF：商品リストコンポーネントに 20 個を超える SKU を追加できない。

### 既知の問題 {#known-issues-20133}

なし。

### 廃止された機能と API {#deprecated-20133}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

#### ユーザーグループと製品プロファイルの同期の変更 {#changes-user-groups}

権限管理に Adobe Admin Console を使用する際、次のグループは AEM に同期されなくなるので、使用しないでください。
* _GROUP_NAME_SUFFIX で終わる AEM グループ。
* 他の環境、プログラム、製品からの製品プロファイル。

詳しくは、[ユーザーグループと製品プロファイルの同期の変更](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)を参照してください。

#### SPA エディターの廃止 {#deprecate-spa-editor}

[SPA エディター](/help/implementing/developing/hybrid/introduction.md)は、リリース 2025.4.0 以降の新しいプロジェクトでは廃止されました。SPA エディターは、既存のプロジェクトでは引き続きサポートされますが、新しいプロジェクトには使用しないでください。

AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のとおりです。

* ビジュアル編集用の[ユニバーサルエディター](/help/edge/wysiwyg-authoring/authoring.md)。
* フォームベース編集用の[コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-managing.md)。

この廃止について詳しくは、[SPA エディターの廃止](/help/implementing/developing/hybrid/spa-editor-deprecation.md)ドキュメントを参照してください。

### セキュリティ修正 {#security-20133}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 34 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-20133}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.28.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
