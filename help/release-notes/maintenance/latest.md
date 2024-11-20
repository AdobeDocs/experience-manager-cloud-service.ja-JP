---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f9f3d1fcb32445269e5ca4b9479b8e9075c73c10
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 98%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 18598 {#18598}

2024年11月13日（PT）に公開された、メンテナンスリリース 18598 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 18311 でした。リリース 18459 は、問題が発生したことにより非公開になりました。

2024.11.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-18598}

* CQ-4357471：AEMaaCS に i18n 辞書翻訳のサポートを追加。
* FORMS-11646：AEM Forms 関連ページの globalContext 変数を設定。
* FORMS-14833：AEM Forms には、最終的なレコードのドキュメント（DoR）にアダプティブフォームフラグメントを含める機能が搭載されました。
* FORMS-14255：一部が完了したフォームを自動的にドラフトとして保存する、自動保存機能を利用できるようになりました。後で戻って、同じデバイスまたは他のデバイスで入力を完了できます。
* SITES-23591：コンテンツフラグメント：UUID サポートのコンテンツフラグメントのアップグレード。
* SITES-25440：コンテンツフラグメント：レプリケーションステータスを表示する CFM 検索 API。
* SITES-24369：コンテンツフラグメント：OpenAPI ドキュメントの改善。
* SITES-25478：コンテンツフラグメント：外部アセット参照のバックエンドサポートを追加。
* SITES-26119：コンテンツフラグメント：参照タイプに外部アセット参照のサポートを追加。
* SITES-24609：コンテンツフラグメント：コンテンツフラグメントを削除する際の検証を強化します。
* SITES-21199：ユニバーサルエディターを使用した Edge Delivery：ページから作成されたテンプレートのサポートを追加。
* SITES-20311：ユニバーサルエディターを使用した Edge Delivery：CSV をスプレッドシートに読み込むサポートを追加。
* SITES-24821：ユニバーサルエディターを使用した Edge Delivery：aem.page／aem.live をデフォルトに設定して Edge Delivery と統合。

### 修正された問題 {#fixed-issues-18598}

* CQ-4358730：翻訳するキーが 10 個を超えると、CQPagePreviewGenerator が失敗する。
* CQ-4358028：プロジェクト管理者グループのみを持つユーザーがプロジェクト作成ページで新しいサムネールをアップロードすると、AEM プロジェクトの作成が失敗する。
* FORMS-14978：テーマエディターのコアコンポーネントベースのフォームのページ読み込みが有効になる。
* FORMS-15682：AEM Forms と Dynamics FDM の統合に問題が含まれる。ユーザーがフォームを送信すると、指定したエンティティフィールドにレコードのドキュメント（DOR）が PDF 添付ファイルとして送信されない。
* FORMS-15799：Adobe Sign GovCloud 署名ページが iframe でレンダリングされない。
* FORMS-16113：Adobe Sign アカウントの管理者であるユーザーが、別のユーザー（または管理者）によって送信されたドキュメントにアクセスしようとすると、契約の作成時に最初に生成されたものとは異なる契約 ID が get agreement API から返される場合がある。
* FORMS-16596：アクセシビリティの問題：無効なボタンがスクリーンリーダーで認識されない。
* GRANITE-53907：サービスユーザーをワークフロースーパーユーザーとして識別できない。
* SKYOPS-90560：最新の Sling Model リリースが、Sling Model の書き出しのパフォーマンスに影響を与える。
* SITES-10575：MSM：ブループリントブルームフィルターローダーが 100,000 行を超える行を読み込もうとする。
* SITES-20755：コンテンツフラグメント：UUID 更新によるアセット参照で、サムネールが表示されない。
* SITES-26253：コンテンツフラグメント：UUID の移行：Sling ジョブのトピックが汎用に変更される。
* SITES-21338：コンテンツフラグメント：referencedBy エンドポイントが正しいページ参照を返さない。
* SITES-24421：コンテンツフラグメント：CF を編集エンドポイントが、GET CF 経由で取得した CF に対して機能しない。
* SITES-25461：コンテンツフラグメント：CF を検索する際のモデルによるフィルタリングでは、大文字と小文字を区別しないにする必要がある。
* SITES-25471：コンテンツフラグメント：ModelValidatorServlet でのグローバルモデルの検証を修正。
* SITES-25795：コンテンツフラグメント：cq の日付が設定されていない場合、CF モデル API が失敗する。
* SITES-25817：コンテンツフラグメント：PromoteLaunch の強化：CF ローンチの最新プロモーションを更新。
* SITES-26030：コンテンツフラグメント：エンドポイント /referencesTree が必要なヘッダーを返さない。
* SITES-26031：コンテンツフラグメント：CFM 検索エンドポイントでレプリケーションステータスが返されない。
* SITES-26213：コンテンツフラグメント：コンテンツフラグメントを非公開にする場合は、公開済みの参照のみを検証する必要がある。
* SITES-26226：コンテンツフラグメント：指定されたパスのいずれも使用できない場合にワークフローの問題が開始される。
* SITES-26238：コンテンツフラグメント：API によって返されるアセット参照の順序が、JCR からの順序とは異なる。
* SITES-25456：イベント：ページを移動する際、ページ移動イベントの他に、ページ削除イベントが生成される。
* SITES-25658：イベント：層と sourceUrl が、ページコンテンツ状態イベントに入力されない。
* SITES-6497：ローンチ：ローンチでページを作成が機能しない。
* SITES-25938：ローンチ：翻訳プロジェクト後に予期しない削除が発生する。
* SITES-25393：ユニバーサルエディターを使用した Edge Delivery：単一の段落で書式設定されたリッチテキストをレンダリングする際にテキストノードが失われる。
* SITES-24643：ユニバーサルエディターを使用した Edge Delivery：OpenGraph および Twitter メタデータ属性がページメタデータモデルで機能しない。
* SITES-25401：エクスペリエンスフラグメント：XF 参照の更新が遅れる。

### 既知の問題 {#known-issues-18598}

なし。

### 廃止された機能と API {#deprecated-18598}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-18598}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 21 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-18598}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
