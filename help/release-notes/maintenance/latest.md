---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3be366e5fa0a7625203a052426be6a2fd2412cf6
workflow-type: ht
source-wordcount: '723'
ht-degree: 100%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 16145 {#release-16145}

2024年5月1日（PT）に公開された、メンテナンスリリース 16145 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 15977 でした。

2024.5.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-16145}

* ASSETS-23489：リポジトリインサイトの機能強化。
* ASSETS-26926：Dynamic Media アップロードポーリングの改善。
* ASSETS-30351：ダウンロードダイアログは、Dynamic Media レンディションのサイズを非同期で読み込む必要があります。
* ASSETS-30379：ダウンロード時の DRM ライセンスの解決策を向上します。
* ASSETS-31058：「レンディション」タブのAEM Assets UI でスマート切り抜きレンディションを表示し、これらのレンディションをクリックすると、スマート切り抜き画像が生成されます。
* ASSETS-31218：アセット配信 API での名前付きスマート切り抜きのサポートを追加します。
* ASSETS-31979：非同期アセット操作中に視覚的なインジケーターを追加し、UI 関数を無効にします。
* ASSETS-32735：アセットメタデータ更新済みイベントの改善。
* ASSETS-34661：AEMaaCS パブリッシュからの DM プレビューや配信 URL の API。
* ASSETS-37259：XMP 解析の改善。
* ASSETS-37263：失敗した Assets 非同期ジョブのキャンセルを許可します。
* CNTBF-114：コンテンツバックフローの改善。
* CNTBF-148：コンテンツバックフローの改善。
* CQ-4356992：最新の AEM および Granite の翻訳。
* SITES-19326：Assets UI のリンクを更新して、新しい CF エディターで CF を開きます。
* SITES-20686：GraphQL - _dmS7Url を使用して Dynamic Media URL を公開します（非画像アセットの場合）。
* SKYOPS-68091：Java 11.0.20 にアップデートします。

### 修正された問題 {#fixed-issues-16145}

* ASSETS-32321：上位フォルダーに「jcr:content」サブノードがない場合、後処理ワークフローの解決が失敗する。
* ASSETS-33856：JPEG 画像プリセットが、ファイルを TXT としてダウンロードする。
* ASSETS-34096：非同期ダウンロードレポートのタッチ UI 表示を修正する。
* ASSETS-34493：複数の会社機能の切替スイッチを有効にした後、ダウンロードダイアログボックスの読み込み中にエラーが発生する。
* ASSETS-34824：DM が無効なフォルダーでは、URL をコピーすると空白が表示される。
* ASSETS-35226：DAM ルートで指定している場合、後処理ワークフローが解決されない。
* ASSETS-35559：DM バッチアップロードの失敗ログが WARN に削減される。
* ASSETS-35860：AEM Assets 列表示でのタイムゾーンが正しく変換されない。
* ASSETS-35935：ペイロードレビューを閉じた後、フォルダーナビゲーションが正しくない。
* ASSETS-35961：画像プロファイルの下で「切り抜きを追加」ボタンが機能しない。
* ASSETS-36227：公開時に FolderPreviewUpdaterImpl サービスが無効になる。
* ASSETS-36943：CF およびその他の CF 以外のアイテムがリスト表示のフォルダーに存在する場合、正しく整列されない。
* ASSETS-36990：多数のプロパティがある場合、書き出されたメタデータジョブが失敗／遅い。
* ASSETS-37113：クエリが CF 結果のみを返した場合、アセットを再処理ジョブが直ちに終了する。
* ASSETS-37260：AEM でのメタデータの書き出しによって、無効な CSV が生成される可能性がある。
* ASSETS-37261：AEM Assets の PPTx およびPDF 注釈の問題。
* ASSETS-37282：大きなフォルダーを開くリクエストが遅い可能性がある。
* ASSETS-37330：OneDrive からの一括読み込みによって、正しくない AEM フォルダー構造が作成される。
* ASSETS-37609：従来の scene7 設定の参照が削除される。
* ASSETS-38016：イベントで一部のメタデータの更新が正しく追跡されない。
* CQ-4357161：AEM インボックスペイロード画面が 404 を返す。
* GRANITE-50041：ドロップダウンオプションで「レンディションを追加」オプションのみを指定する場合、解像度が 1440px 幅を超えると、「レンディションを追加」が機能しない。
* GRANITE-5027：Coral 日付選択コンポーネントの週名が乱れる。
* SCRNS-3949：Screens チャネルの取得リクエストに時間がかかりすぎる。
* SCRNS-3981：[シーケンスチャネル] 要素の読み込み／アンロードイベントのシーケンスが歪むと、黒い画面が発生する。
* SCRNS-4180：[シーケンスチャネル] フォールバックサムネールから復元すると、ビデオのデュレーションが -1 のチャネルでは、空白の画面が表示されてシーケンスが停止する。
* SCRNS-4245：[シーケンスチャネル] ビデオが読み込まれてフォールバックサムネールから切り替わる際に、空白画面が表示される期間が制限される。
* SITES-16055：それぞれのプロパティページ内のライブコピーと、ライブコピーのソースリンクが修正される。
* SCRNS-4243：管理者以外のユーザーのコンテンツプロバイダーでボタンが欠落する。

### 既知の問題 {#known-issues-16145}

なし。

### 廃止された機能と API {#deprecated-16145}

* [Adobe Developer Console での JWT 資格情報の廃止](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* 2024年5月1日（PT）以降、Adobe Dynamic Media は次のサポートを終了します。

   * SSL（Secure Socket Layer）2.0
   * SSL 3.0
   * TLS（Transport Layer Security）1.0 および 1.1
   * TLS 1.2 での以下の脆弱な暗号：
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


AEM as a Cloud Service で非推奨（廃止予定）または削除された機能については、[非推奨（廃止予定）および削除された機能と API](/help/release-notes/deprecated-removed-features.md)を参照してください。

### 組み込みテクノロジー {#embedded-tech-16145}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.24.6 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
