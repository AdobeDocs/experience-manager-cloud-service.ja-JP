---
title: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
description: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: 7e66c9f26211bd92119c74f311f3e9b3195a8d98
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 6%

---


# メンテナンスリリースノート {#maintenance-release-notes}

以下の節では、as a Cloud ServiceExperience Managerの現在のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース11382 {#release-11382}

2023 年 3 月 28 日に公開されたメンテナンスリリース11382の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース11289のアップデートです。

このメンテナンスリリースで機能を有効にすると、すべての機能セットが提供されます。 詳しくは、 [最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md) 詳細はこちら。

### 修正された問題 {#fixed-issues}

- ASSETS-21023 — スマート切り抜きレンディションを修正しました。API を使用してこれらのレンディションにアクセスしようとすると、すべてのAEM環境の公開者インスタンスでヌルポインターの例外が発生する可能性がありました。
- SKYOPS-49280 - RDE を使用して設定またはバンドルの更新を Publish にインストールする場合、Publish Dispatcher のキャッシュが無効化されていないので、結果を観察できない可能性があります

#### Sites {#sites-issues}

- SITES-7796 — ターゲットに書き出す際に、コンテンツ作成者がマスターコンテンツフラグメントとそれぞれのバリエーションを公開する機能

#### Assets {#assets-issues}

- ASSETS-20076 — 現在の画像の透かしのサポートに一致するビデオの透かしのサポートを追加
- ASSETS-21428 - CSS 変更の除外の追加

#### Forms {#forms-issues}

- CQ-4351502 - Sites での読み取りアクセスを許可するようにサービスユーザーマッピングを更新しています

#### プラットフォーム {#platform-issues}

- SITES-11040 - Dispatcher でのGraphQLの永続的なクエリキャッシュの条件付き有効化

### 組み込みテクノロジ {#embedded-tech}

| 科学技術 | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | バージョン2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | バージョン 1.4.20 ～ 1.4.0 | [HTMLテンプレート言語の仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン2.21.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
