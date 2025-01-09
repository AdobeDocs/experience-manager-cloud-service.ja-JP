---
title: ユーザーグループと製品プロファイルの同期の変更
description: AEM as a Cloud Serviceに予定されているユーザーグループと製品プロファイルの同期の変更点について説明します
feature: Security
role: Admin
hide: true
hidefromtoc: true
source-git-commit: c3e3905d3896d79149a386241d798f78631184b3
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# ユーザーグループと製品プロファイルの同期の変更 {#changes-in-user-group-and-product-profile-synchronization}

ユーザーがAEM as a Cloud Serviceにログインしたりアクセストークンが使用されたりすると、Adobe Admin Console ユーザーグループ、製品プロファイルおよび製品プロファイルサービスがグループとしてAEM リポジトリに同期されます。

1 月 28 日（PT）に、UI の混乱を減らし、パフォーマンスを最適化するために、同期の動作にいくつかの変更が加えられ、AEMに表示されるグループが少なくなります。 次の 2 つのカテゴリのAEM グループが削除されます。

1. サフィックス `GROUP_NAME_SUFFIX` のAEM グループ これらのグループは、Adobe Developer Consoleには表示されませんが、AEM グループ管理画面には表示されます（下図を参照）。 万一、AEM アプリケーションがこれらのグループを参照する場合は、代わりにAdobe Admin Console ユーザーグループを使用してください。

   ![ 削除されたグループ 1](/help/security/assets/removed-groups-1.png)

1. 特定のAEM層または環境の組み合わせ（`author` や `e4535` など）に関連しないAdobe Admin Console製品プロファイルに関連付けられたAEM グループ。 これには、次の製品プロファイルが含まれる場合があります。

   * その他Adobe関連商品
   * 他のAEM プログラムと関連する
   * 同じAEM プログラム内の他のAEM環境と関連する
   * 同じAEM環境内の異なる層（例えば `author` と `publish`）に関連付けられる
   * Cloud Managerに関連する（例：`Business Owner - Cloud Service`）

   例えば、以下の画像では、パターン `AEM Administrators-<suffix>` または `AEM Users-<suffix>` を持つ行が多数ありますが、サフィックスは現在の環境に関連していません。

   ![ 削除されたグループ 2](/help/security/assets/removed-groups-2.png)

Cloud Managerの環境のアクションメニューで「管理 **アクセス – 作成者プロファイル** （または **Publish プロファイル**）」を選択することで、現在の環境に関連するサフィックスを確認できます。

![ サフィックスを確認 ](/help/security/assets/suffix-check.png)

これにより、以下のスクリーンショットに示すように、Adobe Admin Consoleに移動します。 `<suffix>` は、文字のランダムセットまたは層、プログラム id と環境 id （例：`author - Program 12345 - Environment 45678`）のいずれかである可能性があります。

![Admin Consoleのサフィックス ](/help/security/assets/admin-console-profile-suffixes.png)

万一、AEM アプリケーションがこれらのグループを参照する場合は、代わりにAdobe Admin Console ユーザーグループを使用してください。

>[!NOTE]
>
>特に、次の潜在的な落とし穴に注意してください。
>
>1. AEM アプリケーションは、Cloud Manager製品プロファイルから同期されたAEM グループに依存しています
>1. AEM アプリケーションのパブリッシュ層は、オーサー層製品プロファイルから同期されたAEM グループに依存しています。 これは、インバースシナリオ（パブリッシュ層に基づくオーサー層）にも当てはまります。