---
title: コンテンツフラグメントのAJO外部参照拡張機能の使用
description: コンテンツフラグメントAJO外部参照拡張機能について説明します
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: f755a5c621b68b3110642e6cfe150798555b6707
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---


# コンテンツフラグメントのAJO外部参照拡張機能 {#content-fragment-external-references-extension}

別のAdobe製品でAEMのエクスペリエンスをプレビューするには、次の手順で UI 拡張機能を有効にします。

* **AJO外部参照**

AJOの外部参照拡張機能は、事前定義済みのタグに関連付けられたすべての組織とサンドボックスからコンテンツフラグメントへの参照を取得することで機能します。 拡張機能に詳細が表示されます。

例えば、Adobe Journey Optimizer（AJO）との統合の場合、詳細は、参照がキャンペーン、ジャーニー、テンプレートのどれであるかによって異なります。

>[!NOTE]
>
>拡張機能を有効にする方法について詳しくは、[AEM Experience ManagerのExtension Managerを参照してください ](https://developer.adobe.com/uix/docs/extension-manager/)。

例えば、AJOで拡張機能を使用するには、次のように指定します。

>[!NOTE]
>
>[AJO統合 ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/integrations/aem-fragments) も参照してください。

1. [ コンテンツフラグメントコンソール ](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console) を開きます。

1. コンテンツフラグメント （様々なAJO チャネルで作成および使用されたフラグメント）に移動します。

1. [ エディター ](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment) でコンテンツフラグメントを開きます。

1. AJO外部参照拡張機能は、右側のパネルのタブとして使用できます。 タブを選択して、拡張機能を開きます。

   ![AJO外部参照拡張機能 ](/help/sites-cloud/administering/content-fragments/assets/cf-ajo-fragment-external-references-extension.png)

   参照タイプを選択すると、対応する外部参照が列を持つテーブルとして表示されます。

   * **名前**：コンテンツフラグメントが使用されている参照の名前
   * **プレビュー** このリンクを選択してプレビューを開始します
   * **ステータス**：参照のステータス

1. ドロップダウンから **参照タイプ** を選択して、次の 3 つの参照タイプを切り替えることができます。

   * **キャンペーン**
      * 現在のコンテンツフラグメントへのリンクを含むすべてのキャンペーンのリストを表示します。
      * その後、選択したキャンペーンをプレビューできます。
      * デフォルト
   * **ジャーニー**
      * 最新のジャーニーが表示されます。
      * その後、選択したジャーニーを選択およびプレビューできます。
   * **テンプレート**
      * コンテンツフラグメントに関連するテンプレートを表示します。
      * その後、選択したテンプレートを選択およびプレビューできます。