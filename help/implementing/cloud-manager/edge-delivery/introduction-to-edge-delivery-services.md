---
title: Cloud ManagerのEdge Delivery Servicesの概要
description: Edge Delivery Servicesを使用してCloud Manager プロジェクトを配信する方法を説明します。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 6%

---

# Cloud ManagerのEdge Delivery Servicesの概要 {#edge-delivery-services}

Edge Delivery Services は、web サイト上のコンテンツの柔軟なオーサリングを実現する、構成可能なサービスセットです。この機能を使用すると、次のことが可能です。

* 完璧な Lighthouse スコアで高速サイトを作成します。
* RUM （Real Use Monitoring）を通じてパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。

ユニバーサルエディターとドキュメントベースのオーサリングを使用して、AEM コンテンツ管理と WYSIWYG オーサリングの両方を使用できます。

AEM as a Cloud ServiceのCloud Managerを使用すると、プロジェクトのEdge Delivery サービスを有効にできます。

>[!TIP]
>
>Edge Delivery Servicesの詳細とAEMでの使用方法については、[Edge Delivery Servicesの概要 ](/help/edge/overview.md) を参照してください。

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->


## Cloud ManagerのEdge Delivery Servicesについて {#edge-in-cloud-manager}

Adobe Experience Manager Sitesの一部としてライセンスをEdge Delivery Servicesしている場合は、Cloud Managerで直接Edge Delivery Servicesを使用してサイトをオンボーディングし、[ ガイド付きのセルフサービスエクスペリエンスを使用して ](/help/implementing/cloud-manager/managing-code/private-repositories.md) 運用を開始できます。

さらに、主要なワークフロー間の一貫性を確保しながら、すべてのAEM プロパティを管理できる統一されたエクスペリエンスにアクセスできます。 これには、ドメイン名の管理、SSL 証明書の管理、CDN マッピングが含まれます。

## 実稼動プログラムまたはサンドボックスプログラムへのEdge Delivery Servicesの追加

プログラムを追加または編集するには、**ビジネスオーナー** の役割のメンバーであるか、その権限が付与されている必要があります。

実稼動プログラムに適用するには、未使用のEdge Delivery Services ライセンスが必要です。

>[!NOTE]
>
>Edge Delivery Servicesライセンスがプログラムに適用またはプログラムから削除されると、変更はパイプラインを実行しなくても、直ちに有効になります。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

ユースケースに応じて、次のいずれかの操作を行います。

| ユースケース | 説明 |
| --- | --- |
| 新しい実稼動プログラムにEdge Delivery Servicesを追加したいのですが、 | [ 実稼動プログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) を参照してください。<br> ウィザードの「**ソリューションとアドオン**」タブで、「**Edge Delivery Services**」を選択します。 |
| 既存の実稼動プログラムにEdge Delivery Servicesを追加したいのですが、 | [ プログラムの編集 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) を参照してください。<br>**プログラムを編集** ダイアログボックスの「**ソリューションとアドオン**」タブで、「**Edge Delivery Services**」を選択します。 |
| Cloud ManagerにEdge Delivery サイトを追加したいのですが | [Edge Delivery サイトの追加 ](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) を参照してください。 |
| 新規または既存のサンドボックスプログラムにEdge Delivery Servicesを追加したいのですが、 | [ サンドボックスプログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) を参照してください。<br> サンドボックスプログラムを作成すると、デフォルトでEdge Delivery Servicesがプログラムに追加されるので、選択する必要はありません。<br>Edge Deliveryが一般提供される前の既存のサンドボックスプログラムは、Edge Delivery Servicesを自動的に継承します。 |

## 契約済みのお客様に対するAdobeの推奨パス {#recommended-path-eds}

契約先のお客様は、Cloud Managerを通じてEdge Delivery Servicesライセンスにアクセスして利用することで、Adobeから最大限のメリットを得ることができます。 このアプローチを使用すると、[Adobe管理による CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) を使用して、DV 証明書の設定や追加など、セルフサービス CDN 管理などの主なメリットを活用できます。 さらに、DV 証明書を作成した後、Adobeは、削除されない限り、3 か月ごとに自動的に更新します。 AdobeのEdge Delivery Services ライセンスを持っておらず、これらの利点を回避する場合は、お客様が管理する CDN のみを使用できます。 この設定は、`aem.live` プラットフォーム上に存在する必要があります。

AEM as a Cloud Service Sites Edge Delivery Servicesライセンスを契約している場合は、Cloud Managerにログインして、以下を実行できるようにします。

* 選択したプログラムでライセンスを使用します。
* [API ファースト ](https://developer.adobe.com/experience-cloud/experience-manager-apis/) の利点を活用して、CRUD （作成、読み取り、更新、削除）操作を実行します。
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* SLA レポートへのアクセス （*近日公開*） <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* Adobeのサポートを得る。 Adobeから適切に認識され、サポートを受けるために、Edge Delivery ServicesサイトがCloud Managerの実稼動プログラムを通じて登録されていることを確認します。


## Edge Delivery To Do リストについて {#ed-todo-list}

**Edge Delivery To-Do リスト** はオンボーディングタスクのチェックリストで、オンボーディング、Edge Delivery サイトの管理を [ 運用開始 ](/help/journey-onboarding/go-live-checklist.md) までガイドすることを目的としています。

![Edge Delivery サイトの To Do リスト ](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|  | タスク | 説明 |
| --- | --- | --- |
| 1 | 製品コラボレーションチャネルに参加 | **リクエストを今すぐ送信** をクリックすると、会社のチャネルを作成するためのリクエストがAdobeに送信されます。 チャネルが既に存在する場合は、会社のチャネルに転送されます。 |
| 2 | 前提条件を完了 | **入門チュートリアルを表示** をクリックすると、[ 入門 – 開発者チュートリアル ](https://www.aem.live/developer/tutorial) に移動します。 |
| 3 | Edge Delivery サイトを追加 | [Edge Delivery サイトの追加 ](#eds-add-site) を参照してください。 |
| 4 | ドメインを追加 | [ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。 |
| 5 | SSL 証明書を追加 | [SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を参照してください。 |
| 6 | Edge Delivery サイトの CDN の設定 | [CDN 設定の追加 ](#add-cdn) を参照してください。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->
