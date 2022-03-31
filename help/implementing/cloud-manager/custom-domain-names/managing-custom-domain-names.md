---
title: カスタムドメイン名の管理
description: Cloud Manager を使用して、カスタムドメイン名を表示、更新、置換、削除する方法について説明します。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
source-git-commit: 878381f9c5780864f218a00a272b1600d578dcca
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 31%

---

# カスタムドメイン名の管理 {#managing-custom-domain-names}

Cloud Manager では、カスタムドメイン名の表示、更新、置換、削除をおこなうことができます。

## 表示と更新 {#view-and-update}

以下を使用： **表示と更新** メニューを使用して、カスタムドメイン名の詳細を表示できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 次に移動： **環境** 画面から **概要** ページ。

1. 表示または更新するカスタムドメイン名の行を特定します。

1. 行の右端にある省略記号ボタンをクリックします。

1. 「**表示と更新**」オプションを選択します。

## カスタムドメイン名の SSL 証明書の更新 {#update-cert}

フォロー可能 [カスタムドメイン名を表示および更新する同じ手順](#view-and-update) をクリックして、カスタムドメイン名の SSL 証明書を更新します。

>[!NOTE]
>
>SSL 証明書が有効である必要があります。 [既に設定済み](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) には、更新するカスタムドメイン名が含まれます。

##  カスタムドメイン名の削除 {#deleting}

ユーザーが **ビジネスオーナー** または **デプロイメントマネージャー** の役割では、 Cloud Manager を使用してカスタムドメイン名を削除できます。

### 関連するすべての環境からカスタムドメイン名を削除する方法 {#delete-cdn-all}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 次に移動： **環境** 画面から **概要** ページ。

1. **環境**&#x200B;画面から&#x200B;**ドメイン設定**&#x200B;ページに移動します。

1. 削除するカスタムドメイン名の行を特定します。

1. 行の右端にある省略記号ボタンをクリックします。

1. 「**削除**」を選択します。

   ![カスタムドメイン名の削除](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. 送信を確認します。

### 特定の環境からカスタムドメイン名を削除する方法 {#delete-cdn-specific}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. 次に移動： **環境** 画面から **概要** ページ。
1. 次の **環境** ページで、目的の環境の詳細画面に移動します。
1. ドメイン名テーブルから、削除するカスタムドメイン名の行を特定します。
1. 行の右端にある省略記号ボタンをクリックします。
1. 「**削除**」を選択します。
1. 送信を確認します。
