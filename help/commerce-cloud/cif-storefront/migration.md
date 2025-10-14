---
title: AEM Commerce Integration Framework（CIF）アドオンへの移行
description: 旧バージョンから AEM Commerce Integration Framework（CIF）アドオンに移行する方法
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 0664e5dc4a7619a52cd28c171a44ba02c592ea3d
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 73%

---


# Experience Manager Cloud Service の移行ガイド {#cif-migration}

このガイドは、Experience Manager Cloud Service への移行の際に更新が必要な領域の特定に役立ちます。

## CIF アドオン {#cif-add-on}

Experience Manager as a Cloud Service の場合、Adobe Commerce およびサードパーティ製コマースソリューション向けにサポートされるコマース統合ソリューションは CIF アドオンだけです。CIF アドオンは、Experience Manager as a Cloud Service を使用するお客様の場合は自動的にデプロイされるので、手動でデプロイする必要はありません。[AEM Commerce as a Cloud Serviceの概要 &#x200B;](/help/commerce-cloud/cif-storefront/getting-started.md) を参照してください。

CIF Adobeをデプロイするプロジェクトをサポートするために、[AEM CIF コアコンポーネントを提供します。](https://github.com/adobe/aem-core-cif-components)

CIF アドオンは、AEM 6.5 で利用可能で、[&#x200B; ソフトウェア配布ポータル」からも入手できます。](/help/implementing/developing/tools/package-manager.md) このアドオンはExperience Manager as a Cloud Service用のCIF アドオンと互換性があり、同じ機能を提供します。調整は不要です。

依存関係を持つクラシック CIF は使用できなくなりました。`com.adobe.cq.commerce.api` Java API を使用しているこの CIF バージョンに依存するコードは、CIF アドオンとその原則に従って調整する必要があります。

以前に使用可能であった CIF コネクタは、インストールできなくなりました。このコネクタに依存するコードは、CIF アドオンとその原則に従って調整する必要があります。

## プロジェクト構造 {#project-structure}

[AEM プロジェクト構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md)、および AEM as a Cloud Service の特性を説明します。プロジェクトの設定をAEM as a Cloud Serviceのレイアウトに合わせます。

AEM 6.5 デプロイメントと比較して、主な違いは次の 2 つです。

* GraphQL クライアント OSGi バンドル **AEM プロジェクトに含める必要はありません** は、CIF アドオンを使用してデプロイされます
* GraphQL クライアントと Graphql データサービスの OSGi 設定は **AEM プロジェクトに含めないでください**。

>[!TIP]
>
>GitHub の [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトを確認します。このプロジェクトでは、AEM as a Cloud Service 用の Maven プロファイルを提供し、様々なフレームワーク条件を考慮したオンプレミスデプロイメントを行います。

## 製品カタログ {#product-catalog}

製品カタログデータの読み込みは、サポートされなくなりました。CIF アドオンの原則に従って、製品およびカタログリクエストは、外部コマースソリューションへのリアルタイム呼び出しを通じてオンデマンドで行われます。コマースソリューションの統合について詳しくは、「統合」の章を参照してください。

>[!TIP]
>
>リアルタイム API を使用できない場合は、API を使用した外部製品キャッシュを統合に使用する必要があります。例 [Magento オープンソース &#x200B;](https://business.adobe.com/jp/products/magento/open-source.html)

## AEM レンダリングを使用した製品カタログエクスペリエンス {#aem-rendering}

クラシック CIF でカタログブループリントを使用する場合は、製品カタログワークフローを更新する必要があります。CIF アドオンは、AEM カタログテンプレートを使用して、製品カタログエクスペリエンスをその場でレンダリングするようになりました。製品データや製品ページのレプリケーションは不要になりました。

## キャッシュ不可データとショッピングインタラクション {#non-cacheable}

キャッシュ不可データおよびインタラクションについてのクライアントサイドのリクエスト（例：買い物かごへの追加、検索）は、CDN や Dispatcher を介してコマースエンドポイント（コマースソリューションまたは統合レイヤー）に直接送信する必要があります。AEM がプロキシに過ぎない呼び出しは、すべて削除します。
