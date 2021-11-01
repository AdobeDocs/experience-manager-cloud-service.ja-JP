---
title: AEM as a Cloud Service チームおよび製品プロファイル
description: このページでは、AEM as a Cloud Service チームおよび製品プロファイルについて説明します。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 56ca8e80081e62ceb3f5fc2bf9c32aa3bcee12c6
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 100%

---

# AEM as a Cloud Service チームおよび製品プロファイル {#product-profiles}

## 製品プロファイル {#profiles}

特定のアドビソリューションに対するアクセス権をユーザーに付与する場合、必ずしも完全なアクセス権を付与する必要はありません。製品プロファイルを使用すると、ソリューションごとに独自のユーザー権限を設定できます。これらのプロファイルは、[Adobe Admin Console](/help/onboarding/learn-concepts/admin-console.md) を通じて使用でき、アクセスできます。

チームのセットアップ時にこれらのプロファイルがどのように連携するかについて詳しくは、[AEM as a Cloud Service 製品プロファイル](#aem-product-profiles)および [Cloud Manager 製品プロファイル](#cloud-manager-product-profiles)を参照してください。

## AEM as a Cloud Service 製品プロファイル {#aem-product-profiles}

AEM as a Cloud Service は、AEM をサービスとして提供する、完全にクラウドネイティブな製品です。常時稼動で、常に最新、常に安全、常にスケーラブルといった新しい属性を備えた AEM をクラウドネイティブな方法で提供します。それと同時に、カスタマイズ可能なプラットフォームとしての AEM の価値を維持し、エンタープライズクラスのチームが開発および配信の手順に統合することができます。AEM as a Cloud Service の詳細については、[Adobe Experience Manager as a Cloud Service の概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=ja)を参照してください。

AEM as a Cloud Service チームのメンバーは、オンボーディング中に Admin Console で次の 1 つ以上の製品プロファイルに追加され割り当てられます。

* **AEM 管理者**：AEM 管理者は、通常、開発者、特に開発環境などにアクセスする必要がある開発者に割り当てられます。「AEM 管理者」製品プロファイルは、関連する AEM インスタンスで管理者権限を付与するために使用されます。

* **AEM ユーザー**：AEM ユーザーは、アドビとの契約の一環として AEM as a Cloud Service を使用する組織内のユーザーです。これらのメンバーは、作業を実行するために AEM にアクセスする必要があります。「AEM ユーザー」製品プロファイルは、通常、コンテンツを作成して Web サイトへの公開前にレビューする AEM コンテンツ作成者に割り当てられます（コンテンツには、ページ、アセット、パブリケーションなど、いくつかのタイプがあります）。これらのメンバーには、以下に示す「AEM ユーザー」製品プロファイルが割り当てられます。

   ![](/help/onboarding/learn-concepts/assets/admin-console-profiles.png)

   >[!NOTE]
   >AEM as a Cloud Service 製品プロファイルに割り当てられたすべてのユーザーは、Cloud Manager への（読み取り専用）アクセスが可能になります。

## Cloud Manager 製品プロファイル {#cloud-manager-product-profiles}

Cloud Manager には、事前設定済みの製品プロファイル（簡単に言えば、役割に基づく権限）があります。システム管理者は、Cloud Manager チームをこれらの製品プロファイルに割り当ててセットアップします。また、システム管理者は、これらの製品プロファイルと、それらのプロファイルをどのチームメンバーに割り当てるかを把握しておく必要があります。
>[!NOTE]
>詳しくは、[Cloud Manager での役割に基づく権限](/help/onboarding/learn-concepts/cloud-manager-introduction.md##role-based-permissions)を参照してください。

それぞれの製品プロファイルには、固有の権限が関連付けられています。以下は、役割と権限の例です。

* **ビジネスオーナー** - 新しいプログラムの追加またはプログラムの編集、環境の追加またはアップデート、パイプラインの追加／編集／削除およびパイプラインの実行、AEM 環境またはコード品質へのコードのデプロイを行う権限があります。

* **デプロイメントマネージャー** - 環境の追加またはアップデート、任意のパイプラインの実行、AEM 環境またはコード品質へのコードのデプロイを行う権限があります。

* **デベロッパー** - Git にアクセスするための個人用アクセストークンを生成する権限があります。

* **プログラムマネージャー** - パイプラインのスケジュール設定、3 層品質ゲートのオーバーライド、実稼動の承認を行う権限があります。

1 人のユーザーを複数の製品プロファイルに割り当てることができます。例えば、ビジネスオーナーとデプロイメントマネージャーの両方の役割をユーザーに割り当てると、これらの権限の組み合わせ（合計）が割り当てられます。

Cloud Manager チームには、少なくとも次の役割が含まれます。

* 1 人のビジネスオーナー。通常はシステム管理者も兼ねており、Cloud Manager にログインしてアクセスする最初のユーザーである必要があります
* 1 人のデプロイメントマネージャー
* 1 人の開発者

   >[!NOTE]
   >ユーザーが AEM as a Cloud Service へのアクセス権を付与されるには、「`AEM Users`」または「`AEM Administrators`」のどちらかの製品プロファイルに属している必要があります。インスタンスに対する権限を付与される必要があります。関連する Cloud Manager を管理する権限だけでは不十分です。
