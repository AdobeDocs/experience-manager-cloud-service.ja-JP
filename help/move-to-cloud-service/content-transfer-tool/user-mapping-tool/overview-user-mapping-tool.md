---
title: ユーザーマッピングツールの概要
description: ユーザーマッピングツールの概要
source-git-commit: 9d131daf5b6a0b1530ebff48627f6130ef716f3e
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 71%

---


# ユーザーマッピングツールの概要 {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="ユーザーマッピングツール"
>abstract="コンテンツ転送ツールは、ユーザーとグループを既存の AEM システムから AEM as a Cloud Service に移動する際に役に立ちます。Cloud Service オーサーインスタンスでのユーザーおよびグループの重複を避けるために、既存のユーザーおよびグループをそれぞれの IMS ID にマッピングする必要があります。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#important-considerations" text="ユーザーマッピングツール使用時の重要な考慮事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#using-user-mapping-tool" text="ユーザーマッピングツールの使用"

## はじめに {#introduction}

Adobe Experience Manager（AEM）as a Cloud Service への移行の一環として、ユーザーとグループを既存の AEM システムから AEM as a Cloud Service に移行する必要があります。これには、コンテンツ転送ツールを使用します。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。それには、[Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用してユーザーとユーザーグループを管理する必要があります。ユーザープロファイル情報が Adobe Identity Management System（IMS）に一元化され、すべての Adobe クラウドアプリケーションでシングルサインオンが利用可能です。詳しくは、[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=ja#identity-management) を参照してください。この変更により、Cloud Service オーサーインスタンスでのユーザーおよびグループの重複を避けるために、既存のユーザーおよびグループをそれぞれの IMS ID にマッピングする必要があります。

## ユーザーマッピングツール {#mapping-tool}

コンテンツ転送ツール（ユーザーマッピングなし）は、移行されるコンテンツに関連付けられているすべてのユーザーとグループを移行します。 ユーザーマッピングツールはコンテンツ転送ツールの一部で、AEM as a Cloud Serviceで使用されるシングルサインオン機能である IMS で正しく認識されるようにユーザーとグループを変更することだけが目的です。 これらの変更が完了すると、コンテンツ転送ツールは、指定したコンテンツのユーザーとグループを通常どおり移行します。
