---
title: コマース統合フレームワーク(CIF)アドオンの主な変更点
description: 古いCIFバージョンと比較した、コマース統合フレームワーク(CIF)の主な変更点です。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
source-git-commit: 7a52e4b62f5a18f9c68e5afb0d464bd11be732d2
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 15%

---

# コマース統合フレームワーク(CIF)アドオンの主な変更点{#notable-changes}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。これらの機能の詳細については、[Experience Managerの変更点をCloud Service](/help/release-notes/aem-cloud-changes.md)として参照してください。

このドキュメントでは、主にCIF Classic（クイックスタート）とCIFオープンソースと呼ばれる、Commerce Integration Framework(CIF)アドオンと古いCIFバージョンの重要な違いについて説明します。

## インストールと更新

AEM CIFアドオンは、Cloud Managerを使用してインストールされます。 インストールには、クレジットなしでCIFをインストールできるサンドボックスを除き、CIFクレジットが必要です。 クレジットは、AEM契約のCIFアドオンのプロビジョニングを通じて自動的に受け取られます。

アドオンは、通常のAEM as aの更新の一環として自動的に更新され、Cloud Serviceは更新されます。

**以前のCIFバージョン**

* CIF Classic:インストールは不要で、CIFはクイックスタートの一部でした。 CIFの更新は、通常のAEMまたはサービスパックの更新に含まれていました
* AEM On-premises用のCIFオープンソース：GitHubを使用したインストール。 更新は、手動更新/メンテナンス作業の一部でした。
* AEM Adobe Managed Services用のCIFオープンソース：カスタマーサクセスマネージャーを使用したインストール。 更新は、手動更新/メンテナンス作業の一部でした。

## エンドポイントの設定

エンドポイントは、Cloud Manager UIまたはCLIを使用して設定および更新されます。

**以前のCIFバージョン**

* CIF Classic:AEMのOSGi設定を使用
* CIFオープンソース：CIF設定ブラウザーを使用

## CIF Veniaプロジェクトのデプロイメント

プロジェクトは[Cloud Manager Gitリポジトリ](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)で使用でき、[Cloud Manager](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/deploying/overview.html)を介してデプロイされます。

**以前のCIFバージョン**

* CIF Classic:AEMパッケージのインストールを使用
* CIFオープンソース：[Cloud Manager](https://docs.adobe.com/content/help/ja/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)経由

## 製品カタログデータ

製品カタログデータは、必要なGraphQL APIをサポートする外部エンドポイントへのリアルタイム呼び出しを通じて、オンデマンドでリクエストされます。 これらのAPIは、任意の日付でのライブデータまたはステージングデータへのアクセスをサポートします。 レプリケーションは不要。

**以前のCIFバージョン**

* CIF Classic:ライブおよびステージングされた製品データは、完全または差分の製品読み込みを通じてAEMオーサー上のJCRに読み込まれ、保持されます。 ライブ製品データがAEMパブリッシュにレプリケートされます。

## AEMレンダリングを使用した製品カタログエクスペリエンス

AEMは、製品やカテゴリに割り当てられたAEMカタログテンプレートを使用して、製品カタログのエクスペリエンスをその場でレンダリングします。 レプリケーションは不要。

**以前のCIFバージョン**

* CIF Classic:AEMオーサーは、カタログのブループリントツールを使用して、各カテゴリ/製品のAEMページを作成します。 これらのページはAEMパブリッシュにレプリケートされます。

>[!NOTE]
>
>AEM Managed Service またはオンプレミスの AEM での CIF の使用方法に関する追加ドキュメントについては、[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html) を参照してください。
