---
title: サイトテーマ
description: AEMサイトのテーマを使用して、サイトのスタイルやデザインをカスタマイズする方法を説明します。
feature: Administering
role: Admin
source-git-commit: 9e7ad4a640f1783be5aed75e01e860b647662f52
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---


# サイトテーマ {#site-themes}

AEMサイトのテーマを使用して、サイトのスタイルやデザインをカスタマイズする方法を説明します。

>[!CAUTION]
>
>現在、クイックサイト作成ツールはテクニカルプレビューです。 テストおよび評価の目的で使用できるようになり、Adobeサポートに同意しない限り、実稼動での使用は意図されません。

## 概要 {#overview}

AEMサイトテーマは、AEMサイトのスタイルを定義し、AEMサイトテーマの構造に準拠する CSS、JavaScript および静的リソースを含むパッケージです。

AEMのサイトテンプレートを使用して作成されたサイトでは、テーマを簡単にダウンロード、カスタマイズ、再デプロイできます。

>[!NOTE]
>
>AEMサイトのテーマを [AEMのサイトテンプレート。](site-templates.md) AEMサイトテーマには、AEMサイトのスタイル設定情報のみが含まれます。 AEMのサイトテンプレートは、次の目的でサイト構造と初期コンテンツを定義し、AEMのサイトテーマを含めます。 [クイックサイトの作成。](create-site.md)

## サイトテーマの使用 {#using-themes}

サイトテーマは、次の 2 つの方法で使用されます。

* これらは、サイトテンプレートの一部として使用され、 [サイトの作成](create-site.md)
* これらは、サイトテンプレートに基づいてサイトを作成した後にダウンロードされるので、フロントエンド開発者はスタイル設定をさらにカスタマイズできます。

>[!TIP]
>
>テンプレートからサイトを作成し、そのテーマをカスタマイズするプロセスに関するエンドツーエンドの説明については、 [クイックサイト作成ジャーニー。](/help/journey-sites/quick-site/overview.md)

## サイトテーマの構造 {#structure}

サイトテーマは、パッケージのコンテンツの目的を明確に反映した論理構造を持つ単純なパッケージです。 サイトテーマは、フロントエンドプロジェクトの典型的な次の構造を持ちます。

* `src/main.ts`:JS および CSS テーマの主なエントリポイント
* `src/site`:サイト全体に適用される JS および CSS ファイル
* `src/components`:AEMコンポーネント固有の JS および CSS ファイル
* `src/resources`:アイコン、ロゴ、フォントなどの静的ファイル

## 標準のサイトテーマ {#standard-site-theme}

Adobeは、独自のテーマを作成する際の基礎として使用できる、ベストプラクティスのリファレンステーマを提供します。 [標準のサイトテーマは GitHub で入手できます。](https://github.com/adobe/aem-site-template-standard-theme-e2e)

## サイトテーマの開発 {#developing-themes}

Adobeは、新しいサイトテーマを作成するための一連のスクリプトとして、およびAEM Site Theme Builder を提供します。

[AEM Site Theme Builder は、GitHub の使用方法ドキュメントと共に利用できます。](https://github.com/adobe/aem-site-theme-builder) テーマをカスタマイズするには、フロントエンド開発エクスペリエンスが必要です。
