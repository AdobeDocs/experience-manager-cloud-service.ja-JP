---
title: オーサー層の保護
description: オーサー層へのアクセスを保護するためのネットワークポリシーを設定する方法について説明します。
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: 31e6ec8e9977c8787e14481ee3a94df767262aec
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 36%

---

# オーサー層の保護 {#securing-the-author-tier}

AEM as a Cloud Serviceを使用して環境を作成する場合、オーサー層には、デフォルトでインターネットからアクセスできます。 オーサー層へのアクセスを保護するために、ネットワークポリシーをさらに設定することができます。 詳しくは、[IP 許可リストの適用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=en)を参照してください。この手順は、オーサー環境に対してネットワークアクセスが許可される IP 範囲を承認することに基づいています。

これらのルールを適切に配置するには、 [Adobe Admin Console](https://adminconsole.adobe.com/) リクエストされた情報を使用：

* プログラム ID
* 環境 ID
* 承認する IP アドレスの範囲

