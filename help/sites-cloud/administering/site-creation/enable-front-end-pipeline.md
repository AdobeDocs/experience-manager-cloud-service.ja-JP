---
title: フロントエンドパイプラインを有効にする
description: 既存の従来の AEM オーサリングサイトに対してフロントエンドパイプラインを有効にし、パブリッシュ配信でサイトテーマを使用して、サイトをより迅速にカスタマイズする方法について説明します。
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
recommendations: noDisplay, noCatalog
source-git-commit: 8c4b34a77ef85869048fae254728c58cf0d99b66
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 90%

---


# フロントエンドパイプラインを有効にする {#enable-front-end-pipeline}

{{traditional-aem}}

既存の従来の AEM オーサリングサイトに対してフロントエンドパイプラインを有効にし、パブリッシュ配信でサイトテーマを使用して、サイトをより迅速にカスタマイズする方法について説明します。

## 概要 {#overview}

フロントエンドパイプラインは、[パブリッシュ配信](/help/sites-cloud/authoring/author-publish.md)を使用した従来のAEM オーサリングプロジェクトのメカニズムであり、[サイトテーマ](site-themes.md)および [サイトテンプレート](site-templates.md)に基づいて web サイトのフロントエンドコードのみを迅速にデプロイできます。

このパイプラインはフロントエンドコードのみを処理するので、フルスタックデプロイメントよりデプロイメントプロセスが高速になります。これにより、フロントエンド開発者は AEM の知識がなくても、サイトを簡単にカスタマイズできます。

サイトテンプレートに基づくサイトでは、フロントエンドパイプラインをデフォルトで使用できます。このドキュメントでは、フロントエンドパイプラインを利用するように既存のサイトを適応させる方法について説明します。

>[!TIP]
>
>フロントエンドパイプラインにも、フロントエンドパイプラインとサイトテンプレートを使用してサイトを迅速にデプロイする方法にも詳しくない場合は、[クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)で概要を確認してください。

AEM では、サイトがサイトテンプレートとテーマを使用して作成されていない場合でも、既存のクライアントライブラリの上にテーマをレイヤー化することで、フロントエンドパイプラインでデプロイされたテーマを読み込むようにサイトを設定できます。

## 技術的詳細 {#technical-details}

サイトのフロントエンドパイプラインを有効にすると、AEM はサイト構造に次のような変更を加えます。

* サイトのすべてのページには、追加の CSS および JS ファイルが 1 つ含まれており、専用の Cloud Manager フロントエンドパイプラインを通じて更新をデプロイすることで、このファイルを変更できます。
* 追加された CSS および JS ファイルは最初は空です。ただし、「テーマソース」フォルダーをダウンロードすると、パイプラインを通じて CSS コードと JS コードの更新をデプロイするために必要なフォルダー構造を設定できます。
* この操作によって `/conf/<site-name>/sling:configs` の下に作成される `SiteConfig` ノードと `HtmlPageItemsConfig` ノードを削除することで、変更を取り消すことができるのは、開発者のみです。

>[!NOTE]
>
>このアクションによって、フロントエンドパイプラインを使用するようにサイトの既存のクライアントライブラリが自動的に変換されることはありません。これらのソースをクライアントライブラリフォルダーからフロントエンドパイプラインフォルダーに移動するには、フロントエンド開発者が手動で行う必要があります。

## 要件 {#requirements}

AEM では、フロントエンドパイプラインを使用するように既存のサイトを自動的に適応させることができます。このワークフローを実行するには、サイトで[コアコンポーネントのページコンポーネント v2 以降](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/wcm-components/page)を使用する必要があります。

## フロントエンドパイプラインの有効化 {#enabling}

{{add-cm-allowlist-frontend-pipeline}}

サイトを有効にするには、Sites コンソールの[サイトパネル](site-rail.md)を使用して行います。

