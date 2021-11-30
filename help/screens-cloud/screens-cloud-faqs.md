---
title: Screensas a Cloud ServiceFAQ
description: ここでは、hScreens に関するas a Cloud Service的な FAQ について説明します。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 489cc9963910ba9f94d30906127beb75f9ad37df
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Screensas a Cloud ServiceFAQ {#screens-cloud-faqs}

次の節では、Screensas a Cloud Serviceプロジェクトに関するよくある質問 (FAQ) に対する回答を示します。

## Screens as a Cloud Serviceを指すAEM Screens Player が/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css 形式のカスタム clientlib を選択しない場合は、どうすればよいですか？

AEMas a Cloud Serviceは、デプロイメントごとに長いキャッシュキーを変更します。 AEM Screensは、Cloud Manager がデプロイメントを実行する際ではなく、コンテンツが変更された際にオフラインキャッシュを生成します。 マニフェスト内のこれらの長いキャッシュキーは無効なので、プレーヤーはこれらのキーをダウンロードできません *clientlibs*.

使用 `longCacheKey="none"` の `clientlib` フォルダーは、これらの長いキャッシュキーを完全に削除します *clientlibs*.


## オフラインマニフェストに意図したすべてのリソースが含まれていない場合は、どうすればよいですか？ {#offline-manifest}

オフラインキャッシュは、 **bulk-offline-update-screens-service** サービスユーザー。 特定のパス（からはアクセス不可） `bulk-offline-update-screens-service`オフラインマニフェストにコンテンツが見つからない原因となります。

コードでは、つまり、 `ui.config or ui.apps`を作成し、次の内容を含む OSGi 設定を configuration フォルダーに作成し、ファイル名のタイトルをに設定します。 `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

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

画像は形式で使用することをお勧めします `.png` および `.jpeg` AEM Screensas a Cloud Serviceチャネルでの、最高のデジタルサイネージエクスペリエンスを実現します。
形式の画像 `*.tif` （タグ画像ファイル形式）は、AEM Screens as a Cloud Serviceではサポートされていません。 チャネルにこの形式の画像が含まれる場合、その画像はプレーヤー側ではレンダリングされません。

## 開発者モード（オンライン）のチャネルがAEM Screens Player でレンダリングされない場合、管理者はどうすればよいですか？{#screens-cloud-online-channel-blank-iframe}

AEM Screensのキャッシュ機能を活用することをお勧めしますが、チャネルを開発者モードで実行する必要があり、AEM Screens Player に空白の画面が表示される場合は、Player の開発者ツールを確認し、 `X-Frame-Options` または `frame-ancestors` エラー。 解決策は、iFrame で実行するコンテンツを許可するように Dispatcher を設定することです。 通常、次の設定が機能します。

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## 登録コード制限の使用方法

ベストプラクティスとして、登録コードの使用を制限できます。 登録コードに問題が生じ、100 件の登録が制限されている場合、攻撃者はその数までしか登録できませんが、それ以上登録できません。 登録コードが作成され、顧客のプレーヤーの一部が既に登録されている場合は、いつでも使用制限を更新できます。 顧客が特定の登録コードに対して異常な登録アクティビティを観察した場合、調査中に制限をリアルタイムで下げ、既に登録されているプレーヤーに影響を与えることなく、誤報の場合は数を増やすことができます。