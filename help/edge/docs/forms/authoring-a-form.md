---
title: AEM でのフォームの作成方法
description: Adobe Experience Manager（AEM）で使用可能な様々なフォームオーサリングプラットフォームと、要件に基づいて適切なプラットフォームを選択する方法について説明します。
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
exl-id: bd9cb623-c272-4cdf-ad39-f97043f781a6
hide: true
hidefromToC: true
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 100%

---

# Adobe Experience Manager（AEM）でのフォームの作成方法

Adobe Experience Manager（AEM）では、魅力的でレスポンシブ、かつ動的でアダプティブなフォームを作成するための柔軟なプラットフォームを提供します。これには、直感的なユーザーインターフェイスと、アダプティブフォームを作成および管理するための豊富なセットの標準コンポーネントが用意されています。フォームは、必要に応じて、フォームモデルやスキーマの有無にかかわらず作成できます。

## オーサリングプラットフォームを選択する際の主な考慮事項

AEM では、インタラクティブで魅力的なフォームを作成するための複数のフォームオーサリングオプションを提供します。フォームオーサリング環境を選択する際は、次の要因を考慮します。

| 📝 **考慮事項** | 💡 **質問すること** |
|----------------------|--------------------|
| **ユーザーの専門知識** | フォームを作成するのは、開発者、ビジネスユーザー、コンテンツ作成者の誰ですか？ |
| **フォームの複雑さ** | フォームには、高度なルール、動的セクションまたは統合が必要ですか？ |
| **再利用性のニーズ** | フォームの一部は、異なるフォームやプロジェクト間で再利用されますか？ |
| **デザインの柔軟性** | レイアウト、テーマ、スタイル設定を完全に制御する必要がありますか？ |
| **統合要件** | フォームは、データモデル、ワークフローまたは外部システムに接続する必要がありますか？ |
| **使いやすさ** | プラットフォームは、チームの技術スキルレベルに対して直感的ですか？ |
| **パフォーマンスとスケーラビリティ** | フォームは、大規模な環境や高トラフィック環境で使用されますか？ |
| **オムニチャネル配信** | フォームは、web サイト、モバイルアプリ、キオスクまたは複数のチャネルで使用されますか？ |
| **公開の柔軟性** | フォームは、AEM、Edge Delivery またはカスタムアプリのどこに公開されますか？ |

## AEM のフォームオーサリング方法の概要

AEM では、様々なユーザーのニーズ、技術スキルレベル、公開の宛先に適した複数のオーサリング方法をサポートしています。

- [基盤コンポーネント](/help/forms/create-adaptive-form-tutorial.md)：基盤コンポーネントを使用して、従来のインタラクティブなフォームを作成します。レガシーシステムと統合されるフォームや、長年確立されたワークフローに依存するフォームに最適です。基盤コンポーネントを使用して作成したフォームは、AEM でのみ公開でき、Edge Delivery Services とは互換性がありません。

- [コアコンポーネント](/help/forms/creating-adaptive-form-core-components.md)：コアコンポーネントを使用して、最新でレスポンシブかつスケーラブルなフォームを作成します。再利用性、アクセシビリティ、パフォーマンスの向上をサポートします。コアコンポーネントを使用して作成したフォームは、AEM と Edge Delivery Services の両方で公開できるので、プラットフォーム間で柔軟性が得られます。

