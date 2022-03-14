---
title: AEMでの GraphiQL IDE の使用
description: Adobe Experience Managerでの GraphiQL IDE の使用方法を説明します。
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 24%

---

# GraphiQL IDE の使用 {#graphiql-ide}

標準の実装 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE はAEM GraphQL で使用できます。 これは [AEM と共にインストール](#installing-graphiql-ide)できます。

>[!NOTE]
>
>GraphiQL はグローバルエンドポイントにバインドされます（特定の Sites 設定の他のエンドポイントでは機能しません）。

GraphiQL ツールを使用すると、クエリを直接入力、テスト、デバッグできます。 また、GraphiQL はドキュメントに簡単にアクセスでき、使用可能なメソッドを簡単に学習し、理解できます。

例えば、次のようなものです。

* `http://localhost:4502/content/graphiql.html`

構文のハイライト表示機能、オートコンプリート、自動候補表示などの機能と共に、履歴およびオンラインドキュメントが提供されています。

![GraphiQL インターフェイス](assets/cfm-graphiql-interface.png "GraphiQL インターフェイス")

## AEM GraphiQL IDE のインストール {#installing-graphiql-ide}

GraphiQL IDE は開発ツールで、開発インスタンスやローカルインスタンスなどの下位レベルの環境でのみ必要です。 したがって、AEMプロジェクトには含まれず、アドホックベースでインストールできる個別のパッケージとして提供されます。

1. 次に移動： **[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)** > **AEMas a Cloud Service**.
1. 「GraphiQL」を検索します ( 必ず **i** in **GraphiQL**.
1. 最新の **GraphiQL コンテンツパッケージ v.x.x.x**
1. 次の **AEM Start** メニュー移動先 **ツール** > **導入** > **パッケージ**.
1. クリック **パッケージをアップロード** 前の手順でダウンロードしたパッケージを選択します。 クリック **インストール** をクリックしてパッケージをインストールします。
