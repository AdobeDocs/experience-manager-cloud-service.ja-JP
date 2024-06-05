---
title: レスポンシブデザイン
description: レスポンシブデザインを使用すると、同じエクスペリエンスを複数のデバイスで、複数の向きで効果的に表示できます。
exl-id: be645062-d6d6-45a2-97dc-d8aa235539b8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 100%

---

# レスポンシブデザイン {#responsive-design}

エクスペリエンスが表示されるクライアントの表示域に適応するようにエクスペリエンスをデザインします。レスポンシブデザインを使用すると、同じページを複数のデバイスで、縦、横の両方の向きで効果的に表示できます。以下の画像は、ビューポートサイズの変更に対するページの応答方法の例を示しています。

* レイアウト：ビューポートが小さい場合は 1 列レイアウトを使用し、ビューポートが大きい場合は複数列レイアウトを使用します。
* テキストサイズ：ビューポートが大きい場合は、（見出しなどの適切な箇所で）大きいテキストサイズを使用します。
* コンテンツ：小型デバイスに表示する場合は、重要なコンテンツのみを表示します。
* ナビゲーション：他のページにアクセスするためのデバイス専用のツールを提供します。
* 画像：ウィンドウのサイズに応じて、クライアントの表示域に適した画像レンディションを提供します

![レスポンシブデザインの例](assets/responsive-example.png)

複数のウィンドウサイズと向きに適応可能な HTML5 を生成する Adobe Experience Manager（AEM）アプリケーションを開発します。例えば、次のようなビューポートの幅の範囲が、様々なデバイスタイプと向きに対応します。

* 幅 480 ピクセル以下（スマートフォン、縦置き）
* 幅 767 ピクセル以下（スマートフォン、横置き）
* 幅 768～979 ピクセル（タブレット、縦置き）
* 幅 980 ～ 1,199 ピクセル（タブレット、横置き）
* 幅 1,200 ピクセル以上（デスクトップ）

レスポンシブデザインの動作の実装について詳しくは、次のトピックを参照してください。

