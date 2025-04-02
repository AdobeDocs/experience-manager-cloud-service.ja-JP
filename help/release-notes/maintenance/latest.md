---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 7d93af706d8b0556e9e26282d339794447eb0a41
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 21%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 20133 {#20133}

2025年4月1日（PT）に公開された、メンテナンスリリース 20133 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 19823 でした。

2025.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-20133}

* ASSETS-47850:AEM CS が ES 有効になっている場合、Scene7 設定の追加を制限する
* CQ-4359547:https://git.corp.adobe.com/target-sdk/tsdk-core リポジトリから Guava が完全に削除される。
* FORMS-17551:SharePoint リスト統合でレコードのドキュメント（DoR）がサポートされるようになりました。
* FORMS-18432: フォーム固有の（正規表現ベースの）クライアントサイドの事前入力設定が実装されて、OSGI レベルを変更せずに選択的に事前入力機能が有効になりました。
* FORMS-18513: AEP コネクタにデータツリー変換のサポートを実装して、ウィザード機能とデータ処理機能を強化しました。
* FORMS-19068: フォームデータの統合機能を強化するために、Forms Manager API でAEP コネクタの送信アクションがサポートされるようになりました。
* GRANITE-57717:AEMでクライアントバンドルを更新します。
* SITES-10469: AdapterFactory は、常に同じ PageManager インスタンスを返す必要があります。
* SITES-25130：リリースコアコンポーネント 2.28.0。
* SITES-25433：古いバージョンを比較する際のフルページレンダリングをサポートします。
* SITES-25923:URL が保存されなくなった場合に、LinkInfoStorageImpl でブロックできるようになりました。
* SITES-26208：ワークフローを使用してコンテンツフラグメントを削除すると、新しく削除されたフラグメントを削除することで、参照リソースを更新できるオプションが追加されました。
* SITES-26500：ワークフロー – `move-fragments` を使用してコンテンツフラグメントを移動するオプションを追加。
* SITES-26711：ロールアウトトリガー- リンクが更新されない。
* SITES-27583：移動後にバージョン履歴が失われるエクスペリエンスフラグメント。
* SITES-27618：ページ内のフラグメントの参照を検索しても、必ずしもすべての結果が返されない。
* SITES-27781：コンテンツフラグメント参照のモデルレベル検証が実装され、参照されるフラグメントをモデル制約および必要なタグに照らして検証できるようになりました。
* SITES-27784: `jcr:path` の代わりに PATH 関数を使用するように SQL クエリの生成を更新します。
* SITES-28040:Adobe Target ExperienceFragmentsReplicationListener が壊れている。
* SITES-28051：コンテンツフラグメントに対する現在のユーザーの権限を取得します：GET /cf/fragments/{fragmentId}/permissions。
* SITES-28190：統合テストのプレビューのセットアップ。
* SITES-28227：フラグメントへの参照としてアセットを追加する場合、アセットが存在することを検証します。
* SITES-28248: OSGI 設定に基づいて Sites イベントを切り替えます。
* SITES-28255：作成、変更、公開の 3 つの監査プロパティすべてでフルネームが見つからない。
* SITES-28390: PageImpl：最適化 hasContent （）.
* SITES-28404：オーサー環境でページを削除すると、プレビューサービスから非公開になる。
* SITES-28446：応答に表示されない 2 つの新しいフィールド（NumberModelField のプレースホルダーと LongTextModelField の許可されたモデル）を追加しました。
* SITES-28536：コンテンツフラグメント `RENAME` エンドポイントを作成する。
* SITES-28537：ワークフロー – `rename-fragments` を使用してコンテンツフラグメントの名前を変更するオプションを追加。
* SITES-28538：オーサー環境とパブリッシュ環境で有効なコンテンツを維持するには、参照を再公開する必要があります。
* SITES-28549:AEM層に基づいてドメイン ID を返す `/cf/domains` を作成します。
* SITES-29026：言語と国コードを使用してコンテンツフラグメントのロケールを指定するオプションのパラメーターが追加されました。
* SITES-29031: PATCH処理フラグメントのロジックが改善され、パフォーマンスが向上しました。
* SITES-29169：移動、名前変更、または削除されたリソースを参照している場合、すべての公開済みリソースが（「公開済み」または「変更済み」ステータスであるかどうかに関係なく）再公開されます。
* SITES-29376：公開済みリソースの削除を検証するコード切り替えスイッチを追加。
* SITES-29417：を含めるのではなく、jcr:content ノードにリクエストを転送するように、/libs/cq/Page/proxy.jspを更新します。
* SITES-2947:kibana ビジュアライゼーションを作成/変更して、公開ラップを比較します。
* SITES-29733：コンテンツフラグメントのタグによるモデル検索のパフォーマンスが向上しました。
* SITES-8316: コンテンツポリシー：ContentPolicyManager をキャッシュします。
* SITES-24906：ユニバーサルエディターを使用したEdge Delivery：マッピングを使用せずに、作成者が作成したスプレッドシートをサポートする（アーリーアクセス）
* SITES-24907：ユニバーサルエディターを使用したEdge Delivery:MSM のユースケース向けに、複数のサイトへのAssetsの公開をサポート（アーリーアクセス）
* SITES-27956：ユニバーサルエディターを使用したEdge Delivery：公開スループットの向上（早期アクセス）
* SITES-27956：ユニバーサルエディターを使用したEdge Delivery:Edge Delivery Servicesに公開する際のエラー処理の改善（アーリーアクセス）

### 修正された問題 {#fixed-issues-20133}

