---
title: AEM Headless Content Architect Journey
description: An introduction to the powerful, and flexible, headless features of Adobe Experience Manager as a Cloud Service, and how to model content for your project.
exl-id: 62061d73-6fdb-440b-a7dd-b0d530d49186
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 37%

---

# Content Modeling for Headless with AEM - An Introduction {#architect-headless-introduction}

[](overview.md)

This document helps you understand headless content delivery, how AEM supports headless, and how content is modeled for headless. ドキュメントを読めば、以下が可能です。

* Understand the basic concepts of headless content delivery.
* Be familiar with how AEM supports headless and content modeling.

## 目的 {#objective}

* **オーディエンス**：初心者
* ****

## フルスタックコンテンツ配信 {#full-stack}

使いやすい大規模なコンテンツ管理システム（CMS）が登場して以来、組織はこれらをメッセージング、ブランディング、コミュニケーションを管理する一元的な場所として活用してきました。CMS をエクスペリエンス管理の中心として使用することで、異なるシステムでタスクを重複させる必要がなくなり、効率が向上しました。

![従来のフルスタック CMS](/help/journey-headless/developer/assets/full-stack.png)

In a full-stack CMS, all of the functionality for manipulating content is in the CMS. システムの機能は、CMS スタックの異なるコンポーネントを構成します。フルスタックソリューションには多くの利点があります。

* There is one system to maintain.
* コンテンツを一元的に管理できる。
* システムのすべてのサービスが統合されている。
* コンテンツのオーサリングはシームレスである。

So if new channel needs to be added or support for new types of experiences is required, one (or more) new components can be inserted into the stack and there is only one place to make changes.

![スタックへの新しいチャネルの追加](/help/journey-headless/developer/assets/adding-channel.png)

However the complexity of the dependencies within the stack quickly become apparent as other items in the stack need to be adjusted to accommodate the changes.

## ヘッドレスのヘッド {#the-head}

システムのヘッドは、通常、そのシステムの出力レンダラーです。一般的には、GUI やその他のグラフィカル出力の形式です。

ヘッドレス CMS では、CMS がコンテンツを管理し、コンシューマーに配信します。ただし、ヘッドレス CMS では、標準化された方法で&#x200B;**コンテンツ**&#x200B;を配信だけで、最終的な出力のレンダリングは省略され、コンテンツの&#x200B;**プレゼンテーション**&#x200B;は消費サービスに委ねられます。

![ヘッドレス CMS](/help/journey-headless/developer/assets/headless-cms.png)

消費サービス（AR エクスペリエンス、Web ショップ、モバイルエクスペリエンス、プログレッシブ Web アプリ（PWA）など）では、ヘッドレス CMS からコンテンツを取り込み、独自にレンダリングを提供します。ヘッドレス CMS は、コンテンツに合わせて独自のヘッドを提供します。

ヘッドを省略することで、複雑さが減り、CMS をシンプルになります。また、コンテンツのレンダリングの責任は、実際にコンテンツを必要とするサービスに移ります。多くの場合、サービスのほうがレンダリングに適しています。

## コンテンツモデリング {#content-modeling}

Content Modeling (also known as data modeling) is your specialty, so what needs to be considered when modeling for headless?

For the headless applications to be able to access your content, and do something with it, the content really needs to have a predefined structure. **

********

### Accessing the Content {#access-content}

This is more of a development detail - but it might interest you, just to complete the story.

Once you&#39;ve created the Content Fragment Models, and your authors have used them to generate the content, the headless applications will need to access this content.

Adobe Experience Manager (AEM) as a Cloud Service, can selectively access your Content Fragments using the AEM GraphQL API, to return only the content that is needed. **

This means your project can realize headless delivery of structured content for use in your applications.

## 次の手順 {#whats-next}

[](basics.md)

## その他のリソース {#additional-resources}

* AEM ヘッドレスデベロッパージャーニー
   * [CMS ヘッドレス開発について](/help/journey-headless/developer/learn-about.md)
   * [Learn how to Model Your Content](/help/journey-headless/developer/model-your-content.md)
