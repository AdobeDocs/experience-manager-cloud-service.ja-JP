---
title: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
description: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3823b9369c612058998e265346b3f727001aef4b
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 21%

---

# メンテナンスリリースノート {#maintenance-release-notes}

以下の節では、as a Cloud ServiceExperience Managerの現在のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 11873 {#release-11873}

2023 年 5 月 3 日に公開されたメンテナンスリリース11873の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース11835のアップデートです。

このメンテナンスリリースにおける機能イネーブルメントでは、包括的な機能セットを提供します。詳しくは、[最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

### 機能強化 {#enhancements}

- SITES-1200 — タグベースのフィルタリングによる Search API の強化
- GRANITE-42939 - OAUTH-server コードに廃止の注釈と警告を追加する

### 既知の問題 {#known-issues-11873}

- SITES-13253 — コアコンポーネント v2.22.6の RecursionTooDeepException
- SITES-13256 — 特別な URL で設定されたコア WCM ティーザーにより、ページのレンダリングが壊れる
- GRANITE-45462 — メッセージングクライアントの複数地域設定
- GRANITE-45562 — 画像の組み合わせで 404 ではなく 200 が返される問題

### 修正された問題 {#fixed-issues-11873}

- SKYSI-19884/SKYOPS-53745 - PublishPageRenderingErrorsHigh の問題を修正しました。
- GRANITE-4388 - Mongo で大量の DAM アセット書き込みがおこなわれた後のスループットの低下を修正しました。
- SITES-11922 — プレビューから非公開にすると同期ステータスが削除されなかった問題を修正しました。
- ASSETS-21648 — アセット関連機能に関する権限の問題を修正しました。

### 組み込みテクノロジー {#embedded-tech-11873}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | バージョン 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | バージョン 1.4.20 ～ 1.4.0 | [HTMLテンプレート言語の仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.21.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
