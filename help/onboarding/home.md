---
title: Adobe Experience Manager as a Cloud Service のオンボーディング
description: Adobe Experience Manager as a Cloud Service のオンボーディングに関するセルフヘルプリソースおよびドキュメントリンク
translation-type: tm+mt
source-git-commit: 826c15ecca494f98fbe7a4c3ef129a45bd4cea7c
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 42%

---


# Adobe Experience Manager as a Cloud Service のオンボーディング {#aem-onboarding-guide}

AEMをCloud Serviceとしてジャーニーを開始して、ありがとうございます。 新しいアプリケーションをデプロイする場合でも、既存のアプリケーションを移行する場合でも、このガイドは、アプリケーションが最適化され、Cloud Serviceに対する成功の準備ができるようにするための出発点として機能します。

このガイドは、Cloud Managerの使い始めを迅速に行う際に役立ちます。 Cloud Managerに追加されたユーザーに、割り当てられたロール(Admin Consoleの製品プロファイル)と関連する権限を与えるには、Adobe IDおよびシステム管理者の支援が必要です。 システム管理者がAdmin Consoleを使用してこれを行う方法については、説明しています。 Cloud Managerの役割のリスト(Admin Consoleでは製品プロファイルと呼ばれる)と、その関連する権限について詳しく説明し、組織の様々なユーザーにどの役割が必要かを判断できます。

次の図は、Cloud Service管理者が受け取ったご案内の電子メールから始まり、AEM用Cloud Managerにとしてアクセスするユーザーを最終的に管理しているオンボーディングジャーニーを示しています。

![](/help/onboarding/what-is-required/assets/cust-journey.png)

## オンボーディングに関する主要な記事 {#key-articles}

ここでは、AEMをCloud Serviceとして使用する場合の、ジャーニーに重点を置いた主要記事について説明します。

**オンボーディング中の期待事項**

契約書に署名すると、次のイベントが行われます。

1. Adobeは、組織のプロビジョニングを完了します。システム管理者は、ユーザーの追加、ロールへの割り当て、Cloud Managerへの適切なアクセス権の付与など、[システム管理者タスク](/help/onboarding/what-is-required/add-users-assign-cm-roles.md)を行うように通知する電子メールを受け取ります。

1. システム管理者が追加したユーザーにはご案内の電子メールが送信され、ユーザーは[Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md)に正常に移動できます。 ユーザーはAdobe IDを使用してログインし、ここからCloud Managerとのジャーニーを開始できます。

