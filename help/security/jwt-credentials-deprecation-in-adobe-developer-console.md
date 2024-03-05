---
title: Adobe Developer Console での JWT 資格情報の非推奨（廃止予定）
description: AEM の Adobe Developer Console での JWT 資格情報の非推奨（廃止予定）の影響について説明します。
source-git-commit: a354786f1ddfe50b01def85d3c83da09c6a35d2f
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 86%

---


# Adobe Developer Console での JWT 資格情報の非推奨（廃止予定） {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM as a Cloud Service のお客様は、 [この記事](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) を参照してください。

アドビのお客様は、[Adobe Developer Console](https://developer.adobe.com/console) を使用すると、様々な API へのアクセスを可能にする資格情報を生成できます。お客様は、OAuth サーバー間からシングルページアプリまで、様々な資格情報タイプから選択できます。これらの資格情報タイプの 1 つであるサービスアカウント（JWT）資格情報は、OAuth サーバー間資格情報に代わって非推奨（廃止予定）になりました。新しいサービスアカウント（JWT）資格情報は 2024年5月1日（PT）以降は作成できなくなり、既存の JWT 資格情報は 2025年1月1日（PT）以降は機能しなくなります。非推奨（廃止予定）については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)を参照してください。

この記事では、AEMas a Cloud Serviceによる非推奨の処理方法に関する追加のコンテキストを説明します。

現時点での主な留意点は、AEM の機能で新しい OAuth サーバー間資格情報がまだサポートされていないことです。2024 年 4 月中旬に、AEM as a Cloud ServiceのAEMリリースを通じて、サポートが近日中に提供される予定です。 JWT 格情報を移行する手順が記載されたメールが届いている可能性がありますが、AEM で新しい OAuth サーバー間資格情報タイプがサポートされるまで、資格情報の移行を保留しても問題ありません。

以下の節では、AEM で 4 月中旬にサポートされた後、お客様がサービスアカウント（JWT）資格情報を OAuth サーバー間資格情報に置き換える必要がある（場合によっては置き換えてはいけない）シナリオを示します。今後、資格情報を置き換える方法については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)を参照してください。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)（**Adobe** Developer Console と区別するために名前に **AEM** が含まれています）では、サーバー間 API に使用される [JWT トークン](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)を生成するユーティリティを提供します。これらの資格情報は非推奨（廃止予定）ではなく、引き続き使用できます。


## AEM と他のアドビソリューションの統合 {#integrating-aem-with-other-adobe-solutions}

**アクション**：AEM でサポートされる 2024年4月中旬以降まで移行を待ちます。

**関連するAEMバージョン**: AEMas a Cloud Service

AEM のお客様は、AEM オーサー UI を使用すると、他のすべてのアドビソリューション（例えば、Adobe Target、Adobe Analytics、Adobe Launch、AFCS など）との統合を設定できます。

![AEM と他のソリューションの統合](/help/security/assets/jwt-deprecation.png)

例えば、Adobe Target との統合を設定する手順については、[こちら](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=ja)を参照してください。[AEM での IMS 設定の完了](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=ja#completing-the-ims-configuration-in-aem)の節に記載されている API キーは、4月中旬に AEM でこれらの資格情報がサポートされたら、OAuth サーバー間資格情報タイプに移行する必要があります。これらの手順は、新しい OAuth サーバー間資格情報を適用できるように、4月中旬に改訂される予定です。

## Cloud Manager API {#cloud-manager-apis}

**アクション**：AEM でサポートされる 2024年4月中旬以降まで移行を待ちます。

**関連するAEMバージョン**: AEMas a Cloud Service

お客様は Adobe Developer Console プロジェクトを作成すると、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) を呼び出すことができます。AEM と Cloud Manager でサポートされたら、Adobe Developer プロジェクトの資格情報を OAuth サーバー間資格情報タイプに移行する必要があります。

## 自動生成されたプロジェクト {#autogen-projects}

**アクション**：アドビがお客様に代わって移行するので、移行しないでください。

**関連するAEMバージョン**:AEMas a Cloud Service。

Cloud Manager で AEM as a Cloud Service 環境をプロビジョニングすると、JWT 資格情報を使用して Adobe Developer Console プロジェクトが自動生成されます。以下のスクリーンショットに示すように、このプロジェクトは読み取り専用としてマークされます。お客様は、これらのプロジェクトを OAuth サーバー間資格情報に移行できません。試さないでください。代わりに、資格情報が使用できなくなる前に、アドビがこれらのプロジェクトを独自に移行します。

![自動生成されたプロジェクト](/help/security/assets/jwt-deprecation-autogen-projects.png)

