---
product: adobe experience manager
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.ja-JP
index: y
type: Documentation
solution-title: Adobe Experience Manager as a Cloud Service
solution-hub-url: https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/landing/home.html
getting-started-title: 概要
getting-started-url: https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/overview/home.html
tutorials-title: チュートリアル
tutorials-url: https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: d311c87c1ae1cdfe9f50d41750aecbab960dc7ef
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 85%

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

メタデータに関する追加情報は、[内部オーサリングガイド](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/markdown/metadata.html#solution-metadata)を参照してください。
