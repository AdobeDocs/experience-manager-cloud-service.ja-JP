---
title: Edge Delivery ServicesとCloud ManagerのAdobe管理による CDN の統合
description: null
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 2d2a206fea14d7e786a98e848bc2f2592ac65429
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Edge Delivery ServicesとCloud ManagerのAdobe管理による CDN の統合 {#integrate-adbe-cdn-with-edservices-in-cm}

Adobeの管理による CDN （AMC-D）は、Edge Delivery Servicesとネイティブに統合され、Adobe Experience Manager（AEM）サイトに対して、パフォーマンスが高く、グローバルに分散したエクスペリエンスを提供します。

これらを合わせると、次のような利点があります。

* Adobeが管理する、自動のエンタープライズグレード CDN。
* リクエストを高速化、キャッシュを最適化、一般的な攻撃から保護する最新のエッジ配信レイヤー。
* ドメイン管理、SSL 証明書、パイプラインドリブンなデプロイメントのための統合Cloud Manager ワークフロー。

<!--
Adobe's Edge Delivery Services (EDS) can take advantage of an Adobe managed CDN. EDS is a framework that optimizes website delivery for speed, simplicity, and scalability by pushing content closer to the user through edge nodes. It is not a replacement for a CDN, but rather a way to enhance content delivery, especially when you use the Adobe managed CDN. It offers you the following benefits:

* Adobe-Managed CDN: EDS can use an Adobe-managed CDN, offering features like self-service CDN management and automatic certificate renewal. 
* EDS and AEM: EDS is a feature of AEM as a Cloud Service and works alongside the AEM authoring environment. 
* Performance enhancement: EDS, in conjunction with an Adobe Managed CDN, improves website performance by caching content at edge locations closer to users, reducing latency. 
* Flexibility: EDS provides flexibility in content delivery, allowing your organization to choose between the Adobe-managed CDN or their own CDN setup, based on their needs and existing infrastructure. 
Self-Service CDN Management:
Adobe-managed CDN within EDS enables self-service configuration and management tasks like SSL certificate setup. 
 
Use Cases:
EDS with CDN integration is beneficial for various scenarios, including e-commerce storefronts and websites requiring high performance and scalability. -->

## Cloud ManagerのAdobe管理 CDN でのEdge Delivery Services デプロイメントオプション {#deployment-options}

このトピックでは、Cloud ManagerのAdobe管理 CDN にEdge Delivery Servicesをデプロイする 2 つの方法について説明します。また、同様に重要なこととして、どのオプションがユースケースに最適かを判断するのに役立ちます。

Edge Delivery Servicesは、次の 2 つのオプションのいずれかを使用して設定できます。 それぞれに異なる機能があります。

|  | デプロイメントオプション | 主要ドキュメント | 機能 | に最適 |
| --- | --- | --- | --- | --- |
| オプション 1 | *使用可*：既存のAEM as a Cloud Service（AEMaaCS）環境 | [ 既存の環境からのプロキシの設定 ](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment) | 設定パイプラインは、AEMaaCS 環境で一般公開されています | Cloud Managerで既に Sites を実行していて、迅速でリスクの低いパフォーマンスの向上を望んでいるチーム。 |
| オプション 2 | *なし* スタンドアロンの「Edge環境」と呼ばれる既存の AEMaaCS 環境。 | [ 既存の環境を使用しないEdge Delivery サイトのセットアップ ](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment) | 設定パイプラインは現在、限定的なBeta プログラムを通じてEdge環境でのみ利用できます。<br>Edge Delivery設定パイプラインの追加 [ を参照 ](help/implementing/cloud-manager/release-notes/current.md##add-eds-pipeline)。 | Edge Deliveryのアーキテクチャ全体と詳細なルーティングを採用したい新しいビルドまたは移行。 |

<!-- Ultimately this URL above will need to be updated on GA -->

| オプション | 概要 | に最適 | 主要なドキュメント |
| --- | --- | --- | --- |
| Adobeの管理による CDN プロキシ | Adobeの管理による CDN は、既存のAEM Sites環境に対応します。 現在の Sites パイプラインは「オリジン」のままですが、AMC-D はエッジキャッシュと TLS 終了を処理します。 | Cloud Managerで既に Sites を実行していて、迅速でリスクの低いパフォーマンスの向上を望んでいるチーム。 | AMC-D プロキシの設定 |
| originSelectors を使用した設定パイプライン | 専用のEdge Delivery設定パイプラインが、静的コンテンツと動的コンテンツをエッジに直接公開します。 AMC-D とAEMのオーサー層/パブリッシュ層の間でトラフィックをルーティングで `originSelectors` ません。 | Edge Deliveryのアーキテクチャ全体と詳細なルーティングを採用したい新しいビルドまたは移行。 | Edge Delivery パイプラインを設定 |

>[!TIP]
>
>どのパスを選択するか不明な場合は、 決定のガイドラインについては、以下の [ デプロイメントモデルの選択 ](#choose-deployment-model) を参照してください。

## デプロイメントモデルを選択 {#choose-deployment-model}

両方のモデルを同じCloud Manager プログラム内で共存させて、段階的な移行を実現できます。

| もし… | 次に… |
| :--- | :--- |
| 迅速で最小限の変更ロールアウトと、既にCloud Managerでサイトをホストする必要がある | AMC-D プロキシ |
| Edge Delivery用にコンテンツの再構築を計画する、または複数のオリジン間の詳細なルーティングが必要 | Edge パイプラインの配信と `originSelectors` の設定 |

## 前提条件 {#prerequisites}

1. Cloud Managerでのサイトのオンボード
 – 両方のデプロイメントモデルで必須。 AEM サイトでオンボーディングを行います。

2. 独自の Git の取り込み（BYOG）（オプション）
- Adobe Git の外部にサイトコードを保存する場合は、BYOG のオンボーディングを実施します。

3. Edge Delivery ライセンス
- プログラムがEdge Delivery Servicesのライセンスを取得していることを確認します。


