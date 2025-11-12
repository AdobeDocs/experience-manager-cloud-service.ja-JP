---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c58e4645ddc9390728d6ac5cf92588caaeffae01
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 20%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 23320 {#23320}

2025年11月12日（PT）に公開された、メンテナンスリリース 23320 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 22943 でした。

2025.11.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

>[!NOTE]
>
>リリース 23122 は 11 月 3 日に非公開になりました。

### 機能強化 {#enhancements-23320}

* CQ-4361363：最新の AEM および Granite の翻訳。
* FORMS-21594：コンテンツ作成者が、インタラクティブ通信テンプレートのコンテンツとレイアウトをロックできるようにします。
* FORMS-20385：インタラクティブ通信エディターでの XDP 編集のサポート。
* FORMS-10883:API を介して送信されたリッチテキストデータの正確なレンダリングを保証するために、DoR 生成で XHTML 名前空間タグを使用した JSON がサポートされます。
* FORMS-21751：キャンバス機能 – テキストオーバーフロー、改ページ用 UI
* FORMS-22049:Interactive Communications Editor - Spectrum 2 への移行。
* FORMS-22050：インタラクティブ通信エディターでの動的なページ番号のサポート。
* FORMS-21606：インタラクティブ通信用のパブリック OSGi レンダリング SPI。
* FORMS-21613: Render Interactive Communications SPI のトランザクションレポートとパフォーマンスログ。
* GRANITE-62394: joda-time を 2.12.7 に更新しました。
* GRANITE-36205:Oak リリースを 1.88.0 に更新します。
* GRANITE-62020:`RepositoryServiceHttpClient` の再試行ポリシーを改善しました。
* GRANITE-62169: commons-lang を 3.19.0 に更新します。
* SITES-35092：コンテンツフラグメント – 新しい Mixin と、セマンティック検索のアップグレード手順。
* SITES-32319：配信 OpenAPI - サポートページリファレンス。
* SITES-20123:GraphQL:JSON 応答で上付き文字要素をサポートします。
* SITES-34744：サムネールのレンダリングに使用できるデータを含む、コンテンツフラグメント応答内の新しい「card」プロパティ。
* SITES-34571：列挙フィールドを空にすることができます。
* SITES-34812：値「none」を持つ「references」パラメーターを使用して、参照なしでコンテンツフラグメントを取得する機能が追加されました。
* SITES-35176：タッチ UI を使用してコンテンツフラグメントをチェックアウトする際に、新しいエディターで他のユーザーがコンテンツフラグメントを編集できなくなりました。
* SITES-30371:uuid ベースの参照フィールドのサポートを追加。
* SITES-19309：ページ移動ウィザードを開いたときに、最大 150 個の参照を取得します。
* SITES-32515：ユニバーサルエディターを使用したEdge Delivery – 複数フィールドおよび複合複数フィールドのサポートを追加しました（アーリーアクセス）。
* SITES-33784：ユニバーサルエディターを使用したEdge Delivery - ページメタデータで ld-json のサポートを追加。
* SITES-34832：ユニバーサルエディターを使用したEdge Delivery - ページのパブリックパスを page info サーブレットの応答に追加する
* SITES-25893：ユニバーサルエディターを備えたEdge Delivery - ブロック内のテキストレンダリングに対する強力で強調のサポートを追加。
* SITES-26158：ユニバーサルエディターを使用したEdge Delivery - ブロックおよび列でのテーブルマークアップのサポートを追加しました（アーリーアクセス）。
* SITES-27949：ユニバーサルエディターを使用したEdge Delivery - パスマッピングをオプションにします。
* SITES-35811：コンテンツフラグメントクエリで新しいインデックスを使用します。
* SKYOPS-120857: filevault を 4.1.4 に更新します。
* SKYOPS-118390: JCR リソースを 3.3.6 に更新します。
* SKYOPS-121082:`org.apache.sling.discovery.standalone`、`org.apache.sling.jcr.packageinit` および `org.apache.sling.commons.fsclassloader` Sling バンドルのバージョンを更新します。

### 修正された問題 {#fixed-issues-23320}

* ASSETS-58926:DM のビデオ変更サムネール機能を修正。
* ASSETS-58623：設定が存在する場合、オムニサーチで npe を修正。
* CQ-4361144：翻訳ジョブからのコンテンツフラグメントのスキップを修正しました。
* CQ-4355446：翻訳ジョブをキャンセルダイアログで発生した翻訳プロジェクトのローカライズされていない文字列を修正。
* CQ-4360747：繰り返し可能なトリガージョブによって空のペイロードや翻訳が頻繁に作成される問題を修正しました。
* GRANITE-61318：ページ作成ウィザードの「基本」タブで必須フィールドのみがハイライト表示される問題を修正しました。
* GRANITE-60514：フルスタックパイプラインの実行中にスケジュールされたパブリケーションが停止する問題を修正しました。
* GRANITE-61019:AEMの再起動後に初めて実行する際の GC の問題を修正。
* GRANITE-60456：管理者がユーザーのプロパティページを開く際の問題を修正。
* SITES-34555:GraphQL - デプロイメント後の QueryValidationError。
* SITES-35077：コンテンツフラグメント - URL エンコーディングが正しくないことが原因で、括弧で囲まれたフラグメントで非公開が失敗します。
* SITES-35374：コンテンツフラグメント – 編集したコンテンツフラグメントが戻った後に表示されない。
* SITES-36130:`EditorRestrictionsStatusImpl` の NPE。
* SITES-35810：ローンチの NullPointerException が publishEdgeDeliverySubscriber キューをブロックする。
* SITES-34368:AEM CIFは、12 個のGraphQL エイリアスを生成します。Magento 2.4.6-P12 の制限である 10 を超えます。
* SITES-36193:CCS コネクタの修正。
* SITES-35169：検索で無効なフラグメントリソースが返された場合に、誤ったページネーションが発生する問題を解決しました。
* SITES-34574：場合によってはコンテンツフラグメント検索 API でカーソルが返されない問題を修正しました。
* SITES-35520：コンテンツを公開しようとすると ClassCastException またはタイムアウトが発生する問題を修正しました。
* SITES-35210：空の参照フィルターを含む壊れたフラグメントを公開しようとすると発生する NullPointerException を修正しました。
* SITES-35933：コンテンツフラグメントの公開後に、空の「アクティベーションをリクエスト」ワークフローがトリガーされるバグを修正しました。
* SITES-35925：コンテンツフラグメントモデルのパッチ適用に関連して、モデルから「翻訳可能」および「showThumbnail」プロパティが削除されるバグを修正しました。
* SITES-35409：ページを移動する際に、調整されたフラグメントを再公開できないバグを修正しました。
* SITES-15757：ページを移動する際に、調整済みページを再公開できないバグを修正しました。
* SITES-34638：新しいバージョンを作成する際に、祖父母のページのプロパティが含まれなかったバグを修正しました。
* SITES-35071: オムニサーチで引用符で囲まれた語句が使用されている場合、CSV エクスポートでフィルタリングされていない結果が返される。
* SITES-32182：ユニバーサルエディターを使用したEdge Delivery – 既にエンコードされたリクエストパラメーターを含む URL のエンコードの問題を修正します。
* SITES-34324：ユニバーサルエディターを使用したEdge Delivery - tel: プロトコルを使用したリンクのレンダリングを修正します。
* SITES-35333：ユニバーサルエディターを使用したEdge Delivery - ページメタデータ内の画像のアセットレンディション選択を修正しました。
* SITES-35549：ユニバーサルエディターを使用したEdge Delivery - ページメタデータ内の二重エンコードされた HTML エンティティを修正。

#### AEM ガイド {#guides-23320}

* GUIDES-33597：属性や値を持たない空の `prop` 要素を DITAVAL ファイルに追加した場合、追加の `prop` 要素を追加することはできません。
* GUIDES-33693：編集した画像をExperience Manager Guides UI から再度アップロードすると、画像の元のレンディションは更新されますが、関連する DITA コンテンツには、以前のバージョンの画像が引き続き表示されます。
* GUIDES-35607:Assets UI を使用してアセットをアップロードする際、またはエディターインターフェイスから新しいファイルを作成する際に生成されるエラーログで、ログメッセージに `predecessor` ではなく `successor` という用語が誤って使用されています。
* GUIDES-37649: （従来のコンポーネントマッピングを使用して）AEM Sites上でベースラインを使用して DITA マップを公開すると、属性 `processing-role = resource-only` を持つマップ要素も公開されます。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。


### 既知の問題 {#known-issues-23320}

なし。

### 廃止された機能と API {#deprecated-23320}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-23320}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 31 個の脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-23320}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.88.0 | [Oak 1.88.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.30.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
