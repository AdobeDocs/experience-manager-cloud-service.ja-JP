---
title: IP 許可リストの概要
description: AEM as a Cloud Service のドメインにユーザーがアクセスできるアドレスを、IP 許可リストで制限する方法について説明します。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f3cd1bc761c513ebb85351185e7aa0b6f6eb6f33
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 100%

---


# IP 許可リストの概要 {#introduction}

AEM as a Cloud Service のドメインにユーザーがアクセスできるアドレスを、IP 許可リストで制限する方法について説明します。

<!-- Alexandru: contextual help links are broken, temporarily comminting this out until they,re fixed.

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Manage IP Allow Lists"
>abstract="AEM as a Cloud Service is accessible by way of the Internet and is secured through user authentication and authorization. Cloud Manager's IP Allow Lists can be used to limit and control access only to trusted IP addresses. Cloud Manager users with appropriate permissions can create allowlists of trusted IP addresses from which their site's users can access their AEM domains."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="Add an IP Allow List"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="View and update an IP Allow List"

-->

## 概要 {#overview}

AEM as a Cloud Service は、デフォルトでは、インターネット経由でアクセスできます。セキュリティはユーザーの認証および認可によって処理されますが、信頼できる IP アドレスにのみアクセスを制限する方法は IP 許可リストです。

Cloud Manager の IP 許可リストを使用すると、そのような信頼できる IP アドレスのみにアクセスを制限および制御できます。適切な権限を持つ Cloud Manager ユーザーは、信頼できる IP アドレスの [IP 許可リストを作成および追加](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)し、自分のサイトのユーザーがそのアドレスから AEM ドメインにアクセスできるようにすることができます。

IP 許可リストを追加すれば、環境内のオーサーサービスとパブリッシュサービスのいずれか一方または両方に対して、ユニットまたはエンティティとして何度でも [IP 許可リストを適用または適用解除](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)することができます。

>[!NOTE]
>
>IP 許可リストが適用されない場合、デフォルトでは、すべての IP アドレスが許可されます。IP 許可リストが適用されると、IP 許可リストに記載されている IP アドレス以外は禁止されます。

## 使用上のメモ {#usage-notes}

* プログラムに追加できる IP 許可リストは最大 50 個です。
* 各 IP 許可リストに追加できる IP／CIDR アドレスは最大 50 個です。
* 環境内のオーサーサービスとパブリッシュサービスのいずれか一方または両方に対応する IP 許可リスト名が Cloud Manager でサポートされています。

### フロントエンドパイプラインと IP 許可リスト {#front-end-pipeline}

[フロントエンドパイプラインを使用してサイトを開発する場合や、使用する予定がある場合は](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)、事前に次の Cloud Manager IP 許可リストを追加する必要があります。

[IP 許可リストを追加](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md#add-cm-allowlist)する際は、*`Cloud Manager`* という名前を付け、以下のアドレスのリストをコピーして、IP 許可リストダイアログボックスにペーストします。

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

フロントエンドパイプラインの実行が中断されないようにするには、この Cloud Manager IP 許可リストを確実に追加します。次に、パイプラインを有効にする&#x200B;*前*&#x200B;に、リストをオーサー環境に適用します。

詳しくは、[IP 許可リストを適用](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)および[フロントエンドパイプラインを有効にする](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)を参照してください。

### ユニバーサルエディターと IP 許可リスト {#universal-editor}

ユニバーサルエディターを使用してコンテンツを作成する場合は、ユニバーサルエディターサービスが使用する IP アドレスを許可リストに追加して適用する必要があります。

1. `http://universal-editor-service.adobe.io/ip-ranges` の API エンドポイントから、ユニバーサルエディターサービスで使用される IP アドレスを取得します。
1. これらの IP アドレスを含む許可リストを作成し、`Universal Editor Service` などの名前を付けます。
1. `Universal Editor Service` 許可リストを適用します。

ユニバーサルエディターサービスで使用される IP アドレスのリストは変更される可能性があり、それに応じて許可リストを更新する必要があります。
