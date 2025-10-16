---
title: 設定の作成 – ヘッドレスセットアップ
description: AEM as a Cloud Service でヘッドレスを使い始めるための最初の手順として設定を作成します。
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 91%

---

# 設定の作成 – ヘッドレスセットアップ {#create-configuration}

AEM as a Cloud Service でヘッドレス機能を使い始めるには、まず設定を作成する必要があります。

## 設定とは  {#what-is-a-configuration}

設定ブラウザーには、AEM の設定用の汎用設定 API、コンテンツ構造、解決メカニズムが用意されています。

AEM のヘッドレスなコンテンツ管理に関しては、AEM 内でコンテンツモデルを作成できるワークプレイスとして設定を考えてみてください。これにより、将来のコンテンツとコンテンツフラグメントの構造を定義できます。複数の設定を作成して、これらのモデルを分離できます。

コンテンツモデルの管理での設定の使用方法は、[フルスタック AEM の実装ページテンプレート](/help/sites-cloud/authoring/page-editor/templates.md)と似ています。

## 設定の作成方法 {#how-to-create-a-configuration}

管理者は、設定を 1 回だけ作成する必要があります。コンテンツモデルの整理のために新しいワークスペースが必要になることはほとんどありません。この「はじめる前に」ガイドの目的上、設定を 1 つ作成する必要があります。

詳しい手順については、[&#x200B; 設定ブラウザーでのコンテンツフラグメント機能の有効化 &#x200B;](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser) を参照してください。

>[!NOTE]
>
>実装要件によっては、**コンテンツフラグメントモデル**&#x200B;および **GraphQL 永続クエリ**&#x200B;に加えて、設定オプションが必要になる場合があります。

## 次の手順 {#next-steps}

この設定を使用して、「はじめる前に」の第 2 部に進み、[コンテンツフラグメントモデルを作成](create-content-model.md)できるようになりました。

>[!TIP]
>
>設定ブラウザーについて詳しくは、[設定ブラウザーのドキュメント](/help/implementing/developing/introduction/configurations.md)を参照してください。
