---
title: Cloud ServiceとしてのScreensでのDispatcher設定
description: ここでは、ScreensでのDispatcherの設定をCloud Serviceとして説明します。
source-git-commit: b00856e1be8842c4e9fa6ed4ada9129926c73ef5
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 2%

---


# Cloud ServiceとしてのScreensでのDispatcher設定{#dispatcher-configurations-screens-cloud}

ここでは、ScreensをCloud Serviceとして使用する際のDispatcherの設定について説明します。

## DispatcherデプロイメントとしてのScreensのCloud Service設定 {#deployment}

Screensのパブリッシュインスタンス用のDispatcherで、以下のフィルターとキャッシュルールをCloud Serviceとして許可します。

### フィルター {#filters}

## AEM Screens Filters

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you're using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

## キャッシュルール {#cache-rules}

* `/statfileslevel "10"`を`publish_farm.any`/の`/cache`セクションに追加します。

   >[!NOTE]
   >これは、キャッシュドキュメントルートから最大10レベルのキャッシュをサポートし、すべてを無効化するのではなく、コンテンツが公開されたタイミングを無効化します。 このレベルは、コンテンツ構造の深さに基づいて変更できます。

* `publish_farm.any`の`/invalidate`セクションに次の内容を追加します。

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* 次のルールを、publish_farm.anyの`/cache`の`/rules`セクションまたは`publish_farm.any`からインクルードされたファイルに追加します。

   ```
   ## Allow Dispatcher Cache for Screens channels
    /0002
        {
        /glob "/content/screens/*.html"
        /type "allow"
            }
   
   ## Allow Dispatcher Cache for Screens offline manifests
   
   /0003
       {
       /glob "/content/screens/*.manifest.json"
       /type "allow"
       }
   
   ## Allow Dispatcher Cache for Assets
   /0004
       {
       /glob "/content/dam/*"
       /type "allow"
       }
   
   ## Deny Screens Channels json
   /0005
       {
       /glob "/screens/channels.json"
       /type "deny"
       }
   ```
