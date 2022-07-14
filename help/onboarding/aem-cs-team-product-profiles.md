---
title: AEM as a Cloud Service チームおよび製品プロファイル
description: AEMのas a Cloud Serviceチームおよび製品プロファイルを使用して、ライセンスを取得したAdobeソリューションへのアクセスを許可および制限する方法について説明します。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 2d793f22e554c2a4bde8831b5053d1640ba07c70
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 28%

---

# AEM as a Cloud Service チームおよび製品プロファイル {#product-profiles}

AEMのas a Cloud Serviceチームおよび製品プロファイルを使用して、ライセンスを取得したAdobeソリューションへのアクセスを許可および制限する方法について説明します。

## 製品プロファイル {#profiles}

特定のアドビソリューションに対するアクセス権をユーザーに付与する場合、必ずしも完全なアクセス権を付与する必要はありません。製品プロファイルを使用すると、各ソリューションに独自のユーザー権限セットを設定できます。 これらは、 [Admin Console。](/help/journey-onboarding/admin-console.md)

## AEM as a Cloud Service 製品プロファイル {#aem-product-profiles}

AEMas a Cloud Serviceは、AEMをサービスとして提供する、完全にクラウドネイティブな製品です。 常時稼動で、常に最新、常に安全、常にスケーラブルといった新しい属性を備えた AEM をクラウドネイティブな方法で提供します。それと同時に、カスタマイズ可能なプラットフォームとしての AEM の価値を維持し、エンタープライズクラスのチームが開発および配信の手順に統合することができます。AEM as a Cloud Service の詳細については、[Adobe Experience Manager as a Cloud Service の概要](/help/overview/introduction.md)を参照してください。

オンボーディング中に、Admin Consoleを通じてAEMas a Cloud Serviceチームメンバーが追加され、次の 1 つ以上の製品プロファイルに割り当てられます。

* **AEM Administrators**:通常、AEM管理者は開発者、特に開発環境などへのアクセス権が必要な開発者に割り当てられます。 AEM管理者の製品プロファイルは、関連するAEMインスタンスで管理者権限を付与するために使用されます。

* **AEM Users**:AEMユーザーとは、AEM as a Cloud Serviceを一般的に使用してコンテンツを作成する、組織内のユーザーです。 これらのユーザーは、タスクを実行するためにAEMにアクセスする必要があります。 通常、AEMユーザー製品プロファイルは、コンテンツを作成およびレビューするAEMコンテンツ作成者に割り当てられます。 このコンテンツには、ページ、アセット、パブリケーションなど、様々なタイプがあります。 以下に示すAEMユーザー製品プロファイルが、これらのメンバーに割り当てられます。

![製品プロファイル](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>AEM as a Cloud Service 製品プロファイルに割り当てられたすべてのユーザーは、Cloud Manager への（読み取り専用）アクセスが可能になります。

>[!TIP]
>
>オンボーディングプロセスについて詳しくは、 [オンボーディングジャーニー。](/help/journey-onboarding/overview.md)

## Cloud Manager 製品プロファイル {#cloud-manager-product-profiles}

Cloud Manager には、ロールベースの権限と考えられる、事前設定済みの製品プロファイルがあります。 システム管理者は、Cloud Manager チームをこれらの製品プロファイルに割り当てて設定する必要があります。

>[!TIP]
>
>ドキュメントを参照してください [Cloud Manager のロールに基づく権限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) を参照してください。

各製品プロファイルには、関連付けられた特定の権限があります。

* **ビジネスオーナー**  — この役割では、新しいプログラムの追加、プログラムの編集、環境の追加または更新、パイプラインの追加/編集/削除/実行、AEM環境へのコードのデプロイ、コード品質チェックの実行の権限を持っています。
* **デプロイメントマネージャー**  — このロールでは、環境の追加または更新、任意のパイプラインの実行、AEM環境へのコードのデプロイ、コード品質チェックの実行をおこなう権限を持っています。
* **開発者**  — このロールでは、Git にアクセスするための個人用アクセストークンを生成する権限を持っています。
* **プログラムマネージャ**  — この役割では、パイプラインのスケジュール、3 層品質ゲートの上書き、実稼動の承認をおこなう権限を持っています。

1 人のユーザーを複数の製品プロファイルに割り当てることができます。例： **ビジネスオーナー** および **デプロイメント管理**&#x200B;ユーザーに対する r の役割は、これらの権限の合計を与えます。

Cloud Manager チームには、少なくとも次の役割が含まれます。

* 1 **ビジネスオーナー**（通常はシステム管理者で、Cloud Manager に初めてログインしてアクセスする必要があります）
* 1 **デプロイメントマネージャー**
* 1 **開発者**

>[!NOTE]
>
>ユーザーが AEM as a Cloud Service へのアクセス権を付与されるには、「`AEM Users`」または「`AEM Administrators`」のどちらかの製品プロファイルに属している必要があります。Cloud Manager を管理する権限では不十分です。
