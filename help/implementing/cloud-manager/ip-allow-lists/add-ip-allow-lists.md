---
title: IP 許可リストの追加
description: Cloud Manager を使用して独自の IP許可リストに加えるを追加する方法を説明します。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 30%

---


# IP 許可リストの追加 {#add-ip-allow-list}

Cloud Manager を使用して独自の IP許可リストに加えるを追加する方法を説明します。

Adobe Analytics の **ビジネスオーナー** または **デプロイメントマネージャー** 役割は、次の手順に従って IP アドレスを追加でき許可リストに加えるます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 次から： **概要** ページで、 **環境** 画面。

1. 次から： **環境** 画面で、 **IP許可リスト** ページに貼り付けます。

   ![サイドパネルの「IP 許可リスト」オプション](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. クリック **IP の追加許可リスト**.

   ![[IP許可リストの追加 ] ダイアログボックス](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Adobe Analytics の **IP の追加許可リスト** ダイアログボックスで、の参照に使用する名前を許可リストに加える **IP許可リスト名** フィールドに入力します。

   * この名前は情報提供のみを目的としており、リストを識別するのに役立つ説明的な名前にする必要があります。

1. 「**IP アドレス／CIDR**」フィールドに、IP または IP CIDR ブロックを入力します。

   * 複数のブロックは、コンマまたはタブで区切ることができます。

1. 「**保存**」をクリックします。

保存後、新しく作成された IP許可リストに加えるは、 **IP許可リスト** ページに貼り付けます。
