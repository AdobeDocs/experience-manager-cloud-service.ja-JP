---
title: 製品コックピット
description: 製品コックピットの操作
exl-id: 6dbf039c-e040-48f1-88f3-ebbd70cdf94d
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 73%

---

# 製品コックピット {#product-cockpit}

## 概要 {#overview}

製品コックピットでは、リンクされた製品カタログと関連コンテンツの概要を統一して提供します。関連するすべてのコンテンツには、コックピットからすぐにアクセスできるリンクがあります。

ステージングされた製品データには、新しいカテゴリや製品、更新されたプロパティなど、将来的にあらゆる変異が含まれます。

>[!NOTE]
>
>製品カタログという用語は、コマースストア、ストア表示などの同じような表現で置き換えられます。

## 設定 {#configuration}

商品カタログは、AEMで設定する必要があります。 詳しくは、 [ストアとカタログの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/getting-started.html#catalog) を参照してください。

ステージングされたカタログ機能を有効にするには、認証が必要です。詳しくは、 [はじめに](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/getting-started.html) を参照してください。

>[!NOTE]
>
>ステージング済みカタログ機能は、トークンベースの認証をサポートするAdobe Commerceおよびサードパーティコネクタでのみ使用できます。

## 製品コックピットを開く {#opening-product-cockpit}

製品コックピットにアクセスする最も簡単な方法は、AEM のメインメニューの「コマース」メニューを使用することです。オムニサーチ（コマースを検索）を使用したり、`https://<yourAEMInstance>/commerce.html` を開いたりすることもできます。

![AEM メニュー](../assets/aem-menu.png)

## 製品カタログの参照 {#browsing-product-catalogs}

製品コックピットは、製品カタログ構造に従って階層的に編成されています。第 1 レベルは、コマースバックエンドのメタ情報を含む、設定済みのすべての製品カタログのカタログルートレベルを示します。

![設定済みのカタログ](../assets/catalog-overview.png)

カテゴリをクリックすると、クリックされたカテゴリの子が読み込まれます。

![カテゴリの子](../assets/catalog-category-children.png)

製品をクリックすると、製品のバリエーションが読み込まれます（使用可能な場合）。

![製品のバリエーション](../assets/catalog-product-variation.png)

>[!NOTE]
>
>AEM の製品カタログデータは、設定されたコマースエンドポイントを介してリアルタイムに取得されるデータです。製品カタログデータはAEMに保存されません。

## 製品カタログの検索 {#searching-product-catalog}

製品カタログ全体に対する全文検索が左側のフィルタータブで使用でき、製品をすばやく検索できます。

![検索](../assets/search-cockpit.png)

## ステージングされた製品カタログの参照 {#staged-product-catalogs}

デフォルトでは、製品コックピットには、ライブの製品カタログデータが表示されます。左のフィルタータブの「STAGED CATALOG」を使用すると、選択した日付の商品カタログが読み込まれます。

![ステージングされたカタログ](../assets/staged-cockpit.png)

## 製品カタログのプロパティ {#catalog-properties}

製品またはカテゴリのプロパティアイコンをクリックすると、選択したオブジェクトのプロパティビューが開きます。 製品バリアントの開くプロパティは、メインの製品プロパティを開くことと同じです。

### 「コマース」タブ {#tabs}

「一般」タブと「バリアント」タブには、コマースバックエンドから取得された事前定義済みのコマースプロパティが表示されます。このデータ（バリアントなど）は AEM の読み取り専用データです。レコードのシステムがコマースバックエンドであるためです。バリアントを含む製品の場合にのみ「バリアント」タブが表示され、すべてのバリアントのリストが表示されます。

![カタログのプロパティ](../assets/catalog-properties.png)

### 「AEM コンテンツ」タブ {#content-tabs}

これらのタブは AEM コンテンツタイプ（エクスペリエンスフラグメント、コンテンツフラグメント、関連アセット）別にグループ化され、コマースオブジェクトに関連付けられた AEM コンテンツを表示します。「詳細を表示」アクションを実行すると、選択したコンテンツを含む新しいブラウザータブが開きます。

![コンテンツのプロパティ](../assets/content-properties.png)
