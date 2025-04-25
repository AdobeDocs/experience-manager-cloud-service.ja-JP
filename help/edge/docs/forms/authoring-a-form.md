---
title: AEMでのフォームの作成方法
description: Adobe Experience Manager（AEM）で使用可能な様々なフォームオーサリングプラットフォームと、要件に基づいて適切なフォームオーサリングプラットフォームを選択する方法について説明します。
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: f6c6b4c17482eb519fb0d4287704d775d0a5da00
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 12%

---


# Adobe Experience Manager（AEM）でのFormsの作成方法

Adobe Experience Manager（AEM）は、魅力的でレスポンシブ、かつ動的でアダプティブなフォームを作成するための柔軟なプラットフォームを提供します。 直感的なユーザーインターフェイスに加え、アダプティブ Formsを作成および管理するための豊富な既製のコンポーネント群が用意されています。 Formsは、要件に応じて、フォームモデルやスキーマを使用せずにオーサリングすることもできます。

## オーサリングプラットフォームを選択する際の主な考慮事項

AEMには、インタラクティブで魅力的なフォームを作成するための複数のフォームオーサリングオプションが用意されています。 フォームオーサリング環境を選択する際には、次の要因を考慮してください。

| ??**配慮等** | ??**質問** |
|----------------------|--------------------|
| **ユーザーの専門知識** | 開発者、ビジネスユーザー、コンテンツ作成者など、フォームの作成者は誰ですか？ |
| **フォームの複雑さ** | フォームに高度なルール、動的セクションまたは統合が必要かどうか。 |
| **再利用性の必要性** | フォームの一部が様々なフォームやプロジェクトで再利用されますか？ |
| **柔軟な設計** | レイアウト、テーマ、スタイル設定を完全に制御する必要がありますか？ |
| **統合要件** | フォームは、データモデル、ワークフロー、外部システムのいずれかに接続する必要がありますか？ |
| **使いやすさ** | プラットフォームは、チームの技術スキルレベルに応じて直感的ですか？ |
| **パフォーマンスと拡張性** | フォームは大規模または高トラフィック環境で使用されますか？ |
| **オムニチャネル配信** | フォームは web サイト、モバイルアプリ、キオスク、または複数のチャネルで使用しますか？ |
| **柔軟な公開** | フォームは、AEM、Edge Delivery、カスタムアプリのどこに公開されますか？ |

## AEMのフォームオーサリングメソッドの概要

AEMでは、様々なユーザーのニーズ、技術的なスキルレベル、公開先に適した複数のオーサリング方法をサポートしています。

* [ 基盤コンポーネント ](/help/forms/create-adaptive-form-tutorial.md)：基盤コンポーネントを使用して、従来のインタラクティブなフォームを構築します。 レガシーシステムと統合するフォームや、長年のワークフローに依存するフォームに最適です。 基盤コンポーネントを使用して作成されたFormsは、AEMでのみ公開でき、Edge Delivery Servicesとは互換性がありません。

* [ コアコンポーネント ](/help/forms/creating-adaptive-form-core-components.md)：コアコンポーネントを使用して、レスポンシブで拡張性の高い最新のフォームを作成します。 再利用性、アクセシビリティ、パフォーマンスの向上をサポートします。 コアコンポーネントを使用して作成されたFormsは、AEMとEdge Delivery Servicesの両方で公開でき、プラットフォーム間の柔軟性を提供します。

