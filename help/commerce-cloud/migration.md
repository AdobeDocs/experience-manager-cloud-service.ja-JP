---
title: AEM Commerce Integration Framework (CIF)アドオンへの移行
description: 古いバージョンからAEM Commerce Integration Framework (CIF)アドオンに移行する方法
translation-type: tm+mt
source-git-commit: cda25048e171f6aacd5349706ad4192965e703db
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 22%

---

# Experience Manager Cloud Serviceの移行ガイド{#cif-migration}

このガイドは、Experience Manager Cloud Serviceの移行時に更新する必要がある領域の特定に役立ちます。

## CIFアドオン

Cloud ServiceとしてのExperience Managerの場合、CIFアドオンは、Adobeコマースおよびサードパーティコマースソリューションでサポートされる唯一のコマース統合ソリューションです。 CIFアドオンは、Cloud ServiceとしてExperience Managerを利用しているお客様向けに自動的に導入されるので、手動での導入は必要ありません。 [Cloud ServiceとしてAEMコマースを使い始める](getting-started.md)を参照してください。

CIFAdobeを導入するプロジェクトをサポートするために、[AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)を提供します。

CIFアドオンは、AEM 6.5では、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からも入手できます。 互換性があり、Experience Manager用のCIFアドオンと同じ機能をCloud Serviceとして提供します。調整は必要ありません。

依存関係を持つ従来のCIFは、使用できなくなりました。 `com.adobe.cq.commerce.api` Java APIを使用するこのCIFバージョンに依存するコードは、CIFアドオンとその原則に合わせて調整する必要があります。

以前に使用可能だったCIFコネクタは、インストールできなくなりました。 このコネクタに依存するコードは、CIFアドオンとその原則に合わせて調整する必要があります。

## プロジェクト構造

[AEMプロジェクト構造](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)とAEMの特性をCloud Serviceとして学びます。 プロジェクトの設定を AEM as a Cloud Service レイアウトとして適応させます。
AEM 6.5のデプロイメントと比較して、主に次の2つの違いがあります。

* GraphQL クライアント OSGI バンドルは、AEM プロジェクトに含める&#x200B;**べきではなく**、CIF アドオンを介してデプロイされます。
* GraphQL クライアントおよび Graphql データサービス用の OSGI 設定を AEM プロジェクトに含めることは&#x200B;**できません**。

>[!TIP]
>
>GitHub の [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトを確認します。このプロジェクトでは、AEM as a Cloud Service 用の Maven プロファイルを提供し、さまざまなフレームワーク条件を考慮したオンプレミスデプロイメントをおこないます。

## 製品カタログ

製品カタログデータの読み込みは、サポートされなくなりました。 CIFアドオンプリンシパル製品とカタログのリクエストを使用すると、外部コマースソリューションへのリアルタイム呼び出しを介して、オンデマンドで実行できます。 コマースソリューションの統合について詳しくは、「統合」の章を参照してください。

>[!TIP]
>
>リアルタイムAPIが使用できない場合は、APIを使用した外部製品キャッシュを統合に使用する必要があります。 例[Magentoオープンソース](https://magento.com/products/magento-open-source)

## AEMレンダリングでの商品カタログのエクスペリエンス

Classic CIFでカタログのブループリントを使用する場合は、商品カタログのワークフローを更新する必要があります。 CIFアドオンは、AEMカタログテンプレートを使用して、製品カタログのエクスペリエンスをその場でレンダリングするようになりました。 製品データや製品ページの複製は不要になりました。

## キャッシュ不可能なデータおよび買い物のインタラクション

キャッシュ不可能なデータおよびインタラクション（例：買い物かごへの追加、検索）に対するクライアント側のリクエストは、CDN/ディスパッチャーを介して、コマースエンドポイント（コマースソリューションまたは統合レイヤー）に直接送信する必要があります。 AEMが単なるプロキシであった場合は、呼び出しを削除します。
