---
title: ユーザーグループと製品プロファイルの同期の変更
description: AEM as a Cloud Serviceに予定されているユーザーグループと製品プロファイルの同期の変更点について説明します
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: 605a8032430b1be4aacebfcf73cfc16ba7691349
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# ユーザーグループと製品プロファイルの同期の変更 {#changes-in-user-group-and-product-profile-synchronization}

ユーザーがAEM as a Cloud Serviceにログインしたりアクセストークンが使用されたりすると、Adobe Admin Console ユーザーグループ、製品プロファイルおよび製品プロファイルサービスがグループとしてAEM リポジトリに同期されます。

1 月 27 日（PT）に、UI の混乱を減らし、パフォーマンスを最適化するために、同期の動作にいくつかの変更が加えられ、AEMに表示されるグループが少なくなります。 次の 2 つのカテゴリのAEM グループが削除されます。

1. サフィックス `GROUP_NAME_SUFFIX` のAEM グループ これらのグループは、Adobe Developer Consoleには表示されませんが、AEM グループ管理画面には表示されます（下図を参照）。 万一、AEM アプリケーションがこれらのグループを参照する場合は、代わりに、このサフィックスを付けずにAdobe Admin Console ユーザーグループを参照してください。

   ![ 削除されたグループ 1](/help/security/assets/removed-groups-1.png)

1. 特定の環境に関係なく、Adobe Admin Console製品プロファイルに関連付けられたAEM グループ。 これには、次の製品プロファイルが含まれる場合があります。

   * その他Adobe関連商品
   * 他のAEM プログラムと関連する
   * 同じAEM プログラム内の他のAEM環境と関連する
   * Cloud Managerに関連する（例：`Business Owner - Cloud Service`）

   例えば、以下の画像では、パターン `AEM Administrators-<suffix>` または `AEM Users-<suffix>` を持つ行が多数ありますが、サフィックスは現在の環境に関連していません。

   ![ 削除されたグループ 2](/help/security/assets/removed-groups-2.png)

Cloud Managerの環境のアクションメニューで「管理 **アクセス – 作成者プロファイル** （または **Publish プロファイル**）」を選択することで、現在の環境に関連するサフィックスを確認できます。

![ サフィックスを確認 ](/help/security/assets/suffix-check.png)

これにより、以下のスクリーンショットに示すように、Adobe Admin Consoleに移動します。 `<suffix>` は、文字のランダムセットまたは層、プログラム id と環境 id （例：`author - Program 12345 - Environment 45678`）のいずれかである可能性があります。

![Admin Consoleのサフィックス ](/help/security/assets/admin-console-profile-suffixes.png)

万一、AEM アプリケーションで、AEMに表示されないグループが参照されている場合は、代わりに、i）適切なAEM インスタンスの製品プロファイルまたは ii） Adobe Admin Console ユーザーグループを使用するようにします。

