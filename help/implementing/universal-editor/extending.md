---
title: ユニバーサルエディターの拡張
description: コンテンツ作成者のニーズをサポートするために、ユニバーサルエディターの機能を拡張する様々なオプションについて説明します。
feature: Developing
role: Admin, Architect, Developer
exl-id: 2f487fa5-57a7-477a-ad68-590e6cc12f4e
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 16%

---

# ユニバーサルエディターの拡張 {#extending}

コンテンツ作成者のニーズをサポートするために、ユニバーサルエディターの機能を拡張する様々なオプションについて説明します。

>[!TIP]
>
>ユニバーサルエディターには、プロジェクトのニーズをより適切に満たすことができる [ カスタマイズオプション ](/help/implementing/universal-editor/customizing.md) も複数あります。

## 拡張子 {#extensions}

Adobe Experience Cloud サービスとして、ユニバーサルエディターの UI は、App BuilderとExperience Managerを使用して拡張できます。 Adobeでは、[Extension Manager](https://experience.adobe.com/aem/extension-manager) を通じて使用できる、プロジェクトに対応した多くの既製の拡張機能を提供しています。

* **[AEM Multi-Site-Management （MSM）拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)**: コンポーネントレベルでの継承の解除または復元
* **[AEMのページプロパティ拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties)**: ユニバーサルエディターでページのページプロパティウィンドウにアクセスします
* **[AEM Site Admin Extension](/help/sites-cloud/authoring/universal-editor/authoring.md#sites-console)**: Sites コンソールを開いて、ユニバーサルエディターでページの場所を指定します
* **[AEM ページロック拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#locking-pages)**: ユニバーサルエディターでページロックステータスを表示して変更できます
* **[AEM ワークフロー拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#workflows)**: ページおよびページコンテンツでユニバーサルエディターからワークフローを開始します
* **[AEM Universal Editor Dev Login Extension](/help/sites-cloud/authoring/universal-editor/authoring.md#developer-login)**: ローカルで開発する場合、ローカルのAEM SDKへの認証が容易になります
* **[バリエーションの生成](/help/generative-ai/generate-variations-integrated-editor.md)**：生成人工知能（AI）を使用して、プロパティパネルでコンテンツのバリエーションを直接作成します。
* **[ユニバーサルエディター用のAEM製品ピッカー ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**: エディターで製品データを選択または削除して、Adobe Commerce データを統合します。
* **[ユニバーサルエディターのコンテンツドラフト ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**：複数のコンテンツのドラフトを作成、編集、管理します。
* **[設定可能なアセットピッカー ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**：編集されたページで使用されているリポジトリ以外のリポジトリからのアセット選択を有効にします。
* **Forms ルールエディター**：コーディングを行わずに、AEM Forms フィールドに動的な動作を視覚的に追加します。
* **[コンテンツフラグメントをAdobe Targetに書き出し ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**:Adobe Experience Manager as a Cloud Serviceで作成されたコンテンツフラグメントをAdobe Targetに書き出して、Target アクティビティでオファーとして使用し、エクスペリエンスを大規模にテストおよびパーソナライズします。
* **[コンテンツフラグメントワークフロー ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**：選択したコンテンツフラグメントのAEM ワークフローを開始します。

これらの拡張機能を有効にする方法については、[Extension Managerのドキュメントを参照してください ](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)。

## UI の拡張 {#extending-ui}

ユニバーサルエディターの UI 拡張機能は、Adobe App Builderで作成されたJavaScript アプリケーションです。 これらの同じツールを使用して、ヘッダーメニューとプロパティパネルに独自のボタンとアクションを追加し、ユニバーサルエディター用に独自のイベントを作成することもできます。

独自の拡張機能を作成する可能性については、次のリソースを参照してください。

1. [UI 拡張機能](https://developer.adobe.com/uix/docs/) - UI 拡張機能の開発者向けドキュメント。
1. [UI 拡張機能ガイド](https://developer.adobe.com/uix/docs/guides/) - 独自の拡張機能を開発する方法に関する手順説明
1. [ ユニバーサルエディター UI 拡張ポイント ](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - ユニバーサルエディター固有の拡張ポイントのドキュメント

>[!TIP]
>
>例について詳しくは、[AEM UI 拡張チュートリアル](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview)を参照してください。コンテンツフラグメントコンソールの拡張に重点を置いていますが、ユニバーサルエディターで UI 拡張機能を実装する場合の概念は同じです。

[AEM Sites の Extension Manager を使用](https://developer.adobe.com/uix/docs/extension-manager/)すると、拡張機能をインスタンスごとに有効または無効にしたり、ユニバーサルエディターを含むアドビのファーストパーティ拡張機能にアクセスしたりできます。

## 拡張ポイント {#extension-points}

UI の拡張機能に加えて、ユニバーサルエディターには、カスタムビジネス要件のシームレスな統合を可能にする他の多くの柔軟な拡張ポイントが用意されています。

* **[ブロック ](https://www.aem.live/developer/block-collection)**：シンプルな JSON 形式では、プロジェクトで、コンテンツ作成に使用できるブロックと UE 機能を調整できます。
* **[カスタムユーザーインターフェイス](#extending-ui)**：拡張機能では、必要な UI をサイドパネルやモーダルダイアログに表示できます。
* **[イベント](/help/implementing/universal-editor/events.md)**：拡張機能は、作成者のアクションと選択に関するイベントをページで受け取り、適切に応答します。
