---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 79dcf8a4e9834beeb466ed9270a3f5c6aa67aa9a
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 29%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 16145 {#release-16145}

2024年5月1日（PT）に公開された、メンテナンスリリース 16145 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 15977 でした。

2024.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-16145}

* ASSETS-23489：リポジトリインサイトの機能強化。
* ASSETS-26926:Dynamic Media アップロードポーリングの改善。
* ASSETS-30351：ダウンロードダイアログは、Dynamic Media レンディションのサイズを非同期で読み込む必要があります。
* ASSETS-30379：ダウンロード時の DRM ライセンスの解像度を向上。
* ASSETS-31058:「レンディション」タブのAEM Assets UI でスマート切り抜きレンディションを表示し、これらのレンディションをクリックするとスマート切り抜き画像を生成します。
* ASSETS-31218：アセット配信 api での名前付きスマート切り抜きのサポートを追加。
* ASSETS-31979：非同期 Assets 操作中に視覚的なインジケーターを追加し、UI 関数を無効にします。
* ASSETS-32735：アセットメタデータ更新イベントの改善。
* ASSETS-34661:AEMaaCS パブリッシュからの DM プレビューまたは配信 URL （あるいはその両方）の API。
* ASSETS-37259:XMPの解析の改善。
* ASSETS-37263：失敗した Assets 非同期ジョブのキャンセルを許可します。
* CNTBF-114：コンテンツバックフローの改善。
* CNTBF-148：コンテンツバックフローの改善。
* CQ-4356992：最新のAEMおよび Granite の翻訳。
* SITES-19326：Assets UI のリンクを更新して、新しい CF エディターで CF を開きます。
* SITES-20686:GraphQL - _dmS7Url を使用してDynamic Media URL を公開する（非画像アセットの場合）。
* SKYOPS-68091：を Java 11.0.20 に更新します。

### 修正された問題 {#fixed-issues-16145}

* ASSETS-32321：上位フォルダーに「jcr:content」サブノードがない場合、後処理ワークフローの解決が失敗します。
* ASSETS-33856:JPEG画像プリセットが、ファイルを TXT としてダウンロードする。
* ASSETS-34096：非同期ダウンロードレポートのタッチ UI 表示を修正。
* ASSETS-34493：複数会社機能の切り替えを有効にした後、ダウンロードダイアログボックスの読み込み中にエラーが発生しました。
* ASSETS-34824:DM で無効にしたフォルダーに対して、「コピー」 URL に空と表示される。
* ASSETS-35226:DAM ルートで指定されている場合、後処理ワークフローが解決されません。
* ASSETS-35559:DM バッチアップロード失敗ログを WARN に減らします。
* ASSETS-35860：AEM Assets 列表示でのタイムゾーン変換が正しくない。
* ASSETS-35935：ペイロードレビューを閉じた後、フォルダーナビゲーションが正しくありません。
* ASSETS-35961：画像プロファイルの下で「切り抜きを追加」ボタンが機能しない。
* ASSETS-36227：公開時に FolderPreviewUpdaterImpl サービスを無効にします。
* ASSETS-36943:CF およびその他の非 CF アイテムがリスト表示のフォルダーに存在する場合、整列された列がありません。
* ASSETS-36990：多数のプロパティがある場合、書き出されたメタデータジョブが失敗/遅い。
* ASSETS-37113: クエリが CF 結果のみを返した場合、Assets 再処理ジョブは直ちに終了します。
* ASSETS-37260:AEMでのメタデータのエクスポートによって、無効な CSV が生成される可能性があります。
* ASSETS-37261:AEM Assetsの PPTx およびPDF注釈の問題。
* ASSETS-37282：大きなフォルダーを開くリクエストが遅い可能性があります。
* ASSETS-37330:OneDrive からの一括読み込みによって、間違ったAEM フォルダー構造が作成される。
* ASSETS-37609：従来の scene7 設定の参照を削除。
* ASSETS-38016：イベントで一部のメタデータの更新が正しく追跡されない。
* CQ-4357161:AEM インボックスペイロード画面が 404 を返す。
* GRANITE-50041：ドロップダウンオプションで「レンディションを追加」オプションのみが指定されている場合、解像度が 1,440 px の幅を超えると、「レンディションを追加」が機能しない。
* GRANITE-50279:Coral 日付選択コンポーネントの週名が乱れる。
* SCRNS-3949:Screens チャネルの取得リクエスト時間が長すぎます。
* SCRNS-3981: [シーケンスチャネル] 要素の読み込み/読み込み解除イベントのシーケンスが歪むと、黒い画面が表示されます。
* SCRNS-4180: [シーケンスチャネル] フォールバックサムネールから復元すると、シーケンスが、デュレーション -1 のビデオを含むチャネルの空白画面で停止する。
* SCRNS-4245: [シーケンスチャネル] ビデオが読み込まれてフォールバックサムネールから切り替わるときの、空白画面の期間制限。
* SITES-16055：それぞれのプロパティページ内のライブコピーおよびライブコピーのソースリンクを修正します。
* SCRNS-4243：管理者以外のユーザーのコンテンツ プロバイダーにボタンが見つかりません。

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


AEMのas a Cloud Service機能で非推奨（廃止予定）または削除された機能については、以下を参照してください。 [非推奨（廃止予定）の機能および削除された API](/help/release-notes/deprecated-removed-features.md).

### 組み込みテクノロジー {#embedded-tech-16145}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.24.6 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
