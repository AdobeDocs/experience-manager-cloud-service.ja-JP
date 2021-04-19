---
title: Commerce Integration Framework (CIF)アドオンの注目すべき変更点
description: 古いCIFバージョンと比較したCommerce Integration Framework(CIF)の顕著な変更。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: 7a52e4b62f5a18f9c68e5afb0d464bd11be732d2
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 15%

---

# Commerce Integration Framework (CIF)追加-on{#notable-changes}の主な変更点

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。これらの機能の詳細については、[Cloud Service](/help/release-notes/aem-cloud-changes.md)としてのExperience Managerの変更のリンクを参照してください。

このドキュメントでは、主にCIF Classic(Quickstart)とCIF Open-sourceと呼ばれる、Commerce Integration Framework(CIF)アドオンと古いCIFバージョンとの重要な違いに焦点を当ててます。

## インストールとアップデート

AEM CIFアドオンは、Cloud Managerを使用してインストールされます。 インストールにはCIFクレジットが必要ですが、クレジットなしでCIFをインストールできるサンドボックスは例外です。 AEM契約のCIFアドオンのプロビジョニングにより、クレジットが自動的に受け取られます。

アドオンは、通常のAEMの一部として、Cloud Serviceの更新として自動的に更新されます。

**以前のCIFバージョン**

* CIF Classic:インストールは必要ありません。CIFはQuickstartの一部でした。 CIFのアップデートは、通常のAEMまたはサービスパックのアップデートの一部でした。
* AEM On-premises用のCIF Open-source:GitHubを介したインストール。 アップデートは、手動アップデート/メンテナンス作業の一部でした。
* AEM Adobe Managed Services用CIFオープンソース：Customer Success Managerを使用したインストール アップデートは、手動アップデート/メンテナンス作業の一部でした。

## エンドポイントの設定

エンドポイントは、Cloud Manager UIまたはCLIを使用して設定および更新されます。

**以前のCIFバージョン**

* CIF Classic:AEMでのOSGi設定を使用
* CIF Open-source:CIF設定ブラウザを使用

## CIFベニアプロジェクトの導入

プロジェクトは[Cloud Manager Gitリポジトリ](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)で使用可能で、[Cloud Manager](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/deploying/overview.html)を介して展開されます

**以前のCIFバージョン**

* CIF Classic:AEMパッケージのインストールを使用
* CIF Open-source:[Cloud Manager](https://docs.adobe.com/content/help/ja/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)経由

## 商品カタログデータ

必要なGraphQL APIをサポートする外部エンドポイントへのリアルタイム呼び出しを通じて、製品カタログデータがオンデマンドでリクエストされます。 これらのAPIは、任意の日にライブデータまたはステージデータへのアクセスをサポートします。 レプリケーションは必要ありません。

**以前のCIFバージョン**

* CIF Classic:製品のライブデータとステージデータが、完全または差分の製品インポートを通じて、AEM AuthorのJCRにインポートされて保持されます。 ライブ製品のデータがAEM Publishに複製されます。

## AEMレンダリングでの商品カタログのエクスペリエンス

AEMは、製品やカテゴリに割り当てられたAEMカタログテンプレートを使用して、製品カタログのエクスペリエンスをその場でレンダリングします。 レプリケーションは必要ありません。

**以前のCIFバージョン**

* CIF Classic:AEM Authorは、カタログのBluePrintツールを使用して、すべてのカテゴリ/製品のAEMページを作成します。 これらのページはAEM Publishに複製されます。

>[!NOTE]
>
>AEM Managed Service またはオンプレミスの AEM での CIF の使用方法に関する追加ドキュメントについては、[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html) を参照してください。
