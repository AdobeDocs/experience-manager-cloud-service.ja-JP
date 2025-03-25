---
title: ' [!DNL AEM Assets View] の UI 拡張機能を有効にする'
description: 特定のビジネスニーズに合わせてカスタム UI コンポーネントを追加できる  [!DNL AEM Assets View]. [!DNL AEM Assets View] UI の UI 拡張機能について説明します。
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: 969860593670ce490cc688a92c349addb952b3b4
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 4%

---

# [!DNL AEM Assets View] で UI 拡張機能を有効にする {#AEM-Assets-View-UI-Extensibility}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
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

[!DNL AEM Assets View] は UI 拡張機能をサポートしており、[!DNL AEM Assets View] の標準機能では満たされない特定のワークフローおよびビジネス要件に対して、カスタム UI コンポーネントを [!DNL Assets View] UI に追加できます。 [!DNL AEM Assets View] の UI 拡張機能により柔軟性が向上し、組織は特定のワークフローと要件に合わせてインターフェイスを調整できます。\
拡張機能は **アセット**、**フォルダー** および **コレクション** レベルに追加できます。 追加された拡張機能は、**アセット**、**コレクション** または **フォルダー** **[!UICONTROL 詳細]** ページの専用パネルに表示されます。

>[!IMPORTANT]
>
> * [[!DNL Assets Ultimate]](/help/assets/assets-ultimate-overview.md) で [!DNL AEM Assets View]UI 拡張機能を使用できます。
> * UI 拡張機能 [!DNL Assets view] アクセスするには、[ カスタマーサポートケースを作成して送信  [!DNL Adobe]  を行います ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)。
> * 「詳細なフィードバックオプション **[!UICONTROL を展開し、「**[!UICONTROL  問題を報告 ]**」をクリックすることで、ドキュメントに関するフィードバックを提供でき]** す。

## Assets ビューへの <a id="1"></a> アクセス{#add-UI-Extensibility-in-AEM-Assets-View}

次の画像に示す手順に従って、[!DNL Assets View] にアクセスします。
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## [!DNL Assets View] での UI 拡張機能の表示 {#ui-extensibility-panel-assets-view}

[!DNL Assets View] 内で、アセット、フォルダーまたはコレクションの **[!UICONTROL 詳細]** ページに移動します。 **[!UICONTROL 詳細]** ページには、追加された UI 拡張機能が専用パネルに表示されます。
![ マイワークスペース ](/help/assets/assets/my-workspace-assets-view3.png)

## 拡張コンポーネントを追加するための前提条件{#assets-view-ui-extensibility}

[!DNL Assets View UI] ージに拡張コンポーネントを追加するには、次の要件を満たします。

* [ アクセス先  [!DNL Assets View]](#1)。
* [[!DNL Adobe app builder]](https://developer.adobe.com/app-builder/docs/overview/) へのアクセス。
* 組織内のシステム管理者の役割の開発者に対する使用権限。 詳しくは、[ このドキュメント ](https://developer.adobe.com/uix/docs/guides/get-access/) を参照してください。
* [!DNL Adobe IO command line tool (AIO CLI)] がローカルマシンにインストールされている。 このツールは、拡張機能プロジェクトの作成とデプロイに不可欠です。 詳しくは、[ このドキュメント ](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up) を参照してください。
* [!DNL JavaScript]、[!DNL Node.js]、[!DNL React] のテクノロジーに関する十分な理解。

## UI 拡張機能コンポーネントを [!DNL Assets View] に追加します {#ui-extensibility-in-assets-view}

1. UI 拡張機能と [!DNL Adobe App Builder] フレームワークに関する重要な情報については、「[ はじめに ](https://developer.adobe.com/uix/docs/getting-started/)」を参照してください。 UI 拡張機能によって [!DNL Adobe Experience Cloud services] 内でカスタムロジックと UI の統合を可能にする方法と、UI 拡張機能を実装するためのアーキテクチャとワークフローについて説明します。
1. ローカル環境の設定、ローカルプレビュー、公開、管理など、UI の拡張機能に関する一般的な情報については、[ ガイド ](https://developer.adobe.com/uix/docs/guides/) を参照してください。
1. [!DNL AEM Assets View] 用の UI 拡張機能を開発するために必要な基本事項を理解するには、[ 拡張機能の作成における一般的な概念 ](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) を参照してください。
1. [!DNL Assets View] インターフェイスへのカスタムサイドパネルの追加 ホストアプリケーション（[!DNL Assets View]）は、これらのパネルを管理して、切り替えやディープリンクなど、UI のインタラクションを処理します。 拡張機能では、`aem/assets/details/1` 拡張機能ポイントを使用して、パネル ID、タイトル、コンテンツ URL などのプロパティを指定するカスタムパネルを統合します。 開発者は、`getPanels()` メソッドでカスタムパネルを登録し、カスタムコンテンツを表示するルートを構築します。 API リファレンスやコード例などの詳細な実装については、[ 詳細ビュー ](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/) を参照してください。
1. ローカル環境を設定し、最初の UI 拡張機能を作成して、[!DNL Assets View] で UI 拡張機能を開発するプロセスを直接体験します。 詳しくは [ ステップバイステップのAEM Assets ビュー拡張機能の開発 ](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/) を参照してください。
1. AIO CLI を使用してアプリケーションを設定し、基本的な拡張機能構造と必要なコードを生成します。 詳しくは、[ のコード生成  [!DNL AEM Assets View]](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/) を参照してください。
1. 拡張機能をローカルでテストして、デプロイメント前に想定どおりに動作することを確認します。 拡張機能を完全に分離された環境または部分的に分離された環境で実行し、テスト用に拡張機能を実稼動 [!DNL AEM Assets View] に接続します。 詳しくは、[ トラブルシューティング - [!DNL AEM Assets View]  拡張機能 ](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/) を参照してください。
