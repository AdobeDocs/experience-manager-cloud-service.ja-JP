---
title: AEM の AI アシスタントの設定
description: Adobe Experience Manager の Admin Console を使用して、AI アシスタントを設定および構成する方法について説明します。
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: cc80a36b-2fd2-41cc-8cb7-6c25e8e89a4e
source-git-commit: 2f02b9d70e56f4aafd802e986974533197f7d7a5
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 83%

---

# AEM の AI アシスタントの設定 {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

AEM（Adobe Experience Manager）で AI アシスタントを使用するには、AI アシスタントを通じて製品知識にアクセスする権限が必要です。 Adobeでは、この権限がデフォルトでオンになります。

製品知識にアクセスできるユーザーを管理するには、Adobe ID に関連付けられているメールアドレスから [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) にメールを送信してください。 アドビでは、ユーザーレベルのアクセス制御を有効にできます。 有効にすると、管理者は次の手順に従ってユーザーレベルのアクセス権を付与できます。

ユーザーレベルのアクセス制御をリクエストした場合、組織はAdobe Admin Consoleを通じてオプトインする必要があります。 製品管理者がユーザーグループを作成（または選択）し、新しい「AI アシスタント」権限を付与します。 そのグループに追加すれば、AEM 全体で AI アシスタントに誰でも即座にアクセスできるようになります。 目標が全社的な可用性である場合、管理者はすべてのユーザーをそのグループに割り当てます。

ユーザーの場合、プロセスは簡単です。組織内のAdobe Experience Managerの製品管理者を特定し、AI対応ユーザーグループに追加することをリクエストします。 そのグループに追加すると、次回ログインしたときにアシスタントアイコンが自動的に表示されます。

管理者は、通常のCloud Manager ガバナンスに従う必要があります。 プロファイルの作成、ユーザーグループの管理、権限の編集を行うには、Admin Consoleでプロダクト管理者権限を保持します。 ユーザーがアシスタントの組み込み&#x200B;**サポートチケット作成**&#x200B;機能も必要な場合は、同じ個人またはグループに標準の&#x200B;**サポート管理者**&#x200B;ロール（標準の Admin Console ロール）を追加してください。

AEM の AI アシスタントの設定プロセスは、次の手順で構成されます。

