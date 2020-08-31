---
title: コンポーネント 概要
description: コンポーネントは、特定の機能を実現し、Web サイトにコンテンツを提供するためのモジュールユニットです。
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 50%

---


# コンポーネントの概要 {#components-overview}

このページでは、[ページオーサリングで使用される](/help/sites-cloud/authoring/fundamentals/components.md)コンポーネントなど、Adobe Experience Manager（AEM）のコンポーネントの概要を示します。

## コンポーネントとは{#what-are-components}

AEMのコンポーネントは次のとおりです。

* Webサイトにコンテンツを表示するための特定の機能を実現するモジュラー型ユニット。
* 再利用可能。
* リポジトリの1つのフォルダー内に自己完結型のユニットとして開発。
* 非表示の設定ファイルを持ちません。
* 他のコンポーネントを組み込むことができます。
* どのAEMシステムでもどこでも実行でき、また、特定のコンポーネントで実行できるように制限することもできます。
* 標準化されたユーザーインターフェイスがあります。
* 設定可能な編集動作がある。
* Granite UIコンポーネントに基づくサブ要素を使用して構築されたダイアログボックスを使用します。
* HTLを使用して開発され [ます](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/overview.html)。
* デフォルトの機能を拡張するカスタマイズされたコンポーネントを作成するために開発できます。

コンポーネントはモジュールなので、次のことができます。

* ローカルインスタンスで新しいコンポーネントを開発する。
* テスト環境に展開します。
* ライブオーサリング環境にデプロイする。そこで、作成者や管理者のコンテンツの追加および設定を許可します。
* ライブパブリッシュ環境にデプロイします。この画像を使用して、Webサイトの訪問者向けにコンテンツをレンダリングします。

各 AEM コンポーネント：

* リソースタイプです。
* 特定の機能を完全に実現するスクリプトの集まりです。
* AEM内またはポータル内で、単独で機能します。

## AEM コアコンポーネント {#aem-core-components}

[AEMコアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html) は、Webサイトの開発時間を短縮し、メンテナンスコストを削減するための、AEM用の標準化されたWebコンテンツ管理(WCM)コンポーネントのセットです。

コアコンポーネントは、Cloud ServiceとしてAEMと共に提供され、 [WKNDチュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md) では、コンポーネントの実装方法と使用方法を説明します。 コンポーネントは、すべてのソースコードと共に提供されており、そのまま使用することも、コンポーネントを変更または拡張する出発点として使用することもできます。

### 利用可能なコンポーネントの表示 {#viewing-available-components}

AEM インスタンスで利用可能なすべてのコンポーネントの概要を確認するには、[コンポーネントコンソール](/help/sites-cloud/authoring/features/components-console.md)を使用します。

または、CRXDE Lite を使用して、リポジトリで利用可能なすべてのコンポーネントのリストを取得することもできます。

1. In **[!UICONTROL CRXDE Lite]**, select **[!UICONTROL Tools]** from the toolbar, then **[!UICONTROL Query]**, which opens the **[!UICONTROL Query]** tab.

1. 「**[!UICONTROL クエリー]**」タブで、「`XPath`タイプ&#x200B;**[!UICONTROL 」として「]**」を選択します。

1. **[!UICONTROL クエリ]**&#x200B;入力フィールドに次の文字列を入力します。

   `//element(*, cq:Component)`

1. Click **[!UICONTROL Execute]** and the components are listed.

