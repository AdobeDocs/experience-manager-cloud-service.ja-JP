---
title: オンボーディングジャーニー
description: このページでは、オンボーディングジャーニーの概要について説明します
hide: true
hidefromtoc: true
index: false
source-git-commit: ae7b9f45b0a50bf6816c85934997c7562718c2be
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 7%

---

# オンボーディングジャーニー {#onboarding-jourrney}

AEM as a Cloud Service のジャーニーが始まりました。お客様のご参加をお待ちしております。 新しいアプリケーションをデプロイする場合でも、既存のアプリケーションを移行する場合でも、このガイドは、チームを設定し、AEM as aCloud Serviceにアクセスできるようにするための出発点として機能します。

## はじめに {#introduction}

このガイドでは、最も重要なトピックを順を追って説明し、完了時に以下をおこないます。

* AEM as a Cloud Service onboarding journeyの期待事項を完全に理解している。
* AEM as a Content Applicationのコンテンツを作成および開発する方法を学ぶための最初の手順を、チームが開始および実行できるようになりました。

つまり、

* チームが設定され、クラウドリソースにアクセスできるようになります。
* AEM作成者は、AEM as aCloud Service
* AEM開発者およびデプロイメントマネージャーは、AEM as aCloud Serviceにアクセスできます。


## 対象者 {#audience}

オンボーディングとは、指定された[システム管理者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en)が組織のCloud ServiceとしてAEMを設定するプロセスです。 これには、各メンバーがCloud Serviceリソースとしてログインし、AEMにアクセスできるクラウドリソースの初期プロビジョニングや、その後の職務責任に基づく適切な役割へのユーザーの割り当てが含まれます。

オンボーディングジャーニーを以下に示します。ジャーニーの各手順について、以降の節で詳しく説明します。

![](/help/onboarding/onboarding-journey/assets/onboarding-journey.png)

このジャーニーは、システム管理者のペルソナ向けに設計され、要件、手順、アプローチをレイアウトします。 ジャーニーは、プロジェクトを成功させるためにシステム管理者がやり取りする必要がある追加のペルソナを定義しますが、ジャーニーの視点は管理者のものです。

次に、このジャーニーでやり取りするペルソナを示します。

| ペルソナ | 説明 | ジャーニーでの役割 |
|---|---|---|
| システム管理者 | 各メンバーがログインし、Cloud ServiceリソースとしてAEMにアクセスできる職務上の責任に基づいて、クラウドリソースの初期プロビジョニングとユーザーの役割割り当てを提供します。 | アクセスから権限まで、ユーザーのすべての側面を管理します。 |
| AEM オーサー | コンテンツを作成およびレビューします（複数のタイプがあります）。（ページ、アセット、パブリケーションなど）をWebサイトに公開する前に設定する必要があります。 | 権限が付与されると、は独自のデプロイメントマネージャーのジャーニーを開始できます。 |
| デベロッパー | 様々なソースのコンテンツを使用するAEMアプリケーションの開発経験がある | 権限が付与されると、は独自の開発者ジャーニーを開始できます |
| デプロイメントマネージャー | 環境を追加または更新し、任意のパイプラインを実行して、コードをAEM環境またはコード品質にデプロイします。 | 権限が付与されると、は独自のデプロイメントマネージャーのジャーニーを開始できます。 |

## オンボーディングジャーニー {#exploring-onboarding-journey}

このジャーニーでは、多くのトピックを参照します。次の記事では、AEM as aCloud Serviceのオンボーディング手順に関する基礎知識を提供します。 ジャーニーの特定の部分に直接移動することはできますが、多くの概念はそれ以前の記事の概念に基づいて構築されています。したがって、初めてオンボーディングする場合は、最初から順に開始し、順番に進むことをお勧めします。

| # | 記事 | 説明 |
|---|---|---|
| 0 | オンボーディングジャーニー | このドキュメントでは、以下について説明します。 |
| 1 | 次のようなオンボーディングの概念を学習します。<br>[System Administrator](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en)<br>[Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)<br>[AdobeIdentity Management System](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/ims.html?lang=en)<br>[Adobe ID](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/adobe-id.html?lang=en)<br>[AEM as a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)<br>[Cloud Service as a Product Profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en)<br>[Adobeサポートへのお問い合わせ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/onboarding-help-resources.html?lang=en) | オンボーディングの概念について説明します。 |
| 2 | オンボーディングの概要 | システムへのログインとAdmin Console管理者としてのプロファイルの確認について説明します |
| 3 | Cloud Manager製品プロファイルへのチームメンバーの割り当て | Cloud Manager製品プロファイルを確認し、Cloud Manager製品プロファイルにチームメンバーを割り当てる方法を学びます。 |
| 4 | Cloud Managerを使用したクラウドリソースの設定 | クラウドリソースの作成方法と実行者について説明します。 さらに、クラウドプログラムと環境の作成方法についても説明します。 |
| 5 | チームメンバーを製品プロファイルとしてAEMに割り当てるCloud Service | システム管理者がチームメンバーを製品プロファイルとしてAEMに割り当てる方法をCloud Serviceします。 |
| 6 | AEM DevelopersおよびDeployment Managerの学習パス | 開発者としてCloud Manager Gitにアクセスして管理する方法、およびデプロイメントマネージャーとしてCloud Managerにパイプラインを設定してコードをデプロイする方法について説明します。 |
| 7 | AEMユーザーの学習パス | AEMオーサーとしてAEMにCloud Serviceインスタンスとしてアクセスする方法と、AEM as aCloud Service用のコンテンツのオーサリングについて説明します。 |

## 次の手順 {#what-is-next}

これで、オンボーディングジャーニーを開始する準備が整いました。 このジャーニーの次の部分に進み、オンボーディングプロセスの概要に関する記事をお読みください。