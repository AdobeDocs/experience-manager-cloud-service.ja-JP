---
title: オーサー層の保護
description: オーサー層の保護
translation-type: tm+mt
source-git-commit: e772687c4034a364912aa426a133134571246db9
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