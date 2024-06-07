---
title: Cloud Manager でのEdge Delivery Servicesのサポート
description: Edge Delivery Servicesを使用して Cloud Manager プロジェクトを配信する方法について説明します。
source-git-commit: 73bd693d47f37b453209208816dfed15d65e9e09
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 15%

---


# Cloud Manager でのEdge Delivery Servicesのサポート {#edge-delivery-services}

Edge Delivery Servicesを使用して Cloud Manager プロジェクトを配信する方法について説明します。

>[!NOTE]
>
>この機能は、[早期導入プログラム](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)でのみ利用できます。

## Brief のEdge Delivery Services {#edge-overview}

Edge Delivery Services は、web サイト上のコンテンツの柔軟なオーサリングを実現する、構成可能なサービスセットです。これにより、以下のことが可能になります。

* 完璧な Lighthouse スコアで高速サイトを作成し、リアルタイムユーザーモニタリング（RUM）を通じてパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。

ユニバーサルエディターを使用したAEM コンテンツ管理とAEM ベースのオーサリング、およびドキュメントベースのオーサリングの両方を使用できます。

AEMas a Cloud Serviceの Cloud Manager を使用すると、プロジェクトのエッジ配信サービスを有効にできます。

>[!TIP]
>
>Edge Delivery Servicesの詳細とAEMでの使用方法については、ドキュメントを参照してください。 [Edge Delivery Servicesの概要。](/help/edge/overview.md)

## Cloud Manager のEdge Delivery Services {#edge-in-cloud-manager}

Adobe Experience Manager Sitesの一部としてライセンスをEdge Delivery Servicesしている場合は、Cloud Manager で直接Edge Delivery Servicesを使用してサイトをオンボーディングし、運用を開始できます [ガイド付きのセルフサービスエクスペリエンスを使用する。](/help/implementing/cloud-manager/managing-code/private-repositories.md)

これにより、すべてのAEM プロパティでエクスペリエンスが統合され、ドメイン名の管理、SSL 証明書の管理、CDN マッピングなど、すべての重要なワークフローとの一貫性が確保されます。

Edge Delivery Servicesは、次の両方で使用できます [実稼動およびサンドボックスプログラム。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Edge Delivery Servicesの有効化 {#enabling}

新しいプログラムを追加する際に、Edge Delivery Servicesを有効にできます。

![Edge Delivery Servicesを使用した実稼動プログラムの追加](assets/add-production-program-with-edge.png)

プログラムの追加について詳しくは、次のドキュメントを参照してください。

* [実稼働プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [サンドボックスプログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
