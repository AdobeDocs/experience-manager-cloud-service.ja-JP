---
title: IP 許可リストの追加
description: Cloud Manager を使用して独自の IP許可リストを追加する方法を説明します。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: fa6d0670a011276facc561f62f52c6e69147a49e
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 87%

---


# IP 許可リストの追加 {#add-ip-allow-list}

Cloud Manager を使用して独自の IP許可リストを追加する方法を説明します。

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、次の手順に従って IP 許可リストを追加できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 日 **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、プログラムを選択します。

1. から **概要** ページで、に移動します **IP許可リスト** 「サイドナビゲーション」タブを使用してページします。

   ![サイドパネルの「IP 許可リスト」オプション](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 「**IP 許可リストを追加**」をクリックします。

   ![IP 許可リストを追加ダイアログボックス](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. **IP許可リストを追加**&#x200B;ダイアログボックスで、「**IP 許可リスト名**」フィールドに許可リストの参照に使用する名前を入力します。

   * この名前は情報提供のみで、リストを識別するのに役立つ説明的なものにする必要があります。

1. 「**IP アドレス／CIDR**」フィールドに、IP または IP CIDR ブロックを入力します。

   * 複数のブロックは、コンマまたはタブで区切ることができます。

1. 「**保存**」をクリックします。

保存すると、新しく作成した IP 許可リストが、**IP 許可リスト**&#x200B;ページのテーブルの 1 行として表示されます。
