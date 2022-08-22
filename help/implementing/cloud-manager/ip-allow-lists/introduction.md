---
title: IP 許可リストの概要
description: AEM as a Cloud Service ドメインにユーザーがアクセスできるアドレスを IP 許可リストで制限する方法を説明します。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 100%

---


# IP 許可リストの概要 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="IP 許可リストの管理"
>abstract="AEM as a Cloud Service はインターネット経由でアクセスでき、ユーザー認証および承認を通じて安全性が確保されています。Cloud Manager の IP 許可リストを使用すると、信頼できる IP アドレスのみにアクセスを制限して制御することができます。適切な権限を持つ Cloud Manager ユーザーは、信頼できる IP アドレスの許可リストを作成し、そのアドレスから、サイトのユーザーが AEM ドメインにアクセスできるようにすることができます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=ja" text="IP 許可リストの追加"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html?lang=ja" text="IP 許可リストの表示および更新"

AEM as a Cloud Service はインターネット経由でアクセスでき、ユーザー認証および承認を通じて安全性が確保されています。Cloud Manager の IP 許可リストを使用すると、信頼できる IP アドレスのみにアクセスを制限して制御することができます。適切な権限を持つ Cloud Manager ユーザーは、信頼できる IP アドレスの許可リストを作成し、そのアドレスから、サイトのユーザーが AEM ドメインにアクセスできるようにすることができます。

IP 許可リストを一度追加すれば、環境のオーサーサービスやパブリッシュサービスにユニットまたはエンティティとして何度でも適用または適用解除できます。

## 制限事項 {#limitations}

IP 許可リストには、注意すべき制限がいくつかあります。

* プログラムに追加できる IP 許可リストは最大 50 個です。
* 各 IP 許可リストには、最大 50 個の IP／CIDR アドレスを追加できます。
* 環境のオーサー／パブリッシュサービスに対応する IP 許可リストの名前は、Cloud Manager でサポートされています。
