---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9d081b468e42306c56238bee6117d92c6afd48d4
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 25%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 23122 {#23122}

2025年10月29日（PT）に公開された、メンテナンスリリース 23122 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 22943 でした。

2025.11.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-23122}

* FORMS-21594：コンテンツ作成者が、インタラクティブ通信テンプレートのコンテンツとレイアウトをロックできるようにします。
* FORMS-20385：インタラクティブ通信エディターでの XDP 編集のサポート。
* FORMS-10883:API を介して送信されたリッチテキストデータの正確なレンダリングを保証するために、DoR 生成で XHTML 名前空間タグを使用した JSON がサポートされます。
* FORMS-21751：キャンバス機能 – テキストオーバーフロー、改ページ用 UI
* FORMS-22049:Interactive Communications Editor - Spectrum 2 への移行。
* FORMS-22050：インタラクティブ通信エディターでの動的なページ番号のサポート。
* FORMS-21606：インタラクティブ通信用のパブリック OSGi レンダリング SPI。
* FORMS-21613: Render Interactive Communications SPI のトランザクションレポートとパフォーマンスログ。
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

### 修正された問題 {#fixed-issues-23122}

* CQ-4361144：翻訳ジョブからのコンテンツフラグメントのスキップを修正しました。
* CQ-4355446：翻訳ジョブをキャンセルダイアログで発生した翻訳プロジェクトのローカライズされていない文字列を修正。
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

### 既知の問題 {#known-issues-23122}

なし。

### 廃止された機能と API {#deprecated-23122}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-23122}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 18 個の脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-23122}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.30.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
