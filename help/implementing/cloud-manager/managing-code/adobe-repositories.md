---
title: Cloud ManagerでのAdobeリポジトリの追加
description: Cloud ManagerでAdobeが管理するリポジトリを追加する方法について説明します。
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f2364de6237ca9f0285815b581bcf3881488188d
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 7%

---

# Cloud ManagerでのAdobeリポジトリの追加 {#adobe-repositories}

Cloud ManagerでAdobeが管理するリポジトリを追加する方法について説明します。

**リポジトリ** ページを使用すると、Adobeが管理するリポジトリを、選択したプログラムに簡単に追加できます。

**Cloud ManagerにAdobeリポジトリを追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) でCloud Managerにログインし、Adobeが管理するリポジトリを追加する適切な組織とプログラムを選択します。

1. **プログラムの概要** ページのサイドメニューで、![&#x200B; フォルダーアイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg)**リポジトリ** タブをクリックします。

1. **リポジトリ** ページで、右上隅付近の「**リポジトリを追加**」をクリックします。

   ![「リポジトリーを追加」ボタン](assets/add-repository.png)

1. **リポジトリを追加** ダイアログボックスで、リポジトリタイプとして **2&rbrace;Adobeリポジトリ &rbrace; が選択されていることを確認します。**

1. それぞれのテキストフィールドに、以下を入力します。

   * **リポジトリ名** – 新しいリポジトリの名前を表す名前。
   * **リポジトリ URL のプレビュー** - リポジトリインフラストラクチャは既に配置され、Adobeによって完全に統合および管理されているので、URL パスを入力したり、既存のパスを編集したりする必要はありません。
   * **説明（オプション）** - リポジトリの詳細な説明。

   ![&#x200B; リポジトリを追加ダイアログボックス &#x200B;](assets/add-adobe-repository.png)

1. **保存** をクリックします。
新しいリポジトリが、**リポジトリ** ページのテーブルに表示されます。

[CI/CD パイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) を関連付けたり、[**リポジトリ** ページ &#x200B;](managing-repositories.md) 内で管理したりできるようになりました。

>[!TIP]
>
>また、自分で管理する GitHub リポジトリを[プライベートリポジトリ](private-repositories.md)として追加することもできます。
