---
title: Adobe Developer App Builder を使用した [!DNL Adobe Experience Manager] as a Cloud Service の拡張
description: Adobe Developer App Builder を使用した [!DNL Adobe Experience Manager] as a Cloud Service の拡張
exl-id: 50d82745-5deb-4bfa-961b-714842403601
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 100%

---

# Adobe Developer App Builder を使用した [!DNL Adobe Experience Manager] as a Cloud Service の拡張 {#extend-using-app-builder}

## AEM as a Cloud Service の App Builder とは {#project-firefly}

新しい Adobe Developer App Builder は、AEM as a Cloud Service の機能を開発者が容易に拡張できる拡張フレームワークを提供します。

App Builder は、Adobe Experience Manager を拡張したカスタムエクスペリエンスを統合および作成するための統一サードパーティ拡張フレームワークを提供します。アドビのインフラストラクチャに基づいて構築されたこの包括的な拡張フレームワークにより、開発者は、あらゆるアドビソリューションおよびそれ以外の IT スタックにわたって、カスタムマイクロサービスを構築し、Adobe Experience Manager を拡張および統合できます。

App Builder を使用すると、次のような様々なユースケースで Adobe Experience Manager を容易に拡張できます。

* ミドルウェア拡張 - カスタムコネクタを構築するか、事前に構築された統合のスイートを活用して、外部システムとアドビアプリケーションを接続します。
* コアサービス拡張 - カスタム機能およびビジネスロジックを使用してデフォルトの動作を拡張することで、コアアプリケーション機能を拡張します。
* ユーザーエクスペリエンス拡張 - コアエクスペリエンスを拡張してビジネス要件をサポートするか、顧客固有のデジタルプロパティ、ストアフロントおよびバックオフィスアプリを構築します。

App Builder（旧称 Project Firefly）は、2020年夏以降、開発者プレビューを通じて、法人のお客様やパートナーが利用できるようになりました。App Builder の一般リリース（GA）は 2021年12月に予定されています。アドビの[体験版プログラム](http://adobe.ly/appbuilder-trial)を通じて開発者が App Builder を試すことを歓迎します。

>[!NOTE]
>
> AEM 6.5 のお客様が App Builder を利用する場合は、[Adobe Developer App Builder を使用した Adobe Experience Manager 6.5 の拡張](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html?lang=ja)を参照してください。

## アーキテクチャ {#architecture}

標準のソリューションではなく、Adobe Developer App Builder では、AEM などのアドビクラウドソリューションを拡張するための、一貫性のある標準化された共通の開発プラットフォームを提供します。例えば、次のようなものがありす。

* アドビ開発者コンソール - カスタムマイクロサービスおよび拡張機能の開発の場合、開発者は、プラグインや統合の作成に必要なすべてのツールと API にアクセスしながら、プロジェクトを構築および管理できます。
* 開発者ツール - 開発者がカスタムの拡張機能や統合を容易に構築できるオープンソースのツール、SDK およびライブラリです。React Spectrum（アドビの UI ツールキット）を使用すれば、すべてのアドビアプリに共通の UI を 1 つ用意できます。
* サービス - サーバーレスプラットフォーム上でインフラストラクチャをホスティングするための I/O Runtime や、イベントベースの統合のための I/O Events があります。また、データやファイルの保存も標準でサポートされています。
* Adobe Experience Cloud - 開発者は、拡張機能や統合を送信して Experience Cloud 組織内で公開できます。その後、システム管理者がこれらの拡張機能を審査、管理および承認できます。App Builder のカスタム拡張機能およびツールは、公開されると、他の Adobe Experience Cloud アプリと一緒に表示されます。

次の図は、App Builder 上で構築された標準アプリケーションでこれらの機能がどのように利用されているかを示しています。

![アーキテクチャ](/help/implementing/developing/extending/assets/firefly-architecture.jpg)

App Builder のアーキテクチャについて詳しくは、[アーキテクチャの概要](https://www.adobe.io/app-builder/docs/guides/)を参照してください。

## App Builder の基本を学ぶ {#additional-resources}

App Builder を使い始める際に役立つように、参考になる一連のドキュメントを作成しました。

* [App Builder の基礎知識](https://www.adobe.io/app-builder/docs/getting_started/)

## ドキュメントを利用した学習の続行 {#appbuilder-documentation}

App Builder には、開発者向けのビデオとドキュメントが用意されています。ガイドや、独自のカスタムアプリケーションの開発を開始する際に役立つリファレンスドキュメントなどです。

* [App Builder ドキュメント](https://www.adobe.io/app-builder/docs/overview/)
* [App Builder ビデオ](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## サンプルアプリケーションの試用 {#appbuilder-codesamples}

開発を開始する準備はできていますか？迅速に作業を進めるのに役立つサンプルアプリケーションが多数用意されています。

* [Adobe Developer Web サイトの App Builder コードラボ](https://www.adobe.io/app-builder/docs/resources/)

## サポート {#support}

開発者サポートに類するリクエストについては、開発者が [Experience League フォーラム](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly?profile.language=ja)を使用することをお勧めします。
