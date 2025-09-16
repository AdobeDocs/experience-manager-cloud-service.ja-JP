---
title: ユニバーサルエディターの拡張
description: コンテンツ作成者のニーズに合わせてユニバーサルエディターの機能を拡張する様々なオプションについて説明します。
feature: Developing
role: Admin, Architect, Developer
exl-id: 2f487fa5-57a7-477a-ad68-590e6cc12f4e
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: ht
source-wordcount: '581'
ht-degree: 100%

---

# ユニバーサルエディターの拡張 {#extending}

コンテンツ作成者のニーズに合わせてユニバーサルエディターの機能を拡張する様々なオプションについて説明します。

>[!TIP]
>
>ユニバーサルエディターには、プロジェクトのニーズをより適切に満たすことができる[カスタマイズオプション](/help/implementing/universal-editor/customizing.md)もいくつか用意されています。

## 拡張子 {#extensions}

Adobe Experience Cloud サービスとして、ユニバーサルエディターの UI は、App Builder とExperience Manager を使用して拡張できます。アドビでは、[Extension Manager](https://experience.adobe.com/aem/extension-manager) を通じてプロジェクトに使用できる、既製の拡張機能を多数提供しています。

* **[AEM マルチサイト管理（MSM）拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)**：コンポーネントレベルで継承を解除または復元します
* **[AEM ページプロパティ拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties)**：ユニバーサルエディターでページのページプロパティウィンドウにアクセスします
* **[AEM サイト管理拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#sites-console)**：ユニバーサルエディター内のページの場所まで Sites コンソールを開きます
* **[AEM ページロック拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#locking-pages)**：ユニバーサルエディターからページロックステータスを表示および変更します
* **[AEM ワークフロー拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#workflows)**：ユニバーサルエディターからページおよびページコンテンツのワークフローを開始します
* **[AEM ユニバーサルエディター開発ログイン拡張機能](/help/sites-cloud/authoring/universal-editor/authoring.md#developer-login)**：ローカルで開発する際に、ローカルの AEM SDK に簡単に認証します
* **[バリエーションを生成](/help/generative-ai/generate-variations-integrated-editor.md)**：生成人工知能（AI）を使用して、プロパティパネルでコンテンツのバリエーションを直接作成します。
* **[ユニバーサルエディター用の AEM 製品ピッカー](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**：エディターから製品データを選択または削除して、Adobe Commerce データを統合します。
* **[ユニバーサルエディターコンテンツドラフト](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**：複数のコンテンツドラフトを作成、編集、管理します。
* **[設定可能なアセットピッカー](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**：編集したページで使用されているリポジトリ以外のリポジトリからのアセット選択を有効にします。
* **Forms ルールエディター**：コーディングせずに、視覚的に AEM Forms フィールドに動的な動作を追加します。
* **[コンテンツフラグメントを Adobe Target に書き出し](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**：Adobe Experience Manager as a Cloud Service で作成されたコンテンツフラグメントを Adobe Target に書き出し、Target アクティビティのオファーとして使用して、大規模なエクスペリエンスをテストおよびパーソナライズします。
* **[コンテンツフラグメントワークフロー](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**：選択したコンテンツフラグメントの AEM ワークフローを開始します。

これらの拡張機能を有効にする方法について詳しくは、[Extension Manager ドキュメント](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)を参照してください。

## UI の拡張 {#extending-ui}

ユニバーサルエディターの UI 拡張機能は、Adobe App Builder を使用して作成された JavaScript アプリケーションです。また、これらの同じツールを使用して、ヘッダーメニューとプロパティパネルに独自のボタンとアクションを追加したり、ユニバーサルエディター用に独自のイベントを作成したりすることもできます。

独自の拡張機能を作成する可能性について詳しくは、次のリソースを参照してください。

1. [UI 拡張機能](https://developer.adobe.com/uix/docs/) - UI 拡張機能の開発者向けドキュメント。
1. [UI 拡張機能ガイド](https://developer.adobe.com/uix/docs/guides/) - 独自の拡張機能を開発する方法に関する手順説明
1. [ユニバーサルエディター UI 拡張ポイント](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - ユニバーサルエディター固有の拡張ポイントについてのドキュメント

>[!TIP]
>
>例について詳しくは、[AEM UI 拡張チュートリアル](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview)を参照してください。コンテンツフラグメントコンソールの拡張に重点を置いていますが、ユニバーサルエディターで UI 拡張機能を実装する場合の概念は同じです。

[AEM Sites の Extension Manager を使用](https://developer.adobe.com/uix/docs/extension-manager/)すると、拡張機能をインスタンスごとに有効または無効にしたり、ユニバーサルエディターを含むアドビのファーストパーティ拡張機能にアクセスしたりできます。

## 拡張ポイント {#extension-points}

UI 拡張機能に加えて、ユニバーサルエディターには、カスタムビジネス要件のシームレスな統合を可能にする他の多くの柔軟な拡張ポイントが用意されています。

* **[ブロック](https://www.aem.live/developer/block-collection)**：シンプルな JSON 形式で、プロジェクトではコンテンツ作成に使用できるブロックと UE 機能を調整できます。
* **[カスタムユーザーインターフェイス](#extending-ui)**：拡張機能では、サイドパネルまたはモーダルダイアログに必要な UI を表示できます。
* **[イベント](/help/implementing/universal-editor/events.md)**：拡張機能では、ページ上での作成者のアクションと選択に関するイベントを受信し、適切に応答します。
