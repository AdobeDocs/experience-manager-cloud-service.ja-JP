---
title: カスタムドメイン名の管理
description: Cloud Manager を使用して、カスタムドメイン名を表示、更新、置換、削除する方法について説明します。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: ht
source-wordcount: '326'
ht-degree: 100%

---

# カスタムドメイン名の管理 {#managing-custom-domain-names}

Cloud Manager では、カスタムドメイン名の表示、更新、置換、削除を行うことができます。

## 表示と更新 {#view-and-update}

**表示と更新**&#x200B;メニューを使用すると、どのカスタムドメイン名の詳細でも表示できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. 表示または更新するカスタムドメイン名の行を見つけます。

1. 行の右端にある省略記号ボタンをクリックします。

1. 「**表示と更新**」オプションを選択します。

## カスタムドメイン名の SSL 証明書の更新 {#update-cert}

[カスタムドメイン名を表示および更新する場合と同じ手順](#view-and-update)に従って、カスタムドメイン名の SSL 証明書を更新します。

>[!NOTE]
>
>SSL 証明書が有効であり、[既に設定済み](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)で、更新するカスタムドメイン名が含まれている必要があります。

## カスタムドメイン名の削除 {#deleting}

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーが、Cloud Manager を使用してカスタムドメイン名を削除できます。

### 関連するすべての環境からカスタムドメイン名を削除する方法 {#delete-cdn-all}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;画面から&#x200B;**ドメイン設定**&#x200B;ページに移動します。

1. 削除するカスタムドメイン名の行を見つけます。

1. 行の右端にある省略記号ボタンをクリックします。

1. 「**削除**」を選択します。

1. 送信を確認します。

### 特定の環境からカスタムドメイン名を削除する方法 {#delete-cdn-specific}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. **概要**&#x200B;ページの&#x200B;**環境**&#x200B;画面に移動します。
1. **環境**&#x200B;ページから、対象となる環境の詳細画面に移動します。
1. ドメイン名のテーブルで、削除するカスタムドメイン名の行を見つけます。
1. 行の右端にある省略記号ボタンをクリックします。
1. 「**削除**」を選択します。
1. 送信を確認します。
