---
title: AEM as a Cloud Service オンボーディングジャーニーの概要
description: AEM as a Cloud Service のオンボーディングプロセスのガイド付きジャーニーの概要については、ここから始めてください。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 841e30bc279a3859ce9a302b18ddf566d8163100
workflow-type: ht
source-wordcount: '1348'
ht-degree: 100%

---


# オンボーディングジャーニー {#onboarding-journey}

AEM as a Cloud Service を選択していただき、ありがとうございます。このドキュメントは、オンボーディングプロセスのガイド付きジャーニーの出発点です。新しいアプリケーションをデプロイする場合でも、既存のアプリケーションを移行する場合でも、このオンボーディングジャーニーでチームを設定します。これにより、ユーザーが AEM as a Cloud Service にアクセスできるようになります。

## はじめに {#introduction}

Adobe Experience Manager は、あらゆるチャネルにわたって非常にインパクトのあるパーソナライズされたエクスペリエンスを迅速に提供し、すべてのチャネルにコンテンツを解放する、構成可能なコンテンツサービスの強力なスイートです。**Edge 配信サービス**&#x200B;は、Adobe Experience Manager の最新のイノベーションで、優れたコンテンツベロシティを実現し、卓越したエクスペリエンスを提供します。Edge Delivery Services の概要について詳しくは、[Edge Delivery Services の概要](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview)を参照してください。Edge 配信サービスの使用方法については、[開発者向けチュートリアル](https://www.aem.live/developer/tutorial)ページを参照してください。

オンボーディングとは、指定されたシステム管理者が AEM as a Cloud Service を組織用に設定するプロセスです。このプロセスには、クラウドリソースの初期プロビジョニングや、ユーザーを職務に基づいて役割に割り当てる作業が含まれます。これにより、各メンバーが AEM as a Cloud Service にログオンしてリソースにアクセスできるようになります。

![オンボーディングジャーニー](/help/journey-onboarding/assets/onboarding-journey.png)

このガイドでは、オンボーディングに関する最も重要なトピックについて順を追って説明します。完了すると、次のことが可能になります。

* オンボーディングプロセスに関わる様々な用語、サービス、ユーザーの完全な理解。
* AEM as a Cloud Service アプリケーションのコンテンツを作成および開発する方法の習得に向けて、チームが立ち上がり、最初のステップを踏み出せるようにする。

これにより、以下を実現できます。

* チームの設定が完了し、クラウドリソースにアクセスできるようになります。
* AEM オーサーが AEM as a Cloud Service にアクセスし、コンテンツの作成を開始できます。
* AEM デベロッパーと AEM デプロイメントマネージャーが AEM as a Cloud Service にアクセスし、カスタムアプリケーションの作成とデプロイを開始できます。

## 概念と目標 {#concepts}

<!-- Although there may appear to be a lot to learn when getting started with AEM as a Cloud Service, conceptually there are only a few, logical pieces.-->

AEM as a Cloud Service のオンボーディングジャーニーは、次のコア要素を中心に展開されます。

