---
title: AEM as a Cloud Service オンボーディングジャーニーの概要
description: AEM as a Cloud Service のオンボーディングプロセスのガイド付きジャーニーの概要については、ここから始めてください。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 7553d3c9f82c8b675af5f704a48bc316ba0d4885
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 95%

---


# オンボーディングジャーニー {#onboarding-journey}

AEM as a Cloud Service を選択していただき、ありがとうございます。このドキュメントは、オンボーディングプロセスのガイド付きジャーニーの出発点です。新しいアプリケーションをデプロイする場合でも、既存のアプリケーションを移行する場合でも、このオンボーディングジャーニーでチームの準備が確実に整い、AEM as a Cloud Service にアクセスできるようになります。

## はじめに {#introduction}

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

AEM as a Cloud Service を使い始めると、学ぶべきことがたくさんあるように見えるかもしれませんが、概念的には論理的なポイントは少ししかありません。

* **契約** - アドビの契約にはオンボーディングプロセスの側面が定義されているので、内容をよく理解しておく必要があります。
* **Admin Console** - ここで、ユーザーの管理と役割の割り当てを行います。
* **Cloud Manager** - プログラムや環境などのリソースを設定するためのツールです。このツールから Git にアクセスしてパイプラインを作成し、カスタムコードを管理およびデプロイすることもできます。

これらの概念については、このオンボーディングジャーニーで詳しく説明します。ジャーニーの完了時に、次の状態になることが目標です。

* AEM as a Cloud Service へのアクセス権を必要なユーザーに付与している状態。
* プロジェクトの最初のクラウドリソースの設定が完了している状態。
* 最初のコードをデプロイし、最初のコンテンツを作成する方法を理解している状態。

つまり、AEM as a Cloud Service を使用して新しいプロジェクトに取りかかれるようになります。

## 対象読者 {#audience}

オンボーディングジャーニーは、AEM as a Cloud Service および一般的な AEM を初めて使用するお客様の&#x200B;**システム管理者**&#x200B;向けに特別に書かれています。システム管理者とは、AEM as a Cloud Service 契約の署名後に、アドビから最初に連絡を受けるユーザーです。通常は、このユーザーが最初に AEM as a Cloud Service 上のリソースにアクセスして設定を行います。このトピックを読んでいるユーザーは、おそらくシステム管理者です。

システム管理者は、組織の AEMaaCS ユーザーに関して、アクセスから権限に至るすべての側面を管理します。その過程で、システム管理者は他の役割の人とやり取りする必要があります。

| ペルソナ | 説明 | ジャーニーでの役割 |
|---|---|---|
| システム管理者 | このジャーニーの対象者。クラウドリソースの初期プロビジョニングを行い、ユーザーを職務責任に基づいて適切な役割に割り当てます | アクセスから権限に至る、ユーザーのすべての側面を管理します |
| コンテンツ作成者 | AEM でコンテンツの作成とレビューを行います | システム管理者から権限を付与されると、作成者はコンテンツを作成するジャーニーを開始できます |
| デベロッパー | 様々なソースのコンテンツを消費する AEM アプリケーションを開発します。 | システム管理者から権限を付与されると、開発者はソリューションを開発するジャーニーを開始できます |
| デプロイメントマネージャー | 環境の追加や更新を行い、パイプラインを実行し、コードを AEM 環境やコード品質にデプロイします。 | システム管理者から権限を付与されると、デプロイメントマネージャーはデプロイメントを管理するジャーニーを開始できます |

このオンボーディングガイドでは、システム管理者としてオンボーディングする完全なプロセスを説明します。AEM ユーザー、開発者、デプロイメントマネージャーの役割については、このジャーニーの補足のパートで簡単に説明します。

>[!TIP]
>
>AEM as a Cloud Service を初めて使用するものの、AEM ついては既に詳しく、オンプレミスまたは Adobe Managed Services から移行する場合は、必ず [AEM as a Cloud Service への移行ジャーニー](/help/journey-migration/getting-started.md)を確認してください。

## オンボーディングジャーニーの概要 {#overview}

以下の記事では、オンボーディングのコアとなる概念を詳しく説明し、AEM as a Cloud Service に関する基本的な知識を提供します。ジャーニーの特定の部分に直接移動することもできますが、多くの概念は、それまでの記事で紹介された概念に基づいています。したがって、オンボーディングを初めて行う場合は、最初から順に進めることをお勧めします。

