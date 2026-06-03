---
product: adobe experience manager
description: Adobe Experience Manager as a Cloud Serviceのドキュメント。
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.en
index: true
type: Documentation
solution: Experience Manager as a Cloud Service, Experience Manager
feature-set: Experience Manager Assets, Experience Manager Sites, Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager, Experience Manager Screens
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
usetq: true
landing-page-name: experience-manager
landing-page-breadcrumb-title: AEM
version: Experience Manager as a Cloud Service
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: bcbd874dfee4d448eda4e0be8bc508493fb8f058
workflow-type: tm+mt
source-wordcount: 95
ht-degree: 2%

---


# 内部使用のためのメタデータ

GitHub オーサリングシステムのメタデータは階層であり、次のレベルの前例で定義されています。

1. metadata.md
1. ToC
1. 記事

metadata.md ファイルで定義されたメタデータは、リポジトリ全体に適用されますが、ToC レベルとアーティクルレベルで上書きできます。 メタデータの上書きは、可能な限り低いレベルで行う必要があります。

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

ToCs

* `sub-product`
* `user-guide-title`

記事

* `title`
* `description`
* `contentOwner` （`/help/assets`以下のコアアセットコンテンツに対してのみ）
