---
title: AEM でのコンテンツフラグメントモデルの作成について
description: コンテンツフラグメントモデルを使用したヘッドレス CMS のコンテンツモデリングの概念と仕組みについて説明します。
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 83%

---

# AEM でのコンテンツフラグメントモデルの作成について {#architect-headless-content-fragment-models}

## これまでの説明内容 {#story-so-far}

[AEM ヘッドレスコンテンツ作成者ジャーニー](overview.md)の冒頭の [AEM でのヘッドレスのコンテンツモデリングの基本について](basics.md)で、ヘッドレス向けのオーサリングに関連する基本概念と用語について説明しました。

この記事では、これらの原則に基づいて、AEM ヘッドレスプロジェクト用に独自のコンテンツフラグメントモデルを作成する方法について説明します。

## 目的 {#objective}

* **オーディエンス**：初心者
* **目的**：コンテンツフラグメントモデルを使用したヘッドレス CMS のコンテンツモデリングの概念と仕組みについて説明します。

## コンテンツフラグメントモデルの作成 {#creating-content-fragment-models}

次に、コンテンツフラグメントモデルを作成し、構造を定義できます。

1. コンテンツフラグメントコンソールで、コンテンツフラグメントモデルのパネルを選択します。

1. 目的の設定またはサブ設定に適したフォルダーに移動します。

1. **作成**&#x200B;を使用して、**新しいコンテンツフラグメントモデル**&#x200B;ダイアログを開きます。

   ![タイトルと説明](/help/sites-cloud/administering/content-fragments/assets/cf-managing-content-fragment-models-create.png)

1. 詳細を入力します。

1. 「**作成**」を使用して空のモデルを保存するか、「**作成して開く**」を使用します。

## コンテンツフラグメントモデルの定義 {#defining-content-fragment-models}

最初に新しいモデルを開くと、中央に大きな（かなり）空白スペースが表示され、左側に長い **データ型** リストが表示され、右側には **プロパティ** （選択したフィールドの場合と同様に、最初は空）が表示されます。

![空のモデル](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-empty-model.png)

では、何をすればよいのでしょうか。

次のいずれかを実行できます。

* データタイプを左側のパネルから、中央のパネルのフィールドに必要な場所にドラッグします。
* データタイプ別に「+」アイコンを選択して、フィールドリストの下部に追加します。
* 中央のパネルで「追加」を選択し、表示されるドロップダウンリストから必要なデータタイプを選択して、フィールドをリストの下部に追加します。

モデルは既に定義されています。

データタイプを追加したら、そのフィールドの「**プロパティ**」を定義する必要があります。これらのプロパティは、使用するタイプによって異なります。次に例を示します。

![データプロパティ](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-field-properties.png)

### コンテンツ作成者 {#your-content-authors}

コンテンツ作成者には、モデルの作成に使用された実際のデータタイプとプロパティは表示されません。つまり、場合によっては、特定のフィールドへの入力方法に関するヘルプと情報をコンテンツ作成者に提供する必要があります。基本的な情報については「フィールドラベル」と「デフォルト値」を使用できますが、より複雑なケースでは、プロジェクト固有のドキュメントを準備する必要があるかもしれません。

>[!NOTE]
>
>詳しくは、「その他のリソース」の「コンテンツフラグメントモデル」を参照してください。

## コンテンツフラグメントモデルの管理 {#managing-content-fragment-models}

<!-- needs more details -->

コンテンツフラグメントモデルの管理には、以下の操作が必要になります。

* モデルの有効化（または無効化） - コンテンツフラグメントの作成時に作成者がモデルを使用できるようになります（または使用できなくなります）。
* 削除 - 削除は常に必要ですが、コンテンツフラグメントに既に使用されているモデル、特に既に公開されているフラグメントを削除する場合には注意が必要です。

## 公開 {#publishing}

<!-- needs more details -->

コンテンツフラグメントモデルは、そのモデルに依存するコンテンツフラグメントの公開時または公開前に公開する必要があります。

>[!NOTE]
>
>まだ公開されていないモデルに基づくコンテンツフラグメントを作成者が公開しようとすると、選択リストにそのことが示され、モデルがフラグメントと共に公開されます。

モデルは、公開され次第、オーサー環境では読み取り専用モードに&#x200B;*ロック*&#x200B;されます。これは、変更によって、特にパブリッシュ環境で既存の GraphQL スキーマおよびクエリにエラーが発生するのを防ぐためです。コンソールには&#x200B;**ロック済み**&#x200B;と表示されます。

モデルが&#x200B;**ロック済み**（読み取り専用モード）の場合、モデルの内容と構造は表示できますが、モデルを直接編集することはできません。ただし、コンソールまたはモデルエディターを使用すれば&#x200B;**ロック済み**&#x200B;モデルを管理できます。

## 次の手順 {#whats-next}

これで基本を説明したので、次の手順は独自のコンテンツフラグメントモデルの作成を開始することです。

## その他のリソース {#additional-resources}

* [オーサリングに関する概念](/help/sites-cloud/authoring/author-publish.md)

* [基本操作](/help/sites-cloud/authoring/basic-handling.md) - このページは主に **Sites** コンソールに基づいていますが、ほとんどの機能は&#x200B;**一般**&#x200B;コンソールでの&#x200B;**コンテンツフラグメントモデル**&#x200B;への移動やアクションの実行にも関連しています。

* [コンテンツフラグメントの使用方法](/help/sites-cloud/administering/content-fragments/overview.md)

   * [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [コンテンツフラグメントモデルの定義](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

      * [コンテンツフラグメントモデルの有効化または無効化](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#enabling-disabling-a-content-fragment-model)

      * [アセットフォルダーでのコンテンツフラグメントモデルの許可](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder)

      * [コンテンツフラグメントモデルの削除](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#deleting-a-content-fragment-model)

      * [コンテンツフラグメントモデルの公開](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model)

      * [コンテンツフラグメントモデルを非公開にする](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#unpublishing-a-content-fragment-model)

      * [コンテンツフラグメントモデルのロック](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#locked-content-fragment-models)

* はじめる前に

   * [コンテンツフラグメントモデルの作成 - ヘッドレスセットアップ](/help/headless/setup/create-content-model.md)
