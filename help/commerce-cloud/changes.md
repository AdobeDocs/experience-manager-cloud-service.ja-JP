---
title: コマース統合フレームワーク（CIF）アドオンの主な変更点
description: 古い CIF バージョンと比較した、コマース統合フレームワーク（CIF）の主な変更点です。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: b81ac7529e7757fbd9f9fbc48e47e740ab9ecbf3
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 79%

---

# コマース統合フレームワーク（CIF）アドオンの主な変更点{#notable-changes}

Adobe Experience Manager as a Cloud Serviceは、AEMプロジェクトを管理するための様々な新機能と可能性を提供します。 これらの機能の詳細については、「[Experience Manager as a Cloud Service の変更点](/help/release-notes/aem-cloud-changes.md)」を参照してください。

このドキュメントでは、Commerce Integration Framework(CIF) アドオンと、CIF Classic（クイックスタート）と CIF オープンソースと呼ばれる古い CIF バージョンとの重要な違いについて説明します。

## インストールとアップデート

AEM CIF アドオンは、Cloud Manager を使用してインストールされます。インストールには、クレジットなしで CIF をインストールできるサンドボックスを除き、CIF クレジットが必要です。クレジットは、AEM 契約の CIF アドオンのプロビジョニングを通じて自動的に受け取ります。

アドオンは、通常のAEMas a Cloud Service更新の一環として、自動的に更新されます。

**以前の CIF バージョン**

* CIF Classic：インストールは不要で、CIF は Quickstart の一部でした。CIF のアップデートは、通常の AEM またはサービスパックのアップデートに含まれていました。
* AEM オンプレミス用の CIF Open-source：GitHub を使用したインストール。アップデートは、手動アップデートやメンテナンス作業の一部でした。
* AEM Adobe Managed Services 用の CIF オープンソース：アカウントチームによるAdobe。 アップデートは、手動アップデートやメンテナンス作業の一部でした。

## エンドポイントの設定

エンドポイントは、Cloud Manager UI または CLI を使用して設定およびアップデートされます。

**以前の CIF バージョン**

* CIF Classic：AEM の OSGi 設定を使用
* CIF Open-source：CIF 設定ブラウザーを使用

## CIF Venia プロジェクトのデプロイメント

プロジェクトは [Cloud Manager Git リポジトリー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html)で使用可能で、[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=ja) を介してデプロイされます。

**以前の CIF バージョン**

* CIF Classic:AEMパッケージのインストールを使用
* CIF Open-source：[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=ja) を使用

## 製品カタログデータ

製品カタログデータは、必要な GraphQL API をサポートする外部エンドポイントへのリアルタイム呼び出しを通じて、オンデマンドでリクエストされます。これらの API は、任意の日付のライブデータまたはステージングデータへのアクセスをサポートします。レプリケーションは不要です。

**以前の CIF バージョン**

* CIF Classic：ライブおよびステージングされた製品データは、完全または差分の製品読み込みを通じて AEM オーサー上の JCR に読み込まれ、保持されます。ライブ製品データが AEM パブリッシュにレプリケートされます。

## AEM レンダリングを使用した製品カタログエクスペリエンス

AEM は、製品やカテゴリに割り当てられた AEM カタログテンプレートを使用して、製品カタログエクスペリエンスをその場でレンダリングします。レプリケーションは不要です。

**以前の CIF バージョン**

* CIF Classic：AEM オーサーは、カタログのブループリントツールを使用して、各カテゴリ／製品の AEM ページを作成します。これらのページは AEM パブリッシュにレプリケートされます。

>[!NOTE]
>
>AEM Managed Service またはオンプレミスの AEM での CIF の使用方法に関する追加ドキュメントについては、[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html) を参照してください。
