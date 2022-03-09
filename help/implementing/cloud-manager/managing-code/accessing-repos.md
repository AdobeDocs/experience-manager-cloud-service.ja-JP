---
title: リポジトリーへのアクセス
description: Cloud Manager のセルフサービス Git アカウント管理を使用して、Git リポジトリにアクセスし、管理する方法について説明します。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 4729574eb31e01077f0d2a35efcef6d134f6aa5c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 8%

---

# リポジトリーへのアクセス {#accessing-repos}

Cloud Manager のセルフサービス Git アカウント管理を使用して、Git リポジトリにアクセスし、管理する方法について説明します。

## セルフ・サービス・リポジトリ・アカウント管理の使用 {#self-service-repos}

Cloud Manager では、 **リポジトリ情報にアクセス** ボタンがパイプラインカード上で目立つ場所に表示されます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. に移動します。 **パイプライン** カードから **プログラムの概要** ページで **リポジトリ情報にアクセス** ボタンをクリックして、git リポジトリにアクセスして管理します。

   ![環境カードの「リポジトリ情報」ボタンにアクセス](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. をクリックします。 **リポジトリ情報を表示** ボタンをクリックして、表示するダイアログを開きます。

   * Cloud Manager の Git リポジトリの URL です。
   * Git のユーザー名。
   * git パスワード。この値は、 **パスワードを生成** 」ボタンがクリックされたときに表示されます。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

ユーザーは、これらの資格情報を使用して、リポジトリのローカルコピーを複製し、そのローカルリポジトリで変更を加えることができます。準備が整ったら、Cloud Manager のリモートコードリポジトリにコードの変更をコミットして戻すことができます。

この **リポジトリ情報にアクセス** オプションは **非実稼動** の「パイプライン」タブ **パイプライン** カード。

![非実稼動タブの「リポジトリ情報」ボタンにアクセス](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>この **リポジトリ情報にアクセス** オプションは、 **開発者** または **デプロイメントマネージャー** 役割。
