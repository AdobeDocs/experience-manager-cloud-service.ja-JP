---
title: Screens as a Cloud Service での Dispatcher 設定
description: ここでは、Screens as a Cloud Service での Dispatcher 設定について説明します。
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 100%

---

# Screens as a Cloud Service での Dispatcher 設定 {#dispatcher-configurations-screens-cloud}

ここでは、Screens as a Cloud Service の Dispatcher 設定について説明します。

## Screens as a Cloud Service デプロイメントの Dispatcher に対するフィルターとキャッシュルールの追加 {#deployment}

Screens as a Cloud Service におけるパブリッシュインスタンスの Dispatcher で次のフィルターとキャッシュルールを許可します。

### AEM Screens フィルター {#filters}

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

### キャッシュルール {#cache-rules}

* `publish_farm.any`/ の `/cache` セクションに `/statfileslevel "10"` を追加します。

   >[!NOTE]
   >このキャッシュルールでは、キャッシュの docroot から最大 10 レベルまでのキャッシュをサポートしており、すべてを無効化するのではなく、コンテンツの公開時に無効化します。このレベルは、セットアップするコンテンツ構造の深さに基づいて変更できます。

* `publish_farm.any` の `/invalidate` セクションに次の内容を追加します。

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* publish_farm.any または `publish_farm.any` からインクルードされるファイルにある `/cache` の `/rules` セクションに、次のルールを追加します。

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