1. AEM にログインし、**グローバルナビゲーション**／**サイト**&#x200B;を使用して Sites コンソールに移動します。
1. サイトをコンソールで選択します。サイトの子ページではなくルートを選択します。
1. サイトが選択された状態で、左側の[パネルセレクター](/help/sites-cloud/authoring/basic-handling.md#rail-selector)を開き、「**サイト**」を選択します。
1. **サイト**&#x200B;パネルで「**フロントエンドパイプラインを有効化**」ボタンをクリックします。

   ![フロントエンドパイプラインの有効化](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. 実行される変更の概要が表示され、AEM から確認を求められます。確認すると、サイトに適応されます。

これで、サイトでフロントエンドパイプラインを使用する準備が整いました。フロントエンドパイプラインとサイトテーマの管理について詳しくは、以下を参照してください。

* [サイトパネルを使用したサイトテーマの管理](site-rail.md)
* [クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md) - このドキュメントジャーニーでは、フロントエンドパイプラインとクイックサイト作成ツールを使用してサイトを迅速にデプロイするプロセスの包括的な概要を示しています。
* [CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) - このドキュメントでは、フルスタックパイプラインおよび web 階層設定パイプラインとの関連でフロントエンドパイプラインについて説明しています。

## フロントエンドパイプラインとカスタムドメイン {#custom-domains}

フロントエンドパイプラインは [Cloud Manager のカスタムドメイン機能](/help/implementing/cloud-manager/custom-domain-names/introduction.md)と共に使用できますが、2 つの機能を一緒に使用する場合は、次の要件に注意してください。

### 静的フロントエンドファイル {#static-files}

フロントエンドパイプラインを介してデプロイされた静的フロントエンドアセットは、デフォルトで、Adobeの事前定義済みの静的ドメインから提供されます。

フロントエンドアセットにカスタムドメインが必要な場合は、パブリッシュ層にカスタムドメインをインストールし、Dispatcherを設定して、Adobeの静的ホスティングの場所に特定のパス（`/static/` など）をルーティングできます。 この方法では、静的アセットのリクエストを適切に転送およびキャッシュするのに、[Dispatcher ルール](https://experienceleague.adobe.com/ja/docs/experience-manager-dispatcher/using/dispatcher)を更新する必要があります。

カスタムドメインと Dispatcher を設定したら、AEM を設定して、静的ドメインからフロントエンドアセットを提供できます。

### 設定 {#configuration}

[技術的詳細](#technical-details)の節に従って、サイトのフロントエンドパイプライン機能をアクティブ化すると、`/conf/<site-name>/sling:configs` の下に `SiteConfig` ノードと `HtmlPageItemsConfig` ノードが作成されます。

ステータスアセット用のフロントエンドパイプラインと共にサイトに Cloud Manager のカスタムドメイン機能を使用する場合は、これらのノードに追加のプロパティを追加する必要があります。

1. サイトの `SiteConfig` に `customFrontendPrefix` プロパティを設定します。
   1. `/conf/<site-name>/sling:configs/com.adobe.aem.wcm.site.manager.config.SiteConfig` に移動します。
   1. プロパティ `customFrontendPrefix = "https://your-custom-domain.com/static/"` を追加または更新します。
1. これにより、`HtmlPageItemsConfig` の `prefixPath` 値がカスタムドメインで更新されます。
   1. `/conf/<site-name>/sling:configs/com.adobe.cq.wcm.core.components.config.HtmlPageItemsConfig` に移動します。
   1. `prefixPath` がカスタムドメインを反映していることを確認します（例：`prefixPath = "https://your-custom-domain.com/static/<hash>/..."`）。
   * この値は、必要に応じて手動で上書きすることもできます。
1. 設定を確認します。
   1. デプロイメント後、ページがカスタムドメインのテーマアーティファクトを正しく参照していることを確認します。
   1. ブラウザーの開発者ツールを開き、`theme.css` および `theme.js` ファイルパスを調べて、正しいドメインから読み込まれていることを確認します。

その後、サイトのページは、更新された URL からテーマアーティファクトを参照します。次に、Dispatcher はこれらのリソースに対するリクエストを静的ドメインにルーティングします。

## フロントエンド開発者向けのベストプラクティス {#best-practices}

フロントエンドパイプライン経由でデプロイする前に、フロントエンドアセットをローカルで開発およびテストする必要がある場合は、次のアプローチを考慮します。

* テーマアーティファクトをテスト用にローカルで上書きするには、[Site Theme Builder のプロキシモード ](https://github.com/adobe/aem-site-theme-builder?tab=readme-ov-file#proxy) を使用します。
* ローカル開発サーバーからテーマファイルを手動で提供し、`HtmlPageItemsConfig` の `prefixPath` を更新して、ローカルサーバーアドレスと一致させます。
* テスト中にブラウザーのキャッシュが無効になっていることを確認して、ライブ更新を確認します。

ローカルフロントエンド開発について詳しくは、[Site Theme Builder ドキュメント](https://github.com/adobe/aem-site-theme-builder)を参照してください。
