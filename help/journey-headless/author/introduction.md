---
title: AEM as a Headless CMS 用のオーサリング - はじめに
description: Adobe Experience Manager as a Cloud Service の機能をヘッドレス CMS として使用し、プロジェクトのコンテンツをオーサリングする方法を紹介します。
exl-id: 065b00cb-a82d-4bcb-b2c9-44542cee6303
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 100%

---

# AEM as a Headless CMS 用のオーサリング - はじめに {#author-headless-introduction}

[AEM ヘッドレスコンテンツ作成者ジャーニー](overview.md)のこの手順では、Adobe Experience Manager（AEM）as a Cloud Service をヘッドレス CMS として使用した場合の、コンテンツのオーサリングを理解するために必要な（基本）概念と用語について説明します。これには、ヘッドレスコンテンツ配信用のコンテンツの構造化と作成が含まれます。

## 目的 {#objective}

* **オーディエンス**：初心者
* **目的**：ヘッドレスオーサリングに関係する概念と用語を紹介します。

## コンテンツ管理システム（CMS） {#content-management-system}

コンテンツ管理システムとは

コンテンツ管理システム（CMS）は、その名のとおり、コンテンツの管理に使用されるコンピュータシステムです。もう少し正確に言えば、web サイトで公開するコンテンツの管理に（通常）使用されるものです。

## ヘッドレス CMS {#headless-cms}

ヘッドレスとは、コンテンツを web 上でのコンテンツの表示方法から効果的に切り離すシステムを表す用語です。

従来は、CMS でコンテンツを管理し、web ページでのそのコンテンツのレンダリングするのも CMS でした。

しかし、ヘッドレスでは、コンテンツセットを CMS で管理し、1 つ以上の（独立した）アプリケーションからそのコンテンツにアクセスすることができます。

つまり、コンテンツを様々な形式で任意のデバイスに配信できるということです。これにより、プロセス全体がはるかに柔軟になり、レイアウトや書式設定を気にする必要もなくなります。

>[!NOTE]
>
>ヘッドレス CMS の技術的な詳細については、「CMS ヘッドレス開発について」を参照してください。

## Adobe Experience Manager as a Cloud Service {#aem-cloud-service}

では、AEM とは何でしょうか。

第一に、AEM は、要件に合わせてカスタマイズ可能な幅広い機能を備えたコンテンツ管理システムです。

つまり、AEM は以下のものとして使用できます。

* ヘッドレス CMS
   * ヘッドレスの場合、コンテンツは&#x200B;**コンテンツフラグメント**としてオーサリングできます。
これは、様々なアプリケーションから直接アクセスできる自己完結型のコンテンツ項目で、**コンテンツフラグメントモデル**に基づいて構造が事前に定義されています。
つまり、豊富な機能を使用して様々な形式で様々なデバイスにコンテンツを配信できます
（さらに、必要に応じて、これらのフラグメントを AEM web ページの作成時に使用することもできます）。

* 「従来の」CMS
   * コンテンツは、web サイト上でのコンテンツのレンダリング方法を定義する様々なコンポーネントを使用して、web ページ用に作成されます。ここでも AEM は、カスタマイズしたコンポーネントをプロジェクトチームが開発できるので、きわめて柔軟です。

## コンテンツモデリング {#content-modeling}

もう 1 つの技術用語は、コンテンツモデリングです（データモデリングとも呼ばれます）。なぜ、これが作成者の関心事になるのでしょうか。

ヘッドレスアプリケーションがコンテンツにアクセスして何らかの処理を行えるようにするには、事前に定義された構造がコンテンツに必要です。コンテンツを自由形式にすることも可能ですが、その場合は、アプリケーション側の処理が&#x200B;*非常に*&#x200B;複雑になります。

基本的に、コンテンツが従うべき構造を定義するプロセスには、モデルの設計が不可欠です。これをデータモデリングと呼びます。

AEM の場合は、コンテンツアーキテクトの役割（多くの場合、コンテンツ作成者とは別の人物）がデータモデリングを行い、一連の&#x200B;**コンテンツフラグメントモデル**&#x200B;を設計します。コンテンツ作成者は、この一連のモデルをコンテンツの基礎として使用します（その際に&#x200B;**コンテンツフラグメント**&#x200B;を使用します）。

>[!NOTE]
>
>データモデリングについて詳しくは、「AEM ヘッドレスコンテンツアーキテクトジャーニー」を参照してください。

## 次の手順 {#whats-next}

これで、概念と用語を説明したので、次の手順は [AEM を使用したヘッドレスのオーサリングの基本](basics.md)です。ここでは、AEM の基本操作とコンテンツフラグメントのオーサリング方法を紹介します。

## その他のリソース {#additional-resources}

* [ヘッドレス CMS としての AEM の概要](/help/headless/introduction.md)

* [AEM のヘッドレスに関するチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ja)

* AEM ヘッドレスデベロッパージャーニー
   * [CMS ヘッドレス開発について](/help/journey-headless/developer/learn-about.md)
   * [コンテンツをモデル化する方法](/help/journey-headless/developer/model-your-content.md)

* [AEM 開発者ポータル](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)

* [AEM ヘッドレスコンテンツアーキテクトジャーニー](/help/journey-headless/architect/overview.md)

* [AEM ヘッドレス翻訳ジャーニー](/help/journey-headless/translation/overview.md)
