---
title: ユーザーマッピングツールの概要（レガシー）
description: ユーザーマッピングツールの概要（レガシー）
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: 8a258c2c929f9af84a1cde99072291a3e7f6cfc3
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 75%

---

# ユーザーマッピングツールの概要（レガシー） {#overview-user-mapping-tool}

>[!INFO]
>
>このドキュメントでは、ツールの廃止バージョンを参照しています。 最新バージョンについて詳しくは、 [ユーザーマッピングとプリンシパルの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

<!-- Alexandru: drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## はじめに {#introduction}

Adobe Experience Manager（AEM）as a Cloud Service への移行の一環として、ユーザーとグループを既存の AEM システムから AEM as a Cloud Service に移行する必要があります。これには、コンテンツ転送ツールを使用します。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。それには、[Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用してユーザーとユーザーグループを管理する必要があります。ユーザープロファイル情報が Adobe Identity Management System（IMS）に一元化され、すべての Adobe クラウドアプリケーションでシングルサインオンが利用可能です。詳しくは、[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=ja#identity-management) を参照してください。この変更により、Cloud Service オーサーインスタンスでのユーザーおよびグループの重複を避けるために、既存のユーザーおよびグループをそれぞれの IMS ID にマッピングする必要があります。

## ユーザーマッピングツール {#mapping-tool}

コンテンツ転送ツール（ユーザーマッピングなし）では、移行されるコンテンツに関連付けられているすべてのユーザーとグループを移行します。ユーザーマッピングツールはコンテンツ転送ツールの一部で、AEM as a Cloud Serviceで使用されるシングルサインオン機能である IMS でユーザーが正しく認識されるようにユーザーを変更することが唯一の目的です。 これらの修正が完了すると、コンテンツ転送ツールが、指定されたコンテンツのユーザーとグループを通常どおり移行します。

### 次の手順 {#whats-next}

ユーザーマッピングツールの概要を理解したら、ユーザーマッピングツールを使用する前に、重要な考慮事項や例外的状況を確認する準備が整いました。詳しくは、[ユーザーマッピングツールの重要な考慮事項](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)を参照してください。
