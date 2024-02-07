---
title: オーサー層の保護
description: オーサー層へのアクセスを保護するために、ネットワークポリシーを設定する方法を説明します。
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: ht
source-wordcount: '119'
ht-degree: 100%

---

# オーサー層の保護 {#securing-the-author-tier}

AEM as a Cloud Service を使用して環境を作成する場合、オーサー層へはデフォルトでインターネットからアクセスできます。オーサー層へのアクセスを保護するために、ネットワークポリシーをさらに設定することができます。詳しくは、[IP 許可リストの適用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=ja)を参照してください。この手順は、オーサー環境に対してネットワークアクセスが許可される IP 範囲を承認することに基づいています。

これらのルールを設定するには、[Adobe Admin Console](https://adminconsole.adobe.com/) から次の必要な情報を添えてサポートチケットを作成してください。

* プログラム ID
* 環境 ID
* 承認する IP アドレスの範囲

