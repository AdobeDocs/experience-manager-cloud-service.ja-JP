---
title: 概要 - Cloud Manager での IP 許可リスト
description: 概要 - Cloud Manager での IP 許可リスト
translation-type: tm+mt
source-git-commit: 1304a0cfa67c38943b1a36c105fbd5eafb3f8c4f
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 100%

---


# はじめに {#introduction}

AEM as a Cloud Service はインターネットに公開されており、そのセキュリティはユーザー認証および承認を通じて処理されます。IP 許可リストは Cloud Manager の機能で、アクセスを制御して信頼できるユーザーのみに制限するために使用されます。この機能を使用すると、権限を持つユーザーは、サイトユーザーが AEM ドメインにアクセスできる信頼できる IP アドレスの許可リストを作成できます。

IP 許可リストを一度追加すると、環境のオーサーサービスやパブリッシュサービスに 1 つのユニットまたはエンティティとして何度でも適用または適用解除できます。

>[!NOTE]
>環境のオーサー／パブリッシュサービスに対応する IP 許可リストの名前は、Cloud Manager でサポートされています。

権限を持つユーザーは、Cloud Manager UI の IP 許可リストページまたは環境詳細ページを使用して、環境の IP 許可リストを管理するための次のようなタスクを実行できます。

* [IP 許可リストの追加](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
   >[!NOTE]
   > ルールを一度追加すれば、プログラム内のすべての環境サービスで何度でも再利用したり適用したりできます。
* [IP 許可リストの表示または更新](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
* [IP 許可リストの適用または適用解除](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
* [IP 許可リストの削除](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)