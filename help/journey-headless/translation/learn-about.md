---
title: Learn about headless content and how to translate it in AEM
description: Learn headless concepts, how they map to AEM, and the theory of AEM translation.
exl-id: 72bb6646-e573-4576-8d17-49787d8c8c7f
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 32%

---

# Learn about headless content and how to translate it in AEM {#learn-about}

Learn headless concepts, how they map to AEM, and the theory of AEM translation.

## 目的 {#objective}

This document helps you understand headless content delivery, how AEM supports headless, and how such content can be translated. ドキュメントを読めば、以下が可能です。

* Understand the basic concepts of headless content delivery.
* Be familiar with how AEM supports headless and translation.

## フルスタックコンテンツ配信 {#full-stack}

使いやすい大規模なコンテンツ管理システム（CMS）が登場して以来、組織はこれらをメッセージング、ブランディング、コミュニケーションを管理する一元的な場所として活用してきました。CMS をエクスペリエンス管理の中心として使用することで、異なるシステムでタスクを重複させる必要がなくなり、効率が向上しました。

![従来のフルスタック CMS](/help/journey-headless/developer/assets/full-stack.png)

In a full-stack CMS, all of the functionality for manipulating content is in the CMS. システムの機能は、CMS スタックの異なるコンポーネントを構成します。フルスタックソリューションには多くの利点があります。

* There is one system to maintain.
* コンテンツを一元的に管理できる。
* システムのすべてのサービスが統合されている。
* コンテンツのオーサリングはシームレスである。

So if new channel must be added or support for new types of experiences is required, one (or more) new components can be inserted into the stack and there is only one place to make changes.

![スタックへの新しいチャネルの追加](/help/journey-headless/developer/assets/adding-channel.png)

However the complexity of the dependencies within the stack quickly becomes apparent as other items in the stack need to be adjusted to accommodate the changes.

## ヘッドレスのヘッド {#the-head}

システムのヘッドは、通常、そのシステムの出力レンダラーです。一般的には、GUI やその他のグラフィカル出力の形式です。

ヘッドレス CMS では、CMS がコンテンツを管理し、コンシューマーに配信します。ただし、ヘッドレス CMS では、標準化された方法で&#x200B;**コンテンツ**&#x200B;を配信だけで、最終的な出力のレンダリングは省略され、コンテンツの&#x200B;**プレゼンテーション**&#x200B;は消費サービスに委ねられます。

![ヘッドレス CMS](/help/journey-headless/developer/assets/headless-cms.png)

The consuming services, be they AR experiences, a web shop, mobile experiences, progressive web apps (PWAs), etc., take in content from the headless CMS and provide their own rendering. ヘッドレス CMS は、コンテンツに合わせて独自のヘッドを提供します。

ヘッドを省略することで、複雑さが減り、CMS をシンプルになります。また、コンテンツのレンダリングの責任は、実際にコンテンツを必要とするサービスに移ります。多くの場合、サービスのほうがレンダリングに適しています。

## Translating Headless Content in AEM {#translating-in-aem}

In addition to offering robust tools to create, manage, and deliver traditional webpages in the full-stack fashion, AEM also offers the ability to author self-contained selections of content and serve them headlessly.

The power of AEM allows it to deliver content either headlessly, full-stack, or in both models at the same time. For the translation specialist, the same set of translation tools can be applied to both types of content, giving you a unified approach for translating your content.

Further in the journey you will learn the details about how AEM translates content, but at a high level, the concept is simple:

1. Define a connection to a translation service by configuring the translation integration framework.
1. Define which content should be translated using translation rules.
1. Create a translation project to harvest the content, send it to the translation service, and receive the results.
1. Review and publish the translated content.

## 次の手順 {#what-is-next}

Thanks for getting started on your AEM headless translation journey! ドキュメントを読んだので、次を理解しているはずです。

* Understand the basic concepts of headless content delivery.
* Be familiar with how AEM supports headless and translation.

[](getting-started.md)

## その他のリソース {#additional-resources}

[](getting-started.md)

* [](/help/sites-cloud/administering/msm-and-translation.md)
