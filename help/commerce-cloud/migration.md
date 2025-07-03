---
title: AEM Commerce Integration Framework（CIF）アドオンへの移行
description: 旧バージョンから AEM Commerce Integration Framework（CIF）アドオンに移行する方法
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 100%

---

# Experience Manager Cloud Service の移行ガイド {#cif-migration}

このガイドは、Experience Manager Cloud Service への移行の際に更新が必要な領域の特定に役立ちます。

## CIF アドオン

Experience Manager as a Cloud Service の場合、Adobe Commerce およびサードパーティ製コマースソリューション向けにサポートされるコマース統合ソリューションは CIF アドオンだけです。CIF アドオンは、Experience Manager as a Cloud Service を使用するお客様の場合は自動的にデプロイされるので、手動でデプロイする必要はありません。[AEM Commerce as a Cloud Service - はじめに](getting-started.md)を参照してください。

CIF をデプロイするプロジェクトをサポートするために、アドビでは [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)を提供しています。

AEM 6.5 用の CIF アドオンも、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)を通じて入手できます。これは互換性があり、Experience Manager as a Cloud Service 用の CIF アドオンと同じ機能を提供します。調整は不要です。

依存関係を持つクラシック CIF は使用できなくなりました。`com.adobe.cq.commerce.api` Java API を使用しているこの CIF バージョンに依存するコードは、CIF アドオンとその原則に従って調整する必要があります。

以前に使用可能であった CIF コネクタは、インストールできなくなりました。このコネクタに依存するコードは、CIF アドオンとその原則に従って調整する必要があります。

## プロジェクト構造

[AEM プロジェクト構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja)、および AEM as a Cloud Service の特性を説明します。プロジェクトの設定を AEM as a Cloud Service レイアウトとして適応させます。
AEM 6.5 デプロイメントと比較して、主な違いは次の 2 つです。

* GraphQL クライアント OSGI バンドルは、AEM プロジェクトに含める&#x200B;**べきではなく**、CIF アドオンを介してデプロイされます。
* GraphQL クライアントおよび Graphql データサービス用の OSGI 設定を AEM プロジェクトに含めることは&#x200B;**できません**。

>[!TIP]
>
>GitHub の [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトを確認します。このプロジェクトでは、AEM as a Cloud Service 用の Maven プロファイルを提供し、様々なフレームワーク条件を考慮したオンプレミスデプロイメントを行います。

## 製品カタログ

製品カタログデータの読み込みは、サポートされなくなりました。CIF アドオンの原則に従って、製品およびカタログリクエストは、外部コマースソリューションへのリアルタイム呼び出しを通じてオンデマンドで行われます。コマースソリューションの統合について詳しくは、「統合」の章を参照してください。

>[!TIP]
>
>リアルタイム API を使用できない場合は、API を使用した外部製品キャッシュを統合に使用する必要があります。例：[Magento オープンソース](https://business.adobe.com/jp/products/magento/open-source.html)

## AEM レンダリングを使用した製品カタログエクスペリエンス

クラシック CIF でカタログブループリントを使用する場合は、製品カタログワークフローを更新する必要があります。CIF アドオンは、AEM カタログテンプレートを使用して、製品カタログエクスペリエンスをその場でレンダリングするようになりました。製品データや製品ページのレプリケーションは不要になりました。

## キャッシュ不可データとショッピングインタラクション

キャッシュ不可データおよびインタラクションについてのクライアントサイドのリクエスト（例：買い物かごへの追加、検索）は、CDN や Dispatcher を介してコマースエンドポイント（コマースソリューションまたは統合レイヤー）に直接送信する必要があります。AEM がプロキシに過ぎない呼び出しは、すべて削除します。
