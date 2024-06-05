---
title: Adobe Developer App Builder を使用した [!DNL Adobe Experience Manager] as a Cloud Service の拡張
description: Adobe Developer App Builder を使用した [!DNL Adobe Experience Manager] as a Cloud Service の拡張
exl-id: 50d82745-5deb-4bfa-961b-714842403601
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 100%

---

# Adobe Developer App Builder を使用した [!DNL Adobe Experience Manager] as a Cloud Service の拡張 {#extend-using-app-builder}

## AEM as a Cloud Service の App Builder とは {#project-appbuilder}

新しい Adobe Developer Application Builder は、AEM as a Cloud Service の機能をデベロッパーが容易に拡張できる拡張フレームワークを提供します。

App Builder は、Adobe Experience Manager を拡張したカスタムエクスペリエンスを統合および作成するための統一サードパーティ拡張フレームワークを提供します。アドビのインフラストラクチャに基づいて構築されたこの包括的な拡張フレームワークにより、開発者は、あらゆるアドビソリューションおよびそれ以外の IT スタックにわたって、カスタムマイクロサービスを構築し、Adobe Experience Manager を拡張および統合できます。

App Builder を使用すると、次のような様々なユースケースで Adobe Experience Manager を容易に拡張できます。

* ミドルウェア拡張 - カスタムコネクタを構築するか、事前に構築された統合のスイートを活用して、外部システムとアドビアプリケーションを接続します。
* コアサービス拡張 - カスタム機能およびビジネスロジックを使用してデフォルトの動作を拡張することで、コアアプリケーション機能を拡張します。
* ユーザーエクスペリエンス拡張 - コアエクスペリエンスを拡張してビジネス要件をサポートするか、顧客固有のデジタルプロパティ、ストアフロントおよびバックオフィスアプリを構築します。

Application Builder は、2020 年夏以降、アドビのデベロッパープレビューを通じて、法人のお客様やパートナーが利用できるようになりました。App Builder の一般リリース（GA）は 2021年12月に予定されています。デベロッパーのみなさんは、ぜひ[体験版プログラム](https://developer.adobe.com/app-builder/trial/)で Application Builder を試してみてください。

>[!NOTE]
>
> AEM 6.5 のお客様が Application Builder を利用する場合は、[Adobe Developer Application Builder を使用した Adobe Experience Manager 6.5 の拡張](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html?lang=ja)を参照してください。

## アーキテクチャ {#architecture}

標準のソリューションではなく、Adobe Developer App Builder では、AEM などのアドビクラウドソリューションを拡張するための、一貫性のある標準化された共通の開発プラットフォームを提供します。例えば、次のようなものがありす。

* Adobe Developer Console - カスタムマイクロサービスおよび拡張機能の開発の場合、デベロッパーは、プラグインや統合の作成に必要なすべてのツールと API を利用しながら、プロジェクトを構築および管理できます。
* 開発者ツール - 開発者がカスタムの拡張機能や統合を容易に構築できるオープンソースのツール、SDK およびライブラリです。React Spectrum（アドビの UI ツールキット）を使用すると、すべてのアドビアプリに共通の 1 つのユーザーインターフェイスを利用できます。
* サービス - アドビのサーバーレスプラットフォーム上でインフラストラクチャをホスティングするための I/O Runtime や、イベントベースの統合のための I/O Events があります。また、データやファイルの保存も標準でサポートされています。
* Adobe Experience Cloud - 開発者は、拡張機能や統合を送信して Experience Cloud 組織内で公開できます。その後、システム管理者がこれらの拡張機能を審査、管理および承認できます。App Builder のカスタム拡張機能およびツールは、公開されると、他の Adobe Experience Cloud アプリと一緒に表示されます。

次の図は、Application Builder 上で構築された標準アプリケーションでこれらの機能がどのように利用されているかを示しています。

![アーキテクチャ](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

App Builder のアーキテクチャについて詳しくは、[アーキテクチャの概要](https://developer.adobe.com/app-builder/docs/guides/)を参照してください。

## App Builder の基本を学ぶ {#additional-resources}

アドビが作成した入門ドキュメントを使用して、Application Builder の基本を学ぶことができます。

* [App Builder の基礎知識](https://developer.adobe.com/app-builder/docs/getting_started/)

## ドキュメントを利用した学習の続行 {#appbuilder-documentation}

App Builder には、開発者向けのビデオとドキュメントが用意されています。ガイドや、独自のカスタムアプリケーションの開発を開始する際に役立つリファレンスドキュメントなどです。

* [App Builder ドキュメント](https://developer.adobe.com/app-builder/docs/overview/?lang=ja)
* [App Builder ビデオ](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## サンプルアプリケーションの試用 {#appbuilder-codesamples}

開発を開始する準備はできていますか？迅速に作業を進めるのに役立つサンプルアプリケーションが多数用意されています。

* [Adobe Developer Web サイトの App Builder コードラボ](https://developer.adobe.com/app-builder/docs/resources/?lang=ja)