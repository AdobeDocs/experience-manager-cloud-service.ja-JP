---
title: AEM Screens as a Cloud Service の概要
description: このページは、Adobe Experience Manager Screensas a Cloud Serviceの紹介として機能します。
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 56%

---

# AEM Screens as a Cloud Service の概要 {#introduction-screens-cloud}

Adobe Experience Manager(AEM)Screens をas a Cloud Service的に使用すれば、公共の場所で利用するために魅力的で動的なデジタルサイネージエクスペリエンスを作成できます。 これは、AEM Screens 製品の次の進化形であり、操作性と拡張性で大きく飛躍しています。

AEM Screens as a Cloud Service は、マーケターが動的なデジタルエクスペリエンスを大規模に作成および管理できるデジタルサイネージソリューションです。また、包括的なデジタルマーケティング戦略の一環として、様々な種類の物理画面が必要になります。 このソリューションは、アドビが提供するオムニチャネルを、通常のWebやモバイルのチャネルだけでなく、身の回りにあるデジタルサイネージのチャネルにも拡大します。AEM Screens as a Cloud Service を利用すれば、コンテンツの作成、コンテンツの組み立て、トリガーされたイベントの管理、そしてメディアの再生を深く理解することで、あらゆる公共スペースのあらゆる消費者や訪問者に、より関連性が高く、状況に応じた、生産性の高い、予測可能なユーザーエクスペリエンスを提供することができます。

## Screens as a Cloud Service のコンポーネントについて {#understanding-components}

Screens as a Cloud Service には、次の 2 つの主要なコンポーネントがあります。

* **[コンテンツプロバイダー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html)**：AEM Cloud Service または Adobe Managed Services（AMS）上で動作する Screens アドオンです。Screens コンテンツプロバイダーを使用すると、コンテンツ作成者は、チャネルを作成および管理できます。コンテンツ作成者は、ディスプレイの作成やプレーヤーの登録の詳細を気にすることなく、新しいコンテンツを追加したり、コンテンツを編集したりできます。コンテンツプロバイダーは、コンテンツの開発、ディスプレイ、プレーヤーの登録の詳細を抽象化します。

* **[サービスプロバイダー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html)**:Adobe I/O Runtime上で動作するデジタルサイネージ管理サービス。 Screens Services Provider を使用すると、コンテンツ作成者、開発者および管理者は、コンテンツがチャネルに追加された後のコンテンツ再生のディスプレイとプレーヤーを管理できます。 また、Screens サービスプロバイダーは、コンテンツを高レベルで再生する場所とタイミングをオーケストレーターに通知します。


## アーキテクチャの概要 {#architectural-overview}

AEM Screensのas a Cloud Serviceユーザーは、チャネルにコンテンツを追加および管理できます。 ディスプレイとプレーヤーは、Screens as a Cloud Service向けに設計されたインターフェイス ( つまり、 **Screens Services Provider** および **Screens コンテンツプロバイダー**.

![画像](/help/screens-cloud/assets/architecture-screenscloud.png)
