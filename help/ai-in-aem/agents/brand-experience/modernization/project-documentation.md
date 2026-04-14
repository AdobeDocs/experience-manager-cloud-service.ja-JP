---
title: プロジェクト文書作成スキル
description: Experience Modernization Agentのドキュメントスキルが、プロジェクトの引き継ぎを加速させるのにどのように役立つかをご覧ください。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 90fb75c7febc8a8138e13a2f3ff872f38eeb3baa
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# プロジェクト文書作成スキル {#project-documentation}

Experience Modernization Agentのドキュメントスキルが、プロジェクトの引き継ぎを加速させるのにどのように役立つかをご覧ください。

## プロジェクトの引き継ぎを加速 {#project-handovers}

[Experience Modernization Agent](/help/ai-in-aem/agents/brand-experience/modernization/overview.md)は、次の機能を備えたAEM Edge Delivery Services プロジェクトのプロジェクトドキュメントガイドを自動的に生成できます。

* **プロジェクトのチュートリアル** - プロジェクトの設定、構造、規則に関する説明を手作業なしで生成
* **モジュールとコンポーネントの整理** - ブロック、モジュール、コンポーネントの構成方法と相互の関係を明確に文書化します
* **役割ベースのガイド** – 作成者、開発者、管理者向けのドキュメントをターゲットにして、各チームメンバーが必要なものを正確に入手できるようにします

これにより、AEM Edge Delivery Services プロジェクトのプロジェクトの引き継ぎが簡単になります。

## 前提条件 {#prerequisites}

このスキルを使用する前に、次の点を確認してください。

* プロジェクトをコンソールのワークスペースにチェックアウトする必要があります。
* ドキュメントを作成するプロジェクトの管理者権限が必要です。
* エージェントの権限は、コンソールで許可する必要があります。
   * 「**LLMがコンソールの設定で** [に代わってadmin.hlx.pageにアクセスすることを許可する」オプションを選択します。](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)
   * このオプションが有効になっていない場合、担当者はアクセス可能なコードベースに基づいてドキュメントを生成します。

## プロジェクトドキュメントの作成 {#creating-documentation}

前提条件が満たされたら、担当者にプロジェクトのドキュメントの作成を依頼するだけです。

1. チャットで「このプロジェクトのドキュメントを作成する」と尋ねます。
1. エージェントからプロジェクトの組織名が要求された場合に指定します。
1. 作成するドキュメントを担当者が確認します。 通常は、**すべて**&#x200B;を選択します。

   ![&#x200B; ドキュメントを作成](assets/select-documentation.png)

1. 作成したガイドは、ワークスペースに配置されます。 1つを選択して説明を表示し、リンクをクリックしてPDF全体をダウンロードします。

   ![&#x200B; ドキュメントが作成されました](assets/documentation-created.png)

PDFを直接保存してチームに提供したり、DA コンテンツの一部としてアップロードしたりできます。

![管理者ガイド &#x200B;](assets/admin-guide.png)

>[!NOTE]
>
>Edge Delivery Services管理APIにアクセスする権限がない場合、またはコンソールの設定で&#x200B;**&#x200B;**&#x200B;代わりに[LLMにadmin.hlx.pageへのアクセスを許可するオプション の場合。](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)は有効になっていません。エージェントは、アクセス可能なコードベースに基づいてドキュメントを生成します。

## トラブルシューティング {#troubleshooting}

次に、プロジェクトドキュメントのスキルを使用する際に発生する一般的なエラーメッセージとその解決方法を示します。

### 「アクセスが拒否されました」または「許可されていません」 {#unauthorized}

* **原因：**&#x200B;管理者権限がないか、エージェント権限が有効になっていません
* **解決策：**
   1. プロジェクトへの管理者アクセス権があることを確認します
   1. 「**LLMがコンソールの設定で** [に代わってadmin.hlx.pageにアクセスすることを許可する」オプションを選択します。](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)

### 「プロジェクトが見つかりません」 {#not-found}

* **原因：** リポジトリがワークスペースでチェックアウトされていません
* **解決策：**
   1. プロジェクトリポジトリを確認する
   1. 作業空間が正しいことを確認する

### 「Config API エラー」 {#api-error}

* **原因：** Edge Delivery Services設定サービス APIにアクセスできません
* **解決策：**
   1. 「**LLMがコンソールの設定で** [に代わってadmin.hlx.pageにアクセスすることを許可する」オプションを選択します。](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)
   1. ネットワーク/VPN接続を確認する
   1. プロジェクトへの管理者アクセスを確認
