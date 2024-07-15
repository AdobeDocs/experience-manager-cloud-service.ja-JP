---
title: Cloud Manager での Adobe リポジトリの追加
description: Cloud Manager でアドビが管理するリポジトリを作成する方法について説明します。
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 100%

---

# Cloud Manager での Adobe リポジトリの追加 {#adobe-repositories}

Cloud Manager でアドビが管理するリポジトリを作成する方法について説明します。

## アドビが管理するリポジトリの追加 {#add-adobe-repository}

**リポジトリ**&#x200B;ウィンドウを使用すると、アドビが管理するリポジトリをプログラムに容易に追加できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページで、「**リポジトリ**」タブをクリックして「**リポジトリ**」ページに切り替えます。

1. ツールバーで「**リポジトリを追加**」をクリックします。

   ![「リポジトリーを追加」ボタン](assets/add-repository.png)

1. 必要に応じて名前と説明を入力し、「**保存**」をクリックします。

   ![リポジトリーを追加ダイアログ](assets/add-adobe-repository.png)

ウィザードが閉じると、新しいリポジトリが&#x200B;**リポジトリ**&#x200B;ウィンドウのテーブルに表示されます。これで、[CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を関連付けることや、[**リポジトリ**&#x200B;ウィンドウ内で管理することができます。](managing-repositories.md)

>[!TIP]
>
>また、自分で管理する GitHub リポジトリを[プライベートリポジトリ](private-repositories.md)として追加することもできます。
