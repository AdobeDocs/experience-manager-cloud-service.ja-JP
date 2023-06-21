---
title: オーサー層の保護
description: オーサー層の保護
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 69%

---

# オーサー層の保護 {#securing-the-author-tier}

AEM as a Cloud Service を使用して新しい環境を作成する場合、オーサー層へはデフォルトでインターネットからアクセスできます。オーサー層へのアクセスを保護するために、ネットワークポリシーをさらに設定することができます。 詳しくは、[IP 許可リストの適用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=ja)を参照してください。この手順は、オーサー環境に対してネットワークアクセスが許可される IP 範囲を承認することに基づいています。

これらのルールを適切に配置するには、 [Adobe Admin Console](https://adminconsole.adobe.com/) リクエストされた情報を使用：

* プログラム ID
* 環境 ID
* 承認する IP アドレスの範囲

