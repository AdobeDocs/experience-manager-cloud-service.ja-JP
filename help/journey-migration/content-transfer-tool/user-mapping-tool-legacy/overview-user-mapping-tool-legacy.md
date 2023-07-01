---
title: ユーザーマッピングツールの概要（従来）
description: ユーザーマッピングツールの概要（レガシー）
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 28%

---

# ユーザーマッピングツールの概要（従来） {#overview-user-mapping-tool}

>[!INFO]
>
>このドキュメントでは、ツールの廃止バージョンを参照しています。 最新バージョンについて詳しくは、 [ユーザーマッピングとプリンシパルの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

<!-- Alexandru: drafting this for now

NOTE: "LEGACY" for user mapping includes everything before (that is, not including) 2.0.16 of CTT.

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## はじめに {#introduction}

Adobe Experience Manager(AEM)as a Cloud Serviceへの移行プロセスの一環として、ユーザーとグループを既存のAEMシステムからAEM as a Cloud Serviceに移行する必要があります。 この移行は、コンテンツ転送ツールでおこないます。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。この統合では、 [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) ユーザーとユーザーグループを管理するための ユーザープロファイル情報は、すべてのAdobeクラウドアプリケーションに対してシングルサインオンを提供するAdobeIdentity Management System(IMS) で一元化されます。 詳しくは、 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=en#identity-management). この変更により、Cloud Serviceオーサーインスタンスでのユーザーおよびグループの重複を避けるために、既存のユーザーおよびグループを IMS ID にマッピングする必要があります。

## ユーザーマッピングツール {#mapping-tool}

コンテンツ転送ツール（ユーザーマッピングなし）は、移行されるコンテンツに関連付けられているすべてのユーザーとグループを移行します。 ユーザーマッピングツールは、コンテンツ転送ツールの一部です。 AEM as a Cloud Serviceで使用されるシングルサインオン機能である IMS でユーザーが正しく認識されるように編集するのが目的です。 これらの変更が完了すると、コンテンツ転送ツールは指定されたコンテンツのユーザーとグループを通常どおり移行します。

### 次の手順 {#whats-next}

ユーザーマッピングツールの概要を理解したら、ユーザーマッピングツールを使用する前に、重要な考慮事項や例外的状況を確認する準備が整いました。詳しくは、[ユーザーマッピングツールの重要な考慮事項](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)を参照してください。