* [Edge Delivery Services Forms](/help/edge/docs/forms/overview.md): Edge Delivery Services Formsは、フォームの作成、実行、処理の方法を変えます。 Edge Delivery Services を活用することで、組織は高速で安全な、可用性の高いデジタルフォームを作成し、高速開発環境でユーザーエクスペリエンスと運用効率を向上させることができます。Edge Delivery Services Formsは、次の 2 つの方法でオーサリングできます。
   * [WYSIWYG オーサリング ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：技術的な知識が限られたコンテンツ作成者に最適な、ビジュアルでのドラッグ&amp;ドロップによるフォーム作成にユニバーサルエディターを使用します。 ユニバーサルエディターで作成されたFormsは、Edge Delivery Servicesを使用して配信されるので、高速で軽量なレンダリングが可能です。
   * [ ドキュメントベースのオーサリング ](/help/edge/docs/forms/tutorial.md):Microsoft Excel やGoogle シートなどのツールを使用して、フォーム構造とコンテンツを定義します。 この方法は、スプレッドシート主導の入力を好むビジネスユーザーに役立ちます。 これらのフォームは、通常、Edge Delivery Servicesを通じて公開され、軽量で大量のユースケースに適しています。
* [ ヘッドレスオーサリング ](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service):API を使用して、AEMに依存せずに、任意のフロントエンド（React、Angular、モバイルアプリ、キオスクなど）のフォームを JSON としてレンダリングします。 現在、ヘッドレス配信をサポートしているのはコアコンポーネントのみです。 ヘッドレスフォームは、オムニチャネルのユースケースに最適で、AEMのページレンダリングとは独立して使用されるので、カスタムフロントエンドデプロイメントに対して柔軟です。

### AEM フォームのオーサリングメソッドの比較分析

&#x200B;次の表は様々なAEM フォームのオーサリング方法を簡潔に比較し、アプローチ、機能、公開オプションおよび理想的なユースケースをハイライト表示して、ニーズに最も適した方法を選択する際に役立ちます。

| **配慮等** | **基盤コンポーネント** | **コアコンポーネント** | **ユニバーサルエディター（WYSIWYG）** | **ドキュメントベースのオーサリング** | **ヘッドレスオーサリング** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **次に最適** | AEM内での従来のフォームおよびワークフローの維持 | 複雑なワークフローと統合を備えた、スケーラブルで最新のフォーム | 複雑な要件を持つEdge Delivery サービスサイト向けフォームの作成 | 高度な送信サービスを使用しないクイックプロトタイプまたは基本フォーム | プラットフォーム（web、モバイル、キオスクなど）をまたいだオムニチャネルエクスペリエンス |
| **ユーザーの専門知識** | 開発者、コンテンツ作成者 | 開発者、上級作成者 | ビジネスユーザー、コンテンツ作成者 | ビジネスユーザー | デベロッパー向け |
| **フォームの複雑さ** | 基本フォーム | 動的セクションを含む複雑なフォーム | カスタムアクションを含む複雑なフォーム | 単純なフォーム | 非常に複雑な API 駆動型フォーム |
| **柔軟な設計** | 限定的 | 高（CSS/JS のカスタマイズ） | 中程度（テンプレートに基づく） | 限定的 | 高（フロントエンドフレームワーク制御） |
| **統合機能** | AEMの基本的なワークフロー | 詳細（データモデル、ワークフロー） | 外部システムとの統合 | 基本（Google シート、Excel） | API を介したフルコントロール |
| **公開方法** | AEMのみ | AEM と Edge 配信サービス | Edge Delivery Services | Edge Delivery Services | API を介した任意のフロントエンド |
| **パフォーマンスと SEO** | 標準 | 基盤コンポーネントよりも改善される | レンダリングの高速化と SEO の向上を実現する高いGoogle Lighthouse スコア | レンダリングの高速化と SEO の向上を実現する高いGoogle Lighthouse スコア | 実装に依存 |
| **オムニチャネル配信** | 限定的 | モデレート | モデレート | 限定的 | 高 |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### AEM フォームオーサリングメソッドの機能比較

次の表は、様々なAEM フォームオーサリング方法での主な機能の詳細な比較を示しており、要件に最も適したアプローチの選択に役立ち&#x200B;す。

| **機能** | **基盤コンポーネント** | **コアコンポーネント** | **ユニバーサルエディター（WYSIWYG）** | **ドキュメントベースのオーサリング** | **ヘッドレスオーサリング** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **Sites との統合コンポジション** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **埋め込みフォームのサポート** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **ルール（動的動作）** | カスタム関数を備えた高度なルールエディター | カスタム関数を備えた高度なルールエディター | カスタム関数を備えた高度なルールエディター | 制限：表示/非表示、値を計算、カスタム関数 | 制限付き：カスタム実装が必要 |
| **アタッチメント サポート** | ✅ | ✅ | ✅ | ℹ️（アーリーアクセス） | ❌ |
| **CAPTCHA のサポート** | reCAPTCHA v2/エンタープライズ、hCaptcha （EA）、Turnstile （EA） | reCAPTCHA v2/Enterprise、hCaptcha （EA） | reCAPTCHA Enterprise | reCAPTCHA Enterprise | カスタム統合が必要 |
| **送信機能** | REST エンドポイント、メール、フォームデータモデル（FDM）、AEM ワークフローの呼び出し、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion （EA） | REST エンドポイント、メール、フォームデータモデル（FDM）、AEM ワークフローの呼び出し、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion （EA） | REST エンドポイント、メール、フォームデータモデル（FDM）、AEM ワークフローの呼び出し、SharePoint、OneDrive、Azure Blob Storage、Power Automate、Workfront Fusion （EA） | スプレッドシートのみ | カスタム API エンドポイント |
| **データスキーマ** | FDM、カスタム | FDM、カスタム | FDM、カスタム | カスタム | カスタム |
| **事前入力** | ✅ | ✅ | ??（ウィザードを使用） | ✅ | カスタム実装 |
| **フラグメント** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **ビジュアルルールエディター** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **ローカライゼーション** | ✅ | ✅ | ??（サイト経由） | ℹ️ （Excel – 手動，Google Sheets 関数） | カスタム実装 |
| **データスキーマ（データツリー）** | ✅ | ✅ | ??（UI 拡張機能を使用） | ❌ | カスタム実装 |
| **テンプレートのサポート** | ✅ | ✅ | 初期コンテンツのみ、ポリシーなし | ❌ | カスタム実装 |
| **ポータル** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **DoR オーサリング** | ✅ | ✅ | ??（Derlina より） | ❌ | ❌ |
| **DoR の生成** | ✅ | ✅ | ??（FORMS-2475 新規） | ❌ | ❌ |
| **テーマ** | ✅ | ✅ | ℹ️（プロジェクトレベル） | ℹ️（プロジェクトレベル） | カスタム実装 |
| **カスタムコンポーネント** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **OOTB およびカスタム関数** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **フラグメント参照** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Sign 統合** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **RTL サポート** | ❌ | ✅ | ?? | ?? | カスタム実装 |
| **実験** | ❌ | ❌ | ✅ | ✅ | カスタム実装 |
| **Workfrontによるタスクの管理** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Personalization拡張機能** | ❌ | ❌ | ?? | ❌ | カスタム実装 |
| **エディターのカスタマイズ** | ❌ | ❌ | ✅（UI 拡張機能を使用） | ❌ | カスタム実装 |
| **送信アクション** | ✅ | ✅ | ✅ | スプレッドシートのみ | カスタム実装 |


## 関連記事

* [Microsoft Excel またはGoogle Sheets を使用したドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md)
* [WYSIWYG オーサリング用ユニバーサルエディター](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [アダプティブフォームの作成（基盤コンポーネント）](/help/forms/creating-adaptive-form.md)
* [アダプティブフォームの作成（コアコンポーネント）](/help/forms/create-an-adaptive-form.md)
