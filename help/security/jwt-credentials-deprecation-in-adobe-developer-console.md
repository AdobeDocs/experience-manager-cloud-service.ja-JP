---
title: Adobe Developerコンソールでの JWT 資格情報の廃止
description: AEM上のAdobe Developerコンソールでの JWT 資格情報の廃止の影響について説明します。
source-git-commit: e02e38a5267188111f0392a0a5c7b73e6a4f22b5
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Adobe Developerコンソールでの JWT 資格情報の廃止 {#jwt-credentials-deprecation-in-adobe-developer-console}

Adobeのお客様が [Adobe Developer Console](https://developer.adobe.com/console) 様々な API へのアクセスを可能にする資格情報を生成する場合。 お客様は、OAuth サーバー間からシングルページアプリまで、様々な資格情報の種類から選択します。 これらの資格情報の種類の 1 つであるサービスアカウント (JWT) 資格情報は、OAuth サーバー間資格情報に代わって非推奨になりました。 新しいサービスアカウント (JWT) 資格情報は 2024 年 5 月 1 日以降は作成できず、2025 年 1 月 1 日以降は既存の JWT 資格情報は機能しません。 以下が可能です。 [廃止についてお読みください](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

この記事では、AEM as a Cloud ServiceおよびAEM 6.5 のお客様が非推奨をどのように処理するかに関する追加のコンテキストを提供します。

現時点での主な留意点は、AEM機能が新しい OAuth サーバー間資格情報をまだサポートしていないことです。 2024 年 4 月中旬に、AEMas a Cloud Service向けのAEMリリースと、AEM 6.5 向けの特別な互換性パッケージを通じて、最新の Service Pack 20 以降を実行している場合（Service Pack 21 以降では自動的にその機能が含まれます）のサポートがまもなく提供されます。 JWT 資格情報の移行手順が記載された電子メールが届いている可能性がありますが、新しい OAuth サーバー間資格情報タイプがAEMでサポートされるまで、資格情報の移行を保留しておく必要があります。

以下の節では、4 月中旬にAEMがサポートした後に、お客様がサービスアカウント (JWT) 資格情報を OAuth サーバー間資格情報に置き換える（または置き換えない）必要があるシナリオを示します。 [読み方](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) 」をクリックして、将来の資格情報を置き換えます。

>[!NOTE]
>
>The [**AEM** 開発者コンソール](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) ( **AEM** 名前では、 **Adobe** 開発者コンソール ) は、 [JWT トークン](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) サーバー間 API に使用されます。 これらの資格情報は非推奨ではなく、引き続き使用できます。


## AEMと他のAdobeソリューションの統合 {#integrating-aem-with-other-adobe-solutions}

**アクション**:2024 年 4 月中旬以降、AEMが移行をサポートするまで待ちます。

**関連するAEMバージョン**:AEM as a Cloud ServiceおよびAdobeManaged Services（Service Pack 20 以前）。


AEMのお客様は、AEMオーサー UI を使用して、他のすべてのAdobeソリューションとの統合を設定します。 例えば、Adobe Target、Adobe Analytics、AdobeLaunch、AFCS などです。

![AEMと他のソリューションの統合](/help/security/assets/jwt-deprecation.png)

例として、次のようになります。 [説明書](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=en) Adobe Targetとの統合を設定する場合。 の API キー [AEMでの IMS 設定の完了](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) AEMが 4 月中旬にこれらの資格情報をサポートするようになれば、セクションは OAuth サーバー間資格情報タイプに移行する必要があります。 これらの手順は、新しい OAuth サーバー間資格情報を適用するのに役立つよう、4 月中旬に改訂されます。

## Cloud Manager API {#cloud-manager-apis}

**アクション**:2024 年 4 月中旬以降、AEMが移行をサポートするまで待ちます。

**関連するAEMバージョン**:AEM as a Cloud ServiceおよびAdobeManaged Services（Service Pack 20 以前）。

お客様は、Adobe Developer Console プロジェクトを作成して、 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). AEMと Cloud Manager がサポートすると、Adobe Developerプロジェクトの資格情報は、OAuth サーバー間資格情報タイプに移行する必要があります。

## 自動生成されたプロジェクト {#autogen-projects}

**アクション**：お客様に代わってAdobeが移行されるので、移行しないでください。

**関連するAEMバージョン**:as a Cloud Serviceのみ。

Cloud Manager がAEMas a Cloud Service環境をプロビジョニングすると、JWT 資格情報を持つAdobe Developerコンソールプロジェクトが自動生成されます。 このプロジェクトは読み取り専用としてマークされます。下のスクリーンショットを参照してください。 お客様は、これらのプロジェクトを OAuth サーバー間資格情報にAdobeしようとすることはできません。代わりに、お客様は、資格情報が使用できなくなる前に、これらのプロジェクトを単独で移行します。

![自動生成されたプロジェクト](/help/security/assets/jwt-deprecation-autogen-projects.png)

