---
title: Adobe Developer Console での JWT 資格情報の廃止
description: AEM の Adobe Developer Console での JWT 資格情報の廃止の影響について説明します。
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: b6e26ecaa73aaee37b6b824426dc0cd65d459502
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 62%

---

# Adobe Developer Console での JWT 資格情報の廃止 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 のお客様は、[この記事](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console)を参照して、詳細を確認する必要があります。

アドビのお客様は、[Adobe Developer Console](https://developer.adobe.com/console) を使用すると、様々な API へのアクセスを可能にする資格情報を生成できます。お客様は、OAuth サーバー間からシングルページアプリまで、様々な資格情報タイプから選択できます。これらの資格情報タイプの 1 つであるサービスアカウント（JWT）資格情報は、OAuth サーバー間資格情報に代わって非推奨（廃止予定）になりました。新しいサービスアカウント（JWT）資格情報は 2024年6月3日（PT）以降は作成できなくなり、既存の JWT 資格情報は 2025年1月27日（PT）以降は機能しなくなります。非推奨（廃止予定）については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)を参照してください。

この記事では、AEM as a Cloud Service で非推奨（廃止予定）にどのように対処する必要があるかに関する追加のコンテキストを提供します。

主な留意点は、AEMで、AEM as a Cloud Service用に新しい OAuth サーバー間資格情報がサポートされるようになりました。 JWT 資格情報の移行手順を記載したメールが届いている場合は、この移行を実行できます。

以下の節では、AEMでサポートされるようになったため、お客様がサービスアカウント（JWT）資格情報を OAuth サーバー間資格情報に置き換える必要がある（または置き換えない場合がある）シナリオを示します。 [方法を読む](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) をクリックして認証情報を移行します。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)（**Adobe** Developer Console と区別するために名前に **AEM** が含まれています）では、サーバー間 API に使用される [JWT トークン](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)を生成するユーティリティを提供します。これらの資格情報は非推奨（廃止予定）ではなく、引き続き使用できます。

## AEM と他のアドビソリューションの統合 {#integrating-aem-with-other-adobe-solutions}

**アクション**:AEMが OAuth 認証情報をサポートするようになったので、設定を移行します。

**関連する AEM バージョン**：AEM as a Cloud Service

AEMのお客様は、AEMを使用して他の多くのAdobeソリューションとの統合を設定します。 例えば、Adobe Target、Adobe Analyticsなどです。

参照： [AEM用 IMS 統合の設定as a Cloud Service](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) 方法の詳細：

* oauth 資格情報を使用した設定の作成
* jwt 資格情報で作成された設定を移行して、OAuth 資格情報を使用する

## Cloud Manager API {#cloud-manager-apis}

**アクション**:JWT から OAuth 資格情報に移行できるタイミングを確認します。

**関連する AEM バージョン**：AEM as a Cloud Service

お客様は Adobe Developer Console プロジェクトを作成すると、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) を呼び出すことができます。非推奨の JWT 資格情報の有効期限が 2025年1月に切れる前に、Adobe Developer プロジェクトの資格情報を OAuth サーバー間資格情報タイプに移行する必要があります。

## 自動生成されたプロジェクト {#autogen-projects}

**アクション**：アドビがお客様に代わって移行するので、お客様側では移行しないでください。

**関連する AEM バージョン**：AEM as a Cloud Service。

Cloud Manager で AEM as a Cloud Service 環境をプロビジョニングすると、JWT 資格情報を使用して Adobe Developer Console プロジェクトが自動生成されます。以下のスクリーンショットに示すように、このプロジェクトは読み取り専用としてマークされます。お客様は、これらのプロジェクトを OAuth サーバー間資格情報に移行することはできず、移行しようとしないでください。 代わりに、資格情報が使用できなくなる前に、Adobeはこれらのプロジェクトを単独で移行します。

![自動生成されたプロジェクト](/help/security/assets/jwt-deprecation-autogen-projects.png)
