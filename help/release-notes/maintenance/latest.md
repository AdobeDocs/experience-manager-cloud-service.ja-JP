---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a1baa7f29c6e15af11347debdd341f9972c06e83
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 100%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 17258 {#release-17258}

2024年7月30日（PT）に公開された、メンテナンスリリース 17258 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 17098 でした。

2024.8.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-17258}

* ASSETS-31445 - Dynamic Media の初期テンプレート機能
* ASSETS-40399 - DM 自動文字起こしキューの設定を更新しました
* ASSETS-40873 - OSGi 設定を使用してメタデータの書き込みの最大行数を設定できます

### 修正された問題 {#fixed-issues-17258}

* ASSETS-30613 - 「アセットを置換」すると、新しい配信層でアセットが削除および追加されない
* ASSETS-31882 - 作成者のストリーミングマニフェストファイルへのアクセスが禁止されている
* ASSETS-39598 - 名前に特殊文字が含まれるアセットを S3 バックエンドから一括読み込みで削除できない
* CNTBF-209 - バックフロージョブキャンセルの改善
* SCRNS-3762 - ブラウザーでチャネルをプレビューする際にコンソールにログを配置するように、シーケンスチャネルの playerLogger を改善
* SCRNS-4455 - チャネルのコンテンツプロバイダーで、管理者以外のユーザーに対して「公開を管理」および「クイック公開」ボタンが表示されない
* SITES-22940 -コンテンツフラグメントをワークフローペイロードとして表示できない

### 既知の問題 {#known-issues-17258}

なし

### 変更通知 {#change-notice-17258}

* 2024年9月以降、AEM as a Cloud Service では、Sling Model Exporter フレームワークを介したリソースリゾルバーのシリアル化が無効になります。 詳しくは、[ドキュメント](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)を参照してください。

### 廃止された機能と API {#deprecated-17258}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### 組み込みテクノロジー {#embedded-tech-17258}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.25.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
