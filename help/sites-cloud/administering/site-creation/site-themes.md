---
title: サイトテーマ
description: AEM サイトテーマを使用して、サイトのスタイルやデザインをカスタマイズする方法を説明します。
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '353'
ht-degree: 100%

---

# サイトテーマ {#site-themes}

AEM サイトテーマを使用して、サイトのスタイルやデザインをカスタマイズする方法を説明します。

## 概要 {#overview}

AEM サイトテーマは、AEM サイトのスタイルを定義し、AEM サイトテーマの構造に準拠する CSS、JavaScript および静的リソースを含むパッケージです。

AEM サイトテンプレートを使用して作成されたサイトでは、テーマを簡単にダウンロード、カスタマイズ、再デプロイできます。

>[!NOTE]
>
>AEM サイトテーマを [AEM サイトテンプレート](site-templates.md)と混同しないでください。 AEM サイトテーマには、AEM サイトのスタイル設定情報のみが含まれています。AEM サイトテンプレートには、サイト構造と初期コンテンツを定義し、[クイックサイト作成](create-site.md)を可能にする AEM サイトテーマが含まれています。

## サイトテーマの使用 {#using-themes}

サイトテーマは、次の 2 つの方法で使用されます。

* これらは、 [サイトの作成](create-site.md) 時にスタイル設定を定義するためのサイトテンプレートの一部として使用されます。
* これらは、サイトテンプレートに基づいてサイトを作成した後にダウンロードされるので、フロントエンド開発者はスタイル設定をさらにカスタマイズできます。

>[!TIP]
>
>テンプレートからサイトを作成し、そのテーマをカスタマイズするプロセスのエンドツーエンドについては、[クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)を参照してください。

## サイトテーマの構造 {#structure}

サイトテーマは、パッケージのコンテンツの目的を明確に反映した論理構造を持つ単純なパッケージです。サイトテーマは、フロントエンドプロジェクトの典型的な次の構造を持ちます。

* `src/main.ts`：JS および CSS テーマの主なエントリポイント
* `src/site`：サイト全体に適用される JS および CSS ファイル
* `src/components`：AEM コンポーネント固有の JS および CSS ファイル
* `src/resources`：アイコン、ロゴ、フォントなどの静的ファイル

## 標準のサイトテーマ {#standard-site-theme}

アドビは、独自のテーマを作成する際の基礎として使用できる、ベストプラクティスの参照テーマを提供します。[標準のサイトテーマは GitHub で入手することができます](https://github.com/adobe/aem-site-template-standard/tree/main/theme)。

## サイトテーマの開発 {#developing-themes}

アドビは、新しいサイトテーマを作成するための一連のスクリプトとして AEM Site Theme Builder を提供します。

[AEM Site Theme Builder は、GitHub の使用方法ドキュメントと共に利用できます](https://github.com/adobe/aem-site-theme-builder)。 テーマをカスタマイズするには、フロントエンド開発エクスペリエンスが必要です。
