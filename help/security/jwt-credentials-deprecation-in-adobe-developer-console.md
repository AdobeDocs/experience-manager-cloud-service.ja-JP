---
title: Adobe Developer Console での JWT 資格情報の廃止
description: AEM の Adobe Developer Console での JWT 資格情報の廃止の影響について説明します。
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: 802e29017d3f1e59ee1676b4172292cb3453648a
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 74%

---

# Adobe Developer Console での JWT 資格情報の廃止 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 のお客様は、[この記事](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console)を参照して、詳細を確認する必要があります。

アドビのお客様は、[Adobe Developer Console](https://developer.adobe.com/console) を使用すると、様々な API へのアクセスを可能にする資格情報を生成できます。お客様は、OAuth サーバー間からシングルページアプリまで、様々な資格情報タイプから選択できます。これらの資格情報タイプの 1 つであるサービスアカウント（JWT）資格情報は、OAuth サーバー間資格情報に代わって非推奨（廃止予定）になりました。新しいサービスアカウント（JWT）資格情報は 2024年6月3日（PT）以降は作成できなくなり、既存の JWT 資格情報は 2025年1月27日（PT）以降は機能しなくなります。非推奨（廃止予定）については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)を参照してください。

この記事では、AEM as a Cloud Service で非推奨（廃止予定）にどのように対処する必要があるかに関する追加のコンテキストを提供します。

現在のところ、主な留意点は、AEM の機能で新しい OAuth サーバー間資格情報がまだサポートされていないことです。AEM as a Cloud Service版のAEM リリースを通じて、2024 年 5 月中旬を予定しているサポートが近日中に提供されます。 JWT 資格情報を移行する手順が記載されたメールが届いているかもしれませんが、AEM で新しい OAuth サーバー間資格情報タイプがサポートされるまで、資格情報の移行を保留してください。

以下では、AEMが 5 月中旬にサービスアカウント（JWT）資格情報をサポートした後に、お客様が OAuth サーバー間資格情報に置き換える必要がある（または置き換えない場合がある）シナリオを示します。 今後、資格情報を置き換える方法については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)を参照してください。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)（**Adobe** Developer Console と区別するために名前に **AEM** が含まれています）では、サーバー間 API に使用される [JWT トークン](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)を生成するユーティリティを提供します。これらの資格情報は非推奨（廃止予定）ではなく、引き続き使用できます。


## AEM と他のアドビソリューションの統合 {#integrating-aem-with-other-adobe-solutions}

**アクション**:AEMがサポートする 2024 年 5 月中旬以降まで移行します（この記事はその時点で更新されます）

**関連する AEM バージョン**：AEM as a Cloud Service

AEM のお客様は、AEM オーサー UI を使用すると、他のすべてのアドビソリューション（例えば、Adobe Target、Adobe Analytics、Adobe Launch、AFCS など）との統合を設定できます。

![AEM と他のソリューションの統合](/help/security/assets/jwt-deprecation.png)

例えば、Adobe Target との統合を設定する手順については、[こちら](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims)を参照してください。の API キー [AEMでの IMS 設定の完了](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims#completing-the-ims-configuration-in-aem) AEMが 5 月中旬にこれらの資格情報をサポートしたら、セクションを OAuth サーバー間資格情報タイプに移行する必要があります。 これらの手順は、5 月中旬に更新される予定で、新しい OAuth サーバー間資格情報を適用する際に役立ちます。

## Cloud Manager API {#cloud-manager-apis}

**アクション**：サーバー間 OAuth 認証情報に移行します。

**関連する AEM バージョン**：AEM as a Cloud Service

お客様は Adobe Developer Console プロジェクトを作成すると、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) を呼び出すことができます。Adobe Developer プロジェクトの資格情報は、非推奨の JWT 資格情報が 2025 年 1 月に期限切れになる前に、OAuth サーバー間資格情報タイプに移行する必要があります。

## 自動生成されたプロジェクト {#autogen-projects}

**アクション**：アドビがお客様に代わって移行するので、お客様側では移行しないでください。

**関連する AEM バージョン**：AEM as a Cloud Service。

Cloud Manager で AEM as a Cloud Service 環境をプロビジョニングすると、JWT 資格情報を使用して Adobe Developer Console プロジェクトが自動生成されます。以下のスクリーンショットに示すように、このプロジェクトは読み取り専用としてマークされます。お客様は、これらのプロジェクトを OAuth サーバー間資格情報に移行できません。試さないでください。代わりに、資格情報が使用できなくなる前に、アドビがこれらのプロジェクトを独自に移行します。

![自動生成されたプロジェクト](/help/security/assets/jwt-deprecation-autogen-projects.png)
