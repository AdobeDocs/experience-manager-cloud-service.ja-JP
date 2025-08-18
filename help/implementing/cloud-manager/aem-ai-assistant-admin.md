---
title: Adobe Experience Managerでの AI アシスタントの設定
description: Adobe Experience ManagerでAdmin Consoleを使用して AI アシスタントをセットアップおよび設定する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: a7f3dc14-29f7-473a-9870-d52393e6fa6e
source-git-commit: e853e7b46c762ab724d5eecb344897a83e4fb724
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 3%

---

# Adobe Experience Managerでの AI アシスタントの設定 {#aem-ai-asst-admin-setup}

組織内のユーザーがAEM（Adobe Experience Manager） AI アシスタントの機能を使用するには、管理者がアクセス、権限、設定を行う必要があります。

AEM AI アシスタントの設定プロセスは、次の手順で構成されます。

1. [Adobe Admin Consoleで新しい製品プロファイルを作成 ](#create-profile) します。
1. [AI アシスタントの製品ナレッジ権限を有効にします ](#enable-permission)。
1. [ 新しいユーザーグループを作成（または既存のユーザーグループを使用） ](#create-user-group)。
1. [ ユーザーグループにユーザーを追加 ](#add-users)。
1. [ 製品プロファイルをユーザーグループに割り当てます ](#assign-product-profile)。

**前提条件**

開始する前に、次の前提条件を満たしていることを確認してください。

* Adobe Admin Consoleでは、少なくとも製品管理者権限が必要です。
* 組織のユーザー管理構造を理解している。

**設定に関する考慮事項**

* 処理時間：Cloud Managerで作成されたリソースがAdmin Consoleに表示されて権限が設定されるまでに、最大 2 分かかる場合があります。
* 複数のプロファイル：ユーザーは複数のプロファイルの一部であり、割り当てられたすべてのプロファイルから権限が結合されます。
* 組織の範囲：一部の権限は、すべてのプログラムに組織レベルで適用される場合があります。
* 定義済みプロファイル：定義済みの権限プロファイルをAdmin Consoleから削除しないでください。


## 1 - Adobe Admin Consoleでの新しい製品プロファイルの作成{#create-profile}

1. Experience Platformのドキュメントにある [Adobe Admin Consoleで新しい製品プロファイルを作成する ](https://experienceleague.adobe.com/ja/docs/experience-platform/access-control/ui/create-profile) の詳細な手順に従います。

1. 新しい製品プロファイルを作成する際に、AI アシスタントで以下の推奨値を使用できます。

   | テキストフィールド | 推奨値 |
   | --- | --- |
   | 製品プロファイル名 | `AEM AI Assistant` （または好ましい記述名） |
   | 表示名（オプション） | `AI Assistant` |
   | 説明（オプション） | `Product profile for managing AEM AI Assistant access` |
   | 通知 | 組織の環境設定に基づいてを設定します |


## 2 - AI アシスタントの製品ナレッジ権限を有効にします{#enable-permission}

製品プロファイルにカスタム権限を割り当てるプロセスは、標準のAdobe Cloud Manager カスタム権限ワークフローに従います。

リファレンス記事：[ 新しい製品プロファイルへのカスタム権限の割り当て ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Admin Consoleで、新しく作成した製品プロファイルの名前（`AEM AI Assistant`）をクリックします

   ![スクリーンショット](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. 編集可能な権限のリストを表示するには、「**権限** タブをクリックします。

1. テーブルリストで、`AI Assistant Product Knowledge` 権限を見つけます。

   ![Admin Consoleの「AI アシスタントの権限」タブ ](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. 権限名の右側にある ![ 鉛筆アイコンまたは編集アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) をクリックします。

1. **AI アシスタントの権限を編集** ページで、[**AI アシスタントの製品ナレッジ**] 切り替えをオンにします。

   ![AI アシスタントの「製品ナレッジ」切り替えオプションの「権限を編集」ページ ](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. ページの右下隅にある「**保存**」をクリックします。

   これで、製品プロファイルで AI アシスタントの製品ナレッジ権限が有効になりました。


## 3 – 新しいユーザーグループを作成（または既存のユーザーグループを使用）{#create-user-group}

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

>[!TAB  既存のユーザーグループを使用する ]

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

1. **`Add users to this user group`** ページで、AEM AI アシスタントへのアクセスを必要とするユーザーを検索して選択します。

   ![ このユーザーグループにユーザーを追加するページ ](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. ページの右下隅にある「**保存**」をクリックします。
1. 次に、製品プロファイルをユーザーグループに割り当てます &rbrack; （#assign-product-profile）。

>[!TAB ユーザーの一括追加]

Admin Consoleのバルクアップロード機能を使用できます。

1. ユーザー情報を含む CSV ファイルを準備します。
1. 効率的な一括追加には、**`Add users by CSV`** オプションを使用します。
1. 次に、製品プロファイルをユーザーグループに割り当てます &rbrack; （#assign-product-profile）。

>[!ENDTABS]


## 5 – 製品プロファイルのユーザーグループへの割り当て{#assign-product-profile}

この手順は、製品プロファイルをユーザーグループに割り当てるための標準Adobe Admin Console ワークフローに従います。

リファレンス記事：[ エンタープライズユーザーの製品プロファイルの管理 ](https://helpx.adobe.com/jp/enterprise/using/manage-product-profiles.html)

1. [4 - ユーザーグループにユーザーを追加 ](#add-users) からAEM AI アシスタントのユーザーグループを開いている間に、「**割り当てられた製品プロファイル**」タブをクリックします。
1. **プロファイルを割り当て** をクリックします。

   ![ 「製品プロファイルが割り当て済み」タブが選択されたAEM AI アシスタントのユーザーグループページ ](/help/implementing/cloud-manager/assets/ai-assistant-assign-profile.png)

1. **製品とプロファイルを割り当て** ページの **製品プロファイルを選択** ダイアログボックスで、**AI アシスタント** の製品プロファイルを検索して選択します。

   ![ 「製品プロファイルを選択」ダイアログボックスが表示されている「製品とプロファイルの割り当て」ページと、「AI アシスタント」製品プロファイルが選択されている様子 ](/help/implementing/cloud-manager/assets/ai-assistant-select-product-profile.png)

1. ダイアログボックスの右下隅付近にある「**適用**」をクリックします。
1. **製品とプロファイルの割り当て** ページの右下隅付近にある「**保存**」をクリックします。

   ![AEM AI Assistant ユーザーグループに割り当てられている AI アシスタントの製品プロファイルが表示されます ](/help/implementing/cloud-manager/assets/ai-assistant-profile-assigned-to-user-group.png)


## 設定の確認

* 製品プロファイルに、割り当てられたユーザーグループの正しい数が表示されていることを確認します。
* ユーザーグループに正しいユーザー数が表示されていることを確認します。
* AI アシスタントの製品ナレッジ権限が有効であり、適切に設定されていることを確認します。


## 設定のテスト

割り当てられたグループのユーザーに次の操作を行ってもらいます。

1. AEM にログインします。
2. AI アシスタントの機能にアクセスできることを確認します。
3. AI アシスタントの機能をテストして、適切なアクティベーションが行われることを確認します。

## 関連トピック

* [Adobe Experience Platformのアクセス制御 ](https://experienceleague.adobe.com/ja/docs/experience-platform/access-control/ui/overview)
* [Cloud Managerのカスタム権限](/help/implementing/cloud-manager/custom-permissions.md)


