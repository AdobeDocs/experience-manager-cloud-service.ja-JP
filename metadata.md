---
product: adobe experience manager
description: Adobe Experience Manager as aCloud Serviceドキュメント。
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.ja-JP
index: y
type: Documentation
solution: Experience Manager, Experience Manager as a Cloud Service
version: Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: c19c15c4e71c8ead1c3cb05add052a8ffae79d0a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 68%
showfeedback: true

---


# 内部使用メタデータ

GitHub オーサリングシステムのメタデータは階層的で、次の増加する先例レベルが定義されます。

1. metadata.md
1. 目次
1. 記事

metadata.md ファイルで定義されたメタデータはリポジトリ全体に適用されますが、目次と記事のレベルで上書きできます。メタデータの上書きは、可能な限り低いレベルでおこなう必要があります。

最低限必要なのは、experience-manager-cloud-service.enリポジトリのメタデータです。

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
* `contentOwner` （の下のコアアセットコンテンツのみ） `/help/assets`。
