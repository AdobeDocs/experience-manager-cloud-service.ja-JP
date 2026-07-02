---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e1e7fb3d25781a9ecd431b5d0213558876f3ec6a
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 24%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 26908 {#release-26908}

2026年7月2日に公開されたメンテナンスリリース 26908の継続的な改善点を以下にまとめます。 以前のメンテナンスリリースはリリース 26773でした。

2026.7.0機能のアクティベーションは、このメンテナンスリリースの完全な機能セットを提供します。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-26908}

* ASSETS-52412：既存のアセットレポートを再実行または複製する機能を追加しました。
* ASSETS-62263:OpenAPI機能を備えたDynamic Mediaに、AIが生成したキャプションが導入されました。
* ASSETS-62482：最新の機能強化により、Adobe Stockとの統合が更新されました。
* ASSETS-63388: Tags OpenAPIにHEAD オペレーションのサポートを追加しました。
* ASSETS-63652：コンテンツフラグメントを除外するようにアセット検索を更新しました。
* ASSETS-63743: UUID ベースのID用にタグ ID移行サービスを追加しました。
* ASSETS-64240:CAFE API v2を介した署名と透かしのサポートを追加しました。
* ASSETS-64282: API応答の選択メタデータに対する投影フィールドを追加しました。
* ASSETS-64979：新しいタグにUUIDを自動入力するようにTagManagerを更新しました。
* ASSETS-65069：非同期Sling ジョブアクション用の拡張アセット前処理API。
* ASSETS-65492：メタデータとクエリのサポートが改善され、フォルダーAPIが強化されました。
* ASSETS-65525:1 MBを超えるリクエストボディのアップロード情報APIを改善しました。
* ASSETS-65603：最適化されたアセット数クエリによるフォルダーリストのパフォーマンスが向上しました。
* ASSETS-65678:AEM オーサー設定にFrame.io CORS オリジンを追加しました。
* ASSETS-65746:Assets Move APIに上書きパラメーターのサポートを追加しました。
* ASSETS-65889：プログラムによる名前の変更に対応するAssets名前変更PATCH APIを追加しました。
* ASSETS-66032:Assetsの一括読み込みに高度なネットワークプロキシのサポートを追加しました。
* ASSETS-66196：公開API ジョブのポーリングとステータス応答を更新しました。
* ASSETS-66643: UUID ベースの優先度を使用して、タグ検索のパフォーマンスを向上させました。
* ASSETS-67109:AI生成プロンプトのプロンプトグループのサポートを追加しました。
* ASSETS-67517:PATCH APIを介したAEMとCAIのメタデータ同期を追加しました。
* ASSETS-67525：新しいOpenAPI ベースのメタデータ API実装を追加しました。
* ASSETS-67667：新しいOpenAPI ベースのAsset Metadata Schema API実装を追加しました。
* ASSETS-68173：機能チェック APIの名前をOperations APIに変更しました。
* ASSETS-68261: Adobe Stock検索ランディングページを改善しました。
* ASSETS-68446:Dynamic Media用のVideo Transcript Service APIを追加しました。
* ASSETS-68981:DAM Assets APIのアセット PATCHの一部の動作を更新しました。
* ASSETS-69129:Frame.io ネイティブ統合用のIMS クライアント設定を追加しました。
* ASSETS-69156: Dynamic Media コンポーネントにSEO メタデータのサポートを追加しました。
* ASSETS-69214: Polaris アセットビューアでカスタムサムネールサポートを導入しました。
* ASSETS-70416：イベントの許可リストにOrigin ヘッダーを追加しました。
* CQ-4363466:GenAI コネクタのコンテキストに応じた設定パスの解決を追加しました。
* SITES-42076:AEM Sites ページの一括操作のサポートを追加しました。
* SITES-42835：機能トグルの外にAEM FormsのContent API サポートを追加しました。

### 修正された問題 {#fixed-issues-26908}

* ASSETS-36208: DMが無効になっている場合に、フォルダープロパティに画像プロファイルが見つからない問題を修正しました。
* ASSETS-61087：ダウンロード時のスマート切り抜き数の不一致と間違ったレンディションを修正しました。
* ASSETS-63240：複数の選択を行った際に、空白のメタデータエディターにユーザーが残る問題を修正しました。
* ASSETS-65076：誤ったURL スキームが原因で誤った外部URLが発生する問題を修正しました。
* ASSETS-65670:C2PA コンテンツ認証情報マニフェストの固定アセット ID プレフィックス。
* ASSETS-65932：一括操作の監査ダウンロードでCSV ヘッダーが欠落しているのが修正されました。
* ASSETS-66149:Folder APIで末尾のスラッシュ処理を修正しました。
* ASSETS-66226：大文字と小文字を区別するステータスチェックが修正され、承認/プレビューアセットの削除が失敗する問題が修正されました。
* ASSETS-66669：検索の開始画面に戻らないホームボタンを修正しました。
* ASSETS-66711:body以外のHTTP メソッドのbodyIncluded/contentLengthを修正しました。
* ASSETS-67113:SVG ファイル（0個のアセットを読み込む）を無視する一括読み込みを修正しました。
* ASSETS-67836：原料アセットの双方向リファレンスリンクが見つからない問題を修正しました。
* ASSETS-68098：統合シェルを有効にして保存して閉じると、メタデータが失われる問題を修正しました。
* ASSETS-68240：アセットビューにC2PA マニフェストレンディションが表示されない問題を修正しました。
* ASSETS-68283:DM VideoViewer （WCAG 2.1.1）で再生/一時停止ツールチップが見つからない問題を修正しました。
* ASSETS-69186：大量のキーワードに対するAdobe Stockの検索結果が空になる問題を修正しました。
* ASSETS-69662：最初の編集後に後続のアセット編集が適用されない問題を修正しました。
* ASSETS-69920：一括読み込みドライランから古いフォルダー制限の警告を削除しました。
* SITES-44265：安定したcontent-page-idを追加して、search-optimizer 404sを解決しました。

#### AEM ガイド {#guides-26908}

* GUIDES-47432: Sourceとオーサーモードを切り替えると、コンテンツの不整合が発生し、トピックの一部が消えたり、モード間で反映されなくなったりします。
* GUIDES-48319：変更履歴を操作する際に、読み込んだテキストの挿入を拒否すると、特定の挿入されたコンテンツのみを拒否するのではなく、タグ内のすべてのコンテンツが削除されます。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-26908}

なし。

### 廃止された機能と API {#deprecated-26908}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-26908}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースは、22の特定された脆弱性に対応し、堅牢なシステム保護への取り組みを強化します。

### 組み込みテクノロジー {#embedded-tech-26908}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 2.2.0 | [Oak 2.2.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.2.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.67 | [Apache Httpd 2.4.67](https://apache.googlesource.com/httpd/+/refs/tags/2.4.67/CHANGES) |
| Dispatcher | 2.0.274 |  |
| AEM コアコンポーネント | 2.31.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
| Java 21 | 21.0.11 | [JDK 21.0.11](https://www.oracle.com/java/technologies/javase/21-0-11-relnotes.html) |
