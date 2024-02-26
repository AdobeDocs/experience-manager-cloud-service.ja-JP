---
title: コンポーネントの概要
description: コンポーネントは、特定の機能を実現し、Web サイトにコンテンツを提供するためのモジュールユニットです。
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 56%

---

# コンポーネントの概要 {#components-overview}

このページでは、[ページオーサリングで使用される](/help/sites-cloud/authoring/page-editor/components.md)コンポーネントなど、Adobe Experience Manager（AEM）のコンポーネントの概要を示します。

## コンポーネントとは {#what-are-components}

* 特定の機能を実現し、Web サイトにコンテンツを提供するためのモジュールユニットです。
* 再利用可能。
* リポジトリーの 1 つのフォルダー内の自己完結型ユニットとして開発されます。
* 非表示の設定ファイルはありません。
* 他のコンポーネントを含めることができます。
* AEMシステム内の任意の場所で実行でき、特定のコンポーネントでの実行に制限することもできます。
* 標準化されたユーザーインターフェイスがあります。
* 設定可能な編集動作があります。
* Granite UI コンポーネントに基づくサブ要素を使用して構築されたダイアログボックスを使用します。
* これらはを使用して開発されています。 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja).
* デフォルトの機能を拡張するカスタマイズされたコンポーネントを作成するために開発できます。

コンポーネントはモジュラーなので、次のことが可能です。

* ローカルインスタンス上で新しいコンポーネントを開発します。
* テスト環境にデプロイします。
* ライブオーサリング環境にデプロイし、そこで、作成者や管理者のコンテンツの追加および設定を許可します。
* ライブパブリッシュ環境にデプロイします。Web サイトへの訪問者用にコンテンツをレンダリングするために使用します。

各 AEM コンポーネント：

* リソースタイプです。
* 特定の機能を完全に実現するスクリプトのコレクションです。
* 単独で（AEM 内またはポータル内で）機能できます。

## AEM コアコンポーネント {#aem-core-components}

[AEMコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) は、AEMの開発時間を短縮し、Web サイトのメンテナンスコストを削減するための、標準化された Web コンテンツ管理 (WCM) コンポーネントのセットです。

コアコンポーネントは、Cloud Service として AEM と共に提供され、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)では、コンポーネントの実装方法と使用方法を説明します。コンポーネントは、すべてのソースコードと共に提供されており、そのまま使用することも、コンポーネントを変更または拡張する出発点として使用することもできます。

### 利用可能なコンポーネントの表示 {#viewing-available-components}

AEMインスタンスで使用可能なすべてのコンポーネントの概要については、 [コンポーネントコンソール](/help/sites-cloud/authoring/components-console.md).

または、CRXDE Liteを使用して、リポジトリで使用可能なすべてのコンポーネントのリストを取得することもできます。

1. **[!UICONTROL CRXDE Lite]** で、ツールバーから「**[!UICONTROL ツール]**」を選択し、「**[!UICONTROL クエリ]**」を選択して、「**[!UICONTROL クエリ]**」タブを開きます。

1. 「**[!UICONTROL クエリ]**」タブで、「**[!UICONTROL タイプ]**」として「`XPath`」を選択します。

1. Adobe Analytics の **[!UICONTROL クエリ]** 入力フィールドに、次の文字列を入力します。

   `//element(*, cq:Component)`

1. 「**[!UICONTROL 実行]**」をクリックするとコンポーネントがリストされます。
