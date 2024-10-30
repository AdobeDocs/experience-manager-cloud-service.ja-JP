---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: ht
source-wordcount: '569'
ht-degree: 100%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 18311 {#18311}

2024年10月22日（PT）に公開された、メンテナンスリリース 18311 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 18175 でした。

2024.10.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-18311}

* ASSETS-41820：ウォッチドッグの処理に対するインデックス作成の改善。
* ASSETS-43720：ウォッチドッグの処理に対する機能の改善。
* ASSETS-42554：大きなフォルダーに対するパフォーマンスの改善。
* SKYOPS-77603：ビジネスユーザーによるリダイレクトの管理。

### 修正された問題 {#fixed-issues-18311}

* ASSETS-37534：検索で変更を加えると、承認ターゲットに使用されるプロパティを公開できない。
* ASSETS-38322：公開条件プロバイダー設定を削除すると、公開イベント機能が削除される。
* ASSETS-40482：Scene7 ビデオプレーヤーの再生／一時停止およびミュート／ミュート解除ボタンのアクセシビリティに関する問題が発生する。
* ASSETS-40593：アセット／ファイルで「プロパティ」ボタンをクリックすると、エラーページが表示される。
* ASSETS-40598：同期されていないアセットを同期対応フォルダーに移動すると、スマート切り抜きが同期される。
* ASSETS-40743：ファイル名に特定の文字が存在する場合、アセットを置換ダイアログのトリガーに関する問題が発生する。
* ASSETS-40825：検索フォームを編集すると、アセットの検索ファセットが表示されなくなる。
* ASSETS-41007：AEM で削除すると、配信時に孤立したアセットが残ることがある。
* ASSETS-41172：Dynamic Media テンプレートの名前に特殊文字を使用できない。
* ASSETS-41896：フォルダーの cq:discarded プロパティに記載されているアセットを Brand Portal に公開できない。
* ASSETS-42067：Dynamic Media テンプレート - ダウンロードにより、エラーが発生する。
* ASSETS-42070：Dynamic Media テンプレート - 管理者以外のユーザーにテンプレートの作成／編集アクセス権が必要。
* ASSETS-42344：接続されたアセットの同期が切断される - 再接続して顧客にアドバイスする。
* ASSETS-42620：アセットバージョンのプレビューオプションに関する問題が発生する - アセットを開くと、空白のプレビューが表示される。
* ASSETS-42701：Web に最適化された画像配信と切り抜きに関する問題が発生する。
* ASSETS-42966：複数のジョブが同じパスを共有している場合、エラーの発生により、非同期バリケードがブロック解除される場合がある。
* ASSETS-43072：Dynamic Media テンプレート - テンプレート参照ルックアップが無効な参照で中断される。
* ASSETS-43212：メタデータスキーマエディターで国際化に関する問題が発生する。
* ASSETS-43202：タイムラインから印刷する注釈の選択に関する修正が行われる。
* ASSETS-43502：AEM CS の既存の画像プリセット名が編集ページに表示されない。
* ASSETS-43538：アセットの非同期コピージョブで、ソースパスに正しくないプロパティが使用される。
* ASSETS-43798：アセットをコピーする前に、まず宛先パスが確認される。
* ASSETS-43945：アセットの非同期ジョブキューの再試行遅延が 20 分に増やされる。
* ASSETS-44025：個々のアセットを選択した場合、アセットの非同期削除ジョブが失敗する。
* SITES-26128：CreateLiveCopyStep でクラスキャスト例外が発生する。
* SCRNS-4551：ビデオコンポーネントを含む [SG Pools] Screens チャネルで、ブラウザーのプレビューとプレーヤーに「一般的なページエラー」が表示される

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
