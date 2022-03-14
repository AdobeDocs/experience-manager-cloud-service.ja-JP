---
title: コマース統合フレームワーク（CIF）アドオンの主な変更点
description: 古い CIF バージョンと比較した、コマース統合フレームワーク（CIF）の主な変更点です。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 100%

---

# コマース統合フレームワーク（CIF）アドオンの主な変更点{#notable-changes}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。これらの機能の詳細については、「[Experience Manager as a Cloud Service の変更点](/help/release-notes/aem-cloud-changes.md)」を参照してください。

このドキュメントでは、主に CIF Classic（Quickstart）と CIF Open-source と呼ばれる、コマース統合フレームワーク（CIF）アドオンと古い CIF バージョンの重要な相違点について説明します。

## インストールとアップデート

AEM CIF アドオンは、Cloud Manager を使用してインストールされます。インストールには、クレジットなしで CIF をインストールできるサンドボックスを除き、CIF クレジットが必要です。クレジットは、AEM 契約の CIF アドオンのプロビジョニングを通じて自動的に受け取ります。

アドオンは、通常の AEM as a Cloud Service アップデートの一環として自動的にアップデートされます。

**以前の CIF バージョン**

* CIF Classic：インストールは不要で、CIF は Quickstart の一部でした。CIF のアップデートは、通常の AEM またはサービスパックのアップデートに含まれていました。
* AEM オンプレミス用の CIF Open-source：GitHub を使用したインストール。アップデートは、手動アップデートやメンテナンス作業の一部でした。
* AEM Adobe Managed Services 用の CIF Open-source：Customer Success Manager を使用したインストール。アップデートは、手動アップデートやメンテナンス作業の一部でした。

## エンドポイントの設定

エンドポイントは、Cloud Manager UI または CLI を使用して設定およびアップデートされます。

**以前の CIF バージョン**

* CIF Classic：AEM の OSGi 設定を使用
* CIF Open-source：CIF 設定ブラウザーを使用

## CIF Venia プロジェクトのデプロイメント

プロジェクトは [Cloud Manager Git リポジトリー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html?lang=ja)で使用可能で、[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja) を介してデプロイされます。

**以前の CIF バージョン**

* CIF Classic：AEM パッケージのインストールを使用
* CIF Open-source：[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=ja) を使用

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
