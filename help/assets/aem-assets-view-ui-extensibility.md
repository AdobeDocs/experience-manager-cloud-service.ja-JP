---
title: ' [!DNL AEM Assets View] の UI 拡張機能の有効化'
description: UI 拡張機能について説明します。 [!DNL AEM Assets View]. [!DNL AEM Assets View]  の UI では、特定のビジネスニーズを満たすためのカスタム UI コンポーネントを追加できます。
feature: App Builder
role: User, Developer
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: bcdfc9bb418ab405faa82c55820a6ec6062c2b17
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 72%

---

# [!DNL AEM Assets View] の UI 拡張機能の有効化 {#AEM-Assets-View-UI-Extensibility}

[!DNL AEM Assets View] は UI 拡張機能をサポートしており、[!DNL AEM Assets View] の標準機能では満たされない特定のワークフローやビジネス要件に対して、カスタム UI コンポーネントを [!DNL Assets View] の UI に追加できます。 [!DNL AEM Assets View] の UI 拡張機能により柔軟性が向上し、組織は特定のワークフローと要件に合わせてインターフェイスを調整できるようになります。\
拡張機能は&#x200B;**アセット**&#x200B;レベル、**フォルダー**&#x200B;レベル、および&#x200B;**コレクション**&#x200B;レベルに追加できます。 追加された拡張機能は、**アセット**、**コレクション**、または&#x200B;**フォルダー**&#x200B;の&#x200B;**[!UICONTROL 詳細]**&#x200B;ページの専用パネルに表示されます。

>[!IMPORTANT]
>
> * [!DNL AEM Assets View] の UI 拡張機能は [[!DNL Assets Ultimate]](/help/assets/assets-ultimate-overview.md) で使用できます。
> * [!DNL Assets view] の UI 拡張機能へのアクセス権を取得するには、[ [!DNL Adobe] カスタマーサポートケースを作成および送信してください](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)。
> * **[!UICONTROL 詳細なフィードバックオプション]**&#x200B;を展開し、「**[!UICONTROL 問題を報告]**」をクリックすることで、ドキュメントに関するフィードバックを提供できます。

## <a id="1"></a>アセットビューへのアクセス{#add-UI-Extensibility-in-AEM-Assets-View}

次の画像に記載されている手順に従って、[!DNL Assets View]にアクセスします。
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## [!DNL Assets View] での UI 拡張機能の表示 {#ui-extensibility-panel-assets-view}

[!DNL Assets View] 内で、アセット、フォルダーまたはコレクションの&#x200B;**[!UICONTROL 詳細]**&#x200B;ページに移動します。 **[!UICONTROL 詳細]**&#x200B;ページの専用パネルには、追加された UI 拡張機能が表示されます。![マイワークスペース](/help/assets/assets/my-workspace-assets-view3.png)

## 拡張コンポーネントを追加するための前提条件{#assets-view-ui-extensibility}

[!DNL Assets View UI] に拡張コンポーネントを追加するには、次の要件を満たす必要があります。

