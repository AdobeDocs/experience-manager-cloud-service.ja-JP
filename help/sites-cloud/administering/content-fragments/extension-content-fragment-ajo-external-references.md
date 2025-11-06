---
title: コンテンツフラグメント AJO 外部参照拡張機能の使用
description: コンテンツフラグメント AJO 外部参照拡張機能について説明します
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: 79c90e6b-91da-4f5a-ac96-a98ef7f8d4cd
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 100%

---

# コンテンツフラグメント AJO 外部参照拡張機能 {#content-fragment-external-references-extension}

AEM のエクスペリエンスを別のアドビ製品でプレビューするには、次の UI 拡張機能を有効にします。

* **AJO 外部参照**

AJO 外部参照拡張機能は、事前定義済みのタグに関連付けられたすべての組織とサンドボックスからコンテンツフラグメントへの参照を取得することで機能します。 その後、拡張機能は詳細を表示します。

例えば、Adobe Journey Optimizer（AJO）との統合の場合、詳細は、参照がキャンペーン、ジャーニー、テンプレートのいずれであるかによって異なります。

>[!NOTE]
>
>拡張機能を有効にする方法について詳しくは、[AEM Experience Manager の Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/) を参照してください。

例えば、AJO で拡張機能を使用するには：

>[!NOTE]
>
>[AJO 統合](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/integrations/aem-fragments)も参照してください。

1. [コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)を開きます。

1. コンテンツフラグメント（様々な AJO チャネルで作成および使用されたフラグメント）に移動します。

1. [エディター](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment)でコンテンツフラグメントを開きます。

1. AJO 外部参照拡張機能は、右側のパネルのタブとして使用できます。タブを選択して、拡張機能を開きます。

   ![AJO 外部参照拡張機能](/help/sites-cloud/administering/content-fragments/assets/cf-ajo-fragment-external-references-extension.png)

   参照タイプを選択すると、拡張機能により、対応する外部参照が次の列を持つテーブルとして表示されます。

   * **名前**：コンテンツフラグメントが使用されている参照の名前
   * **プレビュー**：このリンクを選択して、プレビューを開始します
   * **ステータス**：参照のステータス

1. ドロップダウンから&#x200B;**参照タイプ**&#x200B;を選択して、次の 3 つの参照タイプを切り替えることができます。

   * **キャンペーン**
      * 現在のコンテンツフラグメントへのリンクを含むすべてのキャンペーンのリストを表示します。
      * その後、選択したキャンペーンをプレビューできます。
      * デフォルト
   * **ジャーニー**
      * 最新のジャーニーを表示します。
      * その後、選択したジャーニーを選択およびプレビューできます。
   * **テンプレート**
      * コンテンツフラグメントに関連するテンプレートを表示します。
      * その後、選択したテンプレートを選択およびプレビューできます。
