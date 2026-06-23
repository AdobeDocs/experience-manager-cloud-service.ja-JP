---
title: IP 許可リストを追加
description: Cloud Manager を使用して独自の IP 許可リストを追加する方法を説明します。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: d36dc453097b1f2507ff1ca6d775acf8b9ac5add
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 63%

---


# IP 許可リストの追加 {#add-ip-allow-list}

Cloud Manager を使用して独自の IP 許可リストを追加する方法を説明します。

IP 許可リストを追加するには、**Business Owner**&#x200B;または&#x200B;**Deployment Manager**&#x200B;の役割を持つユーザーが、次の手順に従います。

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

**IP 許可リストを追加するには：**

{{sign-in-to-cloud-manager}}

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、プログラムを選択します。

1. **プログラムの概要** ページで、左側のメニューを使用して（必要に応じて、左上隅の![ メニューアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)をクリックしてメニューを表示）、![ タスクリストアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP 許可リスト**&#x200B;をクリックします。

   ![左側のサイドメニューの「IP 許可リスト」オプション](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. IP 許可リストページの右上隅付近にある「**IP 許可リストを追加**」をクリックします。

   ![IP 許可リストを追加ダイアログボックス](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. **IP 許可リストを追加**&#x200B;ダイアログボックスの **IP 許可リスト名**&#x200B;フィールドに、IP 許可リストの参照に使用する名前を入力します。 この名前は情報提供のみを目的としています。 リストの特定に役立つ説明文であることを確認します。

1. 「**IP アドレス／CIDR**」フィールドに、最大 50 個の IP アドレスまたは CIDR ブロックを入力します。 次のいずれかの方法で追加できます。

   * 一度に 1 つずつ：アドレスを入力し、`Enter` キーを押します。 追加のアドレスごとに繰り返します。
   * 一度に複数：アドレスをコンマ（,）またはタブで区切って入力し、`Enter`を押して、各アドレスを個別に処理します。

1. 最後の IP アドレスまたは CIDR ブロックの入力が完了したら、`Enter` キーを押して入力を確認します。 `Enter` キーを押すと、エントリに対する確認が行われ、「**保存**」ボタンがアクティブになります。

1. 「**保存**」をクリックします。

保存後、新しく作成されたIP 許可リストは、**IP 許可リスト** ページテーブルに行として表示されます。

