---
title: ユーザーマッピングツールの概要（従来）
description: ユーザーマッピングツールの概要（従来）
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 100%

---


# ユーザーマッピングツールの概要（従来） {#overview-user-mapping-tool}

>[!INFO]
>
>このドキュメントでは、ツールの非推奨（廃止予定）バージョンについて説明します。最新バージョンについて詳しくは、[グループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)を参照してください。

<!-- Alexandru: drafting this for now

NOTE: "LEGACY" for user mapping includes everything before (that is, not including) 2.0.16 of CTT.

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## はじめに {#introduction}

Adobe Experience Manager（AEM）as a Cloud Service への移行の一環として、ユーザーとグループを既存の AEM システムから AEM as a Cloud Service に移行する必要があります。この移行には、コンテンツトランスファーツールを使用します。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。この統合では、ユーザーとユーザーグループを管理するために [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用する必要があります。ユーザープロファイル情報が Adobe Identity Management System（IMS）に一元化され、すべての Adobe クラウドアプリケーションでシングルサインオンが利用可能です。詳しくは、[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=ja#identity-management) を参照してください。この変更により、Cloud Service オーサーインスタンスでのユーザーおよびグループの重複を避けるために、既存のユーザーおよびグループをそれぞれの IMS ID にマッピングする必要があります。

## ユーザーマッピングツール {#mapping-tool}

コンテンツトランスファーツール（ユーザーマッピングなし）では、移行されるコンテンツに関連付けられているすべてのユーザーとグループを移行します。ユーザーマッピングツールは、コンテンツトランスファーツールの一部です。AEM as a Cloud Service で使用されるシングルサインオン機能である IMS で正しく認識されるように、ユーザーを編集することのみを目的としています。これらの修正が完了すると、コンテンツトランスファーツールが、指定されたコンテンツのユーザーとグループを通常どおり移行します。

### 次の手順 {#whats-next}

ユーザーマッピングツールの概要を理解したら、ユーザーマッピングツールを使用する前に、重要な考慮事項や例外的状況を確認する準備が整いました。詳しくは、[ユーザーマッピングツールの重要な考慮事項](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)を参照してください。
