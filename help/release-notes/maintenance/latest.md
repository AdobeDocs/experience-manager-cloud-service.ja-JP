---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 38%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 18311 {#18311}

2024年10月22日（PT）に公開された、メンテナンスリリース 18311 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 18175 でした。

2024.10.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-18311}

* ASSETS-41820：ウォッチドッグを処理するためのインデックス作成の改善。
* ASSETS-43720：処理ウォッチドッグの機能が強化されました。
* ASSETS-42554：大きなフォルダーのパフォーマンスの向上。
* SKYOPS-77603：ビジネスユーザーによるリダイレクトの管理。

### 修正された問題 {#fixed-issues-18311}

* ASSETS-37534：承認ターゲットに使用されるプロパティを公開しないように検索を変更しました。
* ASSETS-38322：公開条件プロバイダー設定の削除公開イベント機能を削除します。
* ASSETS-40482 :Scene7 ビデオプレーヤーの再生/一時停止およびミュート/ミュート解除ボタンのアクセシビリティの問題。
* ASSETS-40593 :Assets/ファイルで「プロパティ」ボタンをクリックすると、エラーページが表示される。
* ASSETS-40598：同期されていないアセットが同期が有効なフォルダーに移動されると、同期スマート切り抜きが行われます。
* ASSETS-40743：ファイル名に特定の文字が存在する場合にアセットを置換ダイアログをトリガーする際の問題。
* ASSETS-40825：検索フォームの編集後、Assets検索ファセットが表示されなくなる。
* ASSETS-41007 :AEMから削除すると、配信に孤立したAssetsが残ることがあります。
* ASSETS-41172 :Dynamic Media テンプレートの特殊文字は名前に使用できません。
* ASSETS-41896：フォルダー上の cq:discarded プロパティに記載されているAssetsは、Brand Portalに公開しないでください。
* ASSETS-42067 :Dynamic Media テンプレート – ダウンロードでエラーが発生する。
* ASSETS-42070 :Dynamic Media テンプレート – 管理者以外のユーザーには、テンプレートの作成/編集アクセス権が必要です。
* ASSETS-42344：接続されたAssets同期が切断されました – 再接続してユーザーにアドバイスします。
* ASSETS-42620：アセットバージョンのプレビューオプションの問題 – アセットを開くと、空白のプレビューが表示される。
* ASSETS-42701 :Web に最適化された画像の配信と切り抜きの問題。
* ASSETS-42966：複数のジョブが同じパスを共有している場合、エラーが発生して非同期バリケードのブロックが解除される可能性があります。
* ASSETS-43072 :Dynamic Media テンプレート – 無効な参照のテンプレート参照ルックアップ区切り。
* ASSETS-43212：メタデータスキーマエディターで国際化に関する問題が発生します。
* ASSETS-43202：タイムラインから印刷する注釈を選択するための修正。
* ASSETS-43502 :AEM CS の既存の画像プリセット名が「編集」ページに表示されない。
* ASSETS-43538：非同期コピーアセットジョブでソースパスに間違ったプロパティが使用されている。
* ASSETS-43798：アセットをコピーする前に、まず、コピー先のパスを確認します。
* ASSETS-43945：非同期アセットジョブキューの再試行遅延を 20 分に増やします。
* ASSETS-44025：個々のアセットが選択されている場合、の非同期削除アセットジョブが失敗します。
* SITES-26128 :CreateLiveCopyStep のクラスキャスト例外。
* SCRNS-4551 : [SG プール ] ビデオコンポーネントを含んだScreens チャネルのブラウザーのプレビューとプレーヤーに「General Page Error」が表示される

### 既知の問題 {#known-issues-18311}

* FORMS-15818：コンポーネント記述子エントリ `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` が見つからないというステートメントがサーバーログに記録される。これらは無害なログステートメントです。

### 廃止された機能と API {#deprecated-18311}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-18311}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 3 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-18311}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
