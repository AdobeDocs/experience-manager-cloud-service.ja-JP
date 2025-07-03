---
title: Cloud Managerでの外部リポジトリのアクセストークンを管理する
description: AEM Cloud Manager の Bring Your Own Git のために使用されるアクセストークンを表示、編集、削除する方法を説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Private Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#manage-access-tokens"
exl-id: bc9f392c-61f5-4d39-972b-4c6c8f9bab4a
source-git-commit: 52e05be90dc1a4997c6b65306bc646d03456c971
workflow-type: ht
source-wordcount: '403'
ht-degree: 100%

---

# 外部リポジトリのアクセストークンを管理する {#manage-access-tokens}

Cloud Managerはアクセストークンを使用して、外部 Git プラットフォームにホストされるリポジトリを管理します。以前は、トークンの有効期限が切れた場合、操作可能な状態を維持するために、関連するリポジトリを再度オンボーディングする必要がありました。

**アクセストークンの管理**&#x200B;機能を使用すると、トークンをより効率的に管理できます。サポートされている外部 Git プロバイダー（GitHub Enterprise、GitLab、Bitbucket、Azure DevOps など）に接続されているトークンを表示、名前変更、削除できます。

[Cloud Manager での外部リポジトリの追加](/help/implementing/cloud-manager/managing-code/external-repositories.md)も参照してください。

>[!NOTE]
>
>この記事で説明する機能は、Private Beta プログラムを通じてのみ使用できます。詳細と Private Beta の新規登録について詳しくは、[独自の Git の導入](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket)を参照してください。

## アクセストークンを表示する {#view-access-tokens}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。
1. **[My Programs](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、Bring Your Own Git アクセストークンを管理するプログラムを選択します。
1. サイドメニューの&#x200B;**プログラム**&#x200B;で、![フォルダーアウトラインアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **リポジトリ**&#x200B;をクリックします。
1. ページの右上隅にある「**アクセストークンの管理**」をクリックします。

   「**アクセストークンの管理**」ボタンは、プログラムが Bring Your Own Git 機能を使用している場合にのみ表示されます。

   ![アクティブなトークンと非アクティブなトークンが 1 つずつ一覧表示されているアクセストークンの管理ダイアログボックス](/help/implementing/cloud-manager/managing-code/assets/access-tokens-manage.png)

1. **アクセストークンの管理**&#x200B;ダイアログボックスで：
   * すべてのアクセストークンがリストされています。
   * 任意のアクセストークンを&#x200B;**編集**&#x200B;できます。
   * **現在使用中ではない** アクセストークンのみ *削除* できます。 トークンが使用中の場合、「![アウトラインアイコンの削除](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)」ボタンは無効になります。

## アクセストークンの編集 {#edit-access-tokens}

1. **アクセストークンの管理**&#x200B;ダイアログボックスで、トークン名の右側にある![編集アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)をクリックします。
1. **アクセストークンを編集**&#x200B;ダイアログボックスで、**トークン名**&#x200B;の値や&#x200B;**アクセストークン**&#x200B;の値またはその両方を更新します。

   ![アクセストークンの編集ダイアログボックス](/help/implementing/cloud-manager/managing-code/assets/access-tokens-edit.png)

1. **アクセストークン**&#x200B;が現在使用中の場合は、更新後に関連するすべてのリポジトリが自動的に再検証されることを警告する通知が表示されます。

1. 「**更新**」をクリックして、変更を保存します。

## アクセストークンの削除 {#delete-access-token}

1. **アクセストークンの管理**&#x200B;ダイアログボックスで、トークン名の右側にある![削除アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)をクリックします。

   現在使用中のトークンでは、このアイコンは無効になります（![アウトラインアイコンの削除](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)）。

1. **アクセストークンの削除**&#x200B;ダイアログボックスで、「**削除**」をクリックしてトークンを永久に削除します。
