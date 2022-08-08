---
title: IP 許可リストの追加
description: Cloud Manager を使用して独自の IP許可リストを追加する方法を説明します。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 378ff582435f1ab3db431a0c9c3e80a4661cccc4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# IP 許可リストの追加 {#add-ip-allow-list}

Cloud Manager を使用して独自の IP許可リストを追加する方法を説明します。

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、次の手順に従って IP 許可リストを追加できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. **環境**&#x200B;画面から **IP 許可リスト**&#x200B;ページに移動します。

   ![サイドパネルの「IP 許可リスト」オプション](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 「**IP 許可リストを追加**」をクリックして、**IP 許可リストを追加**&#x200B;ダイアログを開きます。

   ![IP 許可リストを追加ダイアログ](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 許可リストルールの参照に使用するわかりやすい名前を「**IP 許可リスト名**」フィールドに入力します。

   * これは情報提供のみで、リストを識別するのに役立つ説明的なものにする必要があります。

1. 「**IP アドレス／CIDR**」フィールドに、IP または IP CIDR ブロックを入力します。

   * 複数のブロックは、コンマまたはタブで区切ることができます。

1. 「**保存**」をクリックして、送信を確認します。

保存すると、新しく作成した IP 許可リストが、**IP 許可リスト**&#x200B;ページのテーブルの 1 行として表示されます。
