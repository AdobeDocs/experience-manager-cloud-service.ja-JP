---
title: IP 許可リストを追加
description: Cloud Manager を使用して独自の IP 許可リストを追加する方法を説明します。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 593b8c704c5b016bb55ae6a25420b577044b4126
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 100%

---


# IP 許可リストの追加 {#add-ip-allow-list}

Cloud Manager を使用して独自の IP 許可リストを追加する方法を説明します。

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、次の手順に従って IP 許可リストを追加できます。

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

**IP 許可リストを追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要**&#x200B;ページで、左側のサイドメニューを使用して（メニューを表示するには、左上隅の ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックする必要がある場合があります）、![タスクリストアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg)「**IP 許可リスト**」をクリックします。

   ![左側のサイドメニューの「IP 許可リスト」オプション](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. IP 許可リストページの右上隅付近にある「**IP 許可リストを追加**」をクリックします。

   ![IP 許可リストを追加ダイアログボックス](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. **IP 許可リストを追加**&#x200B;ダイアログボックスの **IP 許可リスト名**&#x200B;フィールドに、IP 許可リストの参照に使用する名前を入力します。この名前は情報提供のみを目的としています。リストを識別しやすいように、説明的な表記にしてください。

1. **IP アドレス／CIDR** フィールドに、IP または IP CIDR ブロックを入力します。複数のブロックはコンマまたはタブで区切ります。

1. 「**保存**」をクリックします。

保存すると、新しく作成した IP 許可リストが、**IP 許可リスト**&#x200B;ページのテーブルの 1 行として表示されます。

