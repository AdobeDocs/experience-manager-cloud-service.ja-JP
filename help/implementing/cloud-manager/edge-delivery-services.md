---
title: Cloud Manager での Edge Delivery Services のサポート
description: Edge Delivery Servicesを使用してCloud Manager プロジェクトを配信する方法を説明します。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 30%

---

# Cloud Manager での Edge Delivery Services のサポート {#edge-delivery-services}

Edge Delivery Servicesを使用してCloud Manager プロジェクトを配信する方法を説明します。

>[!NOTE]
>
>この機能は、[早期導入プログラム](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)でのみ利用できます。

## Brief のEdge Delivery Services {#edge-overview}

Edge Delivery Services は、web サイト上のコンテンツの柔軟なオーサリングを実現する、構成可能なサービスセットです。これにより、以下のことが可能になります。

* 完璧な Lighthouse スコアで高速サイトを作成し、リアルタイムモニタリング（RUM）を通じてパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。

ユニバーサルエディターを使用したAEM コンテンツ管理と WYSIWYG オーサリングの両方、およびドキュメントベースのオーサリングを使用できます。

AEM as a Cloud ServiceのCloud Managerを使用すると、プロジェクトのEdge Delivery サービスを有効にできます。

>[!TIP]
>
>Edge Delivery Servicesの詳細とAEMでの使用方法については、[Edge Delivery Servicesの概要のドキュメントを参照してください。](/help/edge/overview.md)

## Cloud ManagerのEdge Delivery Services {#edge-in-cloud-manager}

Adobe Experience Manager Sitesの一部としてライセンスをEdge Delivery Servicesしている場合は、Cloud Managerで直接Edge Delivery Servicesを使用してサイトをオンボーディングし、[ ガイド付きのセルフサービスエクスペリエンスを使用して ](/help/implementing/cloud-manager/managing-code/private-repositories.md) 運用を開始できます。

これにより、すべての AEM プロパティに対して統一されたエクスペリエンスが実現し、ドメイン名管理、SSL 証明書管理、CDN マッピングなどのすべての重要なワークフローとの一貫性が確保されます。

Edge Delivery Servicesは、[ 実稼動プログラムとサンドボックスプログラム ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) の両方で使用できます。

## Edge Delivery Servicesの有効化 {#enabling}

新しいプログラムを追加する際に、Edge Delivery Servicesを有効にできます。

![ 実稼動プログラムをEdge Delivery Servicesで追加 ](assets/add-production-program-with-edge.png)

プログラムの追加について詳しくは、次のドキュメントを参照してください。

* [実稼働プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [サンドボックスプログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