1. [Adobe Admin Console で新しい製品プロファイルを作成します](#create-profile)。
1. [AI アシスタント製品知識の権限を有効にします](#enable-permission)。
1. [新しいユーザーグループを作成するか、既存のユーザーグループを使用します](#create-user-group)。
1. [ユーザーをユーザーグループに追加します](#add-users)。
1. [製品プロファイルをユーザーグループに割り当てます](#assign-product-profile)。

**前提条件**

開始する前に、次の前提条件を満たしていることを確認してください。

* Adobe Admin Console では、少なくともプロダクト管理者権限が必要です。
* 組織のユーザー管理構造を理解している必要があります。

**設定に関する考慮事項**

* 処理時間：Cloud Managerで作成されたリソースは、権限設定のためにAdmin Consoleに表示するのに最大2分かかります。
* 複数のプロファイル：ユーザーは複数のプロファイルに属することができ、権限は割り当てられたすべてのプロファイルから統合されます。
* 組織スコープ：一部の権限は、すべてのプログラムに対して組織レベルで適用されます。
* 定義済みのプロファイル：定義済みの権限プロファイルを Admin Console から削除しないでください。


## 1 - Adobe Admin Console で新しい製品プロファイルを作成する{#create-profile}

1. Experience Platform ドキュメントにある「[Adobe Admin Console で新しい製品プロファイルを作成する](https://experienceleague.adobe.com/ja/docs/experience-platform/access-control/ui/create-profile)」の詳細な手順に従ってください。

1. 新しい製品プロファイルを作成する際は、AI アシスタントに次の推奨値を使用できます。

   | テキストフィールド | 推奨値 |
   | --- | --- |
   | 製品プロファイル名 | `AI Assistant in AEM`（または任意のわかりやすい名前） |
   | 表示名（オプション） | `AI Assistant` |
   | 説明（オプション） | `Product profile for managing AI Assistant in AEM access` |
   | 通知 | 組織の好みに応じて設定 |


## 2 - AI アシスタント製品知識の権限を有効にする{#enable-permission}

製品プロファイルにカスタム権限を割り当てるプロセスは、Adobe Cloud Manager 標準カスタム権限ワークフローに従います。

参考記事：[新しい製品プロファイルにカスタム権限を割り当てる](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Admin Console で、新しく作成した製品プロファイル（`AI Assistant in AEM`）の名前をクリックします。

   ![スクリーンショット](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. 編集可能な権限のリストを表示するには、「**権限**」タブをクリックします。

1. テーブルリストで、`AI Assistant Product Knowledge` 権限を見つけます。

   ![Admin Console の「AI アシスタント権限」タブ](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. 権限名の右側にある「![鉛筆アイコンまたは編集アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)」をクリックします。

1. **AI アシスタントの権限を編集**&#x200B;ページで、**AI アシスタント製品知識**&#x200B;の切替スイッチをオンにします。

   ![AI アシスタント製品知識の権限を編集ページの切替スイッチオプション](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. ページの右下隅にある「**保存**」をクリックします。

   製品プロファイルで、AI アシスタント製品知識の権限が有効になりました。


## 3 - 新しいユーザーグループを作成するか、既存のユーザーグループを使用する{#create-user-group}

1. 次のいずれかの操作を行います。

>[!BEGINTABS]

>[!TAB 新しいユーザーグループを作成]

1. Admin Console で、**ユーザー**／**ユーザーグループ**&#x200B;の順にクリックします。

   ![ユーザーグループ](/help/implementing/cloud-manager/assets/ai-assistant-user-groups.png)

1. **ユーザーグループ**&#x200B;ページで、「**新しいユーザーグループ**」をクリックします。

   ![ユーザーグループページの「新しいユーザーグループ」ボタン](/help/implementing/cloud-manager/assets/ai-assistant-new-user-group.png)

1. **新しいユーザーグループを作成**&#x200B;ページで、次の情報を入力します。

   | オプション | 推奨値 |
   | --- | --- |
   | ユーザーグループ名 | `AI Assistant in AEM`（または任意の名前） |
   | 説明（オプション） | `User group for managing AI Assistant in AEM access` |

   ![新しいユーザーグループを作成ページ](/help/implementing/cloud-manager/assets/ai-assistant-create-new-user-group.png)

1. ページの右下隅にある「**保存**」をクリックします。

>[!TAB 既存ユーザーグループを使用]

新しいグループを作成する代わりに、AI アシスタントのアクセス要件を満たす既存の AEM ユーザーグループを使用できます。

>[!ENDTABS]

## 4 - ユーザーをユーザーグループに追加する{#add-users}

1. 次のいずれかの操作を行います。

>[!BEGINTABS]

>[!TAB 個別のユーザーを追加]

1. **ユーザーグループ** ページの&#x200B;**グループ名** テーブルで、新しく作成したユーザーグループ名または既存のユーザーグループ名をクリックします。

   ![テーブルの AEM ユーザーグループ名に AI アシスタントを表示するユーザーグループページ](/help/implementing/cloud-manager/assets/ai-assistant-user-group-name-in-table.png)

1. **AEM の AI アシスタント**&#x200B;の&#x200B;**ユーザーグループ**&#x200B;ページで、「**ユーザー**」タブをクリックし、「**ユーザーを追加**」をクリックします。

   AEM ユーザーグループ ページの![AI アシスタント。ユーザーのタブと「ユーザーを追加」ボタンが表示されている](/help/implementing/cloud-manager/assets/ai-assistant-add-users.png)

1. **`Add users to this user group`** ページで、AEM の AI アシスタントにアクセスする必要があるユーザーを検索して選択します。

   ![このユーザーグループページにユーザーを追加](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. ページの右下隅にある「**保存**」をクリックします。
1. 次に、[製品プロファイルをユーザーグループに割り当てます](#assign-product-profile)。

>[!TAB ユーザーの一括追加]

Admin Console のバルクアップロード機能を使用できます。

1. ユーザー情報を含む CSV ファイルを準備します。
1. 効率的な一括追加には、**`Add users by CSV`** オプションを使用します。
1. 次に、[製品プロファイルをユーザーグループに割り当てます](#assign-product-profile)。

>[!ENDTABS]


## 5 - 製品プロファイルをユーザーグループに割り当てる{#assign-product-profile}

この手順は、Adobe Admin Console の標準的なワークフローに従って、製品プロファイルをユーザーグループに割り当てるものです。

参照記事：[エンタープライズユーザー向け製品プロファイルの管理](https://helpx.adobe.com/jp/enterprise/using/manage-product-profiles.html)

1. 「[4 - ユーザーをユーザーグループに追加する](#add-users)」から引き続き、AEM ユーザーグループの AI アシスタントにいる状態で、「**割り当て済み製品プロファイル**」タブをクリックします。
1. 「**プロファイルを割り当て**」をクリックします。

   ![「割り当て済み製品プロファイル」タブが選択された AEM ユーザーグループページの AI アシスタント](/help/implementing/cloud-manager/assets/ai-assistant-assign-profile.png)

1. **製品とプロファイルを割り当て**&#x200B;ページの、**製品プロファイルを選択**&#x200B;ダイアログボックスで、**AI アシスタント**&#x200B;製品プロファイルを検索して選択します。

   ![「製品プロファイルを選択」ダイアログボックスが表示され、「AIアシスタント」製品プロファイルが選択されている、「製品とプロファイルを割り当て」ページ](/help/implementing/cloud-manager/assets/ai-assistant-select-product-profile.png)

1. ダイアログボックスの右下隅付近にある「**適用**」をクリックします。
1. **製品とプロファイルを割り当て**&#x200B;ページの右下隅付近にある「**保存**」をクリックします。

   ![AEM ユーザーグループの AI アシスタントに割り当てられた AI アシスタント製品プロファイル](/help/implementing/cloud-manager/assets/ai-assistant-profile-assigned-to-user-group.png)


## 設定の確認

* 製品プロファイルに、割り当てられているユーザーグループの数が正しいことを確認してください。
* ユーザーグループに、正しいユーザー数が表示されていることを確認します。
* AI アシスタント製品知識の権限が有効で、適切に設定されていることを確認します。


## 設定のテスト

割り当てられたグループのユーザーに次の操作を実行してもらいます。

1. AEM にログインします。
2. AI アシスタント機能にアクセスできることを確認します。
3. 適切にアクティベーションできるように、AI アシスタントの機能をテストします。

## 関連トピック

* [AEM の AI アシスタント](/help/implementing/cloud-manager/ai-assistant-in-aem.md)
* [Adobe Experience Platform のアクセス制御](https://experienceleague.adobe.com/ja/docs/experience-platform/access-control/ui/overview)
* [Cloud Managerのカスタム権限](/help/implementing/cloud-manager/custom-permissions.md)

