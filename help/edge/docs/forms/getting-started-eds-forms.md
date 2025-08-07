---
title: AEM Edge Delivery Services で Forms を使い始める
description: ユニバーサルエディターのオーサリングアプローチに重点を置いて、Adobe Experience Manager Edge Delivery Services でパフォーマンスの高いフォームを作成および配信する方法について説明します。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 100%

---


# AEM Edge Delivery Services で Forms を使い始める

<span class="preview">これは、<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features">プレリリースチャネル</a>を通じて使用できるプレリリース機能です。</span>

Adobe Experience Manager（AEM）Edge Delivery Services（EDS）を使用すると、非常に高速で拡張性の高い web エクスペリエンスをエッジから提供できます。このガイドでは、明確なレコメンデーション階層を持つ&#x200B;**これらのエクスペリエンス向けのフォームを作成および公開する方法**&#x200B;について説明します。

1. **ユニバーサルエディター（UE）- ほとんどのチームに最適な選択肢**
2. **ドキュメントベースのオーサリング（ドキュメント／スプレッドシート） - 迅速でシンプルなフォームに最適**
3. **ドキュメントオーサリング（DA） - DA で作成したページにフォームを埋め込むために使用**

最終的には、適切なオーサリング方法を選択し、送信オプションを理解して、実稼動対応のフォームに向けた次の手順に従うことができるようになります。



## オーサリング方法の選択

| チームと要件 | 推奨される方法 | 理由 |
|--------------------|--------------------|-----|
| マーケター／デザイナーには、ビジュアルコントロール、条件付きロジックまたは AEM 統合が必要です | **ユニバーサルエディター** | ドラッグ＆ドロップ、高度なルール、FSS または AEM パブリッシュへの送信 |
| コンテンツ作成者は、既に Word／Google Docs／Sheets で作業し、スプレッドシート／メールへのシンプルなデータキャプチャが可能です | **ドキュメントベースのオーサリング** | 使い慣れたツール、基本フォームへの最速パス |
| **ドキュメントオーサリング（DA）**&#x200B;で作成された web サイトページ | UE またはドキュメントベースのフォームを DA ページに&#x200B;**埋め込む** | DA ではフォーム自体を作成しません |


## オーサリング方法の詳細

### ユニバーサルエディター

ユニバーサルエディターは、次の速度とエンタープライズグレードの機能を組み合わせた、マーケターやデザイナー向けの視覚的なドラッグ＆ドロップオーサリングツールです。

- リアルタイムの WYSIWYG 編集とデバイスのプレビュー。
- 高度なルールと検証 UI - コードは不要です。
- AEM のアセット、ワークフロー、フォームデータモデル（FDM）との直接統合。
- Vanilla JS／CSS のカスタムコンポーネントの開発者へのシームレスなハンドオフ。
- 柔軟な送信ターゲット：**Forms 送信サービス（FSS）**&#x200B;を使用してシンプルに開始するか、ニーズの拡大に合わせて **AEM パブリッシュの送信アクション**&#x200B;に切り替えます。

> **レコメンデーション**：チームが 100％ドキュメント中心で、フォームが非常に基本的でない限り、すべての新しいフォームプロジェクトはユニバーサルエディターで開始します。


### ドキュメントベースのオーサリング（ドキュメント／スプレッドシート）

ドキュメントベースのオーサリングは、Microsoft Word、Google Docs、Google Sheets などの使い慣れたツールを使用して、シンプルで複雑さの少ないフォームを作成するのに最適です。この方法は、フォームをすばやく簡単に作成する必要があるコンテンツチームに最適です。

- フォームフィールドをテーブル（ドキュメント）内または行（スプレッドシート）として定義します。
- 基本的なフィールド検証と、スパム保護を実現する Google reCAPTCHA をサポートします。
- フォーム送信は、Forms 送信サービスを通じてのみ処理されます。
- 即時公開 - ソースドキュメントで行われた変更は、デプロイメントパイプラインを必要とせずに、すぐにサイトに反映されます。


### ドキュメントオーサリング（DA）でのフォームの埋め込み

ドキュメントオーサリング（DA）は、構造化されたページコンテンツの作成用に設計されており、ネイティブフォームの作成はサポートしていません。DA で作成したページにフォームを追加するには、次の手順に従います。

1. **ユニバーサルエディター**（推奨）またはドキュメントベースのオーサリングを使用してフォームを作成します。
2. フォームを公開して、一意の URL（例：`/forms/contact-us`）を生成します。
3. DA ページに&#x200B;**フォームを埋め込み**&#x200B;ブロックを挿入し、公開されたフォームの URL を指定します。

<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## 次の手順

1. **ユニバーサルエディターでの開始：**&#x200B;フォームのオーサリングを開始するには、[ユニバーサルエディター入門ガイド](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)を参照してください。
2. **フォーム送信の設定：**&#x200B;ご希望の送信方法を選択および設定します。設定手順について詳しくは、[Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) または AEM パブリッシュの送信アクションを参照してください。
3. **ベストプラクティスを適用：** アクセシビリティとパフォーマンスを確保するために、[フォームデザインのベストプラクティス](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md)を確認します。
4. **ドキュメントベースのオーサリングを使用：** Microsoft Excel または Google Sheets でフォームを作成するには、[ドキュメントベースのオーサリングのチュートリアル](/help/edge/docs/forms/tutorial.md) に従います。
5. **ドキュメントオーサリングへのFormsの埋め込み：**&#x200B;ドキュメントオーサリングでページを作成する場合、公開済みフォームの埋め込み手順については、[DA チュートリアル](https://www.aem.live/developer/da-tutorial)を参照してください。

> **これで、AEM Edge Delivery Servicesを使用して最初の高性能フォームを作成する準備が整いました。**