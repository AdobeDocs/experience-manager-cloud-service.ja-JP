---
title: Screens as a Cloud Service の FAQ
description: ここでは、Screens に関するas a Cloud Service的な FAQ について説明します。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 02c9cbff56399ea2ca1baad7d2289d5d4c17c1c5
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 50%

---

# Screens as a Cloud Service の FAQ {#screens-cloud-faqs}

次の節では、Screens as a Cloud Service プロジェクトに関するよくある質問（FAQ）とそれに対する回答を示します。

## Screens as a Cloud Serviceを指すAEM Screens Player が/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css 形式のカスタム clientlib を選択しない場合は、どうすればよいですか？

AEM as a Cloud Service は、デプロイメントごとに長いキャッシュキーを変更します。AEM Screens では、Cloud Manager がデプロイメントを実行するときではなく、コンテンツが変更されたときに、オフラインキャッシュを生成します。マニフェスト内のこれらの長いキャッシュキーは無効なので、プレーヤーはこれらの *clientlibs* をダウンロードできません。

`clientlib` フォルダーで `longCacheKey="none"` を使用すると、これらの *clientlibs* の長いキャッシュキーが完全に削除されます。


## 意図したリソースの一部がオフラインマニフェストに含まれていない場合は、どうすればよいですか？ {#offline-manifest}

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

## AEM Screens as a Cloud Service チャネルでは、画像のシームレスなレンディションには、どのような画像形式がお勧めですか？{#screens-cloud-image-format}

最適なデジタルサイネージエクスペリエンスを実現するには、AEM Screens as a Cloud Service チャネルで `.png` および `.jpeg` 形式の画像を使用することをお勧めします。
`*.tif` 形式の画像（Tag Image File 形式）は、AEM Screens as a Cloud Service ではサポートされていません。チャネルにこの形式の画像が含まれる場合、その画像はプレーヤー側ではレンダリングされません。

## 開発者モード（オンライン）のチャネルがAEM Screens Player でレンダリングされない場合、管理者はどうすればよいですか？{#screens-cloud-online-channel-blank-iframe}

AEM Screensのキャッシュ機能を活用することをお勧めしますが、チャネルを開発者モードで実行する必要があり、AEM Screens Player に空白の画面が表示される場合は、Player の開発者ツールを確認し、 `X-Frame-Options` または `frame-ancestors` エラー。 解決策は、iFrame で実行するコンテンツを許可するように Dispatcher を設定することです。 通常、次の設定が機能します。

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## 登録コード制限の使用方法

ベストプラクティスとして、登録コードの使用を制限できます。 登録コードに問題が生じ、100 件の登録が制限されている場合、攻撃者はその数までしか登録できませんが、それ以上登録できません。 登録コードが作成され、顧客のプレーヤーの一部が既に登録されている場合は、いつでも使用制限を更新できます。 顧客が特定の登録コードに対して異常な登録アクティビティを観察した場合、調査中に制限をリアルタイムで下げ、既に登録されているプレーヤーに影響を与えることなく、誤報の場合は数を増やすことができます。
