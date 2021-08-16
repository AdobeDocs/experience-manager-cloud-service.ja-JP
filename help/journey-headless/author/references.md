---
title: コンテンツフラグメントでの参照の使用について説明します
description: コンテンツフラグメント、他のフラグメント、およびその他のアセット（メディア）での参照の使用について説明します。 ヘッドレスCMSオーサリングのためのネストされたフラグメントの必要性と仕組みを紹介します。
index: false
hide: true
hidefromtoc: true
source-git-commit: 41ad9e8ee77ae4494d28026b5ad9da45c06eaeaf
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 7%

---


# コンテンツフラグメントでの参照の使用について説明します {#author-headless-references}

## 今までの話 {#story-so-far}

[AEMヘッドレスコンテンツ作成者ジャーニー](overview.md)の最初に、[はじめに](introduction.md)では、ヘッドレス作成に関連する基本的な概念と用語について説明しました。

ヘッドレスCMSオーサリングの基本、特にAEMaaCSでのオーサリングの概要、特にコンテンツフラグメントのオーサリングについて学習しました。

この記事はこれらを基に構築されており、参照を使用してAEMヘッドレスプロジェクト用に独自のコンテンツを作成する方法を理解できます。

## 目的 {#objective}

* **オーディエンス**：経験者
* **目的**:ヘッドレスCMSオーサリングの参照の使用を紹介します。使用可能な参照の種類と目的は次のとおりです。

   * コンテンツ参照
   * アセット/メディア参照
   * フラグメント参照
   * テキストブロック内からのアドホック参照

## 参照とは {#what-are-references}

参照は、他のコンテンツ、アセット（画像など）、その他のフラグメントなど、リソースを接続するための単なるメカニズムです。 非常に似ていますが、いくつか違いがあります。

一部の参照には専用のデータ型（コンテンツ参照やフラグメント参照など）があり、それ以外の参照は、テキストブロック内の参照として追加するだけです（アセット参照やアドホック参照など）。

![コンテンツフラグメント — リファレンス](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## コンテンツ参照 {#content-references}

コンテンツ参照はそれを行います。コンテンツ参照を使用すると、他のコンテンツを参照できます。 これにより、コンテンツ項目を選択できるブラウザーが開きます。

## アセット/メディア参照 {#assets-media-references}

アセット（画像やメディアなど）は、「**アセットを挿入**」オプションを使用して、テキストブロック内で参照できます。 これにより、アセットを選択できるブラウザーが開きます。

![コンテンツフラグメント — アセットの挿入](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## フラグメント参照 {#fragment-references}

繰り返しますが、フラグメント参照はそれだけを行い、別のフラグメントを参照できます。 これが重要な理由は、もう少し説明が必要なのです。

例えば、次のコンテンツフラグメントモデルを定義できます。

* City
* 会社
* Person
* awards（受賞歴）

簡単に見えるが、もちろん会社にはCEOと従業員がいる….これらはすべて人で、それぞれが人として定義されます。

そして、1人の人に賞（または2つ）を与えることができます。

* マイ会社 — 会社
   * CEO — 担当者
   * 従業員 — 個人
      * 個人賞 — 賞

それはスターター向けです 複雑さに応じて、賞は会社固有の場合もあれば、会社が特定の都市に主なオフィスを持つ場合もあります。

これらの相互関係は、自分（作成者）とヘッドレスアプリケーションの両方が理解できるように、フラグメント参照を使用して実現できます。

作成者は、（コンテンツフラグメントモデルの作成時にコンテンツアーキテクトがおこなう）これらの関係の定義に対しては責任を負いませんが、参照を認識し編集する方法を理解しておく必要があります。

<!--
![Content Modeling with Content Fragments](/help/journey-headless/developer/assets/headless-modeling-01.png "Content Modeling with Content Fragments")
-->

### ネストされたフラグメントの作成方法 {#author-nested-fragment}

フラグメント参照のオーサリングは、かなり簡単です（ただし、通常、フィールドには「**フラグメント参照**」というラベルは付きません）。 参照を直接入力するか、（可能性が高い場合は）フォルダーアイコンを選択してブラウザーを開き、必要なフラグメントに移動して選択できます。

![コンテンツフラグメント — リファレンス](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

コンテンツフラグメントモデルの定義では、次の操作を行います。

* 複数の参照の追加を選択できるかどうか
* 選択可能なコンテンツフラグメントのモデルタイプ。コンテンツフラグメントモデルは、参照で許可されるフラグメントモデルを定義するので、AEMは、これらのモデルに基づくフラグメントのみを表示します。

### ネストされたフラグメントのナビゲート方法 {#navigate-nested-fragment}

コンテンツフラグメントエディターの「**構造ツリー**」タブを使用すると、フラグメントで参照されているフラグメント間を移動した後、それらに含まれる参照間を移動できます。 参照を選択すると、そのフラグメントが編集用に開きます。

>[!NOTE]
>
>メインパネルのパンくずリストを使用して、開始点に戻ることができます。

![コンテンツフラグメント構造ツリー](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## アドホック参照 {#adhoc-references}

アドホック参照は、テキストブロック内のシンプルなリンクとして追加できます。

![コンテンツフラグメント — アドホック参照](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 次の手順 {#whats-next}

コンテンツフラグメントの参照と構造について学習したので、次の手順は[メタデータとタグ付け](metadata-tagging.md)について学習します。 コンテンツフラグメントのメタデータとタグを定義する方法を紹介し、説明します。

## その他のリソース {#additional-resources}

* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)

   * [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md)

      * [アセットフォルダーへの設定の適用](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [コンテンツフラグメントの作成](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [バリエーション — コンテンツフラグメントのオーサリング](/help/assets/content-fragments/content-fragments-variations.md)

   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)

      * [コンテンツフラグメントモデル — データタイプ](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [コンテンツフラグメントモデル — プロパティ](/help/assets/content-fragments/content-fragments-models.md#properties)


* 「はじめる前に」ガイド 
   * [アセットフォルダーのヘッドレス作成のクイック開始ガイド](/help/implementing/developing/headless/getting-started/create-assets-folder.md)

* AEMヘッドレスコンテンツアーキテクトジャーニー

* AEMヘッドレス翻訳ジャーニー