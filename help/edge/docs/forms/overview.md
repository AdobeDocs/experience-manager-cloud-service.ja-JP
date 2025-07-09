---
title: AEM Forms の Edge Delivery Services の概要
description: Edge Delivery Servicesを使用して、AEM Formsで高パフォーマンスのフォームを作成して配信し、迅速な開発と効率的なデータ収集を可能にする方法を説明します。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 1ddf97f56e5a9b7c95959da47a748f5a6d128e43
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 8%

---


# AEM Forms の Edge Delivery Services


AEM Forms の Edge Delivery Services は、作成者が新しいフォームを迅速に更新、公開、起動できる高速開発環境を可能にする、構成可能な一連のサービスです。これらのサービスは、エンゲージメントとコンバージョンを促進する、優れた効果の高いフォームエクスペリエンスを提供します。これらのフォームエクスペリエンスは、簡単に作成および開発できます。

* **より高速なエクスペリエンス：** Formsはグローバルなコンテンツ配信ネットワーク（CDN）から配信されるので、ユーザーによるコンテンツの読み込みを迅速に行えます。
* **迅速な開発：** 合理化された開発プロセスにより、更新を迅速化できます。 長いパイプラインビルドを待たずに、変更を公開できます。
* **柔軟なオーサリング：** 様々なツールから選択して、ドキュメントベースのオーサリング（Microsoft Word、Google Docs/Sheets）やビジュアルWYSIWYGエディター（ユニバーサルエディター）などのフォームを作成できます。

## 仕組み

Edge Delivery Servicesを使用すると、フォームの構造とコンテンツをAEM as a Cloud Service、Microsoft SharePoint、Google Drive などのソースに格納できます。 このコンテンツは、グローバル CDN に公開されます。 ユーザーがサイトを訪問すると、最適なパフォーマンスを得るために、最も近い CDN エッジサーバーからフォームが直接提供されます。

![ コンテンツソース、CDN およびユーザーを示すシンプルなアーキテクチャ図](/help/forms/assets/eds-simplified-architecture.png)
**FormsによるEdge Delivery Services アーキテクチャのシンプル化**

ユーザーが送信したデータは、シンプルなスプレッドシートから強力なAEM バックエンドに送信して、さらに処理することができます。

## オーサリング方法の選択

Edge Delivery Services サイト用のフォームを作成する方法はいくつかあります。 最適な方法は、チームのスキル、フォームの複雑さ、プロジェクトの要件によって異なります。

![ 決定ツリーは、フォームのオーサリング方法の選択に役立ちます。](/help/forms/assets/eds-authoring-selection.png)
**フォームオーサリングのデシジョンツリー**

### ドキュメントベースのオーサリング

この手法を使用すると、[Microsoft Word またはGoogle Docs/シートを使用してフォームを作成する ](/help/edge/docs/forms/create-forms.md) ことができます。 特定のテーブル形式を使用して、ドキュメント内のフォームフィールド、ラベル、タイプを定義します。 Edge Delivery Servicesは、このドキュメントをインタラクティブなHTML フォームに変換します。

**機能：**

* 使い慣れたツール（Word、Google Docs、Google シート）でオーサリングします。
* テキスト入力、メール、ドロップダウン、チェックボックス、ラジオボタンなどのフィールドを定義します。
* 必須フィールドなど、基本的な検証ルールを設定します。
* スパム対策としてGoogle reCAPTCHA を統合します。
* ファイルアップロードのサポート。
* データをスプレッドシートまたはメールアドレスに直接送信します。
* GitHub を介したカスタムコードを使用した拡張で、高度なコンポーネントとスタイル設定が可能になります。

**次の場合に最適：**

* 主にコンテンツの作成にドキュメントエディターを使用するチーム。
* 単純なフォームから適度に複雑なフォームをすばやく作成します。
* スプレッドシートまたはメールへの簡単なデータ収集。

ドキュメントベースのフォームからの送信は、通常、データを設定済みのスプレッドシートまたはメールアドレスにルーティングする [0}AEM Forms送信サービス } で処理されます。](/help/forms/forms-submission-service.md)

### ユニバーサルエディターのオーサリング

[ ユニバーサルエディターは、ドラッグ&amp;ドロップ操作でフォームを作成するための最新のWYSIWYG インターフェイス ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) を提供します。

**機能：**

* 事前定義済みのコンポーネントのライブラリを使用した、フォームの視覚的なドラッグアンドドロップによる構築。
* リアルタイム検証と複雑なビジネスロジックを設定します（例：ユーザーの選択に基づいたフィールドの表示/非表示）。
* 様々なデバイスのライブプレビュー。
* コンテンツフラグメント、AEM as a Cloud Service ワークフロー、ユーザー権限などのAEM機能との深い統合。
* 「Experience Builder」を介した、AI を利用したフォームの作成と編集。

**次の場合に最適：**

