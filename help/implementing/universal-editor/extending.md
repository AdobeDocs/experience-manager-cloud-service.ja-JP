---
title: ユニバーサルエディターの拡張
description: コンテンツ作成者のニーズをサポートするために、ユニバーサルエディターの機能を拡張する様々なオプションについて説明します。
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0cab4a807be4aa402667feddb6a948f0d2db371f
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 6%

---


# ユニバーサルエディターの拡張 {#extending}

コンテンツ作成者のニーズをサポートするために、ユニバーサルエディターの機能を拡張する様々なオプションについて説明します。

>[!TIP]
>
>ユニバーサルエディターには、プロジェクトのニーズをより適切に満たすことができる [ カスタマイズオプション ](/help/implementing/universal-editor/customizing.md) も複数あります。

## 拡張子 {#extensions}

Adobe Experience Cloud サービスとして、ユニバーサルエディターの UI は、App BuilderとExperience Managerを使用して拡張できます。 Adobeには、プロジェクトに使用できる既製の拡張機能が多数用意されています。

* **[ユニバーサルエディター用のAEM製品ピッカー ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**: エディターで製品データを選択または削除して、Adobe Commerce データを統合します。
* **[ユニバーサルエディターのコンテンツドラフト ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**：複数のコンテンツのドラフトを作成、編集、管理します。
* **[設定可能なアセットピッカー ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**：編集されたページで使用されているリポジトリ以外のリポジトリからのアセット選択を有効にします。
* **Forms ルールエディター**：コーディングを行わずに、AEM Forms フィールドに動的な動作を視覚的に追加します。
* **[コンテンツフラグメントをAdobe Targetに書き出し ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**:Adobe Experience Manager as a Cloud Serviceで作成されたコンテンツフラグメントをAdobe Targetに書き出して、Target アクティビティでオファーとして使用し、エクスペリエンスを大規模にテストおよびパーソナライズします。
* **[コンテンツフラグメントワークフロー ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**：選択したコンテンツフラグメントのAEM ワークフローを開始します。

## UI の拡張 {#extending-ui}

ユニバーサルエディターの UI 拡張機能は、Adobe App Builderで作成されたJavaScript アプリケーションです。 これらの同じツールを使用して、ヘッダーメニューとプロパティパネルに独自のボタンとアクションを追加し、ユニバーサルエディター用に独自のイベントを作成することもできます。

独自の拡張機能を作成する可能性については、次のリソースを参照してください。

1. [UI 拡張機能](https://developer.adobe.com/uix/docs/) - UI 拡張機能の開発者向けドキュメント。
1. [UI 拡張機能ガイド](https://developer.adobe.com/uix/docs/guides/) - 独自の拡張機能を開発する方法に関する手順説明
1. [ ユニバーサルエディター UI 拡張ポイント ](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - ユニバーサルエディター固有の拡張ポイントのドキュメント

>[!TIP]
>
>例によって学びたい場合は、[AEM UI 拡張機能のチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) を参照してください。 コンテンツフラグメントコンソールの拡張に重点を置いていますが、ユニバーサルエディターで UI 拡張機能を実装する場合の概念は同じです。

[AEM SitesでExtension Managerを使用 ](https://developer.adobe.com/uix/docs/extension-manager/) すると、インスタンスごとに拡張機能を有効または無効にしたり、ユニバーサルエディター用の拡張機能を含むAdobeのファーストパーティ拡張機能にアクセスしたりできます。

## 拡張ポイント {#extension-points}

UI の拡張機能に加えて、ユニバーサルエディターには、カスタムビジネス要件のシームレスな統合を可能にする他の多くの柔軟な拡張ポイントが用意されています。

* **[ブロック](/help/edge/developer/block-collection.md)**：シンプルな JSON 形式では、プロジェクトで、コンテンツ作成に使用できるブロックと UE 機能を調整できます。
* **[カスタムユーザーインターフェイス](#extending-ui)**：拡張機能では、必要な UI をサイドパネルやモーダルダイアログに表示できます。
* **[イベント](/help/implementing/universal-editor/events.md)**：拡張機能は、作成者のアクションと選択に関するイベントをページで受け取り、適切に応答します。
