---
title: AEM Screens as a Cloud Service の概要
description: このページでは、AEM Screens as a Cloud Service の概要ついて説明します。
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: ht
source-wordcount: '382'
ht-degree: 100%

---

# AEM Screens as a Cloud Service の概要 {#introduction-screens-cloud}

AEM Screens as a Cloud Service を使用すると、公共の場所で使用するための魅力的で動的なデジタルサイネージエクスペリエンスを作成できます。これは、AEM Screens 製品の次の進化形であり、操作性と拡張性で大きく飛躍しています。

AEM Screens as a Cloud Service は、マーケターが動的なデジタルエクスペリエンスを大規模に作成および管理できるデジタルサイネージソリューションです。さらに、包括的なデジタルマーケティング戦略の一環として、様々な種類の物理画面を使用することができます。このソリューションは、アドビが提供するオムニチャネルを、通常のWebやモバイルのチャネルだけでなく、身の回りにあるデジタルサイネージのチャネルにも拡大します。AEM Screens as a Cloud Service を利用すれば、コンテンツの作成、コンテンツの組み立て、トリガーされたイベントの管理、そしてメディアの再生を深く理解することで、あらゆる公共スペースのあらゆる消費者や訪問者に、より関連性が高く、状況に応じた、生産性の高い、予測可能なユーザーエクスペリエンスを提供することができます。

## Screens as a Cloud Service のコンポーネントについて {#understanding-components}

Screens as a Cloud Service には、次の 2 つの主要なコンポーネントがあります。

* **[コンテンツプロバイダー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=ja)**：AEM Cloud Service または Adobe Managed Services（AMS）上で動作する Screens アドオンです。Screens コンテンツプロバイダーを使用すると、コンテンツ作成者は、チャネルを作成および管理できます。コンテンツ作成者は、ディスプレイの作成やプレーヤーの登録の詳細を気にすることなく、新しいコンテンツを追加したり、コンテンツを編集したりできます。コンテンツプロバイダーは、コンテンツ、ディスプレイ、プレーヤーの登録などの開発の詳細を抽象化して提供します。

* **[サービスプロバイダー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=ja)**：Adobe I/O Runtime で実行されるデジタルサイネージ管理サービスです。Screens サービスプロバイダーを使用すると、コンテンツ作成者、デベロッパー、管理者は、コンテンツがチャネルに追加された後のコンテンツ再生のディスプレイとプレーヤーを管理できます。さらに、Screens サービスプロバイダーは、コンテンツが再生される場所とタイミングをハイレベルでオーケストレーターに通知します。


## アーキテクチャの概要 {#architectural-overview}

AEM Screens as a Cloud Service のユーザーは、Screens as a Cloud Service 専用に設計されたインターフェイス（**Screens サービスプロバイダー**&#x200B;および **Screens コンテンツプロバイダー**）を使用して、チャネルへのコンテンツの追加と管理、ディスプレイとプレーヤーの登録と管理を行えます。

![画像](/help/screens-cloud/assets/architecture-screenscloud.png)
