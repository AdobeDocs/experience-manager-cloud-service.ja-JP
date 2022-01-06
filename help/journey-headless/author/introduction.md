---
title: AEMヘッドレスコンテンツ作成者ジャーニー
description: Adobe Experience Manager as a Cloud Serviceの強力で柔軟なヘッドレス機能と、プロジェクトのコンテンツを作成する方法の紹介です。
exl-id: 065b00cb-a82d-4bcb-b2c9-44542cee6303
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 4%

---

# Authoring for Headless with AEM - An Introduction {#author-headless-introduction}

[](overview.md)

## 目的 {#objective}

* **オーディエンス**：初心者
* **目的**:ヘッドレスオーサリングに関連する概念と用語を紹介します。

## コンテンツ管理システム (CMS) {#content-management-system}

コンテンツ管理システムとは

コンテンツ管理システム (CMS) は、コンテンツの管理に使用されるコンピュータシステムです。 これは少し一般的な操作なので、より正確に言うと、（通常）Web サイトで利用できるようにするコンテンツの管理に使用されます。

## ヘッドレス CMS {#headless-cms}

ヘッドレスとは、Web 上にコンテンツを表示する方法からコンテンツを効果的に分離するシステムを表すために使用される用語です。

従来は CMS でコンテンツを管理し、同じ CMS が Web ページ上でのコンテンツのレンダリングを行います。

Now, headless means that your content-set can be managed in the CMS and then accessed by one, or more, (independent) applications.

This means that your content can be delivered to any device, in a wide range of formats. This makes the whole process much more flexible, and also means that you do not need to worry about layout and formatting.

>[!NOTE]
>
>ヘッドレス CMS の技術的な詳細について詳しくは、 CMS ヘッドレス開発についての詳細を参照してください。

## Adobe Experience Manager as a Cloud Service {#aem-cloud-service}

AEMとは？

最初に、AEMは幅広い機能を備えたコンテンツ管理システムで、要件に合わせてカスタマイズすることもできます。

これは、すべてが次の形式で使用できることを意味します。

* ヘッドレス CMS
   * ヘッドレスの場合は、コンテンツを次の形式で作成できます **コンテンツフラグメント**.
これらは、様々なアプリケーションから直接アクセスできる、自己完結型のコンテンツ項目です。これらの項目は、 **コンテンツフラグメントモデル**.
This means your content can reach a wide range of devices, in a wide range of formats and with a wide selection of functionality.
( また、2 つのホワイトとして、これらのフラグメントはAEM Web ページを構築する際にも使用できます（必要に応じて）。

* &quot;Traditional&quot; CMS
   * Content is authored for web pages, using a range of components that define how the content will be rendered on your website. Even here AEM is extremely flexible as your project team can develop customized components.

## コンテンツモデリング {#content-modeling}

つまり、コンテンツモデリング（データモデリングとも呼ばれます）はもう 1 つの技術的用語です。なぜ作成者として興味を持つ必要があるのでしょうか。

ヘッドレスアプリケーションがコンテンツにアクセスし、それを使用して何らかの処理をおこなうには、コンテンツに事前に定義された構造が必要です。 コンテンツを自由形式として持つことは可能ですが、それは人生を生み出すでしょう *非常に* アプリケーションにとって複雑です。

基本的に、コンテンツが準拠する構造を定義するプロセスは、モデルの設計です。これは、データモデリングと呼ばれます。

AEMの場合、コンテンツアーキテクトの役割（多くの場合、別の人）は、データモデリングを実行して、様々な **コンテンツフラグメントモデル**  — その後、次を使用してコンテンツの基礎として使用します。 **コンテンツフラグメント**.

>[!NOTE]
>
>データモデリングの詳細については、AEMヘッドレスコンテンツアーキテクトジャーニーを参照してください。

## 次の手順 {#whats-next}

[](basics.md)This will introduce the basic handling of AEM together with how to author Content Fragments.

## その他のリソース {#additional-resources}

* AEM ヘッドレスデベロッパージャーニー
   * [CMS ヘッドレス開発について](/help/journey-headless/developer/learn-about.md)
   * [コンテンツのモデル化方法を学ぶ](/help/journey-headless/developer/model-your-content.md)

* AEMヘッドレスコンテンツアーキテクトジャーニー

* AEMヘッドレスコンテンツ翻訳ジャーニー
