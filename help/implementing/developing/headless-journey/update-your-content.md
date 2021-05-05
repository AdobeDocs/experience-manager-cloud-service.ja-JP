---
title: AEM AssetsAPIを使用したコンテンツの更新方法
description: AEMヘッドレス開発者ジャーニーのこの部分では、REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を説明します。
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 3d5ea8df4cefdb8c2bebe26333002a4680fa9fd4
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 3%

---

# AEM AssetsAPIを使用したコンテンツの更新方法{#update-your-content}

>[!CAUTION]
>
>作業中 — このドキュメントの作成は現在進行中で、完全なもの、最終的なもの、または実稼働目的で使用するものとして理解してはなりません。

[AEMヘッドレス開発者ジャーニーのこの部分では、](overview.md)がREST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を学びます。

## {#story-so-far}

以前のドキュメントのAEM headlessジャーニーでは、[AEM配信APIを介したコンテンツへのアクセス方法](access-your-content.md)で、AEM GraphQL APIを介したAEMのheadlessコンテンツへのアクセス方法を学び、次の点に注意してください。

* GraphQLについて高レベルの理解を得る。
* AEM GraphQL APIの仕組みを理解します。
* 実際的なサンプルクエリをいくつか理解します。

この記事は、これらの基本事項に基づいて構築されているので、REST APIを使用してAEMの既存のヘッドレスコンテンツを更新する方法を理解しています。

## 目的 {#objective}

* **オーディエンス**:詳細
* **目的**:REST APIを使用してコンテンツフラグメントのコンテンツにアクセスし、更新する方法を説明します。
   * AEM AssetsHTTP APIを紹介します。
   * APIでコンテンツフラグメントのサポートを紹介し、ディスカッションを行います。
   * APIの詳細を説明します。
   * サンプルコードを見て、実際の動作を確認してください。

## 次の作業{#whats-next}

AEMヘッドレス開発者ジャーニーのこの部分が完了したら、次の作業を行う必要があります。

* AEM AssetsHTTP APIについて説明します。
* このAPIでコンテンツフラグメントがどのようにサポートされているかを理解します。
* サンプルコードの経験があり、APIの実際の動作を理解している。

AEMのヘッドレスジャーニーは、次にドキュメント[How to Put It All Togeter - Your App and Your Content in AEM Headless](put-it-all-together.md)を確認し、AEMヘッドレスプロジェクトの取り組みと運用準備を進めて行く必要があります。

## その他のリソース {#additional-resources}

* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [コンテンツフラグメント REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
