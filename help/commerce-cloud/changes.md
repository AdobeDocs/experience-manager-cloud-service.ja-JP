---
title: Cloud ServiceとしてのAEMコマースに対する顕著な変更
description: Adobe Experience Manager6.5と比較して、AEMコマースのCloud Serviceが顕著に変更されました。
translation-type: tm+mt
source-git-commit: 2934d0d8d3977bb7884bae9654ac26e9fa57b34f
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 12%

---


# Notable changes to AEM Commerce as a Cloud Service {#notable-changes}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。このドキュメントでは、Cloud Serviceとしてのオンプレミス、Adobe管理サービス、およびExperience Manager用のCommerce Integration Framework(CIF)のコマース機能の重要な違いについて説明します。 その他の変更点については、[Experience Manager as a Cloud Service の主な変更点](/help/release-notes/aem-cloud-changes.md)を参照してください。

Adobe Experience Manager 6.5 との主な違いは次の点です。
* [CIF Classicのサポート](#cif-classic)
* [CIFオーサリングツールの導入](#cif-tools)
* [オンプレミスおよびAdobe管理サービスからの移行](#moving-cif-cs)

## Cloud ServiceとしてのExperience ManagerでのCIF Classic/Quickstartのサポート {#cif-classic}

Experience Managerに商品カタログをインポートして保存するための商品インポーターを含むClassic Commerce Integration Frameworkは、Experience ManagerでCloud Serviceとして使用できなくなりました。 Classic CIFの使用は、Experience ManagerでのCloud Serviceとしてはサポートされていません。また、Classic CIFを使用するプロジェクトでは、Cloud Serviceとしての [CIFで説明されているように、Classic CIF実装をサポートされているバージョンに置き換える必要があります](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/architecture/magento.html#overview)

## CIFの導入 {#deployment}

次に、AEMの異なる製品に対するCommerce Integration Frameworkの異なる導入モデルを示します。

|  | AEMオンプレミス | AEMManaged Services | AEMCloud Service |
|-------------     |-----------|-----------|-----------|
| Magentoバックエンド用のCIFオーサリングツールのデプロイ方法 | [AEM 6.5でサポートされているCIF Connector](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) （CIFコネクタ）を参照してください。 | [AEM 6.5でサポートされているCIF Connector](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) （CIFコネクタ）を参照してください。 | AEMをCloud Serviceとして使用するには、CIFアドオンを使用してプロビジョニングする必要があります。 詳細については、セールス担当者にお問い合わせください。 |
| [CIFベニアプロジェクトの導入方法](https://github.com/adobe/aem-cif-guides-venia) | AEMパッケージのインストール | Cloud Managerを使用した [展開](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) | プロジェクトは [Cloud Manager Gitリポジトリに移動され](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) 、 [Cloud Managerを介して展開されます。](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/deploying/overview.html) |

>[!NOTE]
>
>AEM Managed ServiceまたはAEM On-premiseでのCIFの使用方法に関する追加ドキュメントについては、 [Commerce Integration Frameworkを参照してください。](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)

>[!NOTE]
>
>CIF Classic/QuickstartバージョンのCommerce Integration Frameworkは、非常に限られた使用例を対象としたAEMオンプレミスオファーで使用できます。 ただし、これは推奨される解決策ではありません。

## オンプレミスとManaged ServicesからのCloud ServiceとしてAEMコマースへの移行 {#moving-cif-cs}

Cloud ServiceとしてAEMのオンプレミスまたはManaged ServicesのインストールからAEMに移行するお客様は、AEMプロジェクトで若干の調整を行う必要があります。

上述のように、最初の調整はCIFコネクタに必要です。 CIFコネクタは、AdobeがデプロイするCIFアドオンに置き換えられます。 したがって、AEMにCIFコネクタをCloud Serviceとしてインストールしないでください。 また、ローカルのAEM Cloud SDKでの使用はサポートされていません。Adobeは、 [ローカル開発にもCIFアドオンを提供します](develop.md)。

2つ目は、 [AEMプロジェクト構造](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) 、およびAEMの特性をCloud Serviceとして理解します。 プロジェクトの設定をAEMにCloud Serviceレイアウトとして適応させます。
主な違いは次のとおりです。

* GraphQLクライアントOSGIバンドル **は、AEMプロジェクトに含める** べきではなく、CIFアドオンを介してデプロイされます
* GraphQLクライアントおよびGraphql Data Service用のOSGI設定をAEMプロジェクトに含め **ることはで** きません。

>[!TIP]
>
>GitHubの [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) プロジェクトを確認します。 このプロジェクトでは、AEM用のMavenプロファイルをCloud Serviceとして提供し、さまざまなフレームワーク条件を考慮したオンプレミスデプロイメントを行います。
