---
title: 拡張ガイド [!DNL Adobe Experience Manager] App Builder のAdobeを使用したas a Cloud Service
description: 拡張ガイド [!DNL Adobe Experience Manager] App Builder のAdobeを使用したas a Cloud Service
source-git-commit: 528abc0938a71746c2c8b69382c961686cc42634
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# 拡張ガイド [!DNL Adobe Experience Manager] App Builder のAdobeを使用したas a Cloud Service {#extend-using-app-builder}

## AEM as a Cloud Serviceの App Builder とは {#project-firefly}

新しいAdobe開発者アプリビルダーは、AEMas a Cloud Serviceの機能を簡単に拡張できる、開発者向けの拡張フレームワークを提供します。

App Builder は、Adobe Experience Managerを拡張するカスタムエクスペリエンスを統合および作成するための、統合されたサードパーティの拡張フレームワークを提供します。 Adobeのインフラストラクチャに基づいて構築されたこの完全な拡張フレームワークを使用すると、開発者は、Adobeソリューションとその他の IT スタックをまたいで、カスタムマイクロサービスを構築し、Adobe Experience Managerを拡張し、統合できます。

App Builder を使用すると、様々な用途でAdobe Experience Managerを簡単に拡張できます。

* ミドルウェア拡張機能 — 外部システムとAdobeアプリケーションとを接続し、カスタムコネクタを構築するか、事前に構築された統合のスイートを活用します。
* コアサービス拡張機能 — カスタム機能とビジネスロジックを使用してデフォルトの動作を拡張し、コアアプリケーション機能を拡張します。
* ユーザーエクスペリエンス拡張機能 — コアエクスペリエンスを拡張して、ビジネス要件をサポートしたり、顧客固有のデジタルプロパティ、ストアフロント、バックオフィスアプリを構築したりできます。

App Builder（旧称 Project Firefly）は、2020 年夏以降、デベロッパープレビューを通じて、エンタープライズのお客様やパートナーが利用できるようになりました。 App Builder の一般リリース (GA) は 2021 年 12 月に予定されています。 開発者が [体験版プログラム](http://adobe.ly/appbuilder-trial).

>[!NOTE]
>
> AEM 6.5 のお客様が App Builder を利用する場合は、 [Adobe Experience Manager 6.5 の拡張 (Adobe開発者アプリビルダーを使用 )](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## アーキテクチャ {#architecture}

標準のソリューションの代わりに、Adobe開発者アプリビルダーは、AEMなどのAdobeクラウドソリューションを拡張するための、共通の、一貫性のある、標準化された開発プラットフォームを提供します。

* Adobe開発者コンソール — カスタムマイクロサービスおよび拡張機能の開発の場合、開発者は、プラグインおよび統合を作成するために必要なすべてのツールと API にアクセスしながら、プロジェクトを構築および管理できます。
* 開発者ツール — 開発者がカスタム拡張機能や統合を簡単に構築できるオープンソースツール、SDK、ライブラリ。 React Spectrum(Adobeの UI ツールキット ) を使用して、すべてのAdobeアプリに共通の UI を 1 つ用意します。
* サービス — サーバーレスプラットフォーム上のインフラストラクチャをホスティングするための I/O Runtime と、イベントベースの統合のための I/O Events。 また、データとファイルの保存も標準でサポートされています。
* Adobe Experience Cloud — 開発者は、拡張機能や統合を送信し、Experience Cloud組織内で公開できます。その後、システム管理者は、これらの拡張機能を確認、管理および承認できます。 公開すると、カスタムの App Builder 拡張機能とツールが他のAdobe Experience Cloudアプリと共に見つかります。

次の図は、App Builder 上で構築された標準アプリケーションがこれらの機能をどのように利用するかを示しています。

![アーキテクチャ](/help/implementing/developing/extending/assets/firefly-architecture.jpg)

App Builder のアーキテクチャについて詳しくは、 [アーキテクチャの概要](https://www.adobe.io/app-builder/docs/guides/).

## App Builder の概要 {#additional-resources}

App Builder を使い始めるのに役立つ一連のドキュメントを作成しました。

* [App Builder はじめに](https://www.adobe.io/app-builder/docs/getting_started/)

## ドキュメントを使用して学習を続ける {#appbuilder-documentation}

App Builder には、開発者向けのビデオおよびドキュメント（ガイドを含む）、および独自のカスタムアプリケーションの開発を開始するのに役立つリファレンスドキュメントが用意されています。

* [App Builder ドキュメント](https://www.adobe.io/app-builder/docs/overview/)
* [App Builder ビデオ](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## サンプルアプリケーションの 1 つを試してみます。 {#appbuilder-codesamples}

開発を開始する準備はできていますか？ 迅速に作業を進めるのに役立つサンプルアプリケーションが多数用意されています。

* [App Builder コードラボ (Adobe開発者向け Web サイト )](https://www.adobe.io/app-builder/docs/resources/)

## サポート {#support}

開発者サポートのタイプのリクエストについては、開発者が [Experience Leagueフォーラム](https://experienceleaguecommunities.adobe.com/t5/project-firefly/ct-p/project-firefly).
