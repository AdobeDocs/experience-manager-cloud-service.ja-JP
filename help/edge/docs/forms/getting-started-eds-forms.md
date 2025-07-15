---
title: AEM Edge Delivery ServicesのFormsの概要
description: ユニバーサルエディターのオーサリングアプローチに重点を置いて、Adobe Experience Manager Edge Delivery Servicesで高パフォーマンスのフォームを作成して配信する方法を説明します。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---


# AEM Edge Delivery ServicesのFormsの概要

<span class="preview"> これは、アドビの <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features"> プレリリースチャネル </a> で利用できるプレリリース機能です。</span>

Adobe Experience Manager（AEM）Edge Delivery Services（EDS）を使用すると、非常に高速で拡張性の高い web エクスペリエンスをエッジから提供できます。 このガイドでは、**これらのエクスペリエンス用のフォームを作成して公開する方法** を、明確なレコメンデーション階層を使用して説明します。

1. **ユニバーサルエディター（UE） – ほとんどのチームに最適**
2. **ドキュメントベースのオーサリング（ドキュメント/シート） – 迅速でシンプルなフォームに最適**
3. **ドキュメントオーサリング （DA） - DA で作成されたページにフォームを埋め込むために使用します**

最終的には、適切なオーサリング方法を選択し、送信オプションを理解して、次の手順に従って実稼動対応のフォームを作成できるようになります。



## オーサリング方法の選択

| チームと要件 | 推奨される方法 | 理由 |
|--------------------|--------------------|-----|
| マーケター/デザイナーには、ビジュアルコントロール、条件付きロジックまたはAEM統合が必要です | **ユニバーサルエディター** | ドラッグアンドドロップ、詳細ルール、FSS またはAEM公開への送信 |
| コンテンツ作成者は既に Word/Google Docs/シートで作業しており、スプレッドシート/メールへのシンプルなデータキャプチャが可能 | **ドキュメントベースのオーサリング** | 使い慣れたツール、基本フォームの最速パス |
| 組み込み web サイトページ **ドキュメントオーサリング（DA）** | UE またはドキュメントベースのフォームを DA ページに **埋め込み** | DA 自体はフォームを作成しません |


## オーサリング方法の詳細

### ユニバーサルエディター

ユニバーサルエディターは、マーケターやデザイナー向けの視覚的なドラッグ&amp;ドロップオーサリングツールで、スピードとエンタープライズクラスの機能を組み合わせています。

* リアルタイムのWYSIWYG編集とデバイスのプレビュー。
* 高度なルールと検証 UI - コードは不要です。
* AEMのアセット、ワークフロー、フォームデータモデル（FDM）との直接統合。
* Vanilla JS/CSS のカスタムコンポーネントを開発者にシームレスに引き継ぎます。
* 柔軟な送信ターゲット：**Forms送信サービス（FSS）で簡単に開始したり** ニーズの拡大に合わせて **AEM公開送信アクション** に切り替えたりできます。

> **推奨事項**：チームが 100 % ドキュメント中心で、フォームが非常に基本的でない限り、新しいフォームプロジェクトをすべてユニバーサルエディターで開始します。


### ドキュメントベースのオーサリング（ドキュメント/シート）

ドキュメントベースのオーサリングは、Microsoft Word、Google Docs、Google Sheets などの使い慣れたツールを使用して、シンプルで複雑の少ないフォームを作成する場合に適しています。 この方法は、フォームをすばやく簡単に作成する必要があるコンテンツチームに最適です。

* テーブル（ドキュメント）内または行（シート）としてフォームフィールドを定義します。
* 基本的なフィールド検証と、スパム対策のためのGoogle reCAPTCHA をサポートします。
* フォーム送信は、Forms送信サービスでのみ処理されます。
* 即時公開 – ソースドキュメントで行われた変更は、デプロイメントパイプラインを必要とせずに、直ちにサイトに反映されます。


### ドキュメントオーサリング（DA）へのFormsの埋め込み

ドキュメントオーサリング（DA）は、構造化ページコンテンツを作成するために設計されたもので、ネイティブのフォーム作成をサポートしていません。 DA で作成されたページにフォームを追加するには、次の手順に従います。

1. **ユニバーサルエディター** （推奨）またはドキュメントベースのオーサリングを使用してフォームを作成します。
2. フォームを公開して、一意の URL （例：`/forms/contact-us`）を生成します。
3. DA ページに **フォームを埋め込み** ブロックを挿入し、公開されたフォームの URL を指定します。

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

1. **ユニバーサルエディターで開始：** フォームのオーサリングを開始するには、[ ユニバーサルエディター入門ガイド ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) を参照してください。
2. **フォーム送信の設定：** 希望する送信方法を選択して設定します。 設定手順については、[Forms送信サービス ](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) またはAEMの公開送信アクションを参照してください。
3. **適用のベストプラクティス：** アクセシビリティとパフォーマンスを確保するために、[ フォームデザインのベストプラクティス ](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md) を確認します。
4. **ドキュメントベースのオーサリングを使用：** Microsoft Excel またはGoogle Sheets でフォームを作成するには、[ ドキュメントベースのオーサリングのチュートリアル ](/help/edge/docs/forms/tutorial.md) に従います。
5. **ドキュメントオーサリングへのFormsの埋め込み：** ドキュメントオーサリングでページを作成する場合、公開済みフォームの埋め込み手順については、[DA チュートリアル ](https://www.aem.live/developer/da-tutorial) を参照してください。

> **これで、AEM Edge Delivery Servicesを使用して最初の高性能フォームを作成する準備が整いました。**