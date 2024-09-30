---
title: IP 許可リストの適用と適用解除
description: IP 許可リストを Cloud Manager 環境に適用および適用解除する方法を説明します。
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1902e9b237adbdaff172535d0904d0faa615e9d1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# IP 許可リストの適用と適用解除 {#apply-allow-list}

IP 許可リストを適用すると、リストの定義に含まれているすべての IP 範囲が環境内のオーサーサービスまたはパブリッシュサービスに関連付けられます。リストの適用を解除すると、この処理の逆になります。

{{add-cm-allowlist-frontend-pipeline}}

{{ip-allow-lists-ue}}

## IP 許可リストの適用 {#applying}

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、次の手順に従って IP 許可リストを適用できます。

**IP 許可リストを適用するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインします。
1. 適切な組織を選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. **概要**&#x200B;ページから、**環境**&#x200B;画面に移動します。
1. **環境**&#x200B;画面で、特定の環境の詳細ページに移動します。
1. **IP 許可リスト**&#x200B;テーブルに移動します。
1. このテーブルの上部にある入力フィールドを使用すると、IP許可リストと、その適用先となるオーサーサービス、Publish サービスまたはプレビューサービスを選択できます。
IP 許可リストを適用するには、その IP 許可リストが既に Cloud Manager に存在する必要があります。詳しくは、[IP 許可リストの追加](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)を参照してください。
1. ![ 追加アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)**適用** をクリックし、送信を確認します。

## IP 許可リストの適用解除 {#un-applying}

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、次の手順に従って IP 許可リストを適用解除できます。

**IP 許可リストを適用解除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインします。
1. 適切な組織を選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. **概要** ページから **環境** ページに移動します。
1. 特定の環境の詳細ページに移動します。
1. 「一般」タブから、「**IP許可リスト**」テーブルまでスクロールします。
1. 適用を解除する IP 許可リストの行を特定します。
1. 識別された行の右側で、![ その他アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。
1. **適用解除** をクリックします。
1. **IP許可リストの適用解除** ダイアログボックスで、「**適用解除**」をクリックします。
