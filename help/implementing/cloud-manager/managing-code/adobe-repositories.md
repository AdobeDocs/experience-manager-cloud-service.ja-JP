---
title: Cloud Manager での Adobe リポジトリの追加
description: Cloud Manager で、アドビが管理するリポジトリを追加する方法について説明します。
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 100%

---

# Cloud Manager での Adobe リポジトリの追加 {#adobe-repositories}

Cloud Manager でアドビが管理するリポジトリを追加する方法について説明します。

**リポジトリ**&#x200B;ページを使用すると、アドビが管理するリポジトリを選択したプログラムに簡単に追加できます。

**Cloud Manager に Adobe リポジトリを追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、アドビが管理するリポジトリを追加する適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページのサイドメニューで、![フォルダーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg)「**リポジトリ**」タブをクリックします。

1. **リポジトリ**&#x200B;ページの右上付近にある「**リポジトリを追加**」をクリックします。

   ![「リポジトリを追加」ボタン](assets/add-repository.png)

1. **リポジトリを追加**&#x200B;ダイアログボックスで、リポジトリタイプとして「**Adobe リポジトリ**」が選択されていることを確認します。

1. それぞれのテキストフィールドに、次を入力します。

   * **リポジトリ名** - 新しいリポジトリの表現名。
   * **リポジトリ URL のプレビュー** - リポジトリインフラストラクチャは既に配置され、アドビによって完全に統合および管理されているので、URL パスを入力したり、既存のパスを編集したりする必要はありません。
   * **説明（オプション）** - リポジトリの詳細な説明。

   ![リポジトリを追加ダイアログボックス](assets/add-adobe-repository.png)

1. 「**保存**」をクリックします。
新しいリポジトリが**リポジトリ**&#x200B;ページのテーブルに表示されます。

これで、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を関連付けることや、[**リポジトリ**&#x200B;ページ](managing-repositories.md)内で管理することができます。

>[!TIP]
>
>また、自分で管理する GitHub リポジトリを[プライベートリポジトリ](private-repositories.md)として追加することもできます。
