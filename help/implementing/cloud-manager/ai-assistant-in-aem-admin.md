---
title: AEM の AI アシスタントの設定
description: Adobe Experience ManagerでAdmin Consoleを使用して AI アシスタントをセットアップおよび設定する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing, AI Assistant, AI Tools
role: Admin, Architect, Developer
exl-id: cc80a36b-2fd2-41cc-8cb7-6c25e8e89a4e
source-git-commit: c47b1ec8219c7130f1f5767551d442b0af3195c0
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 4%

---

# AEM の AI アシスタントの設定 {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

AEM（Adobe Experience Manager）で AI アシスタントを使用するには、AI アシスタントを通じて製品ナレッジにアクセスする権限が必須です。 この権限は、デフォルトでオンになっています。

製品ナレッジにアクセスできるユーザーを制御する場合は、Adobe IDに関連付けられた電子メールアドレスから [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) に電子メールを送信します。 Adobeでは、ユーザーレベルのアクセス制御を有効にできます。 有効にすると、管理者は次の手順に従ってユーザーレベルのアクセス権を付与できます。

ユーザーレベルのアクセス制御を要求した場合は、Adobe Admin Console経由でオプトインする必要があります。 製品管理者がユーザーグループを作成（または選択）し、新しい「AI アシスタント」権限を付与します。 そのグループに追加されたユーザーは誰でも、AEM全体で AI アシスタントにすぐにアクセスできます。 企業全体での可用性が目標の場合、管理者はそのグループにすべてのユーザーを割り当てるだけです。

従業員の観点からは、組織内のAdobe Experience Managerの製品管理者を特定して、AI 対応のユーザーグループに追加するようリクエストするプロセスは簡単です。 そのグループに表示されると、次回ログインしたときにアシスタント アイコンが自動的に表示されます。

管理者は、通常のCloud Manager ガバナンスを念頭に置く必要があります。 プロファイルの作成、ユーザーグループの管理、権限の編集を行うには、Admin Consoleの製品管理者権限を保持します。 ユーザーがアシスタントの組み込みの **サポートチケットを作成** 機能も必要な場合は、同じ個人またはグループに標準の **サポート管理者** ロール（標準のAdmin Console ロール）を追加します。

AEMでの AI アシスタントの設定プロセスは、次の手順で構成されます。

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

1. Experience Platformのドキュメントにある [Adobe Admin Consoleで新しい製品プロファイルを作成する ](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile) の詳細な手順に従います。

1. 新しい製品プロファイルを作成する際に、AI アシスタントで以下の推奨値を使用できます。

   | テキストフィールド | 推奨値 |
   | --- | --- |
   | 製品プロファイル名 | `AI Assistant in AEM` （または好ましい記述名） |
   | 表示名（オプション） | `AI Assistant` |
   | 説明（オプション） | `Product profile for managing AI Assistant in AEM access` |
   | 通知 | 組織の環境設定に基づいてを設定します |


## 2 - AI アシスタントの製品ナレッジ権限を有効にする{#enable-permission}

製品プロファイルにカスタム権限を割り当てるプロセスは、標準のAdobe Cloud Manager カスタム権限ワークフローに従います。

リファレンス記事：[ 新しい製品プロファイルへのカスタム権限の割り当て ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Admin Consoleで、新しく作成した製品プロファイルの名前（`AI Assistant in AEM`）をクリックします

   ![スクリーンショット](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. 編集可能な権限のリストを表示するには、「**権限** タブをクリックします。

1. テーブルリストで、`AI Assistant Product Knowledge` 権限を見つけます。

   ![Admin Consoleの「AI アシスタントの権限」タブ ](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. 権限名の右側にある ![ 鉛筆アイコンまたは編集アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) をクリックします。

1. **AI アシスタントの権限を編集** ページで、[**AI アシスタントの製品ナレッジ**] 切り替えをオンにします。

   ![AI アシスタントの「製品ナレッジ」切り替えオプションの権限ページを編集 ](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

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
   | ユーザーグループ名 | `AI Assistant in AEM` （または好みの名前） |
   | 説明（オプション） | `User group for managing AI Assistant in AEM access` |

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

   ![ テーブル内のAEM ユーザーグループ名に AI アシスタントが表示されているユーザーグループページ ](/help/implementing/cloud-manager/assets/ai-assistant-user-group-name-in-table.png)

1. **AEMの AI アシスタント** の **ユーザーグループ** ページで、「**ユーザー**」タブをクリックしてから「**ユーザーを追加**」をクリックします。

   ![AEM ユーザーグループページの「ユーザー」タブと「ユーザーを追加」ボタンを表示する AI アシスタント ](/help/implementing/cloud-manager/assets/ai-assistant-add-users.png)

1. **`Add users to this user group`** ページで、AEMの AI アシスタントにアクセスする必要があるユーザーを検索して選択します。

   ![ このユーザーグループにユーザーを追加するページ ](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. ページの右下隅にある「**保存**」をクリックします。
1. ここで、[ 製品プロファイルをユーザーグループに割り当てる ](#assign-product-profile) 必要があります。

>[!TAB ユーザーの一括追加]

Admin Consoleのバルクアップロード機能を使用できます。

1. ユーザー情報を含む CSV ファイルを準備します。
1. 効率的な一括追加には、**`Add users by CSV`** オプションを使用します。
1. ここで、[ 製品プロファイルをユーザーグループに割り当てる ](#assign-product-profile) 必要があります。

>[!ENDTABS]


## 5 – 製品プロファイルのユーザーグループへの割り当て{#assign-product-profile}

この手順は、製品プロファイルをユーザーグループに割り当てるための標準Adobe Admin Console ワークフローに従います。

リファレンス記事：[ エンタープライズユーザーの製品プロファイルの管理 ](https://helpx.adobe.com/jp/enterprise/using/manage-product-profiles.html)

1. [4 - ユーザーグループにユーザーを追加 ](#add-users) からAEM ユーザーグループの AI アシスタントで、「**割り当てられた製品プロファイル**」タブをクリックします。
1. **プロファイルを割り当て** をクリックします。

   ![ 「製品プロファイルが割り当てられた」タブが選択されているAEM ユーザーグループページの AI アシスタント ](/help/implementing/cloud-manager/assets/ai-assistant-assign-profile.png)

1. **製品とプロファイルを割り当て** ページの **製品プロファイルを選択** ダイアログボックスで、**AI アシスタント** の製品プロファイルを検索して選択します。

   ![ 「製品プロファイルを選択」ダイアログボックスが表示されている「製品とプロファイルの割り当て」ページと、「AI アシスタント」製品プロファイルが選択されている様子 ](/help/implementing/cloud-manager/assets/ai-assistant-select-product-profile.png)

1. ダイアログボックスの右下隅付近にある「**適用**」をクリックします。
1. **製品とプロファイルの割り当て** ページの右下隅付近にある「**保存**」をクリックします。

   ![AEM ユーザーグループで AI アシスタントに割り当てられた AI アシスタントの製品プロファイルが表示される ](/help/implementing/cloud-manager/assets/ai-assistant-profile-assigned-to-user-group.png)


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

* [AEM の AI アシスタント](/help/implementing/cloud-manager/ai-assistant-in-aem.md)
* [Adobe Experience Platformのアクセス制御 ](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
* [Cloud Managerのカスタム権限](/help/implementing/cloud-manager/custom-permissions.md)
