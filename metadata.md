---
product: adobe experience manager
description: Adobe Experience Manager as a Cloud Serviceのドキュメント。
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.ja-JP
index: true
type: Documentation
solution: Experience Manager, Experience Manager as a Cloud Service
feature-set: Experience Manager Assets, Experience Manager Sites, Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager, Experience Manager Screens
landing-page-name: experience-manager
landing-page-breadcrumb-title: AEM
version: Experience Manager as a Cloud Service
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 51%

---


# 内部使用メタデータ

GitHub オーサリングシステムのメタデータは階層であり、次のレベルの前例で定義されています。

1. metadata.md
1. 目次
1. 記事

metadata.md ファイルで定義されたメタデータはリポジトリ全体に適用されますが、目次と記事のレベルで上書きできます。メタデータの上書きは、可能な限り低いレベルで行う必要があります。

experience-manager-cloud-service.en リポジトリのメタデータは、必要な最小値です。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

目次

* `sub-product`
* `user-guide-title`

記事

* `title`
* `description`
* `contentOwner` （`/help/assets`以下のコアアセットコンテンツに対してのみ）
