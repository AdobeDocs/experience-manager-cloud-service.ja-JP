---
title: Screensas a Cloud ServiceFAQ
description: ここでは、hScreens に関するas a Cloud Service的な FAQ について説明します。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: cf091056bdb96917a6d22bf1197d9b34ebbf9610
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Screensas a Cloud ServiceFAQ {#screens-cloud-faqs}

以下の節では、Screens as a Cloud Serviceプロジェクトに関するよくある質問 (FAQ) に対する回答を示します。

## AEM Screens Player がas a Cloud Serviceを指している場合に、 /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css 形式のカスタム clientlib を選択しない場合は、どうすればよいですか？

AEM as a Cloud Serviceは、デプロイメントのたびに長いキャッシュキーを変更します。 AEM Screensは、Cloud Manager がデプロイメントを実行する際ではなく、コンテンツが変更された際にオフラインキャッシュを生成します。 マニフェスト内のこれらの長いキャッシュキーは無効なので、プレーヤーはこれらの *clientlibs* をダウンロードできません。

`clientlib` フォルダーで `longCacheKey="none"` を使用すると、これらの *clientlibs* の長いキャッシュキーが完全に削除されます。


## オフラインマニフェストに意図したすべてのリソースが含まれていない場合は、どうすればよいですか？ {#offline-manifest}

オフラインキャッシュは、**bulk-offline-update-screens-service** サービスユーザーを使用して生成されます。 `bulk-offline-update-screens-service` がアクセスできない特定のパスは、オフラインマニフェストにコンテンツが見つからなくなります。

コード (`ui.config or ui.apps`) で、設定フォルダーに次の内容を含む OSGi 設定を作成し、ファイル名のタイトルを `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config` にします。

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## AEM Screens as a Cloud Serviceチャネルで画像をシームレスにレンディションする場合は、どの画像形式をお勧めしますか。{#screens-cloud-image-format}

デジタルサイネージを最大限に活用するには、AEM Screensas a Cloud Serviceチャネルで `.png` および `.jpeg` の形式の画像を使用することをお勧めします。
`*.tif` 形式の画像（Tag Image File 形式）は、AEM Screens as a Cloud Serviceではサポートされていません。 チャネルにこの形式の画像が含まれる場合、プレーヤー側では画像はレンダリングされません。