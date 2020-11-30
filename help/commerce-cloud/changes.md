---
title: AEM Commerce as a Cloud Service の主な変更点
description: Adobe Experience Manager 6.5 と比較して、AEM Commerce as a Cloud Service が顕著に変更されました。
translation-type: tm+mt
source-git-commit: 2934d0d8d3977bb7884bae9654ac26e9fa57b34f
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 100%

---


# AEM Commerce as a Cloud Service の主な変更点 {#notable-changes}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。このドキュメントでは、オンプレミス、Adobe Managed Service、Experience Manager as a Cloud Service 用の Commerce Integration Framework（CIF）のコマース機能の間の重要な違いについて説明します。その他の変更点については、[Experience Manager as a Cloud Service の主な変更点](/help/release-notes/aem-cloud-changes.md)を参照してください。

Adobe Experience Manager 6.5 との主な違いは次の点です。
* [CIF Classic のサポート](#cif-classic)
* [CIF オーサリングツールのデプロイメント](#cif-tools)
* [オンプレミスおよび Adobe Managed Services からの移行](#moving-cif-cs)

## Experience Manager as a Cloud Service での CIF Classic／Quickstart のサポート {#cif-classic}

Experience Manager に製品カタログを読み込んで保存するための Product Importer を含む Classic Commerce Integration Framework は、Experience Manager as a Cloud Service で使用できなくなりました。Classic CIF の使用は、Experience Manager as a Cloud Service ではサポートされていません。また、Classic CIF を使用するプロジェクトでは、[CIF on Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/commerce/architecture/magento.html#overview) で説明されているように、Classic CIF 実装をサポートされているバージョンに置き換える必要があります

## CIF のデプロイメント {#deployment}

次に、AEM の異なる製品に対する Commerce Integration Framework の異なるデプロイメントモデルを示します。

|  | オンプレミスの AEM | AEM Managed Services | AEM Cloud Service |
|-------------     |-----------|-----------|-----------|
| Magento バックエンド用の CIF オーサリングツールのデプロイ方法 | [AEM 6.5 でサポートされている CIF コネクタ](https://github.com/adobe/commerce-cif-connector/blob/master/README.md)を参照してください。 | [AEM 6.5 でサポートされている CIF コネクタ](https://github.com/adobe/commerce-cif-connector/blob/master/README.md)を参照してください。 | AEM as a Cloud Service は、CIF アドオンを使用してプロビジョニングする必要があります。詳細については、セールス担当者にお問い合わせください。 |
| [CIF Venia プロジェクト](https://github.com/adobe/aem-cif-guides-venia)のデプロイ方法 | AEM パッケージのインストール | [Cloud Manager](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) を使用したデプロイメント | プロジェクトは [Cloud Manager Git リポジトリー](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)に移動され、[Cloud Manager](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/deploying/overview.html) を介してデプロイされます。 |

>[!NOTE]
>
>AEM Managed Service またはオンプレミスの AEM での CIF の使用方法に関する追加ドキュメントについては、[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html) を参照してください。

>[!NOTE]
>
>CIF Classic／Quickstart バージョンの Commerce Integration Framework は、非常に限られたユースケースを対象としており、オンプレミスの AEM で使用できます。ただし、これは推奨される解決策ではありません。

## オンプレミスと Managed Services からの AEM Commerce as a Cloud Service への移行 {#moving-cif-cs}

オンプレミスの AEM または Managed Services のインストールから AEM Commerce as a Cloud Service に移行するお客様は、AEM プロジェクトで若干の調整をおこなう必要があります。

上述のように、最初の調整は CIF コネクタに必要です。CIF コネクタは、アドビがデプロイする CIF アドオンに置き換えられます。したがって、AEM as a Cloud Service に CIF コネクタをインストールしないでください。また、ローカルの AEM Cloud SDK での使用はサポートされていません。アドビは、[ローカル開発](develop.md)にも CIF アドオンを提供します。

2 つ目は、 [AEM プロジェクト構造](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)、および AEM as a Cloud Service の特性を理解することです。プロジェクトの設定を AEM as a Cloud Service レイアウトとして適応させます。
主な違いは次のとおりです。

* GraphQL クライアント OSGI バンドルは、AEM プロジェクトに含める&#x200B;**べきではなく**、CIF アドオンを介してデプロイされます。
* GraphQL クライアントおよび Graphql データサービス用の OSGI 設定を AEM プロジェクトに含めることは&#x200B;**できません**。

>[!TIP]
>
>GitHub の [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトを確認します。このプロジェクトでは、AEM as a Cloud Service 用の Maven プロファイルを提供し、さまざまなフレームワーク条件を考慮したオンプレミスデプロイメントをおこないます。
