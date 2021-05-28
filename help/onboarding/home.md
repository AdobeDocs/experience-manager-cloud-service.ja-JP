---
title: Adobe Experience Manager as a Cloud Service のオンボーディング
description: Adobe Experience Manager as a Cloud Service のオンボーディングに関するセルフヘルプリソースおよびドキュメントリンク
exl-id: 24cc7ad9-3556-4462-89c7-5bc1fc18218a
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 23%

---

# [!DNL Experience Manager as a Cloud Service] {#aem-onboarding-guide}へのオンボーディング

>[!CONTEXTUALHELP]
>id="aemcloud_onboarding_overview"
>title="オンボーディングの概要"
>abstract="新しいアプリケーションをデプロイする場合でも、既存のアプリケーションを移行する場合でも、このガイドは、アプリケーションが最適化され、Cloud Serviceを成功させる準備が整っていることを確認するための出発点として機能します。 Cloud Managerに追加されたユーザーを、割り当てられた役割と関連する権限に導くには、Adobe IDとシステム管理者のヘルプが必要です。"
>additional-url="https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/SLAExhibit-AEMCloudService-2019DEC12.pdf" text="サービス・レベルの展示 — AEM as aCloud Service"

AEM as aをCloud Serviceにして、ジャーニーを開始しました。 新しいアプリケーションをデプロイする場合でも、既存のアプリケーションを移行する場合でも、このガイドは、アプリケーションが最適化され、Cloud Serviceを成功させる準備が整っていることを確認するための出発点として機能します。

このガイドは、ユーザーとチームがCloud Managerの利用をすぐに開始するのに役立ちます。 割り当てられたロール(Admin Consoleの製品プロファイル)と関連する権限にCloud Managerに追加されたユーザーを取得するには、Adobe IDとシステム管理者のヘルプが必要です。 システム管理者がシステムを使用してこれを行う方法については、Admin Consoleを参照してください。 Cloud Managerのロール(Admin Console内の製品プロファイルと呼ばれる)のリストと、それに関連する権限について詳しく説明し、組織内の様々なユーザーに必要なロールを判断できます。

次の画像は、システム管理者が受け取ったお知らせメールから始めて、AEM用Cloud ManagerにCloud Serviceとしてアクセスするユーザーをカウントする、オンボーディングジャーニーを示しています。

![](/help/onboarding/what-is-required/assets/cust-journey.png)

## オンボーディングに関する主要な記事 {#key-articles}

ここでは、AEM as a Cloud Serviceを使い始める際の重要な記事を紹介します。

**オンボーディング中に期待する事項**

契約が結ばれると、次のイベントが発生します。

1. Adobeは組織のプロビジョニングを完了し、組織のシステム管理者に「[システム管理者タスク](/help/onboarding/what-is-required/add-users-assign-cm-roles.md)」の電子メールを受け取ります。ユーザーの追加、役割への割り当て、Cloud Managerへの適切なアクセス権の付与も含まれます。

1. システム管理者が追加したユーザーには、「ようこそ」の電子メールが届き、ユーザーは正常に[Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md)に移動できます。 Adobe IDを使用してログインし、ここからCloud Managerでジャーニーを開始できるようになりました。

1. システム管理者は、開発目的でAEMインスタンス](/help/onboarding/what-is-required/accessing-aem-instance.md)に対するユーザーアクセスを[付与できます。

**[Adobe ID](/help/onboarding/what-is-required/get-your-adobe-id.md)**

Cloud Managerに追加されたユーザーを、割り当てられた役割に導くには、Adobe IDとシステム管理者の支援が必要です。

**[Cloud Manager のロール](/help/onboarding/what-is-required/user-roles-permissions.md)**

システム管理者は、ユーザーを追加して、Cloud Managerの役割に割り当てることができます。 この節では、導入前に、*Cloud Managerのロール*&#x200B;とは何か、およびロールに関連付けられている権限について説明します。

**[システム管理者のタスク](/help/onboarding/what-is-required/add-users-assign-cm-roles.md)**

システム管理者は、アクセスから権限まで、ユーザーのすべての側面を管理します。 このユーザーは、CloudおよびCloud Manager内でタスクの実行を開始する権限を持つ最初のAdmin Consoleです。
次のドキュメントページには、基本的な組織的タスクを説明する情報が含まれています。

* ユーザーの追加
* Cloud Managerの役割と権限へのユーザーの割り当て

**[Cloud Manager に移動する](/help/onboarding/what-is-required/navigate-to-cloud-manager.md)**

これで、ユーザーとして追加され、 Cloud Managerの役割に割り当てられたので、 Cloud Managerにアクセスして、AEMを使用したCloudジャーニーを開始できます。 ユーザーは、[プログラム](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md)の作成、[環境](/help/implementing/cloud-manager/manage-environments.md)の追加、[Git](/help/implementing/cloud-manager/accessing-git.md)へのアクセス、[パイプライン](/help/implementing/cloud-manager/configure-pipeline.md)の設定、[コード](/help/implementing/cloud-manager/deploy-code.md)のデプロイなど、様々なタスクを実行できます。
Cloud Managerは、AEM as a Cloud Serviceの重要な部分です。 これにより、組織はクラウド内の[!DNL Experience Manager]を自己管理できます。 このサービスには継続的統合および継続的配信（CI／CD）フレームワークが備わっているので、IT チームや実装パートナーはパフォーマンスやセキュリティを妥協することなくカスタマイズや更新を迅速に配信できます。ユーザーインターフェイスを使用して、CI/CDパイプラインを設定および開始できます。

**[AEMインスタンスへのユーザーアクセスの許可](/help/onboarding/what-is-required/accessing-aem-instance.md)**

この節では、システム管理者または環境を作成したユーザーが、他のユーザーにAEMインスタンスへのアクセス権を付与する方法について説明します。

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
| [実装ユーザーガイド](/help/implementing/home.md) | AEMの強力な機能を使用してエクスペリエンスを構築およびカスタマイズする方法を理解するには、以下の開発およびデプロイメントに関するトピックを参照してください。 |
| [ヘッドレス開発者ジャーニー](/help/journey-headless/developer/overview.md) | AEMの強力で柔軟なヘッドレス機能を通じて、このガイド付きジャーニーを調べ、最初のヘッドレスプロジェクトに備えます。 |
| [コネクタユーザーガイド](/help/connectors/home.md) | [!DNL Experience Manager as a Cloud Service]にコネクタを統合する方法を説明します。 |
| [運用ユーザーガイド](/help/operations/home.md) | インデックス作成やメンテナンスタスクなど、Adobe [!DNL Experience Manager as a Cloud Service]  のバックエンド運用について説明します。 |
| [Commerce ユーザーガイド](/help/commerce-cloud/home.md) | [!DNL Experience Manager as a Cloud Service]のCommerce Integration Frameworkについて説明します。 |

## その他の[!DNL Experience Manager]リソース{#other-resources}

* [最近のドキュメントの更新](https://helpx.adobe.com/jp/experience-manager/documentation-updates.html#AEMasaCloudService)
* [Dispatcher のドキュメント](/help/implementing/dispatcher/overview.md)
* [HTL のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=ja)
* [コアコンポーネントのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)
* [Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/first-time-login.html)
* [GDPR 対応](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)
* [Adobe Experience Manager as a Cloud Service のチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=ja)
* [Experience League](https://guided.adobe.com/?promoid=K42KVXHD&amp;mv=other#solutions/experience-manager)
* [AEM コミュニティフォーラム](https://forums.adobe.com/community/experience-cloud/marketing-cloud/experience-manager)