* CQ-4358378：翻訳実行でのライセンスエラーの処理。
* CQ-4359263：ジョブの完了時に、ダイアログにメッセージが表示されない。
* CQ-4359386:AEMaaCS の翻訳プロジェクトに i18n 辞書を追加できない。
* FORMS-18068：リッチテキストフィールドを使用するラジオボタンおよびチェックボックスグループのレコードのドキュメント（DoR）で、太字テキストレンダリングの問題が発生する。
* FORMS-18189：空のクライアントライブラリのエラーがログに記録されないようにし、UI でのエラー表示を改善するために、カスタム関数処理を変更。
* FORMS-18213：レコードのドキュメント（DoR）から無効なフィールドを非表示/除外する機能が実装され、ドキュメントの明確さとユーザーエクスペリエンスが向上しました。
* FORMS-18271:Forms テーマエディターにローカライズされていないエラーメッセージが表示され、フォーム設定やテーマのカスタマイズのユーザーエクスペリエンスに影響する。
* FORMS-18304:Acrobatおよび LiveCycle ES4 で検証に成功したPDF/A-1b ドキュメントは、デバイス依存のカラーエラーが原因で、AEM 6.5 Formsで誤って非準拠としてフラグ付けされます。
* FORMS-18325: フォームデータの統合機能と処理機能を強化するためにAdobe Experience Platform（AEP）クラウド設定を追加しました。
* FORMS-18360: SharePoint Document Management でチームサイトのForms リスト範囲の管理を強化して、データ編成とアクセス制御を改善しました。
* FORMS-18375：特定の設定コンテナが選択されていない場合、基盤コンポーネントベースのフォームで `conf/global` フォルダーから recaptcha 設定が誤って選択される。
* FORMS-18426：リスト名に特殊文字（「–」など）が含まれていると、SharePoint リストとのフォームの統合に影響し、SharePoint リスト検索機能が失敗します。
* FORMS-19028：クライアントサイドの事前入力機能により、フォームイベントの処理が中断され、値の commit イベントや DOMContentLoaded イベントがフォーム読み込み時に正しくトリガーされない。
* FORMS-6950：スクリーンリーダーのアクセシビリティを向上し、WCAG 4.1.2 の名前、役割、値（レベル A）の標準に準拠するために、必要な ARIA ロールと属性がファイルシステムナビゲーターツリービューコンポーネントに追加されました。
* FORMS-7016：フォームエディターのキーボードフォーカスの順序が、論理的なナビゲーションに従わない。
* SITES-1960：コンテンツフラグメントエディターの JSON プレビュー操作のパフォーマンスが向上しました。
* SITES-24308：コンテンツのサイズが 400% に変更されると、水平スクロールバーが表示される。
* SITES-24493：必要な役割がインタラクティブ要素にない。
* SITES-24669：参照パネルウィンドウスプリッタにキーボードでアクセスできない。
* SITES-26881:AEMaaCS アクセシビリティのバグ – コメント入力フィールドの横にある「3 つのドット」アイコンに対して、誤った役割が提供される。
* SITES-26956: SITES-24920 のフォローアップ実稼動環境でページを移動できません。
* SITES-27707：アセット名の問題（6.5 SP22 回帰）が原因で、コンテンツファインダーのアセットの表示が失敗する。
* SITES-27757：ユニバーサルエディターを使用したEdge Delivery:helix-html-pipeline セマンティクスに従ってアイコンを書き換えます。
* SITES-27780:SP22 で、プレーンテキストの DefaultPasteMode を使用した RTE に予期しない &lt;br> タグが表示される。
* SITES-27958:Linkchecker が「このセッションは閉じられました」エラーをスローする。
* SITES-28149:Target への XF エクスポート中に、カスタム ExperienceFragmentLinkRewriterProvider がトリガーされない。
* SITES-28449：ワークフローウィジェット UI のバグ - AEMに、一部の子ページが表示されない子を含める。
* SITES-28456:GraphiQL エクスプローラーで誤った永続クエリを保存した場合、UI に通知が表示されない（フォローアップ - SITES-28313）。
* SITES-28464：形式が設定された日付（ミリ秒）を使用するようにフラグメントクエリを更新します。
* SITES-28486：新しいコンテンツフラグメントエディターでインプレース編集を行っても、古いエディターにリダイレクトされない。
* SITES-28570：アセットのメタデータが欠落している問題は、コンテンツフラグメントのGraphQLで適切に処理されます。
* SITES-28580:SP22 へのアップグレード後に、クラシック画像アセットファインダーが壊れる。
* SITES-28600：ローンチ – コンテンツの複製。
* SITES-28668:LaunchPromotionParameters でローンチを昇格できない。
* SITES-28820：リベース時に作成された新しいバリエーション内に、Launch プレフィックスが 2 回追加される。
* SITES-28877: ローカル Externalizer エンドポイントが定義されていない場合、URL サービスで例外がスローされるように設定しました。
* SITES-28956：タグがコンテンツフラグメントで参照されている場合、タグ削除操作で警告が表示される。
* SITES-29208：参照フィールドに無効なパスが含まれている場合、参照とバリエーションが適切に返されます。
* SITES-29363：ネストされたライブコピーコンテンツ階層に対して「ライブコピーをリセット」ボタンが機能しない。
* SITES-29369:AIO のAssets イベントの問題 | ページ公開済み/未公開イベントを誤ってトリガーする。
* SITES-29972：削除アクションや名前変更アクションによって、誤ったワークフローコメントが生成されることがある。

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

この非推奨（廃止予定）について詳しくは、ドキュメント [SPA エディターの非推奨（廃止予定） ](/help/implementing/developing/hybrid/spa-editor-deprecation.md) を参照してください。

### セキュリティ修正 {#security-20133}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 34 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-20133}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.28.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
