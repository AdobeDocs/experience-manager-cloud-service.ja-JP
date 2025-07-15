---
title: サイトテーマ
description: AEM サイトテーマを使用して、従来のAEM オーサリングプロジェクト（公開配信）用にサイトのスタイルとデザインをカスタマイズする方法を説明します。
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
solution: Experience Manager Sites
source-git-commit: 9efba01add46c09e9839da6bb96b138d48018e54
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 75%

---


# サイトテーマ {#site-themes}

{{traditional-aem}}

AEM サイトテーマを使用して、従来のAEM オーサリングプロジェクト（公開配信）用にサイトのスタイルとデザインをカスタマイズする方法を説明します。

## 概要 {#overview}

AEM サイトテーマは、AEM サイトのスタイルを定義し、AEM サイトテーマの構造に準拠する CSS、JavaScript および静的リソースを含むパッケージです。

AEM サイトテンプレートを使用して作成されたサイトでは、従来のAEM オーサリングプロジェクトのテーマを [ 公開配信 ](/help/sites-cloud/authoring/author-publish.md) と簡単にダウンロード、カスタマイズ、再デプロイできます。

>[!NOTE]
>
>AEM サイトテーマを [AEM サイトテンプレート](site-templates.md)と混同しないでください。 AEM サイトテーマには、AEM サイトのスタイル設定情報のみが含まれています。AEM サイトテンプレートは、サイト構造と初期コンテンツを定義します。また、「クイックサイト作成 [ を可能にするAEM サイトテーマが含まれ ](create-site.md) います。

## サイトテーマの使用 {#using-themes}

サイトテーマは、次の 2 つの方法で使用されます。

* これらは、 [サイトの作成](create-site.md) 時にスタイル設定を定義するためのサイトテンプレートの一部として使用されます。
* これらは、サイトテンプレートに基づいてサイトを作成した後にダウンロードされるので、フロントエンド開発者はスタイル設定をさらにカスタマイズできます。

>[!TIP]
>
>テンプレートからサイトを作成し、そのテーマをカスタマイズするプロセスのエンドツーエンドについては、 [クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md) を参照してください。

## サイトテーマの構造 {#structure}

サイトテーマは、パッケージのコンテンツの目的を明確に反映した論理構造を持つ単純なパッケージです。一般的なフロントエンドプロジェクトの場合、アドビではサイトテーマに次の構造をお勧めします。

* `src/theme.ts`：JS および CSS テーマのメインエントリポイント
* `src/site`：サイト全体に適用される JS および CSS ファイル
* `src/components`：AEM コンポーネント固有の JS および CSS ファイル
* `src/resources`：アイコン、ロゴ、フォントなどの静的ファイル

メインエントリポイント `src/theme.ts` が保持されている限り、特定のプロジェクトのニーズに応じて、テーマの構造は異なる場合があります。

## 標準のサイトテーマ {#standard-site-theme}

アドビは、独自のテーマを作成する際の基礎として使用できる、ベストプラクティスの参照テーマを提供します。[標準のサイトテーマは GitHub で入手できます。](https://github.com/adobe/aem-site-template-standard/tree/main/theme)

## サイトテーマの開発 {#developing-themes}

アドビは、新しいサイトテーマを作成するための一連のスクリプトとして AEM Site Theme Builder を提供します。

[AEM Site Theme Builder は、GitHub の使用方法ドキュメントと共に利用できます。](https://github.com/adobe/aem-site-theme-builder) テーマをカスタマイズするには、フロントエンド開発エクスペリエンスが必要です。
