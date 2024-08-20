---
title: IP許可リストの適用と適用解除
description: Cloud Manager環境に IP許可リストを適用および適用解除する方法について説明します。
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 22%

---


# IP許可リストの適用と適用解除 {#apply-allow-list}

IP許可リストを適用すると、リストの定義に含まれているすべての IP 範囲が環境内のオーサーサービスまたはパブリッシュサービスに関連付けられます。 リストの適用を解除すると、この処理の逆になります。

## IP許可リストの適用 {#applying}

**ビジネスオーナー** または **デプロイメントマネージャー** の役割を持つユーザーは、次の手順に従って IP許可リストを適用できます。

**IP許可リストを適用するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインします。
1. 適切な組織を選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。
1. **環境** 画面で特定の環境の詳細ページに移動します。
1. **IP許可リスト** テーブルに移動します。
1. このテーブルの上部にある入力フィールドを使用すると、IP 許可リストと、その適用先となるオーサーサービスまたはパブリッシュサービスを選択できます。
適用するには、IP 許可リストがCloud Managerに既に存在している必要があります。 [IP許可リストの追加 ](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) を参照してください。
1. 「**適用**」をクリックし、送信を確認します。

## IP許可リストの適用解除 {#un-applying}

**ビジネスオーナー** または **デプロイメントマネージャー** の役割を持つユーザーは、次の手順に従って IP許可リストの適用を解除できます。

**IP許可リストの適用を解除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインします。
1. 適切な組織を選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。
1. **環境** 画面で特定の環境の詳細ページに移動します。1.**IP許可リスト** テーブルに移動します。
1. 適用を解除する IP許可リストの行を見つけます。
1. 識別された行の右側で、省略記号ボタンをクリックし、「**適用解除**」を選択します。
1. 送信を確認します。