* **契約** - アドビの契約を確認して、オンボーディングプロセスの主な詳細を理解します。
* **Experience Hub** - [experience.adobe.com](https://experience.adobe.com/) を AEM 機能の中心的なエントリポイントとして使用します。Experience Hub は、ユーザーのペルソナと使用権限に適応されるので、効率的に作業できます。ここから、次の場所に移動します。
   * **Admin Console** - ユーザーの管理と役割の割り当てを行います。
   * **Cloud Manager** - カスタムコードを管理およびデプロイするためのプログラムと環境の設定、Git へのアクセス、パイプラインの作成を行います。
   * **Sites** - デジタルエクスペリエンスを作成、管理および配信します。 （ライセンスベースの使用権限）
   * **Assets** - デジタルアセットを整理、保存および配分します。（ライセンスベースの使用権限）
   * **Forms** - アダプティブフォームとレスポンシブフォームを作成および管理します。（ライセンスベースの使用権限）

これらの概念について詳しくは、このオンボーディングジャーニーを参照してください。目標は、ジャーニーの最後に、次のことができるようになることです。

* 必要なユーザーに AEM as a Cloud Service へのアクセス権を付与する。
* プロジェクトの最初のクラウドリソースを設定する。
* 最初のコードをデプロイし、最初のコンテンツを作成する方法を理解している状態。

つまり、AEM as a Cloud Service を使用して新しいプロジェクトに取りかかれるようになります。

## オーディエンス {#audience}

オンボーディングジャーニーは、AEM as a Cloud Service および一般的な AEM を初めて使用するお客様の&#x200B;**システム管理者**&#x200B;向けに特別に書かれています。システム管理者とは、AEM as a Cloud Service 契約の署名後に、アドビが最初に連絡するユーザーです。通常は、このユーザーが最初に AEM as a Cloud Service 上のリソースにアクセスして設定を行います。このトピックを読んでいるユーザーは、おそらくシステム管理者です。

システム管理者は、組織の AEMaaCS ユーザーに関して、アクセスから権限に至るすべての側面を管理します。その過程で、システム管理者は他のペルソナとやり取りする必要があります。

| ペルソナ | 説明 | ジャーニーでの役割 |
| --- | --- | --- |
| システム管理者 | このジャーニーのターゲットは、クラウドリソースの初期プロビジョニングと、ユーザーを職務責任に基づいて適切な役割に割り当てを行うことです。 | 役割は、アクセスから権限まで、ユーザーのあらゆる側面を管理するのに役立ちます。 |
| コンテンツ作成者 | AEM でコンテンツの作成とレビューを行います。 | システム管理者から権限を付与されると、作成者はコンテンツ作成の独自のジャーニーを開始できます。 |
| 開発者 | 様々なソースのコンテンツを消費する AEM アプリケーションを開発します。 | システム管理者から権限を付与されると、開発者はソリューション開発の独自のジャーニーを開始できます。 |
| デプロイメントマネージャー | 環境の追加や更新を行い、パイプラインを実行し、コードを AEM 環境やコード品質にデプロイします。 | システム管理者から権限を付与されると、デプロイメントマネージャーはデプロイメントを管理するジャーニーを開始できます。 |

このオンボーディングガイドでは、システム管理者としてオンボーディングする完全なプロセスを説明します。AEM ユーザー、開発者、デプロイメントマネージャーの役割については、このジャーニーの補足のパートで簡単に説明します。

>[!TIP]
>
>AEM as a Cloud Service を初めて使用するものの、AEM については既に詳しく、オンプレミスまたは Adobe Managed Services から移行する場合は、[AEM as a Cloud Service への移行ジャーニー](/help/journey-migration/getting-started.md)を確認します。

## オンボーディングジャーニーの概要 {#overview}

以下の記事では、オンボーディングのコアとなる概念を詳しく説明し、AEM as a Cloud Service に関する基本的な知識を提供します。ジャーニーの特定の部分に直接移動することもできますが、多くの概念は、それまでの記事で紹介された概念に基づいています。したがって、オンボーディングを初めて行う場合は、最初から順に進めることをお勧めします。

| | 記事 | 説明 | オーディエンス |
| --- | --- | --- | --- |
| 0 | オンボーディングジャーニー | このドキュメント | システム管理者 |
| 1 | [オンボーディングの準備](preparation.md) | オンボーディングプロセスの開始に先立って、システム管理者がシステムにログインする前に理解しておく必要がある準備手順がいくつかあります。 | システム管理者 |
| 2 | [AEM as a Cloud Service の用語](terminology.md) | AEMaaCS に初めてログインする前に、システムの用語とその基本的な構造を理解しておくと役に立ちます。 | システム管理者 |
| 3 | [Admin Console](admin-console.md) | Admin Console とは何か、ログイン方法およびシステム管理者としてのプロファイルを確認する方法について説明します。 | システム管理者 |
| 4 | [Cloud Manager 製品プロファイルの割り当て](assign-profiles-cloud-manager.md) | Cloud Manager 製品プロファイルを確認し、Cloud Manager 製品プロファイルへのチームメンバーの割り当て方法について説明します。 | システム管理者 |
| 5 | [Experience Hub へのアクセス](/help/experience-hub.md) | AEM エコシステムへの統合された、パーソナライズされたエントリポイントとして機能する Experience Hub を使用します。 | AEM ユーザー |
| 6 | [Cloud Manager へのアクセス](cloud-manager.md) | プロジェクトリソースを設定するための Cloud Manager へのアクセス方法について説明します。 | システム管理者 |
| 7 | [プログラムの作成](create-program.md) | Cloud Manager を使用してプログラムを作成する方法を説明します。 | システム管理者 |
| 8 | [環境の作成](create-environments.md) | Cloud Manager を使用して環境を作成する方法を説明します。 | システム管理者 |
| 9 | [AEM 製品プロファイルの割り当て](assign-profiles-aem.md) | システム管理者が AEM as a Cloud Service の製品プロファイルにチームメンバーを割り当てる方法について説明します。 | システム管理者 |
| 10 | [開発者およびデプロイメントマネージャーのタスク](developers.md) | オプション - 開発者として、Cloud Manager Git にアクセスして管理する方法について説明します。デプロイメントマネージャーとして、パイプラインを設定し、Cloud Manager でコードをデプロイする方法について説明します。 | 開発者およびデプロイメントマネージャー |
| 11 | [AEM ユーザーのタスク](aem-users.md) | オプション - AEM オーサーとして AEM as a Cloud Service インスタンスにアクセスする方法と、AEM as a Cloud Service 用コンテンツのオーサリング方法について説明します。 | AEM ユーザー |

## 次の手順 {#what-is-next}

これで、AEM as a Cloud Service のオンボーディングジャーニーを開始する準備が整いました。このジャーニーの次の手順に進み、[オンボーディングの準備](preparation.md)の記事を読むことをお勧めします。

## AEM ドキュメントジャーニー {#documentation-journeys}

[ドキュメントジャーニー](/help/journey-documentation/documentation-journeys.md)では、多様かつ複雑なトピックおよび機能を組み合わせて説明しています。ここでは、AEM を初めて使用するユーザーが、以前のトピックや AEM に関する最小限の知識を有しているという前提で、ビジネス上の問題の全体を理解して解決するのに役立つ情報が提供されています。

ドキュメントジャーニーは、ベストプラクティスの原則を軸に設計されています。アドビの最新の調査、アドビのコンサルタントによる実装実績、顧客プロジェクトからのフィードバックなどに基づいて情報を提供します。

新しい AEM as a Cloud Service アプリケーションにチームをオンボーディングする方法について、アドビの推奨事項を理解するには、ここが出発点になります。

## その他のリソース {#additional-resources}

オンボーディングジャーニーのコンテンツの範囲を超えた情報について詳しくは、次の追加のオプションリソースを参照してください。

* [AEM as a Cloud Service のオンボーディング](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding) - この短いビデオでは、AEM の Cloud Service オンボーディングプロセスの概要を説明します。
