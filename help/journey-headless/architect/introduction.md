---
title: AEM as a Headless CMS のコンテンツモデリング：概要
description: Adobe Experience Manager as a Cloud Service as a Headless CMS の機能を使用して、プロジェクトのコンテンツをモデル化する方法を紹介します。
exl-id: 62061d73-6fdb-440b-a7dd-b0d530d49186
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 100%

---

# AEM as a Headless CMS のコンテンツモデリング：概要 {#architect-headless-introduction}

[AEM ヘッドレスコンテンツアーキテクトジャーニー](overview.md)のこのステップでは、Adobe Experience Manager（AEM）as a Cloud Service as a Headless CMS の使用時にコンテンツモデリングを理解するうえで必要な（基本）概念と用語について説明します。

このドキュメントを通じて、ヘッドレスコンテンツ配信、AEM によるヘッドレスのサポートおよびコンテンツがヘッドレス向けにどのようにモデル化されるかを理解できるようになります。読み終えると、次のことが習得できます。

* ヘッドレスコンテンツ配信の基本概念を理解する。
* AEM でのヘッドレスとコンテンツモデリングのサポート方法に詳しくなる

## 目的 {#objective}

* **オーディエンス**：初心者
* **目的**：ヘッドレスコンテンツモデリングに関係のある概念と用語を紹介します。

## フルスタックコンテンツ配信 {#full-stack}

使いやすい大規模なコンテンツ管理システム（CMS）が登場して以来、多くの組織はメッセージング、ブランディング、コミュニケーションを管理する一元的な場所としてコンテンツ管理システムを活用してきました。CMS をエクスペリエンス管理の中心として使用することで、異なるシステムでタスクを重複させる必要がなくなり、効率が向上しました。

![従来のフルスタック CMS](/help/journey-headless/developer/assets/full-stack.png)

フルスタック CMS では、コンテンツを操作する機能はすべて CMS 内にあります。システムの機能は、CMS スタックの異なるコンポーネントを構成します。フルスタックソリューションには多くの利点があります。

* 維持管理するシステムは 1 つである。
* コンテンツを一元的に管理できる。
* システムのすべてのサービスが統合されている。
* コンテンツのオーサリングはシームレスである。

したがって、新しいチャネルを追加したり、新しいタイプのエクスペリエンスをサポートしたりする必要がある場合は、1 つ（または複数）の新しいコンポーネントをスタックに挿入します。変更が必要なのは 1 か所だけです。

![スタックへの新しいチャネルの追加](/help/journey-headless/developer/assets/adding-channel.png)

ただし、スタック内の他の項目を、変更に合わせて調整する必要があるので、スタック内の依存関係の複雑さがすぐに明らかになります。

## ヘッドレスのヘッド {#the-head}

システムのヘッドは、通常、そのシステムの出力レンダラーです。一般的には、GUI やその他のグラフィカル出力の形式です。

ヘッドレス CMS では、CMS がコンテンツを管理し、コンシューマーに配信します。ただし、ヘッドレス CMS では、標準化された方法で&#x200B;**コンテンツ**&#x200B;を配信だけで、最終的な出力のレンダリングは省略され、コンテンツの&#x200B;**プレゼンテーション**&#x200B;は消費サービスに委ねられます。

![ヘッドレス CMS](/help/journey-headless/developer/assets/headless-cms.png)

消費サービス（AR エクスペリエンス、web ショップ、モバイルエクスペリエンス、プログレッシブ web アプリ（PWA）など）では、ヘッドレス CMS からコンテンツを取り込み、独自にレンダリングを提供します。ヘッドレス CMS は、コンテンツに合わせて独自のヘッドを提供します。

ヘッドを省略することで、複雑さが減り、CMS をシンプルになります。また、コンテンツのレンダリングの責任は、実際にコンテンツを必要とするサービスに移ります。多くの場合、サービスのほうがレンダリングに適しています。

## コンテンツモデリング {#content-modeling}

コンテンツモデリング（データモデリングとも呼ばれます）は専門分野であり、ヘッドレス向けモデリングの際には、何を考慮すべきでしょうか。

ヘッドレスアプリケーションがコンテンツにアクセスして何らかの処理を行うためには、コンテンツの構造を事前に定義しておく必要があります。コンテンツを自由形式にすることも可能ですが、その場合は、アプリケーション側の処理が&#x200B;*非常に*&#x200B;複雑になります。

AEM の場合は、コンテンツアーキテクトがコンテンツモデリングを実行して、様々な&#x200B;**コンテンツフラグメントモデル**&#x200B;を設計します。これらのモデルは、コンテンツを保持する&#x200B;**コンテンツフラグメント**&#x200B;をコンテンツ作成者が作成する際に使用される構造を定義します。

### コンテンツへのアクセス {#access-content}

これはどちらかと言えば、開発上の詳細になりますが、ストーリーを完結させるうえで興味を引くかもしれません。

コンテンツフラグメントモデルを作成し、作成者がそれらを使用してコンテンツを生成したら、ヘッドレスアプリケーションは、このコンテンツにアクセスする必要があります。

Adobe Experience Manager （AEM）as a Cloud Service では、AEM GraphQL API を使用して、コンテンツフラグメントに選択的にアクセスし、必要なコンテンツのみを返すことができます。開発者は、API を使用して、特定のコンテンツを選択するクエリを作成できます。この選択プロセスは、*使用する*&#x200B;コンテンツフラグメントモデルに基づいています。

つまり、アプリケーションで使用する構造化コンテンツのヘッドレス配信をプロジェクトで実現できることになります。

## 次の手順 {#whats-next}

これで、概念と用語を説明したので、次のステップは [AEM でのヘッドレス向けコンテンツモデリングの基本について](basics.md)です。

## その他のリソース {#additional-resources}

* AEM ヘッドレスデベロッパージャーニー
   * [CMS ヘッドレス開発について](/help/journey-headless/developer/learn-about.md)
   * [コンテンツをモデル化する方法](/help/journey-headless/developer/model-your-content.md)

* [ヘッドレス CMS としての AEM の概要](/help/headless/introduction.md)

* [AEM 開発者ポータル](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)

* [AEM のヘッドレスに関するチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ja)
