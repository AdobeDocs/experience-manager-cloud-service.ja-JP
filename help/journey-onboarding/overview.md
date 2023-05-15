---
title: AEM as a Cloud Service オンボーディングジャーニーの概要
description: AEM as a Cloud Service のオンボーディングプロセスのガイド付きジャーニーの概要については、ここから始めてください。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 58%

---


# オンボーディングジャーニー {#onboarding-journey}

AEM as a Cloud Service を選択していただき、ありがとうございます。このドキュメントは、オンボーディングプロセスのガイド付きジャーニーの出発点です。新しいアプリケーションをデプロイする場合でも、既存のアプリケーションを移行する場合でも、このオンボーディングジャーニーでは、チームが設定され、AEM as a Cloud Serviceにアクセスできるようにします。

## はじめに {#introduction}

オンボーディングとは、指定されたシステム管理者が AEM as a Cloud Service を組織用に設定するプロセスです。このプロセスには、クラウドリソースの初期プロビジョニングと、ユーザーの職務に基づく役割の割り当てが含まれます。 その結果、各メンバーはAEM as a Cloud Service上の自分のリソースにログオンしてアクセスできます。

![オンボーディングジャーニー](/help/journey-onboarding/assets/onboarding-journey.png)

このガイドでは、最も重要なオンボーディングトピックを順を追って説明し、完了時に次の操作をおこないます。

* オンボーディングプロセスに関わる様々な用語、サービス、ユーザーの完全な理解。
* AEM as a Cloud Service アプリケーションのコンテンツを作成および開発する方法の習得に向けて、チームが立ち上がり、最初のステップを踏み出せるようにする。

これにより、以下を実現できます。

* チームが設定され、クラウドリソースにアクセスできます。
* AEM作成者はAEM as a Cloud Serviceにアクセスでき、コンテンツの作成を開始できます。
* AEMの開発者およびデプロイメントマネージャーは、AEM as a Cloud Serviceにアクセスでき、カスタムアプリケーションの作成とデプロイを開始できます。

## 概念と目標 {#concepts}

AEM as a Cloud Service を使い始めると、学ぶべきことがたくさんあるように見えるかもしれませんが、概念的には論理的なポイントは少ししかありません。

* **契約**  — オンボーディングプロセスの側面を定義するので、Adobe契約に詳しい必要があります。
* **Admin Console**  — ユーザーが管理され、役割が割り当てられる場所。
* **Cloud Manager**  — プログラムや環境などのリソースを設定するツール。 また、カスタムコードを管理およびデプロイするために、Git にアクセスしてパイプラインを作成する場所でもあります。

これらの概念については、このオンボーディングジャーニーで詳しく説明します。 目標は、ジャーニーの最後に、次の状態になるようにすることです。

* AEM as a Cloud Serviceへの必要なユーザーのアクセス権を付与済み。
* プロジェクトに最初のクラウドリソースを設定している.
* 最初のコードをデプロイし、最初のコンテンツを作成する方法を理解している

基本的に、新しいAEMas a Cloud Serviceプロジェクトで実行する場面にぶつかります。

## 対象読者 {#audience}

オンボーディングジャーニーは、AEM as a Cloud Service および一般的な AEM を初めて使用するお客様の&#x200B;**システム管理者**&#x200B;向けに特別に書かれています。システム管理者は、AEMas a Cloud Service契約の署名後、Adobeから最初に連絡を受けるユーザーです。 通常は、AEM as a Cloud Serviceでリソースにアクセスして設定するのはこのユーザーが最初です。 このトピックを読む場合は、おそらくシステム管理者です。

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
>AEMを初めて使い慣れており、AEMに慣れており、オンプレミスまたは Adobe Managed Services から移行する場合は、必ず [AEMas a Cloud Service移行ジャーニー](/help/journey-migration/getting-started.md).

## オンボーディングジャーニーの概要 {#overview}

以下の記事では、オンボーディングのコアとなる概念を詳しく説明し、AEM as a Cloud Service に関する基本的な知識を提供します。ジャーニーの特定の部分に直接移動することもできますが、多くの概念は、それまでの記事で紹介された概念に基づいています。したがって、オンボーディングを初めておこなう場合は、最初から順に進めることをAdobeに勧めます。

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
| 8 | [AEM 製品プロファイルの割り当て](assign-profiles-aem.md) | システム管理者がAEM as a Cloud Serviceの製品プロファイルにチームメンバーを割り当てる方法を説明します。 | システム管理者 |
| 9 | [開発者およびデプロイメントマネージャーのタスク](developers.md) | オプション — 開発者は、Cloud Manager Git にアクセスして管理する方法と、Cloud Manager でパイプラインを設定してコードをデプロイする方法を学びます。 | 開発者およびデプロイメントマネージャー |
| 10 | [AEM ユーザーのタスク](aem-users.md) | オプション — AEMの作成者として、AEMas a Cloud Serviceインスタンスにアクセスする方法と、AEMのas a Cloud Service用のコンテンツのオーサリングについて詳しく説明します。 | AEM ユーザー |

## 次のステップ {#what-is-next}

これで、AEM as a Cloud Service のオンボーディングジャーニーを開始する準備が整いました。ジャーニーの次の段階に進み、記事を読むことをお勧めします。 [オンボーディングの準備](preparation.md)

## AEM ドキュメントのジャーニー {#documentation-journeys}

[ドキュメントジャーニー](/help/journey-documentation/documentation-journeys.md) 様々な複雑なトピックや機能を結び付けます。 AEMを初めて使用する読者が、最初から最後までビジネス上の問題を理解し、解決するのに役立つ情報を提供します。また、前のトピックやAEMに関する知識は最小限に抑えられます。

ドキュメントジャーニーは、アドビの最新の調査、アドビのコンサルタントによる実装実績、顧客プロジェクトからのフィードバックなどに基づいて、ベストプラクティス原則を軸に設計されています。

チームを新しいAEMas a Cloud ServiceAdobeにオンボーディングする方法についての推奨事項を知りたい場合は、ここから始めてください。

<!-- ERROR: Not Found (HTTP error 404)
## Additional Resources {#additional-resources}

The following are additional, optional resources if you would like to go beyond the content of the onboarding journey.

* [AEM Champion Tips and Tricks - Cloud Manager Onboarding Playbook](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Watch this video to learn Cloud Manager onboarding tips and trick from an AEM champion. -->