1. システム管理者は、開発を目的として、AEMインスタンス](/help/onboarding/what-is-required/accessing-aem-instance.md)への[ユーザーアクセスを許可することができます。

**[Adobe IDを取得](/help/onboarding/what-is-required/get-your-adobe-id.md)**

Cloud Managerに追加されたユーザーを割り当てられたロールに誘導するには、Adobe IDとシステム管理者の支援が必要です。

**[ユーザーの役割と権限](/help/onboarding/what-is-required/user-roles-permissions.md)**

システム管理者は、ユーザーを追加し、Cloud Managerの役割に割り当てることができます。 この節では、*Cloud Managerの役割*&#x200B;とは何か、およびその役割に関連付けられている権限を理解してから、操作を開始する際に役立ちます。

**[システム管理者のタスク](/help/onboarding/what-is-required/add-users-assign-cm-roles.md)**

システム管理者は、アクセスから権限まで、ユーザーのあらゆる側面を管理します。 このユーザーは、Admin ConsoleおよびCloud Manager内でタスクを行う開始に初めてアクセスできます。
次のドキュメントページには、基本的な組織のタスクを説明する情報が含まれています。

* ユーザーの追加
* Cloud Managerのロールと権限へのユーザーの割り当て

**[Cloud Manager に移動する](/help/onboarding/what-is-required/navigate-to-cloud-manager.md)**

ユーザーとして追加され、Cloud Managerロールに割り当てられたので、Cloud Managerにアクセスして、AEMでCloudジャーニーを使い始めることができます。 [プログラム](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md)の作成、[環境](/help/implementing/cloud-manager/manage-environments.md)の追加、[Git](/help/implementing/cloud-manager/accessing-git.md)へのアクセス、[パイプライン](/help/implementing/cloud-manager/configure-pipeline.md)の設定、[コード](/help/implementing/cloud-manager/deploy-code.md)の導入など、様々なタスクを行う準備が整っています。
Cloud Managerは、Cloud ServiceとしてAEMの重要な部分です。 これにより、組織はクラウド内のExperience Managerを自己管理できます。 このサービスには継続的統合および継続的配信（CI／CD）フレームワークが備わっているので、IT チームや実装パートナーはパフォーマンスやセキュリティを妥協することなくカスタマイズや更新を迅速に配信できます。ユーザーインターフェイスを使用して、CI/CDパイプラインの設定とキックオフを行うことができます。

**[AEMインスタンスへのユーザーアクセスの許可](/help/onboarding/what-is-required/accessing-aem-instance.md)**

このセクションでは、システム管理者または環境を作成したユーザが、他のユーザにAEMインスタンスへのアクセス権を与える方法について説明します。

## Adobe Experience Manager as a Cloud Service に関するガイド {#aem-guides}

| ユーザーガイド | 説明 |
|---|---|
| [Adobe Experience Manager as a Cloud Service のホーム](/help/landing/home.md) | Adobe Experience Manager as a Cloud Service ドキュメントの概要については、まずこちらを参照してください。 |
| [概要](/help/overview/home.md) | このガイドでは、ソリューションの紹介、用語など、Adobe Experience Manager as a Cloud Service の概要を説明します。 |
| [リリースノート](/help/release-notes/home.md) | このガイドでは、新機能、廃止される機能および削除された機能、既知の問題など、Adobe Experience Manager as a Cloud Service の最新リリースに関する重要な情報を提供します。 |
| [中心概念](/help/core-concepts/home.md) | このガイドでは、この新しいサービスのアーキテクチャなど、Adobe Experience Manager as a Cloud Service の中心概念について紹介します。 |
| [セキュリティユーザーガイド](/help/security/home.md) | Adobe Experience Manager as a Cloud Service のセキュリティに関する重要なトピックについて説明します。 |
| [Sites ユーザーガイド](/help/sites-cloud/home.md) | Adobe Experience Manager Sites as a Cloud Service を使用したオーサリングおよび管理方法について説明します。 |
| [Assets ユーザーガイド](/help/assets/home.md) | Adobe Experience Manager Assets as a Cloud Service の使用と管理方法について説明します。 |
| [AEM as a Cloud Service への移行](/help/move-to-cloud-service/home.md) | AEM as a Cloud Service への移行プロセスについて説明します |
| [実装ユーザーガイド](/help/implementing/home.md) | 開発およびデプロイメントに関するトピックなど、Adobe Experience Manager as a Cloud Service のデプロイメントをカスタマイズする方法について説明します。 |
| [コネクタユーザーガイド](/help/connectors/home.md) | Adobe Experience Manager as a Cloud Service にコネクタを統合する方法を説明します。 |
| [運用ユーザーガイド](/help/operations/home.md) | インデックス作成やメンテナンスタスクなど、Adobe Experience Manager as a Cloud Service のバックエンド運用について説明します。 |
| [Commerce ユーザーガイド](/help/commerce-cloud/home.md) | AEM as a Cloud Service の Commerce Integration Framework について説明します。 |

## Adobe Experience Manager のその他のリソース {#other-resources}

* [最近のドキュメントの更新](https://helpx.adobe.com/jp/experience-manager/documentation-updates.html#AEMasaCloudService)
* [Dispatcher のドキュメント](/help/implementing/dispatcher/overview.md)
* [HTL のドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/overview.html)
* [コアコンポーネントのドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)
* [Cloud Manager のドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/first-time-login.html)
* [GDPR 対応](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)
* [Adobe Experience Manager as a Cloud Service のチュートリアル](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/cloud-service/overview.html)
* [Experience League](https://guided.adobe.com/?promoid=K42KVXHD&amp;mv=other#solutions/experience-manager)
* [AEM コミュニティフォーラム](https://forums.adobe.com/community/experience-cloud/marketing-cloud/experience-manager)