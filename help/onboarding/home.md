---
title: Adobe Experience Manager as a Cloud Service のオンボーディング
description: Adobe Experience Manager as a Cloud Service のオンボーディングに関するセルフヘルプリソースおよびドキュメントリンク
exl-id: 24cc7ad9-3556-4462-89c7-5bc1fc18218a
source-git-commit: d022b73d84d150c156695106f4a5fe2c75d90664
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 86%

---

# [!DNL Experience Manager as a Cloud Service]へのオンボーディング {#aem-onboarding-guide}

>[!CONTEXTUALHELP]
>id="aemcloud_onboarding_overview"
>title="オンボーディングの概要"
>abstract="新しいアプリケーションをデプロイする場合でも、既存のアプリケーションを移行する場合でも、このガイドは、アプリケーションが最適化され、Cloud Service で成功するための出発点となります。Cloud Manager にユーザーを追加し、役割と関連する権限を割り当てるには、Adobe ID とシステム管理者の助けが必要です。"

AEM as a Cloud Service のジャーニーが始まりました。新しいアプリケーションをデプロイする場合でも、既存のアプリケーションを移行する場合でも、このガイドは、アプリケーションが最適化され、Cloud Service で成功するための出発点となります。

このガイドは、個人でもチームでも、Cloud Manager をすぐに使い始めるのに役立ちます。Cloud Manager にユーザーを追加し、役割（Admin Console の製品プロファイル）と関連する権限を割り当てるには、Adobe ID とシステム管理者の助けが必要です。システム管理者が Admin Console を介してこれを行う方法を説明します。Cloud Manager の役割（Admin Console では製品プロファイルと呼ぶ）のリストと、それに関連する権限について詳しく説明するので、組織内の様々なユーザーに必要な役割を判断できます。

次の図は、システム管理者が受け取る「ようこそ」メールから始まり、ユーザーが AEM as a Cloud Service の Cloud Manager にアクセスするまでのオンボーディングの流れを示しています。

![](/help/onboarding/what-is-required/assets/cust-journey.png)

## オンボーディングに関する主要な記事 {#key-articles}

ここでは、AEM as a Cloud Service を使い始める際に重要な記事を紹介します。

**オンボーディング中に期待する事項**

契約が締結されると、次のイベントが発生します。

1. アドビが組織のプロビジョニングを完了すると、組織のシステム管理者は「ようこそ」メールを受け取ります。これにより、システム管理者は「[システム管理者タスク](/help/onboarding/what-is-required/add-users-assign-cm-roles.md)」を実行して、ユーザーの追加、役割への割り当て、Cloud Manager への適切なアクセス権の付与などを行えるようになります。

1. システム管理者が追加したユーザーは「ようこそ」メールを受け取り、[Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md) にアクセスできるようになります。ユーザーは Adobe ID を使用してログインし、Cloud Manager でジャーニーを開始できるようになります。

1. システム管理者は、開発目的で [AEM インスタンスにユーザーアクセスを付与](/help/onboarding/what-is-required/accessing-aem-instance.md)できます。

**[Adobe ID を入手](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/adobe-id.html?lang=en)**

ユーザーを Cloud Manager に追加して役割を割り当てるには、Adobe ID とシステム管理者の支援が必要です。

**[Cloud Manager の役割](/help/onboarding/what-is-required/user-roles-permissions.md)**

システム管理者は、ユーザーを追加して、Cloud Manager の役割に割り当てることができます。この節ではまず、*Cloud Manager の役割*&#x200B;と役割に関連付けられている権限について説明します。

**[システム管理者のタスク](/help/onboarding/what-is-required/add-users-assign-cm-roles.md)**

システム管理者は、アクセスから権限まで、ユーザーのすべての側面を管理します。このユーザーは、Admin Console および Cloud Manager 内でタスクの実行を開始する権限を持つ最初のユーザーです。
次のドキュメントページには、組織の基本的なタスクを説明する情報が含まれています。

* ユーザーの追加
* Cloud Manager の役割と権限へのユーザーの割り当て

**[Cloud Manager に移動する](/help/onboarding/what-is-required/navigate-to-cloud-manager.md)**

