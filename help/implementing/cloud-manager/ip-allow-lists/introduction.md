---
title: IP 許可リストの概要
description: AEM as a Cloud Service のドメインにユーザーがアクセスできるアドレスを IP 許可リストで制限する方法を説明します。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 100%

---


# IP 許可リストの概要 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="IP 許可リストの管理"
>abstract="AEM as a Cloud Service はインターネット経由でアクセスでき、ユーザー認証および承認を通じて安全性が確保されています。Cloud Manager の IP 許可リストを使用すると、信頼できる IP アドレスのみにアクセスを制限して制御することができます。適切な権限を持つ Cloud Manager ユーザーは、サイトのユーザーが AEM ドメインにアクセスできる、信頼できる IP アドレスの許可リストを作成できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=ja" text="IP 許可リストの追加"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html?lang=ja" text="IP 許可リストの表示および更新"

AEM as a cloud service は、デフォルトでは、インターネット経由でアクセスできます。 セキュリティはユーザーの認証および認可によって処理されますが、信頼できる IP アドレスにのみアクセスを制限する方法は IP 許可リストです。

Cloud Manager の IP 許可リストを使用すると、そのような信頼できる IP アドレスのみにアクセスを制限および制御できます。適切な権限を持つ Cloud Manager ユーザーは、サイトのユーザーが AEM ドメインにアクセスできる、信頼できる IP アドレスの[許可リストを作成](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)できます。

IP 許可リストを追加すれば、環境内のオーサー／パブリッシュサービスに対して、ユニットやエンティティとして何度でも [IP 許可リストを適用または適用解除](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)できます。

>[!NOTE]
>
>IP 許可リストが適用されない場合、デフォルトでは、すべての IP アドレスが許可されます。 IP 許可リストが適用されると、IP 許可リスト上の IP アドレス以外は禁止されます。

## 制限事項 {#limitations}

IP 許可リストには、留意すべき制限がいくつかあります。

* プログラムに追加できる IP 許可リストは最大 50 個です。
* 各 IP 許可リストには、最大 50 個の IP／CIDR アドレスを追加できます。
* 環境のオーサー／パブリッシュサービス、またはその両方に対応する IP 許可リストの名前は、Cloud Manager でサポートされています。
