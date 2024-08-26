---
title: IP 許可リストを追加
description: Cloud Manager を使用して独自の IP 許可リストを追加する方法を説明します。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1415d07235641262814e81362c806572bcf582ba
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 68%

---


# IP 許可リストの追加 {#add-ip-allow-list}

Cloud Manager を使用して独自の IP 許可リストを追加する方法を説明します。

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、次の手順に従って IP 許可リストを追加できます。

{{add-cm-allowlist-frontend-pipeline}}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要**&#x200B;ページで、左側のサイドパネルを使用して（パネルを表示するには、左上隅のハンバーガーアイコンをクリックしなければならない場合があります）、**IP 許可リスト**&#x200B;をクリックします。

   ![サイドパネルの「IP 許可リスト」オプション](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. IP 許可リストページの右上隅付近にある「**IP 許可リストを追加**」をクリックします。

   ![IP 許可リストを追加ダイアログボックス](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. **IP 許可リストを追加**&#x200B;ダイアログボックスの **IP 許可リスト名**&#x200B;フィールドに、IP 許可リストの参照に使用する名前を入力します。この名前は情報提供のみを目的としています。リストを識別しやすいように、説明的な表記にしてください。

1. **IP アドレス／CIDR** フィールドに、IP または IP CIDR ブロックを入力します。複数のブロックはコンマまたはタブで区切ります。

1. 「**保存**」をクリックします。

保存すると、新しく作成した IP 許可リストが、**IP 許可リスト**&#x200B;ページのテーブルの 1 行として表示されます。

## Cloud Manager IP 許可リストを追加します。 {#add-cm-allowlist}

フロントエンドパイプラインでは、次のCloud Manager IP許可リストを事前に追加する必要があります。

**Cloud Manager の IP 許可リスト**

`52.254.106.192/28,20.186.185.181,52.254.106.240/28,52.254.107.128/28,52.254.105.192/28,52.254.106.176/28,20.186.185.227,52.254.106.144/28,52.254.107.64/28,20.186.185.239,20.22.83.112,52.254.107.80/28,52.254.107.144/28,52.254.106.224/28,20.14.241.153,52.254.107.0/28,52.254.107.32/28,52.254.106.208/28,40.70.154.136/29,52.254.106.160/28,52.254.107.16/28,52.254.106.0/28,4.152.211.251`

フロントエンドパイプラインの実行が中断されないようにするには、このCloud Manager IP許可リストが追加され、環境のオーサーサービスに適用されていることを確認してください *その前に*。パイプラインを有効にします）。

**Cloud Manager IP 許可リストを追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要**&#x200B;ページで、左側のサイドパネルを使用して（パネルを表示するには、左上隅のハンバーガーアイコンをクリックしなければならない場合があります）、**IP 許可リスト**&#x200B;をクリックします。

1. IP 許可リストページの右上隅付近にある「**IP 許可リストを追加**」をクリックします。

1. **IP 許可リストを追加** ダイアログボックスで、「**IP 許可リスト名**」フィールドに「*`Cloud Manager`*」と入力します。

1. 上記のCloud Managerの IP許可リストアドレスのブロックをコピーします。 各アドレスは既にコンマで区切られています。

1. **IP 許可リストを追加** ダイアログボックスで、「**IP アドレス/CIDR**」フィールドにブロックを貼り付けます。

1. アドレスリストの最初のコンマの直後にカーソルを置き、**Enter** キーを押します。

1. 「**保存**」をクリックします。

次に、プログラム環境に [Cloud Manager IP許可リストを適用 ](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) します。