* [メディアクエリ](#using-media-queries)
* [可変グリッド](#developing-a-fluid-grid)
* [アダプティブ画像](#using-adaptive-images)

デザインの際には、**エミュレーター**&#x200B;を使用してページを様々な画面サイズでプレビューします。

## 開発の前に {#before-you-develop}

Web ページをサポートする AEM アプリケーションを開発する前に、デザインについていくつかの決定を行う必要があります。例えば、次の情報が必要になります。

* ターゲットとするデバイス
* ターゲットの表示域サイズ
* ターゲットの表示域サイズごとのページレイアウト

### アプリケーション構造 {#application-structure}

次のような一般的な AEM アプリケーション構造により、すべてのレスポンシブデザイン実装をサポートできます。

* ページコンポーネントは `/apps/<application_name>/components` の下にあります。
* テンプレートは `/apps/<application_name>/templates` の下にあります。

## メディアクエリの使用 {#using-media-queries}

メディアクエリによって、ページレンダリング用の CSS スタイルを選択的に使用できます。AEM 開発ツールおよび機能を使用すれば、アプリケーションでメディアクエリを効果的かつ効率的に実装できます。

W3C グループが、この CSS3 機能と構文について示した、[メディアクエリ](https://www.w3.org/TR/css3-mediaqueries/)に関するレコメンデーションを提供しています。

### CSS ファイルの作成 {#creating-the-css-file}

CSS ファイルでは、ターゲットとしているデバイスのプロパティに基づいてメディアクエリを定義します。次の実装方法は、各メディアクエリのスタイルを管理するのに効果的です。

* [クライアントライブラリフォルダー](clientlibs.md)を使用して、ページのレンダリング時に組み立てられる CSS を定義します。
* 各メディアクエリおよび関連するスタイルを、それぞれ個別の CSS ファイルで定義します。メディアクエリのデバイスの特徴を表したファイル名を使用すると便利です。
* すべてのデバイスに共通するスタイルを、個別の 1 つの CSS ファイルで定義します。
* クライアントライブラリフォルダーの css.txt ファイルで、組み立てられた CSS ファイル内で必要とされる順に CSS ファイルを並べます。

[WKND チュートリアル](develop-wknd-tutorial.md)ではこの実装方法を使用して、サイトデザインのスタイルを定義しています。WKND で使用される CSS ファイルは、`/apps/wknd/clientlibs/clientlib-grid/less/grid.less` にあります。

### AEM ページでのメディアクエリの使用 {#using-media-queries-with-aem-pages}

[WKND サンプルプロジェクト](/help/implementing/developing/introduction/develop-wknd-tutorial.md)と [AEM Project アーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)は、ページポリシーを介した clientlibs を含む[ページコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/page.html?lang=ja)を使用します。

独自のページコンポーネントがページコアコンポーネントに基づいていない場合は、クライアントライブラリフォルダーをその HTL または JSP スクリプトに含めることもできます。これにより、レスポンシブグリッドが機能するために必要なメディアクエリを含む CSS ファイルが生成され、参照されます。

#### HTL {#htl}

```html
<sly data-sly-use.clientlib="${'/libs/granite/sightly/templates/clientlib.html'}">
<sly data-sly-call="${clientlib.all @ categories='apps.weretail.all'}"/>
```

#### JSP {#jsp}

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

この JSP スクリプトにより、スタイルシートを参照する以下の HTML コードが生成されます。

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## 特定のデバイスのプレビュー {#previewing-for-specific-devices}

エミュレーターを起動すると、異なるビューポートサイズでページをプレビューできるようになり、レスポンシブデザインの動作をテストできます。サイトコンソールでページを編集する際に、**エミュレーター**&#x200B;アイコンをクリックしてエミュレーターを表示します。

![ツールバーのエミュレーターアイコン](assets/emulator-icon.png)

エミュレーターツールバーで、**デバイス**&#x200B;アイコンをクリックすると、デバイスを選択できるドロップダウンメニューが表示されます。デバイスを選択すると、その表示域サイズに合わせてページが変更されます。

![エミュレーターツールバー](assets/emulator.png)

### デバイスグループの指定 {#specifying-device-groups}

**デバイス**&#x200B;リストに表示されるデバイスグループを指定するには、`cq:deviceGroups` プロパティをサイトのテンプレートページの `jcr:content` ノードに追加します。プロパティの値は、デバイスグループノードへのパスの配列です。

例えば、WKND サイトのテンプレートページは `/conf/wknd/settings/wcm/template-types/empty-page/structure` です。また、その下の `jcr:content` ノードには次のプロパティが含まれています。

* 名前：`cq:deviceGroups`
* タイプ：`String[]`
* 値：`mobile/groups/responsive`

デバイスグループノードは `/etc/mobile/groups` フォルダー内にあります。

## レスポンシブ画像 {#responsive-images}

レスポンシブページは、レンダリングされるデバイスに動的に適応するため、ユーザーのエクスペリエンスが向上します。ただし、ページ読み込み時間を最小限に抑えるために、アセットをブレークポイントとデバイスに最適化することも重要です。

[コアコンポーネントの画像コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=ja)には、アダプティブ画像選択などの機能があります。

* デフォルトで画像コンポーネントは、[アダプティブ画像サーブレット](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/adaptive-image-servlet.html?lang=ja)を使用して、適切なレンディションを配信します。
* [Web に最適化された画像配信](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html?lang=ja)は、DAM から WebP 形式で画像アセットを配信し、画像のダウンロードサイズを平均で約 25%削減できる、シンプルなチェックボックスをポリシーで選択しても利用できます。

## レイアウトコンテナ {#layout-container}

AEM レイアウトコンテナを使用すると、レスポンシブレイアウトを効率的かつ効果的に実装して、ページのサイズをクライアントビューポートに適応させることができます。

レイアウトコンテナの仕組みと、コンテンツに対してレスポンシブレイアウトを有効にする方法について詳しくは、[レイアウトコンテナとレイアウトモードの設定](/help/sites-cloud/administering/responsive-layout.md)のドキュメントをご覧ください。
