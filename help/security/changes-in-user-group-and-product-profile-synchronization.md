---
title: ユーザーグループと製品プロファイルの同期の変更
description: AEM as a Cloud Service に導入されるユーザーグループと製品プロファイルの同期に関する変更点について説明します。
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: 5c103fcce1ae47bc89f4f572d89967c62c1f7603
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 79%

---

# ユーザーグループと製品プロファイルの同期の変更 {#changes-in-user-group-and-product-profile-synchronization}

ユーザーが AEM as a Cloud Service にログインするか、アクセストークンを使用するたびに、Adobe Admin Console ユーザーグループ、製品プロファイルおよび製品プロファイルサービスがグループとして AEM リポジトリに同期されます。

AEM メンテナンスリリース 19149 以降、UI を整理しパフォーマンスを最適化するために、グループ同期の動作が変更されています。 特に、次の 2 つのカテゴリのAEM グループのユーザーグループのメンバーシップは同期されなくなります。

1. サフィックス `GROUP_NAME_SUFFIX` を持つ AEM グループ。これらのグループは、Adobe Developer Console には表示されませんが、以下に示すように AEM グループ管理画面に表示されます。万が一、AEM アプリケーションがこれらのグループを参照する場合は、代わりにそのサフィックスのない Adobe Admin Console ユーザーグループを参照してください。

   ![削除されたグループ 1](/help/security/assets/removed-groups-1.png)

1. 特定の環境に関連しない Adobe Admin Console 製品プロファイルに関連付けられた AEM グループ。これには、次の製品プロファイルが含まれる場合があります。

   * 他のアドビ製品に関連する
   * 他の AEM プログラムに関連する
   * 同じ AEM プログラム内の他の AEM 環境に関連する
   * Cloud Manager（`Business Owner - Cloud Service` など）に関連する

   例えば、以下の画像では、サフィックスが現在の環境に関連していないパターン `AEM Administrators-<suffix>` または `AEM Users-<suffix>` の行が多数あります。

   ![削除されたグループ 2](/help/security/assets/removed-groups-2.png)

Cloud Manager の環境のアクションメニューでアクセスを管理／**オーサープロファイル**（または&#x200B;**パブリッシュプロファイル**）を選択すると、現在の環境に関連しているサフィックスを確認できます。

![サフィックスを確認](/help/security/assets/suffix-check.png)

これにより、以下のスクリーンショットに示すように、Adobe Admin Console に移動します。`<suffix>` は、ランダムな文字セット、または層、プログラムおよび環境 ID（例：`author - Program 12345 - Environment 45678`）のいずれかである場合があります。

![Admin Console のサフィックス](/help/security/assets/admin-console-profile-suffixes.png)

万が一、AEM アプリケーションが参照しているグループが AEM に表示されなくなる場合は、代わりに i) 適切な AEM インスタンスの製品プロファイル、または ii) Adobe Admin Console ユーザーグループのいずれかを使用してください。

ユーザーのグループメンバーシップは環境にログインする際に同期され、現在の環境に関連しないグループから削除されます。 グループ自体は残り、この機能が有効になってからログインしていないユーザーが含まれます。
