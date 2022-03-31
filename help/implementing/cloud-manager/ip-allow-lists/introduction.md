---
title: IP許可リストの概要
description: IP許可リストが、ユーザーがAEMのas a Cloud Serviceドメインにアクセスできるアドレスを制限する方法を説明します。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 11%

---


# IP許可リストの概要 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="IP 許可リストの管理"
>abstract="AEM as a cloud service は、インターネットを介してアクセスでき、ユーザー認証と承認を通じて保護されます。 Cloud Manager の IP許可リストは、信頼済み IP アドレスへのアクセスのみを制限および制御するために使用できます。 適切な権限を持つ Cloud Manager ユーザーは、信頼済み IP アドレスの許可リストを作成し、そこから、サイトのユーザーがAEMドメインにアクセスできるようにします。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=ja" text="IP 許可リストの追加"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html?lang=ja" text="IP 許可リストの表示および更新"

AEM as a cloud service は、インターネットを介してアクセスでき、ユーザー認証と承認を通じて保護されます。 Cloud Manager の IP許可リストは、信頼済み IP アドレスへのアクセスのみを制限および制御するために使用できます。 適切な権限を持つ Cloud Manager ユーザーは、信頼済み IP アドレスの許可リストを作成し、そこから、サイトのユーザーがAEMドメインにアクセスできるようにします。

IP許可リストは、環境内のオーサーサービスやパブリッシャーサービスに対して、1 つの単位またはエンティティとして 1 回だけ追加したり、複数回適用または適用解除したりできます。

## 制限事項 {#limitations}

IP には、リストに留意できる数多くの制限があります。

* プログラムに追加できる IP許可リストは最大 50 個です
* 各 IP アドレスには、最大で 50 個の IP/CIDR アドレスを追加できます。許可リスト
* IP許可リスト名は、環境内のオーサーサービスやパブリッシュサービスで Cloud Manager でサポートされています。
