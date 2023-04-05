---
title: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
description: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: c56ed1878b89a1f31c5b7b44696511d51cfa5351
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 7%

---


# メンテナンスリリースノート {#maintenance-release-notes}

以下の節では、as a Cloud ServiceExperience Managerの現在のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース11382 {#release-11382}

2023 年 3 月 28 日に公開されたメンテナンスリリース11382の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース11289のアップデートです。

このメンテナンスリリースで機能を有効にすると、すべての機能セットが提供されます。 詳しくは、 [最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md) 詳細はこちら。

### 既知の問題 {#known-issues-11382}

- SITES-12573 - 1 つの変数が指定されていない場合、フィルター内の変数を使用するGraphQLクエリは失敗します。 このリリースにはアップデートしないでください。AEM as a Cloud Serviceと共にGraphQLを使用する必要があります。

### 修正された問題 {#fixed-issues-11382}

- ASSETS-21023 — スマート切り抜きレンディションを修正しました。API を使用してこれらのレンディションにアクセスしようとすると、すべてのAEM環境の公開者インスタンスでヌルポインターの例外が発生する可能性がありました。
- SKYOPS-49280 - RDE を使用して設定またはバンドルの更新を Publish にインストールする場合、Publish Dispatcher のキャッシュが無効化されていないので、結果を観察できない可能性があります

#### Sites {#sites-issues-11382}

- SITES-7796 — ターゲットに書き出す際に、コンテンツ作成者がマスターコンテンツフラグメントとそれぞれのバリエーションを公開する機能
- SITES-97 - GraphQL:ページネーションと並べ替え、ハイブリッドフィルター

>[!NOTE]
>
> SITES-97 では、GraphQLの実装が改善され、予期しない動作を引き起こす可能性がありました。 詳しくは、 [null 値の処理に関するAEM GraphQLの変更](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-21792.html?lang=ja) を参照してください。

#### Assets {#assets-issues-11382}

- ASSETS-20076 — 現在の画像の透かしのサポートに一致するビデオの透かしのサポートを追加
- ASSETS-21428 - CSS 変更の除外の追加

#### Forms {#forms-issues-11382}

- CQ-4351502 - Sites での読み取りアクセスを許可するようにサービスユーザーマッピングを更新しています

#### プラットフォーム {#platform-issues-11382}

- SITES-11040 - Dispatcher でのGraphQLの永続的なクエリキャッシュの条件付き有効化

### 組み込みテクノロジ {#embedded-tech-11382}

| 科学技術 | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | バージョン2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | バージョン 1.4.20 ～ 1.4.0 | [HTMLテンプレート言語の仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン2.21.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
