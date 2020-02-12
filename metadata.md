---
product: adobe experience manager
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.en
index: y
solution-title: クラウドサービスとしてのAdobe Experience Manager
solution-hub-url: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/landing/home.html
getting-started-title: 概要
getting-started-url: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/home.html
tutorials-title: チュートリアル
tutorials-url: https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: 99dce041a6d7554785fd43eb82c671643e903f23

---


# 内部使用メタデータ

GitHubオーサリングシステムのメタデータは階層的で、次の上位レベルの前例が定義されています。

1. metadata.md
1. ToC
1. 記事

metadata.mdファイルで定義されたメタデータはリポジトリ全体に適用されますが、ToCと記事のレベルで上書きできます。 メタデータの上書きは、可能な限り低いレベルで行う必要があります。

最低限必要なのは、Experience-manager-cloud-service.enリポジトリ内のメタデータです。

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
* `contentOwner` (以下に基づくコアアセットコンテンツのみ `/help/assets`)

メタデータに関する追加情報は、内部オーサリングガ [イドを参照してください。](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/markdown/metadata.html#solution-metadata)