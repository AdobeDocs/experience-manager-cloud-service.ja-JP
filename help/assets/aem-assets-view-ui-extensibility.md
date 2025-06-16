---
title: ' [!DNL AEM Assets View] の UI 拡張機能の有効化'
description: UI 拡張機能について説明します。 [!DNL AEM Assets View]. [!DNL AEM Assets View]  の UI では、特定のビジネスニーズを満たすためのカスタム UI コンポーネントを追加できます。
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: a03e6cf842f95f8799f23ed5c7e3b563b092b4e5
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 83%

---

# [!DNL AEM Assets View] の UI 拡張機能の有効化 {#AEM-Assets-View-UI-Extensibility}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
        </td>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

[!DNL AEM Assets View] は UI 拡張機能をサポートしており、[!DNL AEM Assets View] の標準機能では満たされない特定のワークフローやビジネス要件に対して、カスタム UI コンポーネントを [!DNL Assets View] の UI に追加できます。[!DNL AEM Assets View] の UI 拡張機能により柔軟性が向上し、組織は特定のワークフローと要件に合わせてインターフェイスを調整できるようになります。\
拡張機能は&#x200B;**アセット**&#x200B;レベル、**フォルダー**&#x200B;レベル、および&#x200B;**コレクション**&#x200B;レベルに追加できます。追加された拡張機能は、**アセット**、**コレクション**、または&#x200B;**フォルダー**&#x200B;の&#x200B;**[!UICONTROL 詳細]**&#x200B;ページの専用パネルに表示されます。

>[!IMPORTANT]
>
> * [!DNL AEM Assets View] の UI 拡張機能は [[!DNL Assets Ultimate]](/help/assets/assets-ultimate-overview.md) で使用できます。
> * [!DNL Assets view] の UI 拡張機能へのアクセス権を取得するには、[ [!DNL Adobe] カスタマーサポートケースを作成および送信してください](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)。
> * **[!UICONTROL 詳細なフィードバックオプション]**&#x200B;を展開し、「**[!UICONTROL 問題を報告]**」をクリックすることで、ドキュメントに関するフィードバックを提供できます。

## <a id="1"></a>アセットビューへのアクセス{#add-UI-Extensibility-in-AEM-Assets-View}

次の画像に示す手順に従って、[!DNL Assets View] にアクセスします。
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## [!DNL Assets View] での UI 拡張機能の表示 {#ui-extensibility-panel-assets-view}

[!DNL Assets View] 内で、アセット、フォルダーまたはコレクションの&#x200B;**[!UICONTROL 詳細]**&#x200B;ページに移動します。**[!UICONTROL 詳細]**ページの専用パネルには、追加された UI 拡張機能が表示されます。
![マイワークスペース](/help/assets/assets/my-workspace-assets-view3.png)

## 拡張コンポーネントを追加するための前提条件{#assets-view-ui-extensibility}

[!DNL Assets View UI] に拡張コンポーネントを追加するには、次の要件を満たす必要があります。

* [ [!DNL Assets View]](#1) にアクセスします。
* [[!DNL Adobe app builder] にアクセスします](https://developer.adobe.com/app-builder/docs/overview/)。
* 組織内に開発者またはシステム管理者の役割が存在する。詳しくは、[このドキュメント](https://developer.adobe.com/uix/docs/guides/get-access/)を参照してください。
* [!DNL Adobe IO command line tool (AIO CLI)] がローカルマシンにインストールされている。このツールは、拡張プロジェクトの作成とデプロイに不可欠です。詳しくは、[ 最初のApp Builder アプリケーションを作成 ](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app#local-environment-set-up) （アクセスには認証が必要）を参照してください。
* [!DNL JavaScript]、[!DNL Node.js]、[!DNL React] のテクノロジーを十分に理解している。

## UI 拡張機能コンポーネントを [!DNL Assets View] に追加 {#ui-extensibility-in-assets-view}

1. UI 拡張機能と [!DNL Adobe App Builder] フレームワークに関する重要な情報については、[ はじめに ](https://developer.adobe.com/uix/docs/getting-started/)を参照してください。UI 拡張機能によって [!DNL Adobe Experience Cloud services] 内でカスタムロジックと UI の統合を可能にする方法と、UI 拡張機能を実装するためのアーキテクチャとワークフローについて説明します。
1. ローカル環境の設定、ローカルプレビュー、公開、管理など、UI の拡張機能に関する一般的な情報については、[ガイド](https://developer.adobe.com/uix/docs/guides/)を参照してください。
1. [!DNL AEM Assets View] 用の UI 拡張機能の開発に必要な基本事項を理解するには、[拡張機能の作成における一般的な概念](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/)を参照してください。
1. [!DNL Assets View] インターフェイスにカスタムサイドパネルを追加します。ホストアプリケーション（[!DNL Assets View]）は、これらのパネルを管理して、切り替えやディープリンクなど、UI のインタラクションを処理します。拡張機能では、`aem/assets/details/1` 拡張機能ポイントを使用して、パネル ID、タイトル、コンテンツ URL などのプロパティを指定するカスタムパネルを統合します。開発者は、`getPanels()` メソッドでカスタムパネルを登録し、カスタムコンテンツを表示するルートを構築します。API リファレンスやコード例などの詳細な実装については、[詳細ビュー](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/)を参照してください。
1. ローカル環境を設定し、最初の UI 拡張機能を作成して、[!DNL Assets View] で UI 拡張機能を開発するプロセスを直接体験してください。詳しくは、[AEM Assets View 拡張機能の開発手順](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/)を参照してください。
1. AIO CLI を使用してアプリケーションを設定し、基本的な拡張機能構造と必要なコードを生成します。詳しくは、[ [!DNL AEM Assets View] のコード生成](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/)を参照してください。
1. 拡張機能をローカルでテストして、想定どおりに動作することをデプロイメント前に確認します。完全に分離された環境または部分的に分離された環境で拡張機能を実行し、テスト用に拡張機能を [!DNL AEM Assets View] の本番環境に接続します。詳しくは、[トラブルシューティング -  [!DNL AEM Assets View]  の拡張機能](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/)を参照してください。

## Assets ビューのクイックアクションバーとアクションバーのカスタマイズ {#customize-quick-actions-and-actions-bar}

Assets ビューで 1 つ以上のアセットを選択したときに表示されるアクション（アクションバー）をカスタマイズできます。 Assets表示を使用すると、アセットカードで「その他のオプション」（...）をクリックしたときに表示されるアクションをカスタマイズすることもできます。 詳細については、「[ 参照ビュー ](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/browse-view/)」を参照してください。

## Assets ビューでカスタムダイアログを開く {#open-custom-dialogs-assets-view}

Assets ビューでは、選択したテキストでカスタムダイアログを開く機能も提供されます。 テキストにリンクを追加することもできます。 詳しくは、[ モーダル API](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/#modal-api) を参照してください。
