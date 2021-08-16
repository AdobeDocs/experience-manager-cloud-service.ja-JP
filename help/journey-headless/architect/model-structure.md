---
title: AEMでのコンテンツフラグメントモデルの作成について説明します。
description: コンテンツフラグメントモデルを使用してヘッドレスCMSのコンテンツをモデリングする際の概念と仕組みについて説明します。
index: false
hide: true
hidefromtoc: true
source-git-commit: 41ad9e8ee77ae4494d28026b5ad9da45c06eaeaf
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 19%

---


# AEMでのコンテンツフラグメントモデルの作成について説明します。 {#architect-headless-content-fragment-models}

## 今までの話 {#story-so-far}

[AEM Headless Content Authorジャーニー](overview.md)の最初に、[AEM](basics.md)を使用したHeadless向けコンテンツモデリングの基本について、ヘッドレス向けのオーサリングに関連する基本概念と用語を説明しました。

この記事はこれらを基に構築され、AEMヘッドレスプロジェクト用に独自のコンテンツフラグメントモデルを作成する方法を理解できます。

## 目的 {#objective}

* **オーディエンス**：初心者
* **目的**:コンテンツフラグメントモデルを使用してヘッドレスCMSのコンテンツをモデリングする際の概念と仕組み。

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools -> General -> Configuration Browser. You can either select to configure the global entry, or create a new configuration. For example:

![Define configuration](/help/assets/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## コンテンツフラグメントモデルの作成 {#creating-content-fragment-models}

その後、コンテンツフラグメントモデルを作成し、構造を定義できます。これは、ツール／アセット／コンテンツフラグメントモデルで実行できます。

![ツールのコンテンツフラグメントモデル](assets/cfm-tools.png)

これを選択した後、モデルの場所に移動し、「**作成**」を選択します。 ここで、様々な重要な詳細を入力できます。

「**モデルを有効にする**」オプションは、デフォルトで有効になっています。 つまり、モデルを保存するとすぐに、そのモデルを（コンテンツフラグメントの作成時に）使用できるようになります。 必要に応じて、この機能を無効にすることができます。既存のモデルを後で有効（または無効）にすることもできます。

![コンテンツフラグメントモデルを作成](/help/assets/content-fragments/assets/cfm-models-02.png)

**「**&#x200B;を作成」で確認し、その後、モデルを&#x200B;**開いて**&#x200B;構造の定義を開始できます。

## コンテンツフラグメントモデルの定義 {#defining-content-fragment-models}

新しいモデルを初めて開くと、左側に大きな空白が、右側に&#x200B;**データ型**&#x200B;の長いリストが表示されます。

![空のモデル](/help/assets/content-fragments/assets/cfm-models-03.png)

では、どうすればいいのでしょうか。

**データ型**&#x200B;のインスタンスを左側のスペースにドラッグできます。既にモデルを定義しています。

![フィールドの定義](/help/assets/content-fragments/assets/cfm-models-04.png)

データ型を追加したら、そのフィールドの&#x200B;**プロパティ**&#x200B;を定義する必要があります。 これらは、使用するタイプによって異なります。 次に例を示します。

![データのプロパティ](/help/assets/content-fragments/assets/cfm-models-05.png)

フィールドは必要な数だけ追加できます。 次に例を示します。

![コンテンツフラグメントモデル](/help/assets/content-fragments/assets/cfm-models-07.png)

### コンテンツ作成者 {#your-content-authors}

コンテンツ作成者には、モデルの作成に使用した実際のデータタイプとプロパティは表示されません。 つまり、特定のフィールドの入力方法に関するヘルプと情報を提供する必要が生じる場合があります。 基本情報については、フィールドラベルとデフォルト値を使用できますが、プロジェクト固有のドキュメントをより複雑にする必要が生じる場合があります。

>[!NOTE]
>
>「その他のリソース - コンテンツフラグメントモデル」を参照してください。

## コンテンツフラグメントモデルの管理 {#managing-content-fragment-models}

<!-- needs more details -->

コンテンツフラグメントモデルの管理には、次の作業が必要です。

* コンテンツフラグメントを有効（または無効）にする — 作成者がコンテンツフラグメントを作成する際に使用できるようになります。
* 削除 — 削除は常に必要ですが、コンテンツフラグメント（特に公開済みのフラグメント）に既に使用されているモデルの削除に注意する必要があります。

## 公開 {#publishing}

<!-- needs more details -->

コンテンツフラグメントモデルは、依存するコンテンツフラグメントの公開時または公開前に公開する必要があります。

>[!NOTE]
>
>作成者が、まだモデルが公開されていないコンテンツフラグメントを公開しようとすると、選択リストにその旨が示され、モデルはフラグメントと共に公開されます。

## 次の手順 {#whats-next}

これで基本を学習したので、次に、独自のコンテンツフラグメントモデルの作成を開始します。

## その他のリソース {#additional-resources}

* [オーサリングに関する概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — このページは主にサイトコンソールに基づいていま **** すが、多くの機能はアセットコンソールのコンテンツフラグメントモデルに移動し、アクションを実行する場合にも関連して ****  **** います。

* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)

   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)

      * [コンテンツフラグメントモデルの定義](/help/assets/content-fragments/content-fragments-models.md#defining-your-content-fragment-model)

      * [コンテンツフラグメントモデルの有効化または無効化](/help/assets/content-fragments/content-fragments-models.md#enabling-disabling-a-content-fragment-model)

      * [アセットフォルダーでのコンテンツフラグメントモデルの許可](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

      * [コンテンツフラグメントモデルの削除](/help/assets/content-fragments/content-fragments-models.md#deleting-a-content-fragment-model)

      * [コンテンツフラグメントモデルの公開](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)

      * [コンテンツフラグメントモデルを非公開にする](/help/assets/content-fragments/content-fragments-models.md#unpublishing-a-content-fragment-model)

* 「はじめる前に」ガイド 

   * [コンテンツフラグメントモデルのヘッドレス作成のクイック開始ガイド](/help/implementing/developing/headless/getting-started/create-content-model.md)
