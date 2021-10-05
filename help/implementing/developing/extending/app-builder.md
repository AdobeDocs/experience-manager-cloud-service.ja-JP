---
title: ' [!DNL Adobe Experience Manager] as a Cloud Serviceを拡張 (Adobe開発者アプリビルダーを使用 )。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Serviceを拡張 (Adobe開発者アプリビルダーを使用 )。'
source-git-commit: 9287a40518d7026d5361cb61ab3804583e22450f
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager]as a Cloud Serviceを拡張 (Adobe開発者アプリビルダーを使用 ) {#extend-using-app-builder}

## AEM as a Cloud Serviceの App Builder とは {#project-firefly}

新しいAdobe開発者アプリビルダーは、AEMas a Cloud Serviceの機能を簡単に拡張できる拡張フレームワークを開発者に提供します。

App Builder は、Adobe Experience Managerを拡張するカスタムエクスペリエンスを統合および作成するための、統合されたサードパーティの拡張フレームワークを提供します。 Adobeのインフラストラクチャに基づいて構築されたこの完全な拡張フレームワークを使用すると、開発者は、カスタムマイクロサービスを構築し、Adobeソリューションとその他の IT スタックをまたいでAdobe Experience Managerを拡張し、統合できます。

App Builder を使用すると、様々な用途でAdobe Experience Managerを簡単に拡張できます。

* ミドルウェアの拡張機能 — 外部システムとAdobe・アプリケーションを接続してカスタム・コネクタを構築するか、事前に構築された統合のスイートを活用します。
* コアサービスの拡張機能 — カスタム機能とビジネスロジックを使用してデフォルトの動作を拡張し、コアアプリケーション機能を拡張します。
* ユーザーエクスペリエンスの拡張 — コアエクスペリエンスを拡張して、ビジネス要件をサポートしたり、顧客固有のデジタルプロパティ、ストアフロント、バックオフィスアプリを構築したりします。

App Builder（旧 Project Firefly）は、2020 年夏以降、デベロッパープレビューを通じて、エンタープライズのお客様およびパートナーに提供されています。 App Builder の一般公開 (GA) は 2021 年 12 月に予定されています。 アドビの [ 体験版プログラム ](http://adobe.ly/appbuilder-trial) を通じて App Builder を試してみる開発者を歓迎します。

>[!NOTE]
>
> AEM 6.5 のお客様は、App Builder を利用する場合は、[Adobe開発者 App Builder を使用したAdobe Experience Manager 6.5 の拡張 ](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html) に進んでください。

## アーキテクチャ {#architecture}

標準のソリューションの代わりに、Adobe開発者アプリビルダーは、AEMなどのAdobeクラウドソリューションを拡張するための、共通の、一貫性のある、標準化された開発プラットフォームを提供します。

* Adobe開発者コンソール — カスタムマイクロサービスおよび拡張機能の開発のために、開発者は、プラグインや統合を作成するために必要なすべてのツールや API にアクセスしながら、プロジェクトを構築および管理できます。
* 開発者ツール — 開発者がカスタム拡張機能や統合を簡単に構築できるオープンソースツール、SDK、ライブラリ。 React Spectrum(Adobeの UI ツールキット ) を使用して、すべてのAdobeアプリに共通の UI を 1 つ持ちます。
* サービス — サーバーレスプラットフォーム上のインフラストラクチャをホスティングするための I/O Runtime 、イベントベースの統合のための I/O イベント。 また、データとファイルの保存も標準でサポートされています。
* Adobe Experience Cloud — 開発者は、拡張機能や統合を送信し、Experience Cloud組織内で公開できます。その後、システム管理者は、これらの拡張機能を確認、管理および承認できます。 公開されると、カスタムの App Builder 拡張機能とツールが他のAdobe Experience Cloudアプリと共に見つかります。

次の図は、App Builder 上に構築された標準アプリケーションがこれらの機能を利用する方法を示しています。

![アーキテクチャ](/help/implementing/developing/extending/assets/firefly-architecture.jpg)

App Builder のアーキテクチャの詳細については、「[ アーキテクチャの概要 ](https://www.adobe.io/app-builder/docs/guides/)」を参照してください。

## App Builder の概要 {#additional-resources}

App Builder の使用を開始する際に役立つ一連のドキュメントを作成しました。

* [App Builder はじめに](https://www.adobe.io/app-builder/docs/getting_started/)

## ドキュメントで学習を続ける {#appbuilder-documentation}

App Builder には、開発者向けのビデオとドキュメント（ガイドなど）と、独自のカスタムアプリケーションの開発を開始する際に役立つリファレンスドキュメントが用意されています。

* [App Builder ドキュメント](https://www.adobe.io/app-builder/docs/overview/)
* [App Builder ビデオ](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## サンプルアプリケーションの 1 つを試してみる {#appbuilder-codesamples}

開発を始める準備は？ 迅速に作業を進めるのに役立つサンプルアプリケーションが多数あります。

* [App Builder コードラボ (Adobe開発者 Web サイト )](https://www.adobe.io/app-builder/docs/resources/)

## サポート {#support}

開発者サポートのタイプのリクエストについては、開発者に [Experience Leagueフォーラム ](https://experienceleaguecommunities.adobe.com/t5/project-firefly/ct-p/project-firefly) を使用することをお勧めします。
