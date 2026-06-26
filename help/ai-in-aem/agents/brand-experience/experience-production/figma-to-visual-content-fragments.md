---
title: Figmaからビジュアルコンテンツフラグメントジョブ
description: Brand Experience AgentのFigmaからビジュアルコンテンツフラグメントへのジョブとは何か、およびそれが何に役立つかについて説明します。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
source-git-commit: 19931f7cc911376f5096903a2d99d6ff11f928ac
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Figmaからビジュアルコンテンツフラグメントジョブ {#figma-to-visual-content-fragments-job}

[Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md)のFigmaからビジュアルコンテンツフラグメントへのジョブは、Adobe Experience Manager（AEM）as a Cloud ServiceでFigma デザインを再作成するプロセスを自動化します。

## 概要 {#overview}

AEM ビジュアルコンテンツフラグメントを使用すると、[HTML テンプレート &#x200B;](/help/implementing/developing/extending/content-fragments-visualization-templates.md)に基づいたビジュアルレイアウトを使用して、コンテンツフラグメントをプレビューおよび配信できます。

手書きのHTML テンプレートでスタイルとレイアウトの情報を定義することは完全に可能ですが、これは通常、web開発者が実行する高度に技術的なプロセスです。

このプロセスを[&#x200B; ビジュアルコンテンツフラグメント &#x200B;](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md)用に合理化するため、モジュラーエクスペリエンスのビジュアルデザインはFigmaで作成されることが多いため、FigmaからAEMにデザインを直接読み込むこともできます。

## 前提条件 {#prerequisites}

開始する前に：

* Figmaからのインポートには認証が必要です。 Figma ユーザーは、Figmaでアクセストークンを作成し、AEM サービスに保存する必要があります。

  これは、次によって達成されます。

   * Figmaでの個人トークンの生成
   * `https://experience.adobe.com`でAdobe Experience Cloudにログインします
   * トークンを`https://experience.adobe.com/#/aem/figmatocontentfragment`に保持しています

## デザインをアップロードするには {#to-upload-a-design}

フローは次のとおりです。

1. デザイナー（Figma ユーザー）がFigmaでデザインを作成します。
1. Figma ユーザーは、Figmaのデザインオブジェクトへの共有リンクを作成します。
1. Figma ユーザーは、AEM ユーザーに共有リンクを送信します。
1. 最初の[&#x200B; プロンプト &#x200B;](#sample-prompts)から、AEM ユーザーはAI アシスタントを使用してFigma to Visual Content Fragments ジョブを操作し、承認されたデザインをAEMで自動的に再作成できます。 AEMでは、必要なコンテンツフラグメントモデル、コンテンツフラグメント、HTML テンプレートが自動的に作成されます。
   * 必要に応じて、担当者はAEM環境などの詳細情報を求めます。
   * エージェンティック制作プロセスには、既存のコンテンツモデルやフラグメントが利用可能な場合に、その再利用を可能にする機能も含まれています。
1. 担当者は、コンテンツのコンテンツフラグメントおよびコンテンツフラグメントモデルを生成し、レイアウトおよびデザインのHTML テンプレートを生成します。
   * エージェントは、フラグメントへの直接リンクを提供し、そこからモデルとテンプレートにアクセスできます。

## サンプルプロンプト {#sample-prompts}

プロンプトの例には、次のようなものがあります。

* Figmaから読み込むには：
   * Figma {*Figma_share_URL*}からAEMにインポートします
* エージェントの候補からAEM プログラムを選択するには：
   * Figma {*Figma_share_URL*}から{*AEMaaCS_program/environment_link*}にインポートします

## その他のリソース {#additional-resources}

ビジュアルコンテンツフラグメントを引き続き検討する場合は、次のリソースが役立つ可能性があります。

* [ビジュアルコンテンツフラグメント](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md)
* [ビジュアルコンテンツフラグメント – テンプレート](/help/implementing/developing/extending/content-fragments-visualization-templates.md)
* [ビジュアルコンテンツフラグメント – 公開URLを使用した配信](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md)
