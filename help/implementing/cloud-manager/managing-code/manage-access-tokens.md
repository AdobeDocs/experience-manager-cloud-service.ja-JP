---
title: Cloud Managerでの外部リポジトリのアクセストークンの管理
description: AEM Cloud Managerで独自の Git を取り込むために使用されるアクセストークンを表示、編集、削除する方法を説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="早期導入者" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#manage-access-tokens"
exl-id: bc9f392c-61f5-4d39-972b-4c6c8f9bab4a
source-git-commit: 9f9f931a233320014675c6aac86a2cc65f6909c6
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 14%

---

# 外部リポジトリのアクセストークンの管理 {#manage-access-tokens}

Cloud Managerはアクセストークンを使用して、外部 Git プラットフォームにホストされるリポジトリを管理します。 以前は、トークンの有効期限が切れた場合、操作可能な状態を維持するために、関連するリポジトリを再転送する必要がありました。

**アクセストークンの管理** 機能を使用すると、トークンをより効率的に管理できます。 サポートされている外部 Git プロバイダー（GitHub Enterprise、GitLab、Bitbucket、Azure DevOps など）に接続されているトークンを表示、名前変更、削除できます。

[Cloud Managerへの外部リポジトリの追加 ](/help/implementing/cloud-manager/managing-code/external-repositories.md) も参照してください。

>[!NOTE]
>
>この記事で説明する機能は、早期導入プログラムを通じてのみ使用できます。詳細と早期導入者としての新規登録について詳しくは、[独自の Git の導入](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket)を参照してください。

## アクセストークンの表示 {#view-access-tokens}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、独自の Git アクセストークンを管理するプログラムを選択します。
1. サイドメニューの&#x200B;**プログラム**&#x200B;で、![フォルダーアウトラインアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **リポジトリ**&#x200B;をクリックします。
1. ページの右上隅付近にある「**アクセストークンを管理**」をクリックします。

   「**アクセストークンを管理**」ボタンは、プログラムが「独自の Git を作成」機能を使用している場合にのみ表示されます。

   ![ アクティブなトークンと非アクティブなトークンが 1 つずつ一覧表示されている「アクセストークンの管理」ダイアログボックス ](/help/implementing/cloud-manager/managing-code/assets/access-tokens-manage.png)

1. **アクセストークンの管理** ダイアログボックスで、
   * すべてのアクセストークンが表示されます。
   * 任意のアクセストークンを **編集** できます。
   * **現在使用中ではない** アクセストークンのみ *削除* できます。 トークンが使用中の場合、「![ アウトラインの削除アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg) ボタンは無効になります。

## アクセストークンの編集 {#edit-access-tokens}

1. **アクセストークンの管理** ダイアログボックスで、トークン名の右側にある ![ 編集アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) をクリックします。
1. **アクセストークンを編集** ダイアログボックスで、**トークン名** または **アクセストークン** の値、あるいはその両方を更新します。

   **アクセストークン** が現在使用中の場合は、関連するすべてのリポジトリが更新後に自動的に再検証されることを警告する通知が表示されます。

   ![ アクセストークンを編集ダイアログボックス ](/help/implementing/cloud-manager/managing-code/assets/access-tokens-edit.png)

1. トークンが使用中の場合は、関連するすべてのリポジトリーが自動的に再検証されることを警告する通知が表示されます。

1. 「**更新**」をクリックして、変更を保存します。

## アクセストークンの削除 {#delete-access-token}

1. **アクセストークンの管理** ダイアログボックスで、トークン名の右側にある ![ 削除アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) をクリックします。

   現在使用中のトークンでは、このアイコンは無効になります（![ アウトラインの削除アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)）。

1. **アクセストークンを削除** ダイアログボックスで、「**削除**」をクリックして、トークンを永続的に削除します。
