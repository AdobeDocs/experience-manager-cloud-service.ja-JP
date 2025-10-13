---
title: Cloud Manager での Edge Delivery Services と Adobe が管理する CDN の統合
description: null
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 71ea3b810d4145d5581c29e26db9bc157c425a15
workflow-type: ht
source-wordcount: '477'
ht-degree: 100%

---


# Cloud Manager での Edge Delivery Services と Adobe が管理する CDN の統合 {#integrate-adbe-cdn-with-edservices-in-cm}

Adobe が管理する CDN（AMC-D）は、Edge Delivery Services とネイティブに統合され、Adobe Experience Manager（AEM）Sites 向けにパフォーマンスに優れた、グローバルに分散されたエクスペリエンスを提供します。

これらを組み合わせることで、次のメリットが得られます。

* Adobe が管理する、自動のエンタープライズグレードの CDN。
* リクエストを高速化し、キャッシュを最適化し、一般的な攻撃から保護する最新の Edge Delivery レイヤー。
* ドメイン管理、SSL 証明書、パイプライン駆動型のデプロイメント用の統合 Cloud Manager ワークフロー。

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

## Cloud Manager の Adobe が管理する CDN での Edge Delivery Services デプロイメントオプション {#deployment-options}

このトピックでは、Cloud Manager の Adobe が管理する CDN に Edge Delivery Services をデプロイする 2 つの方法について説明します。また、同様に重要なこととして、これは、ユースケースに最適なオプションを決定するのに役立ちます。

Edge Delivery Services は、次の 2 つのオプションのいずれかを使用して設定できます。それぞれ機能が異なります。

|  | デプロイメントオプション | 主なドキュメント | 機能 | 次に最適 |
| --- | --- | --- | --- | --- |
| オプション 1 | 既存の AEM as a Cloud Service（AEMaaCS）環境を&#x200B;*使用する場合* | [既存の環境からのプロキシの設定](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment) | 設定パイプラインは、AEMaaCS 環境で一般公開されています | Cloud Manager で既に Sites を実行しており、迅速で低リスクでパフォーマンスを向上させたいチーム。 |
| オプション 2 | 既存の AEMaaCS 環境を&#x200B;*使用しない場合*。スタンドアロンの「Edge 環境」と呼ばれます。 | [既存の環境を使用しない Edge Delivery サイトの設定](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment) | 設定パイプラインは現在、限定的な Beta プログラムを通じて Edge 環境でのみ使用できます。<br>[Edge Delivery 設定パイプラインの追加](help/implementing/cloud-manager/release-notes/current.md##add-eds-pipeline)を参照してください。 | 完全な Edge Delivery アーキテクチャと詳細なルーティングを採用したい新しいビルドまたは移行。 |

<!-- Ultimately this URL above will need to be updated on GA -->

| オプション | 概要 | 次に最適 | 主なドキュメント |
| --- | --- | --- | --- |
| アドビが管理する CDN プロキシ | Adobe が管理する CDN は、既存の AEM Sites 環境の前面に配置されます。現在の Sites パイプラインは「オリジン」のままですが、AMC-D は Edge キャッシュと TLS 終了を処理します。 | Cloud Manager で既に Sites を実行しており、迅速で低リスクでパフォーマンスを向上させたいチーム。 | AMC-D プロキシの設定 |
| originSelectors を使用した設定パイプライン | 専用の Edge Delivery 設定パイプラインは、静的コンテンツと動的コンテンツを Edge に直接公開します。 `originSelectors` は、AMC-D と AEM のオーサー層／パブリッシュ層の間でトラフィックをルーティングします。 | 完全な Edge Delivery アーキテクチャと詳細なルーティングを採用したい新しいビルドまたは移行。 | Edge Delivery パイプラインの設定 |

>[!TIP]
>
>選択するパスが不明ですか？決定のガイドラインについて詳しくは、以下の[デプロイメントモデルの選択](#choose-deployment-model)を参照してください。

## デプロイメントモデルの選択 {#choose-deployment-model}

両方のモデルは、同じ Cloud Manager プログラム内で共存できるので、段階的な移行が可能です。

| 次の場合... | 次を使用します… |
| :--- | :--- |
| 迅速で最小限の変更でロールアウトする必要があり、既に Cloud Manager で Sites をホストしている場合 | AMC-D プロキシ |
| Edge Delivery 用にコンテンツを再構築する予定、または複数のオリジン間できめ細かなルーティングが必要な場合 | Edge Delivery 設定パイプライン + `originSelectors` |

## 前提条件 {#prerequisites}

1. Cloud Manager でサイトをオンボード - 両方のデプロイメントモデルで必須です。AEM サイトのオンボードに従います。

2. Bring Your Own Git（BYOG）（オプション）- サイトコードを Adobe Git の外部に保存する場合は、BYOG オンボーディングを完了します。

3. Edge Delivery ライセンス - プログラムが Edge Delivery Services のライセンスを取得していることを確認します。


