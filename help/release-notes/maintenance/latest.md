---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 100%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 16971 {#release-16971}

2024年7月3日（PT）に公開された、メンテナンスリリース 16971 の継続的な改善点を以下にまとめます。 以前のメンテナンスリリースは、リリース 16799 でした。

2024.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-16971}

* SITES-22948：AEM CS の基盤コンテンツ内のコマース参照を削除します。
* SITES-22141：[コンテンツフラグメント] OnRC 後の CFM ModelChangeRepositoryImpl からの SegmentNotFoundException。
* SITES-21893：オーサーインスタンスでの画像切り抜きの問題。
* SITES-21788：[コンテンツフラグメント] モデルに対して uiSchema が有効になっている場合、CF および CF モデル エディターでメモを表示します。
* SITES-21688：MSM ロールアウトで、ライブコピーページのエクスペリエンスフラグメント（XF）パスが更新されません。
* SITES-21659：モデルリソースを作成／変更／レプリケートするユーザーのフルネームを返します。
* SITES-21609： OpenAPI エンドポイントで、コンテンツフラグメントをモデル間で移行します。
* SITES-21598：[Open API] CFM を作成 - 指定した設定パスが存在しない場合は、エラーを返します。
* SITES-21491：[Open API] CF PATCH エンドポイントは、フィールドレベルでライブの関係を考慮する必要があります。
* SITES-21434：[Open API] CF GET エンドポイントは、フィールドレベルでライブの関係を考慮する必要があります。
* SITES-21415：CF エディター - UUID 参照をサポートします。
* SITES-21326：[Open API] コンテンツフラグメントの参照の存在に関する情報を提供します。
* SITES-21310：[Open API] 翻訳 API 応答にコンテンツフラグメントの ID を追加します。
* SITES-20859：CF Open API - パスでフラグメントを取得する際に参照を返します。
* SITES-20687：[Open API] バッチ処理ステータス取得用のエンドポイント。
* SITES-20657：[Open API] `FindAndReplace` エンドポイントを使用して文字列を置き換える際に、単語全体を一致させるオプションを提供します。
* SITES-20587：[Open API] コンテンツフラグメントの `COPY` エンドポイントを作成します。
* SITES-20584：[Open API] 参照の取得を最適化します。
* SITES-20308：[Open API] API でのバッチ処理を有効にします。
* SITES-19976：[Open API] 条件付きフィールドの汎用 UI スキーマ。
* SITES-19556：[コンテンツフラグメント] モデルを編集する際に、uiSchema が存在する場合は更新します。
* SITES-18056：[Open API] コンテンツフラグメントをプレビューに公開する際は、参照を含めます。
* SITES-16898：[スキーマ] OpenAPI エンドポイントで、コンテンツフラグメントをモデル間で移行します。
* SITES-16609：「ローンチをリスト表示」エンドポイント。
* SITES-16606：「ローンチを作成」エンドポイント。
* SITES-21617：[Xwalk] UE 内でページプロパティ／メタデータを編集可能にします。
* SITES-19614：[Xwalk] スプレッドシートエディターのページネーションと無限スクロールを実装します。
* SITES-22163：[Xwalk] Edge Delivery Sites のパブリッシュ層から提供されるコンテンツのサポートを改善しました。
* SITES-22109：[Xwalk] リッチテキストマークアップ後処理の処理を改善しました。
* SITES-22035：[Xwalk] MSM とローンチの処理を改善しました。
* SITES-21839：[Xwalk] Edge Delivery から提供されないコンテンツのパスマッピングとサニタイズを改善しました。

### 修正された問題 {#fixed-issues-16971}

* CQ-4356898：[翻訳] 非常に多数のリンクが含まれる CF の outOfMemory エラー。
* CQ-4357055：[翻訳] Rest API を使用した自動翻訳が機能しない。
* CQ-4353931：[翻訳] 翻訳ソースの page/xf/asset に jcr:uuid がない場合は追加される。
* CQ-4357591：[翻訳] Pages/XF で機能するように「Associate JCR:UUID」ワークフローを変更。
* FORMS-14844：アダプティブフォームで、reCAPTCHA 検証に失敗してもフォームの送信が許可される。
* FORMS-14984：CAPTCHA を使用したフォームで、送信したデータに「submitMetaData」が含まれていない場合、検証がスキップされる。
* FORMS-14477：ルールエディターの「次の後」および「次の前」オプションで、日付選択の検証で正常に動作しない。
* FORMS-14019：ルールエディターの「サービスを呼び出し」機能がユニバーサルエディターで機能しない。
* FORMS-14336：フォームフィールドを選択していない場合、エディターではフォーム要素全体に焦点を当てて開く必要がある。
* FORMS-15061：ルールエディターで「サービスを呼び出し」オプションを使用すると、ローダーの円が無期限に保持される。
* SITES-22457：ネスト深度がローンチを昇格してもソースコンテンツが更新されない。
* SITES-22748：[コンテンツフラグメント] コンテンツフラグメント更新ジョブのエラー処理を強化
* SITES-22349：[コンテンツフラグメント] 空の複数行 cf-elements の ContentType を変更できない。
* SITES-22343：[コンテンツフラグメント] セマンティックタイプの「列挙」が壊れる。
* SITES-22194：リダイレクトを設定した後、model.json が機能しない。
* SITES-21953: [Open API] etag が、validationStatus の順序に基づいて変更される。
* SITES-21894：[Open API] CF 作成時の親パス検証を強化。
* SITES-21887：[Open API] POST バリエーションエンドポイントによって無効な ETag が返される。
* SITES-21657：[Open API] CF 検索パスプロパティの検証を改善。
* SITES-21949：検索 API の無効なカーソルで 500 が返される。
* SITES-20927：クエリがない場合、検索 API で 500 が返される。
* SITES-20544：[Open API] Oak の競合を回避するために、公開パッケージ名の生成が変更される。
* SITES-19710：CVE-2022-47937 - ページエディターから org.apache.sling.commons.json の使用がすべて削除される。
* SITES-11992：[アクセシビリティ] 注釈スウォッチセレクターボタンに、アクセス可能な名前がない。
* SITES-10979：[アクセシビリティ] ラベルが永続的ではない。
* SITES-10962：[アクセシビリティ] ボタン：ボタンには役割がない。
* SITES-10905：[アクセシビリティ] アクティブコンポーネントの状態では、3 対 1 のコントラスト比が不足している。
* SITES-2974：[アクセシビリティ]  - 幅 320 px で水平スクロールが行われる。
* SITES-22026：AEM のフォルダー間でエクスペリエンスフラグメントを移動できない
* SITES-22106：新しいコンテンツフラグメントエディターの言語切り替え機能の問題
* SITES-21980：UUID ベースの参照タイプの処理に一貫性がない。
* SITES-7257：ThumbnailServlet の NPE。

### 既知の問題 {#known-issues-16971}

なし。

### 変更通知 {#change-notice-16971}

* 2024年9月以降、AEM as a Cloud Service では、Sling Model Exporter フレームワークを介したリソースリゾルバーのシリアル化が無効になります。 詳しくは、[ドキュメント](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)を参照してください。

### 非推奨（廃止予定）機能と API {#deprecated-16971}

AEM as a Cloud Service で非推奨（廃止予定）または削除された機能については、[非推奨（廃止予定）および削除された機能と API](/help/release-notes/deprecated-removed-features.md)を参照してください。

### 組み込みテクノロジー {#embedded-tech-16971}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.25.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
