---
title: IP 許可リストの概要
description: AEM as a Cloud Service のドメインにユーザーがアクセスできるアドレスを、IP 許可リストで制限する方法について説明します。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 96179c5f88e8546c12674e34afd0269c1f196d65
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 69%

---


# IP 許可リストの概要 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="IP 許可リストの管理"
>abstract="AEM as a Cloud Service はインターネット経由でアクセスでき、ユーザー認証および承認を通じて安全性が確保されています。Cloud Manager の IP 許可リストを使用すると、信頼できる IP アドレスのみにアクセスを制限して制御することができます。適切な権限を持つ Cloud Manager ユーザーは、サイトのユーザーが AEM ドメインにアクセスできる、信頼できる IP アドレスの許可リストを作成できます。"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="IP 許可リストの追加"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="IP 許可リストの表示と更新"

AEM as a Cloud Service は、デフォルトでは、インターネット経由でアクセスできます。セキュリティはユーザーの認証および認可によって処理されますが、信頼できる IP アドレスにのみアクセスを制限する方法は IP 許可リストです。

Cloud Manager の IP 許可リストを使用すると、そのような信頼できる IP アドレスのみにアクセスを制限および制御できます。適切な権限を持つCloud Manager ユーザーは、信頼できる IP アドレスを [ 作成して IP 許可リストを追加 ](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) し、そのアドレスからのみ、サイトのユーザーがAEM ドメインにアクセスできるようにすることができます。

IP 許可リストを追加すれば、環境内のオーサーサービスとパブリッシュサービスのいずれか一方または両方に対して、ユニットまたはエンティティとして何度でも [IP 許可リストを適用または適用解除](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)することができます。

>[!NOTE]
>
>IP 許可リストが適用されない場合、デフォルトでは、すべての IP アドレスが許可されます。IP 許可リストが適用されると、IP 許可リストに記載されている IP アドレス以外は禁止されます。

## フロントエンドパイプラインでのCloud Manager IP許可リストの使用 {#allowlists-frontend-pipeline}

[ フロントエンドパイプラインを使用してサイトを開発する ](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 場合、または使用する予定の場合は、事前に次のCloud Manager IP許可リストを追加する必要があります。

[IP 許可リストを追加 ](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md#add-cm-allowlist) する際に、*`Cloud Manager`* という名前を付け、以下のアドレスのリストをコピーして IP許可リストダイアログボックスに貼り付けます。

**Cloud Manager の IP 許可リスト**

```text
52.254.106.192/28
20.186.185.181
52.254.106.240/28
52.254.107.128/28
52.254.105.192/28
52.254.106.176/28
20.186.185.227
52.254.106.144/28
52.254.107.64/28
20.186.185.239
20.22.83.112
52.254.107.80/28
52.254.107.144/28
52.254.106.224/28
20.14.241.153
52.254.107.0/28
52.254.107.32/28
52.254.106.208/28
40.70.154.136/29
52.254.106.160/28
52.254.107.16/28
52.254.106.0/28
4.152.211.251
```

フロントエンドパイプラインの実行が中断されないようにするには、このCloud Manager IP 許可リストが追加されていることを確認してください。 次に、オーサー環境にリストを適用します *その前に* パイプラインを有効にします。

[IP許可リストの適用 ](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) を参照してください。
[ フロントエンドパイプラインの有効化 ](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md) を参照してください。


## 制限事項 {#limitations}

IP 許可リストには、留意すべき制限がいくつかあります。

* プログラムに追加できる IP 許可リストは最大 50 個です。
* 各 IP 許可リストに追加できる IP／CIDR アドレスは最大 50 個です。
* 環境内のオーサーサービスとパブリッシュサービスのいずれか一方または両方に対応する IP 許可リスト名が Cloud Manager でサポートされています。
