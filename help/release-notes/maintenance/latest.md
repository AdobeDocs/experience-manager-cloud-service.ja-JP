---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 20%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 16971 {#release-16971}

2024年7月3日（PT）に公開された、メンテナンスリリース 16971 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 16799 でした。

2024.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-16971}

* SITES-22948:AEM CS の基盤コンテンツ内のコマース参照を削除する。
* SITES-22141: [コンテンツフラグメント] OnRC 後の CFM ModelChangeRepositoryImpl からの SegmentNotFoundException
* SITES-21893：オーサーインスタンスでの画像切り抜きの問題。
* SITES-21788: [コンテンツフラグメント] モデルで uiSchema が有効になっている場合、CF および CF モデルエディターでメモを表示します。
* SITES-21688:MSM ロールアウトでライブコピーページ上のエクスペリエンスフラグメント（XF）パスが更新されない。
* SITES-21659: モデルリソースを作成/変更/レプリケートするユーザーのフルネームを返します。
* SITES-21609：コンテンツフラグメントをモデル間で移行するための OpenAPI エンドポイント。
* SITES-21598: [API を開く] CFM を作成 – 指定された設定パスが存在しない場合にエラーを返します。
* SITES-21491: [API を開く] CF PATCHのエンドポイントは、フィールドレベルでライブの関係を尊重する必要があります。
* SITES-21434: [API を開く] CF GETのエンドポイントは、フィールドレベルでライブの関係を尊重する必要があります。
* SITES-21415: CF エディター – UUID 参照をサポートします。
* SITES-21326: [API を開く] コンテンツフラグメントの参照の存在に関する情報を提供します。
* SITES-21310: [API を開く] 翻訳 API 応答にコンテンツフラグメントの ID を追加します。
* SITES-20859: CF Open API - パスでフラグメントを取得する際に参照を返します。
* SITES-20687: [API を開く] バッチ処理ステータス取得用のエンドポイント。
* SITES-20657: [API を開く] を使用して文字列を置き換える際に、単語全体をmatchするオプションを提供 `FindAndReplace` エンドポイント。
* SITES-20587: [API を開く] 作成 `COPY` コンテンツフラグメントのエンドポイント。
* SITES-20584: [API を開く] 参照の取得を最適化します。
* SITES-20308: [API を開く] API でのバッチ処理を有効にします。
* SITES-19976: [API を開く] 条件付きフィールドの汎用 UI スキーマ。
* SITES-19556: [コンテンツフラグメント] モデルの編集時に uiSchema が存在する場合は、更新します。
* SITES-18056: [API を開く] コンテンツフラグメントをプレビューに公開する場合、参照を含めます。
* SITES-16898: [スキーマ] OpenAPI エンドポイントを使用して、コンテンツフラグメントをモデル間で移行します。
* SITES-16609：ローンチリストエンドポイント。
* SITES-16606：起動エンドポイントを作成する。
* SITES-21617: [Xwalk] ページプロパティ/メタデータを UE 内で編集可能にします。
* SITES-19614: [Xwalk] スプレッドシートエディターのページネーションと無限スクロール。
* SITES-22163: [Xwalk] Edge Delivery Sites のパブリッシュ層から提供されるコンテンツのサポートを改善しました。
* SITES-22109: [Xwalk] リッチテキストマークアップ後処理の処理を改善しました。
* SITES-22035: [Xwalk] MSM とローンチの処理を改善しました。
* SITES-21839: [Xwalk] Edge Deliveryから提供されないコンテンツのパスマッピングとサニタイズを改善しました。

### 修正された問題 {#fixed-issues-16971}

* CQ-4356898: [翻訳] 非常に多数のリンクが含まれる CF の outOfMemory エラー。
* CQ-4357055: [翻訳] Rest API を使用した自動翻訳が機能しない。
* CQ-4353931: [翻訳] 翻訳のソースページ/xf/asset に jcr:uuid がない場合は追加します。
* CQ-4357591: [翻訳] 「Associate JCR:UUID」ワークフローを変更して、Pages/XF で機能するようにします。
* FORMS-14844:reCAPTCHA の検証に失敗しても、アダプティブFormsでフォーム送信が可能になります。
* FORMS-14984：送信されたデータに「submitMetaData」がない場合、CAPTCHA を使用したFormsが検証をスキップする。
* FORMS-14477：日付選択の検証で、ルールエディターの「次の後」および「次の前」オプションが正しく機能しません。
* FORMS-14019：ルールエディターの「サービスの呼び出し」機能がユニバーサルエディターで機能しない。
* FORMS-14336：フォームフィールドが選択されていない場合、エディターはフォーム要素全体にフォーカスを置いて開く必要があります。
* FORMS-15061：ルールエディターで「サービスを呼び出し」オプションを使用すると、ローダーの円が無期限に保持される。
* SITES-22457：深くないローンチの昇格でソースコンテンツが更新されない。
* SITES-22748: [コンテンツフラグメント] コンテンツフラグメント更新ジョブのエラー処理を強化
* SITES-22349: [コンテンツフラグメント] 空の複数行 cf-elements の ContentType は変更できません。
* SITES-22343: [コンテンツフラグメント] セマンティックタイプの「列挙」が壊れています。
* SITES-22194：リダイレクトを設定した後、model.json が機能しなくなりました。
* SITES-21953: [API を開く] etag は、validationStatus の順序に基づいて変更されます。
* SITES-21894: [API を開く] CF の作成時に親パスの検証を強化します。
* SITES-21887: [API を開く] POSTバリエーションエンドポイントから無効な ETag が返されました。
* SITES-21657: [API を開く] CF 検索パスプロパティの検証を改善しました。
* SITES-21949：検索 API が無効なカーソルは 500 を返します。
* SITES-20927：検索 API は、クエリが見つからない場合、500 を返します。
* SITES-20544: [API を開く] Oak の競合を避けるために、公開パッケージ名の生成を変更する。
* SITES-19710:CVE-2022-47937 - ページエディターから org.apache.sling.commons.json のすべての使用方法を削除します。
* SITES-11992: [アクセシビリティ] 注釈スウォッチセレクターボタンにアクセス可能な名前がありません。
* SITES-10979: [アクセシビリティ] ラベルは永続的ではありません。
* SITES-10962: [アクセシビリティ] ボタン：ボタンには役割がありません。
* SITES-10905: [アクセシビリティ] アクティブなコンポーネントの状態が、3 ～ 1 のコントラスト比を満たしていません。
* SITES-2974:  [アクセシビリティ]  – 幅 320 px の水平スクロール。
* SITES-22026:AEMでフォルダー間でエクスペリエンスフラグメントを移動できない
* SITES-22106：新しいコンテンツフラグメントエディターの言語切り替え機能の問題
* SITES-21980:UUID ベースの参照タイプの処理に一貫性がない。
* SITES-7257：サムネールサーブレットの NPE。

### 既知の問題 {#known-issues-16971}

なし。

### 変更通知 {#change-notice-16971}

* 2024年9月以降、AEM as a Cloud Service では、Sling Model Exporter フレームワークを介したリソースリゾルバーのシリアル化が無効になります。詳しくは、[ドキュメント](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)を参照してください。

### 非推奨（廃止予定）機能と API {#deprecated-16971}

AEM as a Cloud Service で非推奨（廃止予定）または削除された機能については、[非推奨（廃止予定）および削除された機能と API](/help/release-notes/deprecated-removed-features.md)を参照してください。

### 組み込みテクノロジー {#embedded-tech-16971}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.25.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