ユーザーとして追加され、 Cloud Manager の役割に割り当てられたら、 Cloud Manager にアクセスして、AEM で Cloud ジャーニーを開始できます。ユーザーは、プログラムの作成、環境の追加、[Git](/help/implementing/cloud-manager/accessing-git.md)へのアクセス、[パイプラインの設定](/help/implementing/cloud-manager/configure-pipeline.md)、[コードのデプロイ](/help/implementing/cloud-manager/deploy-code.md)など、様々なタスクを実行できます。
Cloud Manager は、AEM as a Cloud Service の重要な部分です。これにより、組織はクラウド内の[!DNL Experience Manager]を自己管理できます。 このサービスには継続的統合および継続的配信（CI／CD）フレームワークが備わっているので、IT チームや実装パートナーはパフォーマンスやセキュリティを妥協することなくカスタマイズや更新を迅速に配信できます。ユーザーインターフェイスを使用して、CI／CD パイプラインを設定および開始できます。

**[AEM インスタンスへのユーザーアクセスの許可](/help/onboarding/what-is-required/accessing-aem-instance.md)**

この節では、システム管理者または環境を作成したユーザーが、他のユーザーに AEM インスタンスへのアクセス権を付与する方法について説明します。

## [!DNL Experience Manager as a Cloud Service] ガイド {#aem-guides}

| ユーザーガイド | 説明 |
|---|---|
| [Adobe Experience Manager as a Cloud Service のホーム](/help/landing/home.md) | Adobe Experience Manager as a Cloud Service ドキュメントの概要については、まずこちらを参照してください。 |
| [概要](/help/overview/home.md) | このガイドでは、導入、用語など、[!DNL Experience Manager as a Cloud Service]の概要を説明します。 |
| [リリースノート](/help/release-notes/home.md) | このガイドでは、新機能、廃止される機能、削除された機能、既知の問題など、[!DNL Experience Manager as a Cloud Service]の最新リリースに関する重要な情報を提供します。 |
| [中心概念](/help/core-concepts/home.md) | このガイドでは、この新しいサービスのアーキテクチャなど、Adobe [!DNL Experience Manager as a Cloud Service]  の中心概念について紹介します。 |
| [セキュリティユーザーガイド](/help/security/home.md) | [!DNL Experience Manager as a Cloud Service]に関する重要なセキュリティトピックについて説明します。 |
| [Sites ユーザーガイド](/help/sites-cloud/home.md) | Cloud Serviceとして[!DNL Experience Manager Sites]を使用してオーサリングおよび管理する方法を理解します。 |
| [Assets ユーザーガイド](/help/assets/home.md) | [!DNL Experience Manager Assets as a Cloud Service]の使い方と管理方法を理解します。 |
| [AEM as a Cloud Service への移行](/help/move-to-cloud-service/home.md) | AEM as a Cloud Service への移行プロセスについて説明します |
| [実装ユーザーガイド](/help/implementing/home.md) | AEM の強力な機能を使用してエクスペリエンスを構築およびカスタマイズする方法を理解するには、以下の開発およびデプロイメントに関するトピックを参照してください。 |
| [ヘッドレスデベロッパージャーニー](/help/journey-headless/developer/overview.md) | AEM の強力で柔軟なヘッドレス機能を紹介するこのガイド付きのジャーニーを進めて、初めてのヘッドレスプロジェクトの準備をしてください。 |
| [コネクタユーザーガイド](/help/connectors/home.md) | [!DNL Experience Manager as a Cloud Service]にコネクタを統合する方法を説明します。 |
| [運用ユーザーガイド](/help/operations/home.md) | インデックス作成やメンテナンスタスクなど、Adobe [!DNL Experience Manager as a Cloud Service]  のバックエンド運用について説明します。 |
| [Commerce ユーザーガイド](/help/commerce-cloud/home.md) | [!DNL Experience Manager as a Cloud Service]のCommerce Integration Frameworkについて説明します。 |

## その他の[!DNL Experience Manager]リソース {#other-resources}

* [最近のドキュメントの更新](https://helpx.adobe.com/jp/experience-manager/documentation-updates.html#AEMasaCloudService)
* [Dispatcher のドキュメント](/help/implementing/dispatcher/overview.md)
* [HTL のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=ja)
* [コアコンポーネントのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)
* [Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/first-time-login.html)
* [GDPR 対応](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md)
* [Adobe Experience Manager as a Cloud Service のチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=ja)
* [Experience League](https://guided.adobe.com/?promoid=K42KVXHD&amp;mv=other#solutions/experience-manager)
* [AEM コミュニティフォーラム](https://forums.adobe.com/community/experience-cloud/marketing-cloud/experience-manager)
