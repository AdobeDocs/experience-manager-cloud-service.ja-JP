---
title: ライブコピーの概要コンソール
description: ライブコピーの概要コンソールの基本について説明し、コンテンツを同期するためにライブコピーのステータスをすばやく把握します。
feature: マルチサイトマネージャー
role: Administrator
exl-id: 3ef7fbce-10a1-4b21-8486-d3c3706e537c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 19%

---

# ライブコピーの概要コンソール {#live-copy-overview-console}

**ライブコピーの概要**&#x200B;コンソールを使用すると、次のことが可能になります。

* サイト全体の継承を表示/管理します。
   * ブループリントツリーと対応するライブコピー構造を、継承ステータスと共に表示します。
   * 休止や再開などの継承ステータスの変更
   * ブループリントおよびライブコピーのプロパティの表示
* ロールアウトアクションの実行.

## ライブコピーの概要を開く {#opening-the-live-copy-overview}

ライブコピーの概要は、以下から開くことができます。

* [ブループリントページの参照サイドパネル（サイトコンソール）](#opening-live-copy-overview-references-for-a-blueprint-page)
* [ブループリントページのプロパティ](#opening-live-copy-overview-properties-of-a-blueprint-page)

### ブループリントページへの参照{#references-to-a-blueprint-page}

**ライブコピーの概要**&#x200B;は、**サイト**&#x200B;コンソールの&#x200B;**参照**&#x200B;サイドパネルから開くことができます。

1. **サイト**&#x200B;コンソールで、[ブループリントページに移動して選択します。](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. **[参照](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**&#x200B;レールを開き、「**ライブコピー**」を選択します。

   ![参照レールのライブコピー](../assets/live-copy-references.png)

   >[!TIP]
   >
   >参照を最初に開いてから、ブループリントを選択することもできます。

1. **ライブコピーの概要**&#x200B;を選択して、選択したブループリントに関連するすべてのライブコピーの概要を表示および使用します。
1. 「**閉じる**」を使用して終了し、**サイト**&#x200B;コンソールに戻ります。

### ブループリントページのプロパティ{#properties-of-a-blueprint-page}

**ライブコピーの概要**&#x200B;は、ブループリントページのプロパティを表示しているときに開くことができます。

1. 該当するブループリントページの&#x200B;**プロパティ**&#x200B;を開きます。
1. 「**ブループリント**」タブを開きます。「**ライブコピーの概要**」オプションが上部のツールバーに表示されます。

   ![「ブループリントのプロパティ」タブ](../assets/live-copy-blueprint-tab.png)

1. **ライブコピーの概要**&#x200B;を選択して、現在のブループリントに関連するすべてのライブコピーの概要を表示および使用します。

1. 「**閉じる**」を使用して終了し、**サイト**&#x200B;コンソールに戻ります。

## ライブコピーの概要の使用  {#using-the-live-copy-overview}

**ライブコピーの概要**&#x200B;ウィンドウには、選択したページに関連するライブコピーのステータスの概要が表示されます。

![ライブコピーの概要ウィンドウ](../assets/live-copy-overview.png)

ロールアウトは、特定のロールアウト設定で定義された同期アクションに依存します。 一部のアクションは、コンテンツの変更に依存します。 ただし、コンテンツの変更に依存せず、ページのアクティベーションなどのイベントに依存するアクションも多数あります。 このようなイベントは、コンテンツを変更するのではなく、コンテンツに関連する内部プロパティを変更します。

ステータスフィールドは、特定のロールアウト設定で定義される同期アクションによって異なり、前回のロールアウトが成功してからブループリントまたはライブコピーに対してそのようなアクションがあったかどうかを示します。 ステータスフィールドは、特定のロールアウト設定内のアクションのみを反映します。 ライブコピーに対してロールアウトが正常に実行されていない場合は、ステータスは常に最新の状態で表示されます。

例えば、ロールアウト設定は`targetActivate`と定義します。 したがって、ロールアウトはアクティベーションイベントにのみ依存します。 「ステータス」フィールドは、前回のロールアウトが正常に完了してからアクティベーションイベントが発生したかどうかを示します。

**ライブコピーの概要**&#x200B;は、ライブコピーに対するアクションの実行にも使用できます。

1. **ライブコピーの概要**&#x200B;を開きます。
1. 必要なブループリントまたはライブコピーページを選択すると、使用可能なアクションを表示するためにツールバーが更新されます。 使用できる[アクション](overview.md#terms-used)は、[ブループリント](#actions-for-a-blueprint-page)と[ライブコピー](#actions-for-a-live-copy-page)のどちらのページを選択したかによって異なります。

### ブループリントページのアクション {#actions-for-a-blueprint-page}

ブループリントページを選択した場合は、以下のアクションを使用できます。

![ブループリントのライブコピーの概要アクション](../assets/live-copy-overview-actions-blueprint.png)

* **編集**  — ブループリントページを編集用に開きます。
* **[ロールアウト](overview.md#rollout-and-synchronize)**  — ロールアウトを実行して、ソースからライブコピーに変更をプッシュします。

### ライブコピーページのアクション {#actions-for-a-live-copy-page}

ライブコピーページを選択すると、次のアクションを使用できます。

![ライブコピーのライブコピーの概要アクション](../assets/live-copy-overview-actions.png)

* **編集**  — ライブコピーページを編集用に開きます。
* **[関係ステータス](#relationship-status)**  — ステータスと継承に関する情報を表示します。
* **[同期](overview.md#rollout-and-synchronize)**  — ライブコピーを同期して、ソースからライブコピーに変更をプルします。
* **[リセット](creating-live-copies.md#resetting-a-live-copy-page)**  — ライブコピーページをリセットして、すべての継承のキャンセルを削除し、ページをソースページと同じ状態に戻します。
* **[休止](overview.md#suspending-and-cancelling-inheritance-and-synchronization)**  — ライブコピーとそのブループリントページの間のライブ関係を一時的に非アクティブ化します。
* **[再開](creating-live-copies.md#resuming-inheritance-for-a-page)**  — 再開：休止した関係を回復できます。
* **[分離](overview.md#detaching-a-live-copy)**  — ライブコピーとそのブループリントページとのライブ関係を完全に削除します。

## 関係ステータス {#relationship-status}

**関係ステータス**&#x200B;コンソールには、様々な機能を提供する2つのタブがあります。

* [関係ステータス](#relationship-status-tab)
* [ライブコピー](#live-copy-tab)

### 関係ステータス {#relationship-status-tab}

このタブには、ブループリントとライブコピーの関係のステータスに関する詳細情報が表示されます。

![「関係ステータス」タブ](../assets/live-copy-relationship-status.png)

### ライブコピー {#live-copy-tab}

このタブでは、ライブコピーの設定を表示および編集できます。

![「ライブコピー」タブ](../assets/live-copy-relationship-status-live-copy.png)
