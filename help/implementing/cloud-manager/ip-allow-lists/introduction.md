---
title: IP 許可リストの概要
description: AEM as a Cloud Serviceでユーザーがドメインにアクセスできるアドレスを IP許可リストで制限する方法を説明します。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 20%

---


# IP 許可リストの概要 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="IP 許可リストの管理"
>abstract="AEM as a Cloud Serviceはインターネット経由でアクセスでき、ユーザー認証および承認を通じて保護されています。 Cloud Managerの IP 許可リストを使用すると、信頼できる IP アドレスのみにアクセスを制限して制御することができます。 適切な権限を持つ Cloud Manager ユーザーは、サイトのユーザーが AEM ドメインにアクセスできる、信頼できる IP アドレスの許可リストを作成できます。"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="IP 許可リストの追加"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="IP許可リストの表示と更新"

AEM as a cloud service は、デフォルトでは、インターネット経由でアクセスできます。 セキュリティはユーザーの認証および認可によって処理されますが、信頼できる IP アドレスにのみアクセスを制限する方法は IP 許可リストです。

Cloud Managerの IP 許可リストを使用すると、そのような信頼できる IP アドレスのみにアクセスを制限および制御できます。 適切な権限を持つCloud Manager ユーザーは、信頼できる IP アドレスから [IP 許可リストを作成 ](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) し、そのアドレスからのみ、サイトのユーザーがAEM ドメインにアクセスできるようにすることができます。

追加後は、環境内のオーサーサービス ](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) パブリッシュサービス、またはその両方に対して、[IP許可リストを 1 つのユニットまたはエンティティとして何度でも適用または適用解除できます。

>[!NOTE]
>
>IP許可リストが適用されない場合、デフォルトでは、すべての IP アドレスが許可されます。 IP許可リストが適用されている場合、IP 許可リスト上のアドレス以外の IP アドレスは許可されません。

## 制限事項 {#limitations}

IP許可リストには、注意すべきいくつかの制限があります。

* プログラムに追加できる IP許可リストは最大 50 個です。
* 各 IP 許可リストには最大 50 個の IP/CIDR アドレスを追加できます。
* Cloud Managerでは、環境内のオーサーサービスとパブリッシュサービスのどちらか一方または両方の IP許可リスト名がサポートされています。
