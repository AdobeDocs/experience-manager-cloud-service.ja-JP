---
title: コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI
description: コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI について説明します。
exl-id: 077eed73-a066-4273-b2f5-da4bf5cd900c
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 1fb1201fa976e4c0e3c87f22bd9327a55828efef
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 89%

---

# コンテンツフラグメントおよびコンテンツフラグメントモデルの管理 OpenAPI {#content-fragments-and-content-fragment-models-management-openapis}

コンテンツフラグメント管理 API の最新の OpenAPI 実装により、開発者は AEM オーサーで作成、読み取り、更新、削除の操作をプログラムで実行し、AEM に保存されているコンテンツフラグメントモデルとコンテンツフラグメントを管理できます。これらの API は、数多くのユースケースをサポートしています。

完全なドキュメントについては、[コンテンツフラグメント管理 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/) を参照してください。

>[!NOTE]
>
>コンテンツフラグメントに対して [Assets HTTP API](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets) を使用している場合は、新しいコンテンツフラグメント管理 OpenAPI に移行する必要があります。

>[!NOTE]
>
>AEM にログインしていない場合、例えば、統合の一環として別の製品から OpenAPI を使用する場合など、OpenAPI にアクセスするには認証が必要です。
>
>OpenAPI へのアクセスを認証する方法について詳しくは、[OpenAPI ベースの API](/help/implementing/developing/open-api-based-apis.md) を参照してください。

>[!CAUTION]
>
>デフォルトでは、コンテンツフラグメント管理 OpenAPI は公開時に無効になっています。この代わりに、配信指向のユースケースでは、[コンテンツフラグメント配信 OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) を使用することをお勧めします。

>[!NOTE]
>
>使用できる様々な API の概要と、関連する概念のいくつかの比較について詳しくは、[構造化コンテンツの配信と管理用の AEM API](/help/headless/apis-headless-and-content-fragments.md) を参照してください。