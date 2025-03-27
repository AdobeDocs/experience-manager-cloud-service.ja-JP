---
title: コンテンツフラグメントでの参照の使用について
description: コンテンツ、他のフラグメントおよび他のアセット（メディア）への参照をコンテンツフラグメントで使用する方法について説明します。ヘッドレス CMS オーサリング用のネストされたフラグメントの必要性と仕組みを紹介します。
exl-id: a65e8a5a-954b-4307-8027-ca8bac5f4261
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 2c74a3a42dd21e2eaf71c1922931d5fa5149f7c5
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 97%

---

# コンテンツフラグメントでの参照の使用について {#author-headless-references}

## これまでの説明内容 {#story-so-far}

[AEM ヘッドレスコンテンツ作成者ジャーニー](overview.md)の冒頭の[はじめに](introduction.md)で、ヘッドレス向けのオーサリングに関連する基本概念と用語について説明しました。

ヘッドレス CMS オーサリングの基本と、AEMaaCS でのオーサリング、特にコンテンツフラグメントのオーサリングの基本を学びました。

この記事では、これらに基づいて、AEM ヘッドレスプロジェクトで独自のコンテンツをオーサリングするための参照の使用方法を説明します。

## 目的 {#objective}

* **オーディエンス**：経験者
* **目的**：ヘッドレス CMS オーサリングでの参照の使用方法を紹介します。使用可能な参照の種類と用途は次のとおりです。

   * コンテンツ参照
   * アセット／メディア参照
   * フラグメント参照
   * テキストブロック内からの即興参照

## 参照とは {#what-are-references}

参照は、他のコンテンツ、アセット（画像など）、他のフラグメントなどのリソースを接続するためのメカニズムです。それぞれよく似ていますが、いくつかの違いがあります。

参照には、専用のデータタイプを持つもの（コンテンツ参照やフラグメント参照など）もあれば、テキストブロック内の参照として追加されるもの（アセット参照や即興参照など）もあります。

![コンテンツフラグメント - 参照](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-overview.png)

## コンテンツ参照 {#content-references}

コンテンツ参照の役割は、他のコンテンツを参照できるようにすることです。これによって、コンテンツ項目を選択できるブラウザーが開きます。

次の 2 つのタイプがあります。

* **コンテンツ参照**
   * 参照されるリソースへのパスを指定します
* **コンテンツ参照（UUID）**
   * エディターでは、参照は参照先リソースへのパスを指定します。内部的には、参照はリソースを参照する Universally Unique ID（UUID）として保持されます

## アセット／メディア参照 {#assets-media-references}

アセット（画像やメディアなど）は、「**アセットを挿入**」オプションを使用して、テキストブロック内で参照することができます。この参照によって、ブラウザーが開き、アセットを選択できます。

![コンテンツフラグメント - アセットを挿入](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## フラグメント参照 {#fragment-references}

フラグメント参照の役割も同様です。つまり、別のフラグメントを参照できるようにします。これが重要な理由については、もう少し説明が必要です。

例えば、次のコンテンツフラグメントモデルが定義されているとします。

* City（市区町村）
* Company（会社）
* Person（ユーザー）
* 授賞歴

とても簡単に見えますが、Company には CEO も Employees（従業員）もいます。これらはすべて人物で、それぞれが Person として定義されます。

また、Person は Award（1 つまたは複数）を持っている可能性があります。

* 私の会社 - Company
   * CEO - Person
   * 従業員 - Person
      * 個人賞 - Award

しかし、これはほんの一例です。複雑さに応じて、Award が Company 固有のものであったり、Company が特定の City に本社を置いていたりすることがあります。

こうした相互関係は、作成者とヘッドレスアプリケーションの双方が理解できるように、フラグメント参照を使用して表すことができます。

作成者は、これらの関係を定義するわけではありません（コンテンツフラグメントモデルの作成時にコンテンツアーキテクトが行います）が、参照を把握して編集する方法を理解しておく必要があります。

次の 2 つの種類があります。

* **フラグメント参照**
   * 参照されるリソースへのパスを指定します
* **フラグメント参照（UUID）**
   * エディターでは、参照は参照先リソースへのパスを指定します。内部的には、参照はリソースを参照する Universally Unique ID（UUID）として保持されます

<!--
![Content Modeling with Content Fragments](/help/journey-headless/developer/assets/headless-modeling-01.png "Content Modeling with Content Fragments")
-->

### ネストされたフラグメントのオーサリング方法 {#author-nested-fragment}

フラグメント参照のオーサリングはどても簡単です（ただし、通常、フィールドには&#x200B;**フラグメント参照**&#x200B;というラベルは付きません）。参照を直接入力するか、フォルダーアイコンを選択してブラウザーを開き、必要なフラグメントを探して選択します（こちらの方が一般的です）。

![コンテンツフラグメント - 参照](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

コンテンツフラグメントモデルの定義で以下が決まります。

* 複数の参照を選択して追加できるかどうか
* 選択できるコンテンツフラグメントモデルのタイプ。参照に使用できるフラグメントモデルはコンテンツフラグメントモデルで定義されるので、AEM は、そのモデルに基づくフラグメントのみを表示します。

### ネストされたフラグメントのナビゲーション方法 {#navigate-nested-fragment}

コンテンツフラグメントエディターの「**構造ツリー**」タブを使用すると、フラグメントで参照されているフラグメント間を移動し、さらに、それらのフラグメントに含まれている参照間を移動できます。参照を選択すると、そのフラグメントが編集用に開きます。

![コンテンツフラグメント構造ツリー](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-structure-tree.png)

## アドホック参照 {#adhoc-references}

即興参照は、テキストブロック内に単純なリンクとして追加できます。

![コンテンツフラグメント - アドホック参照](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 次の手順 {#whats-next}

これで、コンテンツフラグメントにおける参照と構造について説明したので、次のステップは、[コンテンツフラグメントのメタデータとタグの定義について](metadata-tagging.md)です。このステップでは、コンテンツフラグメントのメタデータとタグを定義する方法を説明します。

## その他のリソース {#additional-resources}

* [コンテンツフラグメントの使用方法](/help/sites-cloud/administering/content-fragments/overview.md)

   * [コンテンツフラグメントの管理](/help/sites-cloud/administering/content-fragments/managing.md)

      * [アセットフォルダーへの設定の適用](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)

      * [コンテンツフラグメントの作成](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)

   * [コンテンツフラグメントのオーサリング](/help/sites-cloud/administering/content-fragments/authoring.md)

   * [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [コンテンツフラグメントモデル - データタイプ](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)

      * [コンテンツフラグメントモデル - プロパティ](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)

* はじめる前に
   * [アセットフォルダーの作成 - ヘッドレスセットアップ](/help/headless/setup/create-assets-folder.md)

* AEM ヘッドレスコンテンツアーキテクトジャーニー

* AEM ヘッドレス翻訳ジャーニー
