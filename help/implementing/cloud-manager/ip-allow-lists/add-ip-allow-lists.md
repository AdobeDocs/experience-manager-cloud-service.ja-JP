---
title: IP許可リストを追加
description: Cloud Managerを使用して独自の IP許可リストを追加する方法を説明します。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 14%

---


# IP 許可リストの追加 {#add-ip-allow-list}

Cloud Managerを使用して独自の IP許可リストを追加する方法を説明します。

**ビジネスオーナー** または **デプロイメントマネージャー** の役割を持つユーザーは、次の手順に従って IP 許可リストを追加できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要** ページで、左側のサイドパネルを使用して（パネルを表示するには、左上隅のハンバーガーアイコンをクリックする必要がある場合があります）、**IP許可リスト** をクリックします。

   ![ サイドパネルの「IP許可リスト」オプション ](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. IP許可リストページの右上隅付近にある「**IP許可リストを追加**」をクリックします。

   ![IP 許可リストを追加ダイアログボックス](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. **IP 許可リストを追加** ダイアログボックスの **IP 許可リスト名** フィールドに、IP 許可リストの参照に使用する名前を入力します。 この名前は情報提供のみを目的としています。 リストを識別しやすいように、説明的な表記にしてください。

1. **IP アドレス/CIDR** フィールドに、IP または IP CIDR ブロックを入力します。 複数のブロックはコンマまたはタブで区切ります。

1. 「**保存**」をクリックします。

保存すると、新しく作成した IP 許可リストが **IP許可リスト** ページのテーブルの 1 行として表示されます。
