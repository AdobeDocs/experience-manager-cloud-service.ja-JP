---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 636183e0597bed24b3e437ed53a35c9e64ac0504
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 21%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 19352 {#19352}

2025年2月5日に公開された、メンテナンスリリース 19352 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 19149 でした。

2025.2.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-19352}

* FORMS-13998：アコーディオンコンポーネントを追加。
* FORMS-17913：ラジオグループのカードバリアントを追加。
* FORMS-17333:AEM フォーム送信でHTMLメールテンプレートを有効にする。
* FORMS-17702:Output Sync API で生成されたPDFを Azure Blob Storage にアップロードできるようにします。
* SITES-28282：ユニバーサルエディターを使用したEdge Delivery：任意のページのベースパス、サイト名、組織をページ情報として提供します。
* SITES-27055：ユニバーサルエディターを使用したEdge Delivery：リバースプロキシサーブレットでクエリパラメーターをサポートします。
* SITES-26796：ユニバーサルエディターを使用したEdge Delivery：分類スプレッドシートのカスタム列をサポートします。
* SITES-26087：ユニバーサルエディターを使用したEdge Delivery：スプレッドシートへの CSV の書き出しをサポートします。
* SITES-26265：ユニバーサルエディターを使用したEdge Delivery：設定 UI で、Edge Deliveryと統合する TA アカウントを表示します。
* SITES-20372：ユニバーサルエディターを使用したEdge Delivery：スプレッドシート用の基本的な MSM ユースケースを有効にします。
* SITES-26681：ユニバーサルエディターを使用したEdge Delivery: オーサー上の分類スプレッドシート用に？sheet= パラメーターをサポートします。
* SITES-26479: [ スキーマ ] コンテンツフラグメントモデルのスケジュールされた公開ステータスエンドポイント。
* SITES-25944:[ ライブコピーの概要 ] ステータスを「ライブコピーが最新、制限付き継承」に追加
* SITES-28713: [V2] コンテンツスクレーパーに構造化データのサポートを追加。
* SITES-27896：通知時に自動的に開く「コメント」タブ
* SITES-26720：ユーザーがアセットセレクターからコレクション全体を選択できないようにする。
* SITES-27875：デフォルトでコンテナ内の編集可能なコンテンツを移動可能にします。
* SITES-28340:Dark Alley Universal Editor サービスプラグイン。
* SITES-26098：コンテンツフラグメントを公開する際に、参照ページを公開しない可能性があります。
* SITES-27789:DOM でのデータ属性 data-aue-component のサポート。
* SITES-25997：変更日をサポートするようにバリエーションを強化します。
* SITES-28023：リモートアセット参照のGraphQL出力（リポジトリ + アセット ID）。
* SITES-26058：コンテンツフラグメントモデルのスケジュールされた公開ステータスエンドポイント。
* SITES-25108:UUID 参照のモデル移行。
* SITES-26630：複数のコンテンツフラグメント用にコンテンツフラグメントのスケジュールされた公開ステータスエンドポイント。
* SITES-23432：削除参照機能の改善。
* SITES-25797：外部アセット参照のサポート - GraphQL。
* SITES-17514：コンテンツフラグメントを非公開にするためのエンドポイントの機能強化を削除する。
* SITES-14633：インストール前にコンテンツフラグメントモデルのペイロード作成の検証 – ドライラン。

### 修正された問題 {#fixed-issues-19352}

* CQ-4356756：関連アセットのサポートを翻訳しないでください。
* CQ-4358206：翻訳プロジェクトで繰り返し翻訳スケジューラーが機能しない。
* CQ-4358126：翻訳クラウドサービスで設定サブフォルダーを選択できない。
* FORMS-18098、FORMS-17954:Microsoft Edge ブラウザーの Internet Explorer モードで、アダプティブFormsを読み込めない。
* FORMS-17162：アセットを公開すると OOTB クエリが実行され、公開のパフォーマンスが低下します。
* SITES-28415：ユニバーサルエディターを使用したEdge Delivery：スプレッドシートの「プロパティを開く」ボタンを修正。
* SITES-26669：ユニバーサルエディターを使用したEdge Delivery:BOM がスプレッドシートになっている UTF-8 でエンコードされた CSV ファイルをアップロードする際の問題を修正しました。
* SITES-26543：ユニバーサルエディターを使用したEdge Delivery：間違ったマークアップをレンダリングするモデルを含めずに、空のブロックを修正します。
* SITES-26857：ユニバーサルエディターを使用したEdge Delivery：ファイルベース設定で UI に表示されるサイト認証トークンを修正します。
* SITES-26662：ユニバーサルエディターを使用したEdge Delivery：大文字と小文字を区別するバルクメタデータの問題を修正しました。
* SITES-28133:Publishから「プレビュー」に変更したことにより、実稼動環境でコンテンツを使用できる。
* SITES-27187：参照を含む、スケジュールされたページ/アセットのアクティベーション（試験的）が、参照を公開できません。
* SITES-27264:2 コンテンツフラグメント – ライブコピー作成関連の Selenium テストが、マスターで一貫して失敗する。
* SITES-26559：コンテンツフラグメントモデルのクエリを cqPageLucene インデックスにピン留めします。
* SITES-24469：インタラクティブ要素にキーボードでアクセスできない。
* SITES-24518：親参照テーブルの「名前」ボタンと「モデル」ボタンにキーボードでアクセスできない。
* SITES-27937: モデルを更新した後、UISchema 制約が null に設定されます。
* SITES-27852: モデル UISchema に分類がありません。
* SITES-27904：完全投影用のリスト/検索コンテンツフラグメントモデルに MetadataSchema が見つからない。
* SITES-26827：フラグメントのリストが無限ループに陥る。
* SITES-27678: [ パフォーマンス ]_references の不要な取得を防ぎます。
* SITES-27589：複数のコンテンツ/フラグメント参照フィールドを持つコンテンツフラグメントモデルで、UUID アップグレードに失敗する。
* SITES-26679：コンテンツフラグメントモデルを非公開にする場合は、公開済みの参照のみを検証する必要があります。
* SITES-26666:referencesTree エンドポイントと参照エンドポイントが異なる結果を返す。
* SITES-26499:GETフラグメントおよびPATCHでのタグフィールドの値の順序が正しくなく、順序がランダム化される。
* SITES-26585：スキーマの小さな説明エラーを修正。
* SITES-26647：エンドポイントを削除および UnpublishFragments 参照の検証が、管理者以外のユーザーの場合に失敗する可能性があります。
* SITES-26458: [ コンテンツフラグメントモデルを検索 ] レプリケーションステータスによるフィルタリングを修正。
* SITES-23513:[ コンテンツフラグメントモデルエディター ] 「フラグメント参照」 – 「許可されたコンテンツフラグメントモデル」プロパティの検証が失敗します。
* SITES-26575：プレビューからフラグメントを非公開にすると、previewStatus が更新される。
* SITES-26571: FT_SITES-12435 が有効な場合、ページ参照を保存できません。
* SITES-26660:@ContentType のタイプが「文字列」の場合、コンテンツフラグメントのバージョン比較が壊れる場合があります。
* SITES-26626：数値およびブール値フィールドに customErrorMessage がありません。
* SITES-26268：フラグメントの作成時に参照が無効な場合、誤ったステータスコードが返される。

### 既知の問題 {#known-issues-19352}

なし。

### 廃止された機能と API {#deprecated-19352}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-19352}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 36 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-19352}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
