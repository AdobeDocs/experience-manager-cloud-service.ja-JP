---
title: IP 許可リストの概要
description: AEM as a Cloud Service上のドメインにユ許可リストーザーがアクセスできるアドレスを IP が制限する方法を説明します。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 18%

---


# IP 許可リストの概要 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="IP 管理の許可リスト管理"
>abstract="AEM as a cloud service は、インターネットを介してアクセスでき、ユーザー認証と認証を通じて保護されます。 Cloud Manager の IP アドレスを使用し許可リストて、信頼できる IP アドレスへのアクセスのみを制限および制御できます。 適切な権限を持つ Cloud Manager ユーザーは、信許可リスト頼済み IP アドレスのを作成し、そこからサイトのユーザーがAEMドメインにアクセスできるようにします。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="IP 許可リストの追加"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html" text="IP 許可リストの表示および更新"

AEM as a cloud service は、デフォルトでは、インターネット経由でアクセスできます。 セキュリティはユーザーの認証および認可によって処理されますが、信頼できる IP アドレスにのみアクセスを制限する方法は IP 許可リストです。

Cloud Manager の IP アドレスを使用す許可リストると、そのような信頼済み IP アドレスへのアクセスのみを制限および制御できます。 適切な権限を持つ Cloud Manager ユーザーが以下を実行できる [の許可リスト作成](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) を使用します。

追加後、 [IP許可リストの適用/非適用が可能](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 環境内のオーサーサービスやパブリッシャーサービスに対する単位またはエンティティとして複数回

>[!NOTE]
>
>IP アドレスが適用さ許可リストれない場合は、デフォルトではすべての IP アドレスが許可されます。 IP アドレスが適用さ許可リストれる場合、IP アドレス上のアドレス以外に IP アドレスは許可されま許可リストせん。

## 制限事項 {#limitations}

IP の制限にはいくつか許可リストの制限があります。

* プログラムに追加できる IP許可リストは最大 50 個です
* 各 IP アドレスには、最大で 50 個の IP/CIDR アドレスを追加でき許可リストます。
* IP 名許可リストは、環境内のオーサーサービスとパブリッシュサービス、またはその両方に対して Cloud Manager でサポートされます。
