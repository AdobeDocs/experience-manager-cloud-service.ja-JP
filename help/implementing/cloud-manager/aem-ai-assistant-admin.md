---
title: Adobe Experience Managerでの AI アシスタントの設定
description: Adobe Experience Managerで Admin Console を使用して AI アシスタントをセットアップおよび設定する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ab8fefe18e43c1fe937d0d16df65b6137fc8a292
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 4%

---

# AEM AI アシスタントの設定 – 管理者設定 {#aem-ai-asst-admin-setup}

管理者は、組織内のユーザーがAEM AI アシスタントの機能を使用する前に、アクセス、権限、設定を設定する必要があります。 この記事では、組織で AI アシスタントを有効にする方法、必要な資格情報を設定する方法、設定の変更を保存する方法について説明します。

**AEM AI Assistant の設定プロセスの概要**

設定プロセスは、次の手順で構成されます。

1. Adobe Admin Consoleで新しい製品プロファイルを作成します。
1. 「AI アシスタントの製品知識」権限を有効にします。
1. 既存のユーザーグループを作成または使用します。
1. ユーザーグループにユーザーを追加します。
1. 製品プロファイルをユーザーグループに割り当てます。

**前提条件**

開始する前に、次の前提条件を満たしていることを確認してください。

* Adobe Admin Consoleでは、少なくとも製品管理者権限が必要です。
* 組織のユーザー管理構造を理解している。

## 1 - Adobe Admin Consoleでの新しい製品プロファイルの作成{#create-profile}

1. 詳しくは、Experience Platformのドキュメントにある [Adobe Admin Consoleで新しい製品プロファイルを作成する ](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile) の手順に従ってください。

1. 新しい製品プロファイルを作成する際には、AI アシスタントに使用できる値について、以下の例を使用します。

   | テキストフィールド | 推奨値 |
   | --- | --- |
   | 製品プロファイル名 | `AEM AI Assistant` （または好ましい記述名） |
   | 表示名（オプション） | `AI Assistant` |
   | 説明（オプション） | `Product profile for managing AEM AI Assistant access` |
   | 通知 | 組織の環境設定に基づいてを設定します |




## 2 - 「AI アシスタントの製品知識」権限を有効にします{#enable-permission}

製品プロファイルにカスタム権限を割り当てるプロセスは、標準のAdobe Cloud Manager カスタム権限ワークフローに従います。

リファレンス記事：[ 新しい製品プロファイルへのカスタム権限の割り当て ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Admin Consoleで、新しく作成した製品プロファイルの名前（`AEM AI Assistant`）をクリックします

   ![スクリーンショット](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. 編集可能な権限のリストを表示するには、「**権限** タブをクリックします。

1. テーブルリストで、`AI Assistant Product Knowledge` 権限を見つけます。

   ![Admin Consoleの「AI アシスタントの権限」タブ ](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. 権限名の右側にある ![ 鉛筆アイコンまたは編集アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) をクリックします。

1. **AI アシスタントの権限を編集** ページで **AI アシスタント製品ナレッジ** 切り替えをオンにします。

   ![AI アシスタントの「製品ナレッジ」切り替えオプションの「権限を編集」ページ ](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. ページの右下隅にある「**保存**」をクリックします。

   これで、製品プロファイルで AI アシスタントの製品ナレッジ権限が有効になりました。


## 3 - ユーザーグループを作成（または既存のユーザーグループを使用）{#create-user-group}

1. 次のいずれかの操作を行います。

>[!BEGINTABS]

>[!TAB  新しいユーザーグループの作成 ]

1. Admin Consoleで、**ユーザー**/**ユーザーグループ** をクリックします。

   ![ユーザーグループ](/help/implementing/cloud-manager/assets/ai-assistant-user-groups.png)

1. **ユーザーグループ** ページで、「**新規ユーザーグループ**」をクリックします。

   ![ ユーザーグループ ページの「新規ユーザーグループ」ボタン ](/help/implementing/cloud-manager/assets/ai-assistant-new-user-group.png)

1. **新規ユーザーグループの作成** ページで、次の情報を入力します。

   | オプション | 推奨値 |
   | --- | --- |
   | ユーザーグループ名 | `AEM AI Assistant` （または好みの名前） |
   | 説明（オプション） | `User group for managing AEM AI Assistant access` |

   ![ ユーザーグループの新規作成ページ ](/help/implementing/cloud-manager/assets/ai-assistant-create-new-user-group.png)

1. ページの右下隅にある「**保存**」をクリックします。

>[!TAB  既存のユーザーグループの使用 ]

AI アシスタントのアクセス要件を満たす場合は、新しいグループを作成する代わりに、既存のAEM ユーザーグループを使用できます。

>[!ENDTABS]

## 4 - ユーザーグループへのユーザーの追加{#add-users}

1. 次のいずれかの操作を行います。

>[!BEGINTABS]

>[!TAB  個々のユーザーの追加 ]

1. **ユーザーグループ** ページの **グループ名** テーブルで、新しく作成したユーザーグループ名または既存のユーザーグループ名をクリックします。

   ![ テーブルにAEM AI Assistant のユーザーグループ名を表示するユーザーグループページ ](/help/implementing/cloud-manager/assets/ai-assistant-user-group-name-in-table.png)

1. **2&rbrace;AEM AI アシスタント** の「ユーザーグループ **ページで、「** ユーザー **」タブをクリックしてから「** ユーザーを追加 **」をクリックします。**

   ![ 「ユーザー」タブと「ユーザーを追加」ボタンが表示されているAEM AI Assistant のユーザーグループ ](/help/implementing/cloud-manager/assets/ai-assistant-add-users.png)

1. **このユーザーグループにユーザーを追加** ページで、AEM AI アシスタントへのアクセスを必要とするユーザーを検索して選択します。

   ![ このユーザーグループにユーザーを追加するページ ](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. ページの右下隅にある「**保存**」をクリックします。

>[!TAB ユーザーの一括追加]

Admin Consoleのバルクアップロード機能を使用できます。

1. ユーザー情報を含む CSV ファイルを準備します。

1. 効率的な一括追加には、「**CSV によるユーザーの追加** オプションを使用します。

>[!ENDTABS]




## 5 – 製品プロファイルのユーザーグループへの割り当て{#assign-product-profile}




