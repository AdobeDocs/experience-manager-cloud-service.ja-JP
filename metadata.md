---
product: adobe experience manager
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.ja-JP
index: y
type: Documentation
solution-title: Adobe Experience Manager as a Cloud Service
solution-hub-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/landing/home.html?lang=ja
getting-started-title: はじめに
getting-started-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/home.html
tutorials-title: チュートリアル
tutorials-url: https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: 8832307a96160a3d45cc85942473a5ada288a74f
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 70%

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
