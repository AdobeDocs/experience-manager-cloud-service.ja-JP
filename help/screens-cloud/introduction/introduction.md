---
title: AEM Screens as aCloud Service
description: このページは、AEM ScreensをCloud Serviceとして紹介します。
hide: true
hidefromtoc: true
index: false
source-git-commit: 65b7bc7d911a80fa1ae03dc83eb49956b283a050
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# AEM Screens as aCloud Serviceの概要{#introduction-screens-cloud}

AEM ScreensをCloud Serviceとして使用すると、公共の場所で使用するための魅力的で動的なデジタルサイネージエクスペリエンスを作成できます。 これは、AEM Screens製品の次の進化であり、操作性と拡張性の大きな飛躍を表しています。

AEM Screens as aCloud Serviceは、マーケターが大規模な動的なデジタルエクスペリエンスを作成および管理できるデジタルサイネージソリューションです。 さらに、包括的なデジタルマーケティング戦略の一環として、様々な種類の物理画面が必要になります。 通常のWebチャネルやモバイルチャネルを超えたAdobeのオムニチャネル機能を拡張し、あらゆる地域にデジタルサイネージチャネルが含まれるようにします。 AEM Screens as aCloud Serviceは、コンテンツの作成、コンテンツの組み立て、イベント管理、メディアの再生などを深く理解し、より関連性の高い、状況に応じた、生産的で、予測的なユーザーエクスペリエンスを実現します。

## ScreensのコンポーネントをCloud Serviceとして理解する{#understanding-components}

Cloud ServiceとしてのScreensには、次の2つの主要なコンポーネントがあります。

* **コンテンツプロバイダー**:AEMCloud ServiceまたはAdobe Managed Services(AMS)上で動作するScreensアドオンです。Screensコンテンツプロバイダーを使用すると、コンテンツ作成者は、チャネルを作成および管理できます。 コンテンツ作成者は、ディスプレイやプレーヤー登録の作成の詳細を気にすることなく、新しいコンテンツを追加したり、コンテンツを編集したりできます。 コンテンツプロバイダーは、コンテンツ、ディスプレイまたはプレーヤー登録の開発に関する基礎となる詳細を抽象化します。

* **サービスプロバイダー**：サービスランタイムで実行されるデジタルサイネージ管理サービスです。Adobe I/OScreensサービスプロバイダーを使用すると、コンテンツ作成者、開発者および管理者は、コンテンツがチャネルに追加された後のコンテンツ再生のディスプレイとプレーヤーを管理できます。 さらに、Screensサービスプロバイダーは、コンテンツをハイレベルで再生する場所とタイミングをオーケストレーターに通知します。


## アーキテクチャの概要 {#architectural-overview}

AEM ScreensのCloud Serviceユーザーは、Cloud ServiceとしてScreens専用に設計されたインターフェイス（**Screens Services Provider**&#x200B;および&#x200B;**Screens Content Provider**）から、チャネルのコンテンツの追加と管理、ディスプレイとプレーヤーの登録と管理をおこなえます。

![画像](/help/screens-cloud/assets/architecture-screenscloud.png)

