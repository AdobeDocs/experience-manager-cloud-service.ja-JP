---
title: AEM as a Cloud Service チームおよび製品プロファイル
description: AEM as a Cloud Service チームおよび製品プロファイルでライセンス取得済みアドビソリューションへのアクセスを許可および制限する方法について説明します。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 69ac8e444a0f22649b48ec25b549ad60858f8b1b
workflow-type: ht
source-wordcount: '748'
ht-degree: 100%

---

# AEM as a Cloud Service チームおよび製品プロファイル {#product-profiles}

AEM as a Cloud Service チームおよび製品プロファイルでライセンス取得済みアドビソリューションへのアクセスを許可および制限する方法について説明します。

## 製品プロファイル {#profiles}

特定のアドビソリューションに対するアクセス権をユーザーに付与する場合、必ずしも完全なアクセス権を付与する必要はありません。製品プロファイルを使用すると、ソリューションごとに独自のユーザー権限を設定できます。これらのプロファイルは、[Admin Console](/help/journey-onboarding/admin-console.md) を通じて使用でき、アクセスできます。

## AEM as a Cloud Service 製品プロファイル {#aem-product-profiles}

AEM as a Cloud Service は、AEM をサービスとして提供する、完全にクラウドネイティブな製品です。常時稼動で、常に最新、常に安全、常にスケーラブルといった新しい属性を備えた AEM をクラウドネイティブな方法で提供します。それと同時に、カスタマイズ可能なプラットフォームとしての AEM の価値を維持し、エンタープライズクラスのチームが開発および配信の手順に統合することができます。AEM as a Cloud Service の詳細については、[Adobe Experience Manager as a Cloud Service の概要](/help/overview/introduction.md)を参照してください。

AEM as a Cloud Service チームメンバーは、オンボーディング時に Admin Console で追加され、次の製品プロファイルの 1 つ以上に割り当てられます。

* **AEM 管理者**：AEM 管理者は、通常、デベロッパー、特に開発環境などにアクセスする必要があるデベロッパーに割り当てられます。AEM 管理者の製品プロファイルは、関連する AEM インスタンスでの管理者権限を付与するために使用されます。

* **AEM ユーザー**：AEM ユーザーとは、AEM as a Cloud Service を通常、コンテンツの作成に使用する組織内ユーザーです。 これらのユーザーは、自らのタスクを実行するために AEM にアクセスする必要があります。通常、AEM ユーザー製品プロファイルは、コンテンツを作成およびレビューする AEM コンテンツ作成者に割り当てられます。 このコンテンツには、ページ、アセット、パブリケーションなど、様々なタイプがあります。 これらのメンバーには、以下に示す AEM ユーザー製品プロファイルが割り当てられます。

![製品プロファイル](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>AEM as a Cloud Service の製品プロファイルに割り当てられたすべてのユーザーは、**Cloud Manager ユーザー**&#x200B;の役割を介して Cloud Manager に読み取り専用でアクセスできます。
>
>**Cloud Manager ユーザー**&#x200B;の役割のみを持つユーザーは、Cloud Manager にログインし、**プログラム**&#x200B;メニューオプションを使用して AEM オーサー環境（存在する場合）に移動できます。**Cloud Manager ユーザー**&#x200B;の役割では、プログラムの詳細にアクセスするのに十分ではありません。 そのようなアクセスが必要な場合は、システム管理者から追加の役割を付与してもらう必要があります。

>[!TIP]
>
>* AEM 製品プロファイルについて詳しくは、[AEM 製品プロファイルの割り当て](/help/journey-onboarding/assign-profiles-aem.md)のドキュメントを参照してください。 
>* オンボーディングプロセスについて詳しくは、[オンボーディングジャーニー](/help/journey-onboarding/overview.md)を参照してください。


## Cloud Manager 製品プロファイル {#cloud-manager-product-profiles}

Cloud Manager には、役割ベースの権限と考えられる事前設定済み製品プロファイルがあります。 Cloud Manager チームをこれらの製品プロファイルに割り当てて設定するのは、システム管理者の仕事です。

>[!TIP]
>
>詳しくは、 [Cloud Manager での役割ベースの権限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)のドキュメントを参照してください。

それぞれの製品プロファイルには、固有の権限が関連付けられています。

* **ビジネスオーナー** - この役割には、新しいプログラムの追加、プログラムの編集、環境の追加または更新、AEM 環境へのコードのデプロイ、コード品質チェックの実行などを行う権限があります。
* **デプロイメントマネージャー** - この役割には、環境の追加または更新、任意のパイプラインの実行、AEM 環境へのコードのデプロイ、コード品質チェックの実行などを行う権限があります。
* **デベロッパー** - この役割には、Git にアクセスするための個人用アクセストークンを生成する権限があります。
* **プログラムマネージャー** - この役割には、パイプラインのスケジュール設定、3 層品質ゲートのオーバーライド、実稼動の承認などを行う権限があります。

1 人のユーザーを複数の製品プロファイルに割り当てることができます。例えば、**ビジネスオーナー**&#x200B;と&#x200B;**デプロイメントマネージャー**&#x200B;の両方の役割を 1 人のユーザーに割り当てると、これらの権限の組み合わせ（総和）が付与されます。

Cloud Manager チームには、少なくとも次の役割が含まれています。

* 1 人の&#x200B;**ビジネスオーナー**。通常はシステム管理者も兼ねており、Cloud Manager にログインしてアクセスする最初のユーザーでなければなりません
* 1 人の&#x200B;**デプロイメントマネージャー**
* 1 人の&#x200B;**デベロッパー**

>[!NOTE]
>
>ユーザーに AEM as a Cloud Service へのアクセスを許可するには、ユーザーが「`AEM Users`」または「`AEM Administrators`」のどちらかの製品プロファイルに属している必要があります。Cloud Manager を管理する権限では不十分です。

>[!TIP]
>
>* Cloud Manager 製品プロファイルについて詳しくは、[Cloud Manager 製品プロファイルへのチームメンバーの割り当てのドキュメントを参照してください。](/help/journey-onboarding/assign-profiles-cloud-manager.md)
>* オンボーディングプロセスについて詳しくは、[オンボーディングジャーニー](/help/journey-onboarding/overview.md)を参照してください。

