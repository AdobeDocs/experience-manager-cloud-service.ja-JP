---
title: AEM Commerce Integration Framework(CIF)アドオンへの移行
description: 古いバージョンからAEM Commerce Integration Framework(CIF)アドオンに移行する方法
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 21%

---

# Experience Manager Cloud Service{#cif-migration}の移行ガイド

このガイドは、Experience Manager Cloud Service移行の際に更新が必要な領域の特定に役立ちます。

## CIFアドオン

Experience ManagerをCloud Serviceとして使用する場合、CIFアドオンは、Adobeコマースおよびサードパーティのコマースソリューションでサポートされる唯一のコマース統合ソリューションです。 CIFアドオンは、Cloud ServiceとしてExperience Manager上のお客様に対して自動的にデプロイされるので、手動でデプロイする必要はありません。 [AEM Commerce as aCloud Service](getting-started.md)を参照してください。

CIFAdobeをデプロイするプロジェクトをサポートするには、[AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)を提供します。

CIFアドオンは、AEM 6.5でも[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)を介して使用できます。 互換性があり、Cloud ServiceとしてのExperience Manager用CIFアドオンと同じ機能を提供します。調整は不要です。

依存関係を持つ従来のCIFは使用できなくなりました。 `com.adobe.cq.commerce.api` Java APIを使用してこのCIFバージョンに依存するコードは、CIFアドオンとその原則に従って調整する必要があります。

以前に使用可能だったCIFコネクタは、もうインストールできません。 このコネクタに依存するコードは、CIFアドオンとその原則に従って調整する必要があります。

## プロジェクト構造

[AEMプロジェクト構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja)と、AEMのCloud Serviceとしての特性について説明します。 プロジェクトの設定を AEM as a Cloud Service レイアウトとして適応させます。
AEM 6.5デプロイメントと比較して、主に次の2つの違いがあります。

* GraphQL クライアント OSGI バンドルは、AEM プロジェクトに含める&#x200B;**べきではなく**、CIF アドオンを介してデプロイされます。
* GraphQL クライアントおよび Graphql データサービス用の OSGI 設定を AEM プロジェクトに含めることは&#x200B;**できません**。

>[!TIP]
>
>GitHub の [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトを確認します。このプロジェクトでは、AEM as a Cloud Service 用の Maven プロファイルを提供し、さまざまなフレームワーク条件を考慮したオンプレミスデプロイメントをおこないます。

## 製品カタログ

製品カタログデータの読み込みは、サポートされなくなりました。 CIFアドオンプリンシパルの製品およびカタログのリクエストを使用すると、外部コマースソリューションへのリアルタイム呼び出しを介してオンデマンドで実行できます。 コマースソリューションの統合について詳しくは、「統合」の章を参照してください。

>[!TIP]
>
>リアルタイムAPIが使用できない場合は、APIを使用した外部製品キャッシュを統合に使用する必要があります。 例：[Magentoオープンソース](https://magento.com/products/magento-open-source)

## AEMレンダリングを使用した製品カタログエクスペリエンス

クラシックCIFでカタログブループリントを使用する場合は、製品カタログワークフローを更新する必要があります。 CIFアドオンは、AEMカタログテンプレートを使用して、製品カタログエクスペリエンスをその場でレンダリングするようになりました。 製品データや製品ページのレプリケーションは不要になりました。

## キャッシュ不可能なデータと買い物とのやり取り

キャッシュ不能なデータおよびインタラクション（例：買い物かごへの追加、検索）に対するクライアント側のリクエストは、CDN/Dispatcherを介して、コマースエンドポイント（コマースソリューションまたは統合レイヤー）に直接送信する必要があります。 AEMがプロキシに過ぎない呼び出しをすべて削除します。
