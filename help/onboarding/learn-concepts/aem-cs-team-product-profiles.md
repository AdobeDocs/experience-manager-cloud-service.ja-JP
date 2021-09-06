---
title: AEM as a Cloud Serviceチームと製品プロファイル
description: このページでは、AEM as a Cloud Serviceチームと製品プロファイルについて説明します。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 56ca8e80081e62ceb3f5fc2bf9c32aa3bcee12c6
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 8%

---

# AEM as a Cloud Serviceチームと製品プロファイル {#product-profiles}

## 製品プロファイル {#profiles}

特定のAdobeソリューションに対するアクセス権をユーザーに付与する場合、必ずしも完全なアクセス権を付与する必要はありません。 製品プロファイルを使用すると、各ソリューションに独自のユーザー権限を設定できます。 これらは、[Adobe Admin Console](/help/onboarding/learn-concepts/admin-console.md)を介して使用でき、アクセスできます。

詳しくは、[AEM as a Cloud Product Profiles](#aem-product-profiles)および[Cloud ManagerCloud Serviceプロファイル](#cloud-manager-product-profiles)を参照し、チームのセットアップ中にこれらのプロファイルがどのように連携するかを理解してください。

## AEM as a Cloud Service製品プロファイル {#aem-product-profiles}

AEM as a Cloud Serviceは、AEMをサービスとして提供する、完全にクラウドネイティブな製品です。 常にオン、常に最新、常にセキュリティで保護、常に規模に応じた新しい属性を使用して、AEMをネイティブな方法で提供します。 同時に、AEMが顧客にカスタマイズ可能なプラットフォームとして提供する主な価値提案を保持し、エンタープライズグレードのチームが開発と配信の手順で統合できるようにします。 AEM as aCloud Serviceの詳細については、「 [Cloud ServiceとしてのAdobe Experience Managerの概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=ja) 」を参照してください。

オンボーディング中に、AEM as a  as aCloud Serviceチームのメンバーが追加され、Admin Consoleを介して次の1つ以上の製品プロファイルに割り当てられます。

* **AEM管理者**:AEM管理者は、通常、開発者、特に開発環境などへのアクセス権が必要な開発者に割り当てられます。AEM Administrators製品プロファイルは、関連するAEMインスタンスで管理者権限を付与するために使用されます。

* **AEMユーザー**:AEMユーザーとは、組織内で、AEMをAdobeとの契約の一部としてCloud Serviceとして使用するユーザーです。これらのメンバーは、タスクを実行するためにAEMにアクセスする必要があります。 AEMユーザー製品プロファイルは、通常、コンテンツを作成およびレビューするAEMコンテンツ作成者に割り当てられます（複数のタイプがあります）。（ページ、アセット、パブリケーションなど）をwebサイトに公開する前に設定する必要があります。 以下に示すAEM Users製品プロファイルは、これらのメンバーに割り当てられます。

   ![](/help/onboarding/learn-concepts/assets/admin-console-profiles.png)

   >[!NOTE]
   >AEM as a Cloud製品プロファイルに割り当てられたすべてのCloud Serviceは、Cloud Managerに（読み取り専用）アクセスできます。

## Cloud Manager製品プロファイル {#cloud-manager-product-profiles}

Cloud Managerには、事前設定済みの製品プロファイル、またはより簡単な役割ベースの権限があります。 システム管理者は、これらの製品プロファイルにを割り当ててCloud Managerチームの設定を担当します。また、これらの製品プロファイルと、それらのプロファイルを割り当てるチームメンバーについて理解しておく必要があります。
>[!NOTE]
>詳しくは、[Cloud Managerのロールに基づく権限](/help/onboarding/learn-concepts/cloud-manager-introduction.md##role-based-permissions)を参照してください。

各製品プロファイルには、関連付けられた特定の権限があります。 以下は、ロールと権限の例です。

* **ビジネスオーナー**&#x200B;になると、新しいプログラムの追加やプログラムの編集、環境の追加/更新、パイプラインの追加/編集/削除、および任意のパイプラインの実行、AEM環境またはコード品質へのコードのデプロイができます。

* **デプロイメントマネージャー** - 環境の追加またはアップデート、任意のパイプラインの実行、AEM 環境またはコード品質へのコードのデプロイをおこなう権限があります。

* **デベロッパー** - Git にアクセスするための個人用アクセストークンを生成する権限があります。

* **プログラムマネージャー**&#x200B;を使用すると、パイプラインのスケジュール、3層品質ゲートの上書き、実稼動の承認をおこなう権限を持っています。

ユーザーは複数の製品プロファイルに割り当てることができます。 例えば、ビジネスオーナーとデプロイメントマネージャーの役割の両方をユーザーに割り当てると、これらの権限の組み合わせまたは合計が表示されます。

Cloud Managerチームには、以下が含まれます。

* 1人のビジネスオーナー（通常はシステム管理者で、Cloud Managerにログインしてアクセスする最初のユーザーである必要があります）
* 1つのデプロイメントマネージャ
* 開発者1人

   >[!NOTE]
   >AEM as aCloud Serviceへのアクセス権を付与するには、ユーザーが次の2つの製品プロファイルのいずれかに属している必要があります。`AEM Users`または`AEM Administrators`。 インスタンスに対する権限を付与されている必要があります。関連するCloud Managerを管理する権限では不十分です。
