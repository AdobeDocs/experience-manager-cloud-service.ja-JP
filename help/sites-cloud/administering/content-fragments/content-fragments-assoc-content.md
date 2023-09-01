---
title: 関連コンテンツ
description: コンテンツフラグメントの関連コンテンツ機能が、フラグメントで（オプションで）使用されるアセットの接続を提供し、ページのオーサリングとヘッドレスコンテンツ配信の両方にさらなる柔軟性を追加する方法を理解します。
feature: Content Fragments
role: User
hide: true
index: false
hidefromtoc: true
exl-id: eb524872-1403-42d1-b735-eaab382cf313
source-git-commit: 5ce5746026c5683e79cdc1c9dc96804756321cdb
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 81%

---


# 関連コンテンツ{#associated-content}

<!--
hide: yes
index: no
hidefromtoc: yes
-->

AEM の関連コンテンツ機能には接続が用意されており、フラグメントをコンテンツページに追加する際に、アセットをオプションでフラグメントと共に使用できます。これは、[ページでコンテンツフラグメントを使用する際にアクセスできる様々なアセットを提供](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content)することで行われ、適切なアセットを検索するために必要な時間を短縮させることもできます。これにより、ヘッドレスコンテンツ配信の柔軟性も向上させます。

## 関連コンテンツの追加 {#adding-associated-content}

>[!NOTE]
>
>[ビジュアルアセット（画像など）](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets)をフラグメントやページに追加するための様々な方法があります。

関連付けを作成するには、最初に[メディアアセットをコレクションに追加](/help/assets/manage-collections.md)する必要があります。それが完了した後で以下を実行できます。

1. フラグメントを開き、サイドパネルから「**関連コンテンツ**」を選択します。

   ![関連コンテンツ](assets/cfm-assoc-content-01.png)

1. コレクションが既に関連付けられているかどうかに応じて、次のいずれかを選択します。

   * **コンテンツを関連付け**  — 最初に関連付けられたコレクション
   * **コレクションを関連付け**  — 関連付けられたコレクションは既に設定されています

1. 必要なコレクションを選択します。

   選択したコレクションにフラグメント自体をオプションで追加できます。これにより追跡が可能になります。

   ![コレクションの選択](assets/cfm-assoc-content-02.png)

1. 確定します（「**選択**」を使用）。コレクションが関連付けられて一覧表示されます。

   ![cfm-6420-05](assets/cfm-assoc-content-03.png)

## 関連コンテンツの編集 {#editing-associated-content}

コレクションを関連付けると、次の操作を実行できます。

* **削除** 関連団体。
* **アセットを追加** をコレクションに追加します。
* 追加のアクションを実行するアセットを選択します。
* アセットを編集します。
