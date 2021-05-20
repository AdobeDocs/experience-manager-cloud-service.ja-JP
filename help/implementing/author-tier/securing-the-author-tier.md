---
title: オーサー層の保護
description: オーサー層の保護
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 100%

---

# オーサー層の保護 {#securing-the-author-tier}

AEM as a Cloud Service を使用して新しい環境を作成する場合、オーサー層へはデフォルトでインターネットからアクセスできます。

オーサー層へのアクセスを保護するために、ネットワークポリシーをさらに設定することができます。この手順は、オーサー環境に対してネットワークアクセスが許可される IP 範囲を承認することに基づいています。

これらのルールを設定するには、（Adobe Admin Console から）次の情報をサポートチケットに添付してください。
- プログラム ID
- 環境 ID
- 承認する IP アドレスの範囲