* 条件付きロジック、複数手順のパネルまたはパーソナライゼーションを使用して複雑なフォームを作成する。
* ビジュアルツールを好むチーム（マーケター、ビジネスユーザーなど）。
* データ処理およびワークフローのためにAEM バックエンドとの強力な統合が必要なプロジェクト。

ユニバーサルエディターで作成されたFormsは、[Forms送信サービスを使用するか ](/help/forms/forms-submission-service.md)[ AEM ワークフロー、REST エンドポイントまたはデータベースへのデータの送信など、高度なデータ処理のために OOTB から提供される送信アクション ](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) を使用するように設定できます。

### ドキュメントオーサリングページへのFormsの埋め込み

[ ドキュメントオーサリング（DA） ](https://www.aem.live/developer/da-tutorial) は、Edge Delivery Servicesの web サイトコンテンツを管理するためにAdobeでホストされるサービスです。 DA 自体はフォーム作成ツールではありませんが、DA を使用して web ページを作成し、他の方法で作成されたフォームを埋め込むことができます。

**仕組み：**

1. **フォームの作成：** ドキュメントベースのオーサリングまたはユニバーサルエディターを使用してフォームを作成します。
2. **フォームを公開：** フォームが公開され、独自の URL でアクセス可能であることを確認します。
3. **DA への埋め込み：** ドキュメントオーサリングページで、埋め込むフォームの URL を参照するブロックを追加します。

このアプローチは、Edge Delivery Services Sites のプライマリコンテンツ管理システムとしてドキュメントオーサリングを使用するチーム向けです。

## オーサリング方法の比較

| 条件 | ドキュメントベースのオーサリング | ユニバーサルエディター（WYSIWYG） | ドキュメントオーサリング （DA）におけるForms |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **プライマリ オーサリング ツール** | Word/Google Docs/Sheets | ブラウザー（AEM Universal Editor） | 該当なし（Formsは *埋め込み*） |
| **チームスキルレベル** | ドキュメントエディターに精通している | ビジュアル Web ツールの操作に慣れている | ページコンテンツに DA を使用 |
| **一般的なフォームの複雑さ** | シンプルから中程度 | 中規模から複雑、エンタープライズ・クラス | 埋め込まれたフォームに依存 |
| **送信オプション** | Forms送信サービス （シート/メールへ） | Forms送信サービス、AEM パブリッシュ（ワークフロー、フォームデータモデル、サードパーティ統合） | 埋め込みフォームの設定に従う |
| **AEMのバックエンドの統合** | 最小 | 高（AEM パブリッシュ送信付き） | 間接的（埋め込みユニバーサルエディターフォーム経由） |
| **次の場合に最適…** | コンテンツチームによるシンプルなフォームの迅速な作成、迅速なデータキャプチャ。 | 視覚的な制御、複雑なフォーム、深いAEM統合を必要とするマーケターやビジネスユーザー。 | プライマリコンテンツが DA で管理されるサイト。 |

<!-- 
## Detailed Feature Comparison

| **Capability**                        | **Universal Editor (WYSIWYG)** | **Document-based Authoring** | **Document Authoring (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Unified Composition with Sites**    | ✅                            |                              | ✅ (with embedded forms)     |
| **Embedding Form Support**            | ✅                            | ✅                          | ✅ (embed from Universal Editor or Docs)   |
| **Rules (Dynamic Behavior)**          | Advanced rules editor with custom functions | Limited: Show/hide, compute value, custom functions | Depends on embedded form     |
| **Attachment Support**                | ✅                            | ℹ️ (Early Access)           | Depends on embedded form     |
| **CAPTCHA Support**                   | reCAPTCHA Enterprise          | reCAPTCHA Enterprise       | Depends on embedded form     |
| **Submission Features**               | REST, Email, FDM, Workflow, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Only Spreadsheet            | Follows embedded form's setup |
| **Data Schema**                       | FDM, Custom                   | Custom                      | Based on embedded form       |
| **Pre-fill**                          | 💡 (via Wizard)               | ✅                          | Depends on embedded form     |
| **Fragments**                         | ✅                            | ✅                          | Depends on embedded form     |
| **Visual Rule Editor**                | ✅                            |                              |                              |
| **Localization**                      | 💡 (via Sites)                | ℹ️ (Excel/Sheets manual)    | Depends on embedded form     |
| **Template Support**                  | Only Initial Content          |                              |                              |
| **Theme**                             | ℹ️ (at project level)         | ℹ️ (at project level)        | ℹ️ (based on hosting site)    |
| **Custom Component**                  | ✅                            | ✅                          | ✅ (if embedded component supports it) |
| **Experimentation**                   | ✅                            | ✅                          | Depends on embed context     |
| **Submit Action**                     | ✅                            | Only Spreadsheet            | Based on embedded form       |
-->



## 次の手順

* [ドキュメントベースのオーサリングを使用したフォームの作成](/help/edge/docs/forms/tutorial.md)
* [Forms用ユニバーサルエディターについて](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [フォーム送信アクションの設定](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
* [ ドキュメントオーサリング（DA）について ](https://www.aem.live/developer/da-tutorial)
