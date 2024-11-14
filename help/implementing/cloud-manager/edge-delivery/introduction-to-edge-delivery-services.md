---
title: Cloud Manager の Edge Delivery Services の概要
description: Edge Delivery Servicesを使用してCloud Manager プロジェクトを配信する方法を説明します。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0fb5476b4cff9e26971696bd8352181a71e7b3e4
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 10%

---


# Cloud Manager の Edge Delivery Services の概要 {#edge-delivery-services}

Edge Delivery Services は、web サイト上のコンテンツの柔軟なオーサリングを実現する、構成可能なサービスセットです。この機能を使用すると、次のことが可能です。

* 完璧な Lighthouse スコアで高速サイトを作成します。
* RUM （Real Use Monitoring）を通じてパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。

ユニバーサルエディターとドキュメントベースのオーサリングを使用して、AEM コンテンツ管理とWYSIWYG オーサリングの両方を使用できます。

AEM as a Cloud ServiceのCloud Managerを使用すると、プロジェクトのEdge Delivery サービスを有効にできます。

>[!TIP]
>
>Edge Delivery Servicesの詳細とAEMでの使用方法については、[Edge Delivery Servicesの概要 ](/help/edge/overview.md) を参照してください。

## Cloud ManagerのEdge Delivery Servicesについて {#edge-in-cloud-manager}

Adobe Experience Manager Sitesの一部としてライセンスをEdge Delivery Servicesしている場合は、Cloud Managerで直接Edge Delivery Servicesを使用してサイトをオンボーディングし、[ ガイド付きのセルフサービスエクスペリエンスを使用して ](/help/implementing/cloud-manager/managing-code/private-repositories.md) 運用を開始できます。

さらに、主要なワークフロー間の一貫性を確保しながら、すべてのAEM プロパティを管理できる統一されたエクスペリエンスにアクセスできます。 これらのワークフローには、ドメイン名の管理、SSL 証明書の管理、CDN マッピングが含まれます。

## Edge Delivery ServicesにAdobeの推奨パスを使用するメリット {#recommended-path-eds}

Cloud Managerを通じてEdge Delivery Services ライセンスにアクセスして利用することで、Adobeから得られるメリットを最大限に活用できます。 これにより、いくつかの主なメリットを活用できます。

* [ 選択したプログラムでライセンスを使用する ](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)、[ 他のプログラムを更新する ](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md)、またはその両方。
* [API ファースト ](https://developer.adobe.com/experience-cloud/experience-manager-apis/) の利点を活用して、CRUD （作成、読み取り、更新、削除）操作を実行します。
* [SLA レポートへのアクセス ](/help/implementing/cloud-manager/sla-reporting.md) （*近日公開*）
* 登録済みの実稼動プログラムの [Adobeサポートへのアクセス権を取得します ](/help/edge/overview.md#support-ticket)。

さらに、Cloud Managerを使用すると、[Adobe管理による CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) をEdge Delivery サイトに使用し、DV 証明書の設定や追加など、セルフサービスの CDN 管理などの主なメリットを活用できます。 さらに、DV 証明書を作成した後、Adobeは、削除されない限り、3 か月ごとに自動的に更新します。 AdobeのEdge Delivery Services ライセンスを持っておらず、これらの利点を回避する場合は、自分で管理する CDN のみを使用できます。 この設定は、[`aem.live` プラットフォーム上になければなりません ](https://www.aem.live/docs/go-live-checklist#cdn-configuration)。

## 実稼動プログラムまたはサンドボックスプログラムへのEdge Delivery Servicesの追加について

Edge Delivery Servicesは、プロジェクトの開始方法に応じて、様々な方法で追加できます。

| ユースケース | 説明 |
| --- | --- |
| 新しい実稼動プログラムにEdge Delivery Servicesを追加したいのですが、 | [ 実稼動プログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) を参照してください。<br> ウィザードの「**ソリューションとアドオン**」タブで、「**Edge Delivery Services**」を選択します。 |
| 既存の実稼動プログラムにEdge Delivery Servicesを追加したいのですが、 | [ プログラムの編集 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) を参照してください。<br>**プログラムを編集** ダイアログボックスの「**ソリューションとアドオン**」タブで、「**Edge Delivery Services**」を選択します。 |
| Cloud ManagerにEdge Delivery サイトを追加したいのですが | [Edge Delivery サイトの追加 ](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) を参照してください。 |
| 新規または既存のサンドボックスプログラムにEdge Delivery Servicesを追加したいのですが、 | [ サンドボックスプログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) を参照してください。<br> サンドボックスプログラムを作成すると、デフォルトでEdge Delivery Servicesがプログラムに追加されるので、選択する必要はありません。<br>Edge Deliveryが一般提供される前の既存のサンドボックスプログラムは、Edge Delivery Servicesを自動的に継承します。 |

>[!NOTE]
>
>* プログラムを追加または編集するには、**ビジネスオーナー** の役割のメンバーであるか、その権限が付与されている必要があります。
>* 実稼動プログラムに適用するには、未使用のEdge Delivery Services ライセンスが必要です。
>* Edge Delivery Servicesライセンスがプログラムに適用またはプログラムから削除されると、変更はパイプラインを実行しなくても、直ちに有効になります。


## Cloud ManagerのEdge Delivery To Do リストについて {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

Cloud Managerの **Edge Delivery To-Do リスト** は、オンボーディングタスクのチェックリストで、Edge Delivery サイトのオンボーディング、管理を [ 運用開始 ](/help/journey-onboarding/go-live-checklist.md) までガイドします。

![Cloud ManagerのEdge Delivery サイト to-do リスト ](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | タスク | 説明 |
| --- | --- | --- |
| 1 | 製品コラボレーションチャネルに参加 | **リクエストを今すぐ送信** をクリックすると、会社のチャネルを作成するためのリクエストがAdobeに送信されます。 チャネルが既に存在する場合は、会社のチャネルに転送されます。 |
| 2 | 前提条件を完了 | [ はじめる前にチュートリアルを表示 ](https://www.aem.live/developer/tutorial) を参照してください。 |
| 3 | Edge Delivery サイトを追加 | [Edge Delivery サイトの追加 ](#eds-add-site) を参照してください。 |
| 4 | ドメインを追加 | [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。 |
| 5 | SSL 証明書を追加 | [SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を参照してください。 |
| 6 | Edge Delivery サイトの CDN の設定 | [CDN 設定の追加 ](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) を参照してください。 |
| 7 | プッシュ検証の設定 | [Edge Delivery サイトのプッシュ検証の設定 ](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md) を参照してください。 |
| 8 | 運用開始 | [ 運用開始チェックリスト ](/help/edge/docs/go-live-checklist.md) を参照してください。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## サポートチケットのログ {#eds-support-ticket}

{{support-ticket}}