| # | 記事 | 説明 | 対象読者 |
|---|---|---|---|
| 0 | オンボーディングジャーニー | このドキュメント | システム管理者 |
| 1 | [オンボーディングの準備](preparation.md) | オンボーディングプロセスの開始に先立って、システム管理者がシステムにログインする前に理解しておく必要がある準備手順がいくつかあります。 | システム管理者 |
| 2 | [AEM as a Cloud Service の用語](terminology.md) | AEMaaCS に初めてログインする前に、システムの用語とその基本的な構造を理解しておくと役に立ちます。 | システム管理者 |
| 3 | [Admin Console](admin-console.md) | Admin Console とは何か、ログイン方法およびシステム管理者としてのプロファイルを確認する方法について説明します。 | システム管理者 |
| 4 | [Cloud Manager 製品プロファイルの割り当て](assign-profiles-cloud-manager.md) | Cloud Manager 製品プロファイルを確認し、Cloud Manager 製品プロファイルへのチームメンバーの割り当て方法について説明します。 | システム管理者 |
| 5 | [Cloud Manager へのアクセス](cloud-manager.md) | Cloud Manager にアクセスしてプロジェクトリソースをセットアップできるようにする方法を説明します。 | システム管理者 |
| 6 | [プログラムの作成](create-program.md) | Cloud Manager を使用してプログラムを作成する方法を説明します。 | システム管理者 |
| 7 | [環境の作成](create-environments.md) | Cloud Manager を使用して環境を作成する方法を説明します。 | システム管理者 |
| 8 | [AEM 製品プロファイルの割り当て](assign-profiles-aem.md) | システム管理者が AEM as a Cloud Service の製品プロファイルにチームメンバーを割り当てる方法について説明します。 | システム管理者 |
| 9 | [開発者およびデプロイメントマネージャーのタスク](developers.md) | オプション - デベロッパーとして Cloud Manager Git にアクセスして管理する方法と、デプロイメントマネージャーとして Cloud Manager でパイプラインを設定してコードをデプロイする方法について説明します。 | 開発者およびデプロイメントマネージャー |
| 10 | [AEM ユーザーのタスク](aem-users.md) | オプション - AEM オーサーとして AEM as a Cloud Service インスタンスにアクセスする方法と、AEM as a Cloud Service 用コンテンツのオーサリング方法について説明します。 | AEM ユーザー |

>[!NOTE]
>
>Edge Delivery Servicesは、柔軟で迅速な開発環境を可能にする、合成可能な新しいサービスのセットです。作成者は迅速に更新および公開でき、新しいサイトは迅速に起動します。 Edge 配信サービスについて詳しくは、 [はじめに](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html).

## 次のステップ {#what-is-next}

これで、AEM as a Cloud Service のオンボーディングジャーニーを開始する準備が整いました。このジャーニーの次の手順に進み、[オンボーディングの準備](preparation.md)の記事を読むことをお勧めします。

## AEM ドキュメントジャーニー {#documentation-journeys}

[ドキュメントジャーニー](/help/journey-documentation/documentation-journeys.md)では、多様かつ複雑なトピックおよび機能を組み合わせて説明しています。ここでは、AEM を初めて使用するユーザーが、以前のトピックや AEM に関する最小限の知識を有しているという前提で、ビジネス上の問題の全体を理解して解決するのに役立つ情報が提供されています。

ドキュメントジャーニーは、アドビの最新の調査、アドビのコンサルタントによる実装実績、顧客プロジェクトからのフィードバックなどに基づいて、ベストプラクティスの原則を軸に設計されています。

新しい AEM as a Cloud Service アプリケーションにチームをオンボーディングする方法について、アドビの推奨事項を理解するには、ここが出発点になります。

<!-- ERROR: Not Found (HTTP error 404)
## Additional Resources {#additional-resources}

The following are additional, optional resources if you would like to go beyond the content of the onboarding journey.

* [AEM Champion Tips and Tricks - Cloud Manager Onboarding Playbook](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Watch this video to learn Cloud Manager onboarding tips and trick from an AEM champion. -->


