---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 13124956fcce105ad42767f67b700284c8250012
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 34%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 21644 {#21644}

2025年7月22日（PT）に公開された、メンテナンスリリース 21644 の継続的な改善点を以下にまとめます。 前回のメンテナンスリリースは、リリース 21570 でした。

2025.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-21644}

* ASSETS-39377:Assets Bulk Importer でリモートストレージからの 429 の処理を改善しました。
* ASSETS-46026：メタデータエクスポーターの設定可能な最大深度。
* ASSETS-49172:Dynamic Media テンプレートアセットは、フォルダーからメタデータを継承する必要がある。
* ASSETS-50209:DM テンプレートでの部分文字列のサポート。
* ASSETS-52326:Assetsのタイトルの表示環境設定を行うAEM Assets設定ページ
* ASSETS-52805：一括操作ジョブの CSV 出力/ダウンロードのサポートを追加。
* ASSETS-52873：フォルダーのプロパティに新しい設定を追加して、そのフォルダーの AI 処理を無効にします。
* ASSETS-53535:YouTube ビデオのアップロードパフォーマンスが向上しました。
* ASSETS-53612:Assets オムニサーチでのハイブリッド検索のコントロール。
* GRANITE-60183: commons-fileupload の依存関係を 1.6.0 に更新します。
* GRANITE-60287:QS を Jackrabbit 2.22.1 に更新します。
* SITES-30452:ASO を使用したコンテンツ API - タイトルと説明の提案。
* SITES-31677：カスタムワークスペースは、Target への AEM コンテンツフラグメントの書き出しをサポートします。
* SKYOPS-112741:AEM-CS SDKから `com.adobe.granite.product.support` バンドルを削除します。

### 修正された問題 {#fixed-issues-21644}

* ASSETS-12882：ビューアプリセットを開いた後の UI の関連付けの問題。
* ASSETS-48958:Sites ローカル AEMでアセット同期が公開済みステータスを変更する際の問題。
* ASSETS-50856:completeUpload でリセットされな `dam:processingAttempts`。
* ASSETS-51604：リンク共有レポート CSV に「Shared With」データが見つからない。
* ASSETS-51783：検索クエリで設定が見つからない場合は、`/conf/global` の DM 設定にフォールバックします。
* ASSETS-51857：アセットテーブル項目を並べ替えることができません。
* ASSETS-52169：新しいBATのマシンレンディションがアセットのダウンロードに誤って含まれる。
* ASSETS-52229:AEM as a Cloud Serviceのアセットレポートにインボックス通知がない。
* ASSETS-52399:com.day.cq.dam.api のバージョンが大幅に上昇すると、カスタマーコードが破損する可能性があります。
* ASSETS-52780：切り替えを有効にしなくても、アセットをプレビュー用にマークできます。
* ASSETS-52866：移行された DM ビデオは、DM 同期が無効なフォルダーの下で処理中の状態のままになります。
* ASSETS-53237：画像プリセットエディターのカラープロファイルドロップダウンが空白になる。
* ASSETS-53240：アセットレポート - Dynamic Media からアセットレンディションサイズを取得する際に、ディスク使用量が失敗する。
* ASSETS-53446:NPE が原因で、YouTube認証トークンの更新が断続的に失敗する。
* ASSETS-53827：混在メディアセットを保存する際に、ACL 検証がブロックされる。
* ASSETS-5403：公開インスタンスで使用される Dynamicmedia clientlibs には、`allowProxy=true` が必要です。
* ASSETS-54261：ファイルのダウンロードに失敗すると、メタデータの読み込みによって接続がリークし、ブロックされます。
* CQ-4359863：コンテンツフラグメントエディター/アセットエディターでキーワードのタグ検索が異常に壊れる。
* CQ-4359958:openapi-support をAEM 6.5.22.0 以降と互換性のあるものにします。
* CQ-4360256:`/adobe` サーブレットコンテキストを介して処理される HTTP 要求のリクエストパスに、サーブレットのコンテキストパスを含めます。
* CQ-4360317：応答を作成する際にサンセット日ヘッダーを設定する方法を追加。
* GRANITE-60311:AEM SDK Quickstart - NPE （「OSGi Installer Configuration Printer」を参照）
* GS-15285：ユーザーのアクティベートが解除されたとして表示されています。

### 既知の問題 {#known-issues-21644}

なし。

### 廃止された機能と API {#deprecated-21644}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-21644}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 4 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-21644}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