- [Edge Delivery Services Forms](/help/edge/docs/forms/overview.md)：Adobe Edge Delivery Services Forms は、フォームの作成、実行、処理の方法を変革します。Edge Delivery Services を活用することで、組織は高速で安全な、可用性の高いデジタルフォームを作成し、高速開発環境でユーザーエクスペリエンスと運用効率を向上させることができます。Edge Delivery Services Forms は、次の 2 つの方法で作成できます。
   - [WYSIWYG オーサリング](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：技術的な知識が限られているコンテンツ作成者に最適で、視覚的なドラッグ＆ドロップフォームの作成には、ユニバーサルエディターを使用します。ユニバーサルエディターで作成したフォームは、高速で軽量なレンダリングを実現する Edge Delivery Services を使用して配信します。
   - [ドキュメントベースのオーサリング](/help/edge/docs/forms/tutorial.md)：フォームの構造とコンテンツを定義するには、Microsoft Excel や Google Sheets などのツールを使用します。この方法は、スプレッドシート主導の入力を行うビジネスユーザーに役立ちます。これらのフォームは通常、Edge Delivery Services を通じて公開され、軽量で大量のユースケースに適しています。
- [ヘッドレスオーサリング](https://experienceleague.adobe.com/ja/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)：AEM に依存せずに、React、Angular、モバイルアプリ、キオスクなどの任意のフロントエンドのフォームを JSON としてレンダリングするには、API を使用します。現在、コアコンポーネントのみがヘッドレス配信をサポートしています。ヘッドレスフォームはオムニチャネルのユースケースに最適で、AEM のページレンダリングとは独立して使用されるので、カスタムフロントエンドのデプロイメントに柔軟に対応できます。

### AEM フォームオーサリング方法の比較分析

次の表は、様々な AEM フォームオーサリング方法の簡潔な比較を示し、ニーズに最も適した方法を選択する際に役立つ、アプローチ、機能、公開オプション、理想的なユースケースをハイライト表示しています。

| **考慮事項** | **基盤コンポーネント** | **コアコンポーネント** | **ユニバーサルエディター（WYSIWYG）** | **ドキュメントベースのオーサリング** | **ヘッドレスオーサリング** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **次に最適** | AEM 内でのレガシーフォームとワークフローの維持 | 複雑なワークフローと統合を備えたスケーラブルな最新フォーム | 複雑な要件を持つ Edge Delivery Service サイト用のフォームの作成 | 迅速なプロトタイプ作成や、高度な送信サービスのない基本フォーム | プラットフォーム（web、モバイル、キオスクなど）をまたいだオムニチャネルエクスペリエンス |
| **ユーザーの専門知識** | 開発者、コンテンツ作成者 | 開発者、高度な作成者 | ビジネスユーザー、コンテンツ作成者 | ビジネスユーザー | デベロッパー向け |
| **フォームの複雑さ** | 基本フォーム | 動的セクションを備えた複雑なフォーム | カスタムアクションを備えた複雑なフォーム | シンプルなフォーム | 非常に複雑な API 駆動型フォーム |
| **デザインの柔軟性** | 限定的 | 高（CSS／JS のカスタマイズ） | 中（テンプレートに基づく） | 限定的 | 高（フロントエンドフレームワークコントロール） |
| **統合機能** | AEM の基本的なワークフロー | 高度（データモデル、ワークフロー） | 外部システムとの統合 | 基本（Google Sheets、Excel） | API を介した完全なコントロール |
| **公開方法** | AEM のみ | AEM と Edge Delivery Services | Edge Delivery Services | Edge Delivery Services | API を介した任意のフロントエンド |
| **パフォーマンスと SEO** | 標準 | 基盤コンポーネントの改善 | レンダリングの高速化と SEO の向上を実現する Google Lighthouse の高いスコア | レンダリングの高速化と SEO の向上を実現する Google Lighthouse の高いスコア | 実装に依存 |
| **オムニチャネル配信** | 限定的 | 中 | 中 | 限定的 | 高 |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### AEM フォームオーサリング方法の機能比較

次の表は、様々な AEM フォームオーサリング方法の主な機能の詳細な比較を示し、要件に最も適したアプローチを選択するのに役立ちます。

| **機能** | **基盤コンポーネント** | **コアコンポーネント** | **ユニバーサルエディター（WYSIWYG）** | **ドキュメントベースのオーサリング** | **ヘッドレスオーサリング** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **Sites との統合構成** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **埋め込みフォームのサポート** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **ルール（動的動作）** | カスタム関数を備えた高度なルールエディター | カスタム関数を備えた高度なルールエディター | カスタム関数を備えた高度なルールエディター | 限定的：表示／非表示、値を計算、カスタム関数 | 限定的：カスタム実装が必要 |
| **添付ファイルのサポート** | ✅ | ✅ | ✅ | ℹ (早期アクセス) | ❌ |
| **CAPTCHA サポート** | reCAPTCHA v2／Enterprise、hCaptcha（EA）、Turnstile（EA） | reCAPTCHA v2／Enterprise、hCaptcha（EA） | reCAPTCHA Enterprise | reCAPTCHA Enterprise | カスタム統合が必要 |
| **送信機能** | REST エンドポイント、メール、フォームデータモデル（FDM）、AEM ワークフローを呼び出し、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion（EA） | REST エンドポイント、メール、フォームデータモデル（FDM）、AEM ワークフローを呼び出し、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion（EA） | REST エンドポイント、メール、フォームデータモデル（FDM）、AEM ワークフローを呼び出し、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion（EA） | スプレッドシートのみ | カスタム API エンドポイント |
| **データスキーマ** | FDM、カスタム | FDM、カスタム | FDM、カスタム | カスタム | カスタム |
| **事前入力** | ✅ | ✅ | 💡(ウィザード経由) | ✅ | カスタム実装 |
| **フラグメント** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **ビジュアルルールエディター** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **ローカライゼーション** | ✅ | ✅ | 💡 (サイト経由) | ℹ️（Excel - 手動、Google Sheets 関数） | カスタム実装 |
| **データスキーマ（データツリー）** | ✅ | ✅ | 💡(UI 拡張機能経由) | ❌ | カスタム実装 |
| **テンプレートのサポート** | ✅ | ✅ | 初期コンテンツのみ、ポリシーなし | ❌ | カスタム実装 |
| **ポータル** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **DoR オーサリング** | ✅ | ✅ | 💡Derlina 経由 | ❌ | ❌ |
| **DoR の生成** | ✅ | ✅ | 💡(FORMS-2475 新規) | ❌ | ❌ |
| **テーマ** | ✅ | ✅ | ℹ️（プロジェクトレベルで） | ℹ️（プロジェクトレベルで） | カスタム実装 |
| **カスタムコンポーネント** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **OOTB およびカスタム関数** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **フラグメント参照** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Sign との統合** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **RTL サポート** | ❌ | ✅ | 💡 | 💡 | カスタム実装 |
| **実験** | ❌ | ❌ | ✅ | ✅ | カスタム実装 |
| **Workfront 経由でのタスク管理** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **パーソナライゼーション拡張機能** | ❌ | ❌ | 💡 | ❌ | カスタム実装 |
| **エディターのカスタマイズ** | ❌ | ❌ | ✅ (UI 拡張機能経由) | ❌ | カスタム実装 |
| **送信アクション** | ✅ | ✅ | ✅ | スプレッドシートのみ | カスタム実装 |


## 関連記事

- [Microsoft Excel またはGoogle Sheets を使用したドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md)
- [WYSIWYG オーサリング用ユニバーサルエディター](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
- [アダプティブフォームの作成（基盤コンポーネント）](/help/forms/creating-adaptive-form.md)
- [アダプティブフォームの作成（コアコンポーネント）](/help/forms/create-an-adaptive-form.md)
