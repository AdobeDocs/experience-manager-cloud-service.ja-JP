---
product: adobe experience manager
description: Adobe Experience Manager as a Cloud Service ドキュメント.
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.ja-JP
index: y
type: Documentation
solution: Experience Manager
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 58%

---


# 内部使用メタデータ

GitHub オーサリングシステムのメタデータは階層的で、次に示すように前例のレベルが高くなっていきます。

1. metadata.md
1. 目次
1. 記事

metadata.md ファイルで定義されたメタデータはリポジトリ全体に適用されますが、目次と記事のレベルで上書きできます。メタデータの上書きは、可能な限り低いレベルで行う必要があります。

最低限必要なのは、experience-manager-cloud-service.en リポジトリ内のメタデータです。

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
* `contentOwner` （以下のコアアセットコンテンツのみ） `/help/assets`)
