---
product: adobe experience manager
description: これは、AEMaaCSドキュメントページに必要なメタデータです
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.ja-JP
index: y
type: ドキュメント
solution: Experience Manager
translation-type: tm+mt
source-git-commit: 80a59a02067d478713aa7dcdb436ad1345d89c1a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 68%

---


# 内部使用メタデータ

GitHub オーサリングシステムのメタデータは階層的で、次の増加する先例レベルが定義されます。

1. metadata.md
1. 目次
1. 記事

metadata.md ファイルで定義されたメタデータはリポジトリ全体に適用されますが、目次と記事のレベルで上書きできます。メタデータの上書きは、可能な限り低いレベルでおこなう必要があります。

最低限必要なのは、experience-manager-cloud-service.enリポジトリ内のメタデータです。

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
* `contentOwner` (以下のコアアセットコンテンツのみ `/help/assets`)
