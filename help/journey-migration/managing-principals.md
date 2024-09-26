---
title: プリンシパルの管理
description: Admin Consoleを使用した移行のプリンシパルの管理
exl-id: a75598d0-8f59-466b-984e-dfe527388c2a
source-git-commit: a5bec2c05b46f8db55762b7ee1f346f3bb099d24
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 7%

---

# プリンシパルの管理 {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="プリンシパルの管理"
>abstract="コンテンツ移行中または移行後にユーザーを管理するために必要な操作について説明します"

コンテンツをAEM as a Cloud Service クラウドAdmin Consoleに転送する前に、環境で実行できるタスクがいくつかあります。  ユーザーの作成、グループの作成、グループへのユーザーの割り当て。これらのユーザーとグループは、IMS （AdobeのIdentity Management サービス）に存在します。IMS は、すべてのAdobeクラウドベースのサービスでユーザーとグループを管理するために使用されます。

### Admin Consoleでのグループとそのユーザーの作成

[AEM プリンシパルでAdmin Consoleを使用する ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up) では、IMS でユーザーとグループを作成する方法と、同時または後でユーザーをグループに追加する方法の詳細な手順が説明されています。  ドキュメントには、Admin Consoleからの手動、Admin Consoleからの CSV アップロード、ユーザー同期ツールからの 3 つのオプションがあります。

手動オプションでは、一度に 1 つのグループまたはユーザーを作成できます。CSV アップロードでは、複数のユーザーおよびグループを一度に作成およびリンクできます。ユーザー同期ツールでは、既存の IDP を使用して IMS ユーザーおよびグループを作成および管理できます。

ユーザーが IMS を使用してAEMにログインすると、ユーザーのAEM表現が作成されます。  さらに、ユーザーが属する IMS グループには、AEMで作成された同等のAEM グループが含まれます。  これらの IMS で作成されたAEM ユーザーおよびグループは、引き続き主にAdmin Consoleを使用して管理されます。

コンテンツの移行が完了したら、通常、ユーザーが移行されたコンテンツにアクセスできるように、IMS グループには追加の設定が必要になります。  [ 移行後のプリンシパルの移行 ](/help/journey-migration/managing-principals-after-migration.md) を参照してください

AEMと IMS のユーザーおよびグループを統合および管理する方法について詳しくは、[ チュートリアル、AEM ユーザー、グループ、権限 ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions) も参照してください。
