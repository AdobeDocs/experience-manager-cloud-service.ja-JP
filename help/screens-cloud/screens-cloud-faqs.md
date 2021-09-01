---
title: Screens as aCloud ServiceのFAQ
description: ここでは、hScreensをCloud ServiceFAQとして説明します。
source-git-commit: 7a26bb50a8b95a2358912249e21daeb9c5e9c1a3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Screens as aCloud ServiceのFAQ {#screens-cloud-faqs}

以下の節では、Screens as a Screensプロジェクトに関するよくある質問(FAQ)に対する回答をCloud Serviceします。

## AEM Screens PlayerがCloud ServiceとしてScreensを指している場合、 /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css形式のカスタムclientlibを選択しない場合はどうすればよいですか？

AEM as aCloud Serviceは、デプロイメントのたびに長いキャッシュキーを変更します。 AEM Screensは、Cloud Managerがデプロイメントを実行する際ではなく、コンテンツが変更された際にオフラインキャッシュを生成します。 マニフェスト内のこれらの長いキャッシュキーは無効なので、プレーヤーはこれらの&#x200B;*clientlibs*&#x200B;をダウンロードできません。

`clientlib`フォルダーで`longCacheKey="none"`を使用すると、これらの&#x200B;*clientlibs*&#x200B;の長いキャッシュキーが完全に削除されます。


## オフラインマニフェストに意図したすべてのリソースが含まれていない場合は、どうすればよいですか？ {#offline-manifest}

オフラインキャッシュは、**bulk-offline-update-screens-service**&#x200B;サービスユーザーを使用して生成されます。 特定のパス（`bulk-offline-update-screens-service`がアクセスできない）は、オフラインマニフェストにコンテンツが欠落する原因となります。

コード(`ui.config or ui.apps`)で、設定フォルダーにOSGi設定を作成し、次の内容を指定して、ファイル名のタイトルを`org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`にします。

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```
