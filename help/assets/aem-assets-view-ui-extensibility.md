---
title: AEM Assets ビュー UI 拡張機能
description: AEM Assets ビューの UI 拡張機能について説明します。 AEM Assets ビュー UI を使用すると、特定のビジネスニーズに合わせてカスタム UI コンポーネントを追加できます。
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: bbb183470e12c0fc81c821fc2e0c1e7d77c33707
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 5%

---

# AEM Assets ビュー UI 拡張機能{#AEM-Assets-View-UI-Extensibility}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

AEM Assets ビューには、UI 拡張機能があります。 この機能を使用すると、Assets ビューの標準機能では満たされない特定のビジネスニーズを満たすために、カスタム UI コンポーネントをAEM Assets ビュー UI に追加できます。 この拡張機能により、AEM Assets ビューの柔軟性が向上し、組織は特定のワークフローと要件に合わせてインターフェイスを調整できます。
拡張機能をアセット、フォルダー、コレクションレベルに追加できます。 追加された拡張機能は、アセット、コレクション、フォルダーの詳細ページの専用パネル内に表示されます。

>[!IMPORTANT]
>
> * AEM Assets ビュー UI 拡張機能は、[Assets Ultimate](/help/assets/assets-ultimate-overview.md) で利用できます。
> * Assets ビュー UI 拡張機能にアクセスするには、[Adobeのカスタマーサポートケースを作成して送信 ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) します。
> * 「詳細なフィードバック」オプションを展開し、「問題を報告」をクリックすると、ドキュメントに関するフィードバックを得ることができます。

## Assets ビューへのアクセス方法に <a id="1"></a> いて

次の方法で、Assets ビューにアクセスします。
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## UI 拡張機能は、「Assets ビュー」 UI のどこに表示されますか？ {#ui-extensibility-panel-assets-view}

Assets ビュー内で、アセット、フォルダーまたはコレクションの詳細ページに移動します。 この詳細ページには、追加された UI 拡張機能を表示する専用のパネルがあります。
![ マイワークスペース ](/help/assets/assets/my-workspace-assets-view3.png)


## 拡張コンポーネントを追加するための前提条件

* [Assets ビューへのアクセス ](#1)。
* [Adobeの App Builder](https://developer.adobe.com/app-builder/docs/overview/) にアクセスします。
* 組織内のシステム管理者の役割の開発者の権利。 詳しくは、[this](https://developer.adobe.com/uix/docs/guides/get-access/) を参照してください。
* Adobe IO コマンドラインツール（AIO CLI）をローカルマシンにインストールする必要があります。 このツールは、拡張機能プロジェクトの作成とデプロイに不可欠です。 詳しくは、[this](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up) を参照してください。
* JavaScript、Node.js および React テクノロジーに関する十分な理解。

## Assets ビュー UI での UI 拡張コンポーネントの追加{#Adding-UI-Extensibility-Component-on-Assets-View}

1. UI 拡張機能とAdobeApp Builder フレームワークに関する基本的な情報については、[ はじめに ](https://developer.adobe.com/uix/docs/getting-started/) を参照してください。 UI 拡張機能によってカスタムロジックと UI をAdobe Experience Cloud サービス内で統合する方法と、UI 拡張機能を実装するためのアーキテクチャとワークフローについて説明します。
1. ローカル環境の設定、ローカルプレビュー、公開、管理など、UI の拡張機能に関する一般的な情報については、[ ガイド ](https://developer.adobe.com/uix/docs/guides/) を参照してください。
1. AEM Assets ビュー用の UI 拡張機能を開発するために必要な基本事項を理解するには、[ 拡張機能の作成における一般的な概念 ](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) を参照してください。
1. Assets ビューインターフェイスにカスタムサイドパネルを追加します。 ホストアプリケーション（Assets ビュー）はこれらのパネルを管理し、切り替えやディープリンクなどの UI インタラクションを処理します。 拡張機能では、`aem/assets/details/1` 拡張機能ポイントを使用して、パネル ID、タイトル、コンテンツ URL などのプロパティを指定するカスタムパネルを統合します。 開発者は、`getPanels()` メソッドでカスタムパネルを登録し、カスタムコンテンツを表示するルートを構築します。 API リファレンスやコード例などの詳細な実装については、[ 詳細ビュー ](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/) を参照してください。
1. ローカル環境を設定し、最初の UI 拡張機能を作成して、Assets ビューで UI 拡張機能を開発するプロセスを実際に体験します。 詳しくは [ ステップバイステップのAEM Assets ビュー拡張機能の開発 ](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/) を参照してください。
1. AIO CLI を使用してアプリを設定し、基本的な拡張機能構造と必要なコードを生成します。 詳しくは、[AEM Assets ビューのコード生成 ](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/) を参照してください。
1. 拡張機能をローカルでテストして、デプロイメント前に想定どおりに動作することを確認します。 拡張機能を完全に分離された環境または部分的に分離された環境で実行し、テスト用に拡張機能を実稼動環境のAEM Assets ビューに接続します。 詳しくは、[ トラブルシューティング - AEM Assets ビュー拡張機能 ](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/) を参照してください。
