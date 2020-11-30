---
title: コンポーネントの概要
description: コンポーネントは、特定の機能を実現し、Web サイトにコンテンツを提供するためのモジュールユニットです。
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 100%

---


# コンポーネントの概要 {#components-overview}

このページでは、[ページオーサリングで使用される](/help/sites-cloud/authoring/fundamentals/components.md)コンポーネントなど、Adobe Experience Manager（AEM）のコンポーネントの概要を示します。

## コンポーネントとは{#what-are-components}

AEM のコンポーネント：

* 特定の機能を実現し、Web サイトにコンテンツを提供するためのモジュールユニットです。
* 再利用可能です。
* リポジトリーの 1 つのフォルダー内の自己完結型ユニットとして開発されます。
* 非表示の設定ファイルを持ちません。
* 他のコンポーネントを組み込むことができます。
* AEM システム内ならどこでも実行でき、また、特定のコンポーネントで実行できるように制限することもできます。
* 標準化されたユーザーインターフェイスがあります。
* 設定可能な編集動作があります。
* Granite UI コンポーネントに基づくサブ要素を使用して構築されたダイアログボックスを使用します。
* [HTL](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/overview.html) を使用して開発されています。
* デフォルトの機能を拡張するカスタマイズされたコンポーネントを作成するために開発できます。

コンポーネントはモジュールなので、次のことができます。

* ローカルインスタンスで新しいコンポーネントを開発する。
* テスト環境にデプロイします。
* ライブオーサリング環境にデプロイし、そこで、作成者や管理者のコンテンツの追加および設定を許可します。
* ライブパブリッシュ環境にデプロイします。Web サイトへの訪問者用にコンテンツをレンダリングするために使用します。

各 AEM コンポーネント：

* リソースタイプです。
* 特定の機能を完全に実現するスクリプトのコレクションです。
* 単独で（AEM 内またはポータル内で）機能できます。

## AEM コアコンポーネント {#aem-core-components}

[AEM コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)は、AEM で Web サイトの開発時間を短縮しメンテナンスコストを削減するための、標準化された Web コンテンツ管理（WCM）コンポーネントのセットです。

コアコンポーネントは、Cloud Service として AEM と共に提供され、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)では、コンポーネントの実装方法と使用方法を説明します。コンポーネントは、すべてのソースコードと共に提供されており、そのまま使用することも、コンポーネントを変更または拡張する出発点として使用することもできます。

### 利用可能なコンポーネントの表示 {#viewing-available-components}

AEM インスタンスで利用可能なすべてのコンポーネントの概要を確認するには、[コンポーネントコンソール](/help/sites-cloud/authoring/features/components-console.md)を使用します。

または、CRXDE Lite を使用して、リポジトリで利用可能なすべてのコンポーネントのリストを取得することもできます。

1. **[!UICONTROL CRXDE Lite]** で、ツールバーから「**[!UICONTROL ツール]**」を選択し、「**[!UICONTROL クエリ]**」を選択して、「**[!UICONTROL クエリ]**」タブを開きます。

1. 「**[!UICONTROL クエリ]**」タブで、「**[!UICONTROL タイプ]**」として「`XPath`」を選択します。

1. 「**[!UICONTROL クエリ]**」入力フィールドに次の文字列を入力します。

   `//element(*, cq:Component)`

1. 「**[!UICONTROL 実行]**」をクリックするとコンポーネントがリストされます。

