---
title: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
description: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 7%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、as a Cloud ServiceExperience Managerの最新メンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 11289 {#release-11289}

2023 年 3 月 7 日に公開されたメンテナンスリリース11289の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース10912のアップデートです。

このメンテナンスリリースで機能を有効にすると、すべての機能セットが提供されます。 詳しくは、 [最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md) 詳細はこちら。

### 既知の問題 {#known-issues}

CORS を使用している場合はアップグレードしないでください。 このリリースでは、GraphQLのコンテンツ配信機能に影響を与える問題が特定されました。 GraphQLで保持されたクエリのキャッシュ方法に関するデフォルトのAEM Dispatcher 設定の変更により、そのようなクエリのGraphQLコンテンツ配信が中断される場合があります。 この問題は、次回のメンテナンスリリースで修正されます。

### 修正された問題 {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584注釈の付いたページでライブコピーを作成できなかった問題を修正しました。
- SITES-11683部分的に継承が壊れた状態で MSM ライブコピーを無効化

#### Assets {#assets-issues}

- ASSETS-20879修正回帰により、アセットレポートの UI が正しく機能せず、生成されたレポートで誤った結果が返されていました。
- ASSETS-21020アセットのダウンロードが壊れた問題を修正 — アセットを移動した後、イメージプロファイルが存在しない
- ASSETS-21023 Dynamic Mediaの画像レンディションが API を介してアクセスできない問題を修正しました。

#### Forms {#forms-issues}

- なし

#### プラットフォーム {#platform-issues}

- GRANITE-44467 — 特定のインスタンス下の既存のノードを更新する際に、Filevault が mixin タイプと子ノードを保持しなかった問題を修正しました。

### 組み込みテクノロジ {#embedded-tech}

| 科学技術 | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | バージョン2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | バージョン 1.4.20 ～ 1.4.0 | [HTMLテンプレート言語の仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン2.21.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
