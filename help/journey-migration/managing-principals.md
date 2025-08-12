---
title: プリンシパルの管理
description: Admin Console を使用した移行でのプリンシパルの管理
exl-id: a75598d0-8f59-466b-984e-dfe527388c2a
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 100%

---

# プリンシパルの管理 {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="プリンシパルの管理"
>abstract="コンテンツ移行中または移行後にユーザーを管理するために必要な操作について説明します"

コンテンツを AEM as a Cloud Service クラウド環境に転送する前に、Admin Console で実行できるタスクがいくつかあります。ユーザーの作成、グループの作成、グループへのユーザーの割り当てです。これらのユーザーとグループは、IMS（アドビの Identity Management サービス）に存在します。IMS は、すべてのアドビクラウドベースのサービスでのユーザーとグループの管理に使用されます。

## Admin Console でのグループとユーザーの作成

[AEM プリンシパルに Admin Console を使用](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up)では、IMS でユーザーとグループを作成する方法と、同時にまたは後でユーザーをグループに追加する方法について詳しく説明します。このドキュメントには、それらを作成する 3 つのオプション（Admin Console から手動で作成、Admin Console からの CSV アップロードで作成、ユーザー同期ツールを使用した作成）が含まれています。

手動オプションでは、一度に 1 つのグループまたはユーザーを作成できます。CSV アップロードでは、複数のユーザーとグループを一度に作成およびリンクできます。また、ユーザー同期ツールでは、既存の IDP を使用して IMS ユーザーとグループを作成および管理できます。

ユーザーが IMS を使用して AEM にログインすると、ユーザーの AEM 表示域が作成されます。さらに、ユーザーが属する IMS グループには、AEM で作成された同等の AEM グループが含まれます。これらの IMS で作成された AEM ユーザーとグループは、主に Admin Console を使用して管理されます。

コンテンツの移行が完了したら、通常、ユーザーが移行されたコンテンツにアクセスできるように、IMS グループには追加の設定が必要になります。詳しくは、[移行後のプリンシパルの移行](/help/journey-migration/managing-principals-after-migration.md)を参照してください。

AEM と IMS のユーザーとグループを統合および管理する方法について詳しくは、[チュートリアル、AEM ユーザー、グループ、権限](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions)も参照してください。
