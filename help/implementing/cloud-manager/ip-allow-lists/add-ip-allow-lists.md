---
title: IP許可リストの追加
description: Cloud Manager を使用して独自の IP許可リストを追加する方法を説明します。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 378ff582435f1ab3db431a0c9c3e80a4661cccc4
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 15%

---


# IP 許可リストの追加 {#add-ip-allow-list}

Cloud Manager を使用して独自の IP許可リストを追加する方法を説明します。

ユーザーの **ビジネスオーナー** または **デプロイメントマネージャー** 役割は、次の手順に従って IP許可リストを追加できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. に移動します。 **環境** 画面から **概要** ページ。

1. **環境**&#x200B;画面から **IP 許可リスト**&#x200B;ページに移動します。

   ![サイドパネルの「IP許可リスト」オプション](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. クリック **IP の追加許可リスト** 開く **IP の追加許可リスト** ダイアログ。

   ![[IP許可リストの追加 ] ダイアログ](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 許可リストを参照するために使用する名前を **IP許可リスト名** フィールドに入力します。

   * これは情報提供のみで、リストを識別するのに役立つ説明的なものにする必要があります。

1. で IP または IP CIDR ブロックを入力 **IP アドレス/CIDR** フィールドに入力します。

   * 複数のブロックは、コンマまたはタブで区切ることができます。

1. クリック **保存** 送信を確認するには、をクリックします。

保存すると、新しく作成された IP許可リストが **IP許可リスト** ページ。
