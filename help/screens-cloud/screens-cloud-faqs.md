---
title: Screens as a Cloud Service の FAQ
description: ここでは、Screens に関するas a Cloud Service的なよくある質問について説明します。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 58%

---

# Screens as a Cloud Service の FAQ {#screens-cloud-faqs}

次の節では、Screens as a Cloud Service プロジェクトに関するよくある質問（FAQ）とそれに対する回答を示します。

## Screens as a Cloud Service を指す AEM Screens Player が /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css 形式のカスタム clientlib を選択しない場合は、どうすればよいですか？

AEM as a Cloud Service は、デプロイメントごとに長いキャッシュキーを変更します。AEM Screens では、Cloud Manager がデプロイメントを実行するときではなく、コンテンツが変更されたときに、オフラインキャッシュを生成します。マニフェスト内のこれらの長いキャッシュキーは無効なので、プレーヤーは *clientlibs*.

使用 `longCacheKey="none"` の `clientlib` フォルダーは、 *clientlibs*.


## オフラインマニフェストに意図したすべてのリソースが含まれていない場合は、どうすればよいですか？ {#offline-manifest}

オフラインキャッシュは、**bulk-offline-update-screens-service** サービスユーザーを使用して生成されます。特定のパスが `bulk-offline-update-screens-service` からアクセスできない場合は、オフラインマニフェストにコンテンツが見つからない原因となります。

コードつまり `ui.config or ui.apps` で、configuration フォルダーに OSGi 設定を作成して、次の内容を記述し、ファイル名のタイトルを `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config` に設定します。

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## AEM Screens as a Cloud Serviceチャネルで画像をシームレスにレンディションする場合は、どの画像形式をお勧めしますか？{#screens-cloud-image-format}

最適なデジタルサイネージエクスペリエンスを実現するには、AEM Screens as a Cloud Service チャネルで `.png` および `.jpeg` 形式の画像を使用することをお勧めします。
`*.tif` 形式の画像（Tag Image File 形式）は、AEM Screens as a Cloud Service ではサポートされていません。チャネルにこの形式の画像が含まれる場合、プレーヤー側では画像はレンダリングされません。

## 開発者モード（オンライン）のチャネルが AEM Screens Player でレンダリングされない場合、どうすればよいですか？{#screens-cloud-online-channel-blank-iframe}

Adobeでは、AEM Screensのキャッシュ機能を使用することをお勧めします。 ただし、チャネルを開発者モードで実行する必要があり、AEM Screens Player に空白の画面が表示される場合は、Player の開発者ツールを確認し、 `X-Frame-Options` または `frame-ancestors` エラー。 解決策は、iFrame で実行するコンテンツを許可するように Dispatcher を設定することです。 通常、次の設定が機能します。

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## 登録コード制限の用途は何ですか？

ベストプラクティスとして、登録コードの使用を制限できます。登録コードが侵害を受けても、登録数が 100 件に制限されていると、攻撃者はその数までは登録できますが、それ以上は登録できません。登録コードが作成され、顧客のプレーヤーの一部が既に登録されている場合でも、いつでも使用制限を更新できます。顧客が特定の登録コードに対して異常な登録アクティビティを観察した場合、調査中にリアルタイムで制限を下げることができます。 既に登録されているプレーヤーに影響を与えることなく、誤ったアラームの場合は、数を増やすことができます。
