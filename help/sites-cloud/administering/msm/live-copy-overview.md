---
title: ライブコピーの概要コンソール
description: ライブコピーの概要コンソールの基本事項について説明し、コンテンツを同期するためのライブコピーの状態をすばやく把握します。
feature: Multi Site Manager
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 19%

---


# ライブコピーの概要コンソール {#live-copy-overview-console}

**ライブコピーの概要**&#x200B;コンソールを使用すると、次のことができます。

* サイト全体での継承の表示/管理。
   * ブループリントツリーと対応するライブコピー構造と、その継承ステータスの表示
   * 休止や再開などの継承ステータスの変更
   * 表示ブループリントとライブコピーのプロパティ
* ロールアウトアクションの実行.

## ライブコピーの概要を開く {#opening-the-live-copy-overview}

ライブコピーの概要は、以下から開くことができます。

* [ブループリントページの参照サイドパネル（サイトコンソール）](#opening-live-copy-overview-references-for-a-blueprint-page)
* [ブループリントページのプロパティ](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Blueprintページへの参照{#references-to-a-blueprint-page}

**ライブコピーの概要**&#x200B;は、**サイト**&#x200B;コンソールの&#x200B;**参照**&#x200B;サイドパネルから開くことができます。

1. **サイト**&#x200B;コンソールで、[設計図のページに移動して選択します。](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. **[参照](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**&#x200B;レールを開き、**ライブコピー**&#x200B;を選択します。

   ![参照レールからのライブコピー](../assets/live-copy-references.png)

   >[!TIP]
   >
   >まず参照を開き、次に設計図を選択することもできます。

1. **ライブコピーの概要**&#x200B;を選択して、選択したブループリントに関連するすべてのライブコピーの概要を表示し、使用します。
1. 「**閉じる**」を使用して終了し、**サイト**&#x200B;コンソールに戻ります。

### Blueprintページのプロパティ{#properties-of-a-blueprint-page}

**ライブコピーの概要**&#x200B;は、ブループリントページのプロパティを表示しているときに開くことができます。

1. 該当するブループリントページの&#x200B;**プロパティ**&#x200B;を開きます。
1. 「**ブループリント**」タブを開きます。「**ライブコピーの概要**」オプションが上部のツールバーに表示されます。

   ![「Blueprintプロパティ」タブ](../assets/live-copy-blueprint-tab.png)

1. **ライブコピーの概要**&#x200B;を選択して、現在のブループリントに関連するすべてのライブコピーの概要を表示し、使用します。

1. 「**閉じる**」を使用して終了し、**サイト**&#x200B;コンソールに戻ります。

## ライブコピーの概要の使用  {#using-the-live-copy-overview}

**ライブコピーの概要**&#x200B;ウィンドウには、選択したページに関連するライブコピーのステータスと概要が表示されます。

![ライブコピーの概要ウィンドウ](../assets/live-copy-overview.png)

ロールアウトは、特定のロールアウト設定で定義された同期アクションに依存します。 一部のアクションは、コンテンツの変更に依存します。 ただし、コンテンツの変更に依存しないが、ページのアクティベーションなどのイベントに依存するアクションは多数あります。 このようなイベントでは、コンテンツは変更されませんが、コンテンツに関連する内部プロパティは変更されます。

ステータスフィールドも、特定のロールアウト設定で定義された同期アクションに依存し、最後に成功したロールアウト以降に設計図またはライブコピーに対するそのようなアクションが存在するかどうかを示します。 ステータスフィールドには、特定のロールアウト設定内のアクションのみが反映されます。 ライブコピーでロールアウトが成功しなかった場合は、ステータスは常に最新です。

例えば、ロールアウト設定は`targetActivate`と定義されます。 したがって、ロールアウトはアクティベーションのイベントにのみ依存します。 ステータスフィールドは、最後に成功したロールアウト以降にアクティベーションイベントが発生したかどうかを示すだけです。

**ライブコピーの概要**&#x200B;は、ライブコピーに対するアクションの実行にも使用できます。

1. **ライブコピーの概要**&#x200B;を開きます。
1. 必要なBluePrintページまたはLive Copyページを選択すると、ツールバーが更新され、使用可能なアクションが表示されます。 使用できる[アクション](overview.md#terms-used)は、[blueprint](#actions-for-a-blueprint-page)と[ライブコピー](#actions-for-a-live-copy-page)のどちらのページを選択するかによって異なります。

### ブループリントページのアクション {#actions-for-a-blueprint-page}

ブループリントページを選択した場合は、以下のアクションを使用できます。

![Live Copyの概要アクション（青写真用）](../assets/live-copy-overview-actions-blueprint.png)

* **編集**  — ブループリントページを開いて編集します。
* **[ロールアウト](overview.md#rollout-and-synchronize)**  — ロールアウトを実行して、ソースからライブコピーに変更をプッシュします。

### ライブコピーページのアクション {#actions-for-a-live-copy-page}

ライブコピーページを選択した場合は、次の操作を実行できます。

![ライブコピーのライブコピーの概要アクション](../assets/live-copy-overview-actions.png)

* **編集**  — ライブコピーページを開いて編集します。
* **[「Relationship Status](#relationship-status)** 」：ステータスと継承に関する表示情報。
* **[同期](overview.md#rollout-and-synchronize)**  — ライブコピーを同期して、ソースからライブコピーに変更を引き出します。
* **[Reset](creating-live-copies.md#resetting-a-live-copy-page)**  — ライブコピーページをリセットして、すべての継承キャンセルを削除し、ページをソースページと同じ状態に戻します。
* **[休止](overview.md#suspending-and-cancelling-inheritance-and-synchronization)**  — ライブコピーとその設計図ページの間のライブ関係を一時的に非アクティブにします。
* **[再開](creating-live-copies.md#resuming-inheritance-for-a-page)**  — 再開：休止した関係を復元できます。
* **[Detach](overview.md#detaching-a-live-copy)**  — ライブコピーとそのブループリントページの間のライブ関係を完全に削除します。

## 関係ステータス {#relationship-status}

**リレーションシップステータス**&#x200B;コンソールには、2つのタブがあり、様々な機能を提供します。

* [関係ステータス](#relationship-status-tab)
* [ライブコピー](#live-copy-tab)

### 関係ステータス {#relationship-status-tab}

このタブには、BlueprintとLive Copyの間の関係の状態に関する詳細情報が表示されます。

![「Relationship Status」タブ](../assets/live-copy-relationship-status.png)

### ライブコピー {#live-copy-tab}

このタブでは、ライブコピーの設定を表示および編集できます。

![「Live Copy」タブ](../assets/live-copy-relationship-status-live-copy.png)
