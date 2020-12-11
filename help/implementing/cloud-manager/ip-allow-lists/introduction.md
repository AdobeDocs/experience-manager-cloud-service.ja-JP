---
title: 概要 — Could ManagerでのIP許可リスト
description: 概要 — Could ManagerでのIP許可リスト
translation-type: tm+mt
source-git-commit: e6a8d69ea87ac56a51cde2f131c4accff1bea527
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 概要 {#introduction}

クラウドサービスとしてのAEMはインターネットに公開され、セキュリティはユーザー認証と認証によって処理されます。 IPの許可一覧は、Cloud Managerの機能で、信頼できるユーザーへのアクセスのみを制限および制御するために使用されます。 この機能を使用すると、権限を持つユーザーは、サイトユーザーがAEMドメインにアクセスできる信頼済みIPアドレスの許可リストを作成できます。

IP許可リストは1回追加すると、1つのユニットまたはエンティティとして、環境の作成者サービスや発行者サービスに対して、複数回適用または非適用できます。

>[!NOTE]
>IP許可リスト名は、環境内の作成者サービスと発行サービスのCloud Managerでサポートされています。

権限を持つユーザーは、Cloud Manager UI IP許可リストページまたは環境の詳細ページを使用して、次のような環境のIP許可リストを管理するためのタスクを実行できます。

* [IP許可リストの追加](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
   >[!NOTE]
   > 1回追加だけルールを再利用したり、プログラム内の環境サービス間で任意の回数ルールを適用したりできます。
* [IP許可リストの表示と更新](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
* [IP許可リストの適用または適用解除](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
* [IP許可リストの削除](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)