* [ [!DNL Assets View]](#1) にアクセスします。
* [[!DNL Adobe app builder] にアクセスします](https://developer.adobe.com/app-builder/docs/overview/)。
* 組織内に開発者またはシステム管理者の役割が存在する。 詳しくは、[このドキュメント](https://developer.adobe.com/uix/docs/guides/get-access/)を参照してください。
* [!DNL Adobe IO command line tool (AIO CLI)] がローカルマシンにインストールされている。 このツールは、拡張プロジェクトの作成とデプロイに不可欠です。 詳しくは、[最初の App Builder アプリケーションの作成](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app#local-environment-set-up)（アクセスには認証が必要）を参照してください。
* [!DNL JavaScript]、[!DNL Node.js]、[!DNL React] のテクノロジーを十分に理解している。

## UI 拡張機能コンポーネントを [!DNL Assets View] に追加 {#ui-extensibility-in-assets-view}

1. UI 拡張機能と [!DNL Adobe App Builder] フレームワークに関する重要な情報については、[ はじめに ](https://developer.adobe.com/uix/docs/getting-started/)を参照してください。 UI 拡張機能によって [!DNL Adobe Experience Cloud services] 内でカスタムロジックと UI の統合を可能にする方法と、UI 拡張機能を実装するためのアーキテクチャとワークフローについて説明します。
1. ローカル環境の設定、ローカルプレビュー、公開、管理など、UI の拡張機能に関する一般的な情報については、[ガイド](https://developer.adobe.com/uix/docs/guides/)を参照してください。
1. [!DNL AEM Assets View] 用の UI 拡張機能の開発に必要な基本事項を理解するには、[拡張機能の作成における一般的な概念](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/)を参照してください。
1. [!DNL Assets View] インターフェイスにカスタムサイドパネルを追加します。 ホストアプリケーション（[!DNL Assets View]）は、これらのパネルを管理して、切り替えやディープリンクなど、UI のインタラクションを処理します。 拡張機能では、`aem/assets/details/1` 拡張機能ポイントを使用して、パネル ID、タイトル、コンテンツ URL などのプロパティを指定するカスタムパネルを統合します。 開発者は、`getPanels()` メソッドでカスタムパネルを登録し、カスタムコンテンツを表示するルートを構築します。 API リファレンスやコード例などの詳細な実装については、[詳細ビュー](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/)を参照してください。
1. ローカル環境を設定し、最初の UI 拡張機能を作成して、[!DNL Assets View] で UI 拡張機能を開発するプロセスを直接体験してください。 詳しくは、[AEM Assets View 拡張機能の開発手順](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/)を参照してください。
1. AIO CLI を使用してアプリケーションを設定し、基本的な拡張機能構造と必要なコードを生成します。 詳しくは、[ [!DNL AEM Assets View] のコード生成](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/)を参照してください。
1. 拡張機能をローカルでテストして、想定どおりに動作することをデプロイメント前に確認します。 完全に分離された環境または部分的に分離された環境で拡張機能を実行し、テスト用に拡張機能を [!DNL AEM Assets View] の本番環境に接続します。 詳しくは、[トラブルシューティング -  [!DNL AEM Assets View]  の拡張機能](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/)を参照してください。

## Assets ビューでのアクションのカスタマイズ {#customize-actions-assets-view}

AEM Assets ビューでは、参照ビューで次のアクションをカスタマイズできます。

* アクションバーで1つ以上のアセットを選択したときに表示されるアクションをカスタマイズします。

* その他のオプション（。..）をクリックすると表示されるアクションをカスタマイズします アセットカードに保存されます。

詳しくは、[ビューを参照](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/browse-view/)を参照してください。

## Assets ビューでのヘッダーメニューのカスタマイズ {#customize-header-menu-assets-view}

AEM Assets ビューでは、ヘッダーメニューをカスタマイズできます。 ヘッダーメニューは、ブラウズ画面と詳細画面の右上にあるボタンを指します。 次の操作を実行できます。

* 組み込みのヘッダーメニューボタンの前に、ヘッダーメニューにカスタムボタンを追加します。

* 現在の参照または詳細コンテキストの組み込みヘッダーメニューボタンを非表示にします。

* 組み込みのヘッダーメニューボタンのクリック数を上書きして、デフォルトのハンドラーではなく拡張機能がアクションを処理できるようにします。

ブラウズビューでは、ヘッダーメニューのカスタマイズは、アセット、検索、ごみ箱、最近表示したアセット、コレクションのコンテキストに対応します。 カスタムボタンは、これらのコンテキストのいずれかに追加できます。 **フォルダーを作成**&#x200B;および&#x200B;**アセットを追加** （アセットコンテキスト内）および&#x200B;**コレクションを作成** （コレクション内）などの組み込みボタンは、使用可能な場所で非表示または上書きできます。

詳細ビューでは、カスタムボタンを追加し、**タスクの割り当て**&#x200B;や&#x200B;**ダウンロード**&#x200B;などの組み込みアクションをカスタマイズできます。

API参照やコード例などの詳細については、[ ビューを参照](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/browse-view/#custom-header-menu-buttons)および[詳細ビュー](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/#custom-header-menu-buttons-in-details-view)を参照してください。

## アセットビューでカスタムダイアログを開く {#open-custom-dialogs-assets-view}

アセットビューでは、選択したテキストでカスタムダイアログを開く機能も提供されます。 テキストにリンクを追加することもできます。 詳しくは、[モーダル API](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/#modal-api) を参照してください。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)

