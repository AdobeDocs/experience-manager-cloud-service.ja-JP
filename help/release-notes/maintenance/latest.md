---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3686697c85273ccc13e80b8d7f4ad1ff3c79845d
workflow-type: ht
source-wordcount: '632'
ht-degree: 100%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 21706 {#21706}

2025年7月24日（PT）に公開された、メンテナンスリリース 21706 の継続的な改善点を以下にまとめます。 前回のメンテナンスリリースは、リリース 21570 でした。

>[!NOTE]
>
>リリース 21644 はプライベートになり、リリース 21706 に置き換えられました。

2025.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-21706}

* ASSETS-39377：Assets Bulk Importer でのリモートストレージからの 429 の処理を改善。
* ASSETS-46026：メタデータエクスポーターの設定可能な最大深度。
* ASSETS-49172：Dynamic Media テンプレートアセットは、フォルダーからメタデータを継承する必要がある。
* ASSETS-50209：DM テンプレートでの部分文字列のサポート。
* ASSETS-52326：Assets のタイトル表示環境設定を指定する AEM Assets 設定ページ。
* ASSETS-52805：一括操作ジョブに CSV 出力／ダウンロードのサポートを追加。
* ASSETS-52873：フォルダーのプロパティに新しい設定を追加して、そのフォルダーの AI 処理を無効にする。
* ASSETS-53535：YouTube ビデオのアップロードパフォーマンスを改善済み。
* ASSETS-53612：Assets オムニサーチでのハイブリッド検索のコントロール。
* GRANITE-60183：commons-fileupload 依存関係を 1.6.0 にアップデート。
* GRANITE-60287：QS を Jackrabbit 2.22.1 にアップデート。
* SITES-30452：ASO を使用した Content API - タイトルと説明の提案。
* SITES-31677：カスタムワークスペースは、Target への AEM コンテンツフラグメントの書き出しをサポートします。
* SKYOPS-112741：AEM-CS SDK から `com.adobe.granite.product.support` バンドルを削除。

### 修正された問題 {#fixed-issues-21706}

* ASSETS-12882：ビューアプリセットを開いた後の UI 配置の問題。
* ASSETS-48958：アセット同期により Sites のローカル AEM で公開ステータスが変更される問題。
* ASSETS-50856：completeUpload で `dam:processingAttempts` がリセットされない。
* ASSETS-51604：リンク共有レポート CSV に「共有先」データがない。
* ASSETS-51783：検索クエリを使用して設定が見つからない場合に、`/conf/global` の下にある DM 設定にフォールバック。
* ASSETS-51857：アセットテーブル項目を並べ替えることができない。
* ASSETS-52169：新しい BAT マシンレンディションがアセットのダウンロードに誤って含まれる。
* ASSETS-52229：AEM as a Cloud Service のアセットレポートにインボックス通知がない。
* ASSETS-52399：com.day.cq.dam.api のバージョンが上がると、顧客コードが破損する可能性がある。
* ASSETS-52780：有効に切り替えなくても、アセットをプレビュー用にマークできる。
* ASSETS-52866：移行した DM ビデオが、DM 同期が無効になっているフォルダーの下で処理状態のままになる。
* ASSETS-53237：画像プリセットエディターのカラープロファイルドロップダウンが空白になる。
* ASSETS-53240：アセットレポート - Dynamic Media からアセットレンディションサイズを取得する際に、ディスクの使用に失敗する。
* ASSETS-53446：NPE により、YouTube 認証トークンの更新が断続的に失敗する。
* ASSETS-53827：ACL 検証により、混合メディアセットの保存がブロックされる。
* ASSETS-5403：パブリッシュインスタンスで使用される Dynamicmedia clientlibs には `allowProxy=true` が必要である。
* ASSETS-54261：メタデータの読み込みで接続がリークされ、ファイルのダウンロードに失敗するとブロックされる。
* CQ-4359863：コンテンツフラグメントエディター／アセットエディターで、キーワードの順序が正しくないとタグ検索が破損する。
* CQ-4359958：openapi-support を AEM 6.5.22.0 以降と互換性のあるものにする。
* CQ-4360256：`/adobe` サーブレットコンテキスト経由で処理される HTTP リクエストのリクエストパスにサーブレットコンテキストパスが含まれる。
* CQ-4360317：応答を作成する際に、Sunset 日付ヘッダーを設定するメソッドが追加される。
* GRANITE-60311：AEM SDK Quickstart - 「OSGi インストーラー設定プリンター」の NPE。
* GS-15285：ユーザーが非アクティブとして表示される。

### 既知の問題 {#known-issues-21706}

なし。

### 廃止された機能と API {#deprecated-21706}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-21706}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 4 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-21706}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
