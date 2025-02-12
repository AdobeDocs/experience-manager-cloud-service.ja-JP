---
title: フロントエンドパイプラインを有効にする
description: サイトテーマを使用してサイトをより迅速にカスタマイズできるように、既存のサイトのフロントエンドパイプラインを有効にする方法について説明します。
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: d37bdc060ea569748745011346bc448a569ae91d
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 60%

---

# フロントエンドパイプラインを有効にする {#enable-front-end-pipeline}

サイトテーマを使用してサイトをより迅速にカスタマイズできるように、既存のサイトのフロントエンドパイプラインを有効にする方法について説明します。

## 概要 {#overview}

フロントエンドパイプラインは、[ サイトテーマ ](site-themes.md) と [ サイトテンプレート ](site-templates.md) に基づいて web サイトのフロントエンドコードだけを迅速にデプロイできるメカニズムです。

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

AEM では、フロントエンドパイプラインを使用するように既存のサイトを自動的に適応させることができます。このワークフローを実行するには、サイトがコアコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/wcm-components/page) のページコンポーネント [v2 以降を使用している必要があります。

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

フロントエンドパイプラインは [Cloud Managerのカスタムドメイン機能と共に使用できますが ](/help/implementing/cloud-manager/custom-domain-names/introduction.md)2 つの機能を一緒に使用する場合は、次の要件に注意してください。

### 静的フロントエンドファイル {#static-files}

フロントエンドパイプラインを介してデプロイされた静的フロントエンドアセットは、デフォルトで、Adobeの事前定義済みの静的ドメインから提供されます。

フロントエンドアセットにカスタムドメインが必要な場合は、パブリッシュ層にカスタムドメインをインストールし、Dispatcherを設定して、Adobeの静的ホスティングの場所に特定のパス（`/static/` など）をルーティングできます。 この方法では、静的アセットのリクエストを適切に転送およびキャッシュするために ](https://experienceleague.adobe.com/ja/docs/experience-manager-dispatcher/using/dispatcher)0}Dispatcher ルール } を更新する必要があります。[

カスタムドメインと Dispatcher を設定したら、静的ドメインからフロントエンドアセットを提供するようにAEMを設定できます。

### 設定 {#configuration}

[技術的詳細](#technical-details)の節に従って、サイトのフロントエンドパイプライン機能をアクティブ化すると、`/conf/<site-name>/sling:configs` の下に `SiteConfig` ノードと `HtmlPageItemsConfig` ノードが作成されます。

ステータスアセットのフロントエンドパイプラインと共に、Cloud Managerのカスタムドメイン機能をサイトに使用する場合は、これらのノードにプロパティを追加する必要があります。

1. サイトの `SiteConfig` に `customFrontendPrefix` プロパティを設定します。
   1. `/conf/<site-name>/sling:configs/com.adobe.aem.wcm.site.manager.config.SiteConfig` に移動します。
   1. プロパティ `customFrontendPrefix = "https://your-custom-domain.com/static/"` を追加または更新します。
1. これにより、`HtmlPageItemsConfig` の `prefixPath` 値がカスタムドメインで更新されます。
   1. `/conf/<site-name>/sling:configs/com.adobe.cq.wcm.core.components.config.HtmlPageItemsConfig` に移動します。
   1. `prefixPath` に `prefixPath = "https://your-custom-domain.com/static/<hash>/..."` などのカスタムドメインが反映されていることを確認します。
   * この値は、必要に応じて手動で上書きすることもできます。
1. 設定を確認します。
   1. デプロイメント後、ページがカスタムドメインからテーマアーティファクトを正しく参照していることを確認します。
   1. ブラウザーの開発者ツールを開き、`theme.css` および `theme.js` ファイルパスを調べて、正しいドメインから読み込まれていることを確認します。

その後、サイトのページは、更新された URL からテーマアーティファクトを参照します。 次に、Dispatcher はこれらのリソースのリクエストを静的ドメインにルーティングします。

## フロントエンド開発者向けのベストプラクティス {#best-practices}

フロントエンドパイプラインを介してデプロイする前に、フロントエンドアセットをローカルに開発およびテストする必要がある場合は、次のアプローチを考慮します。

* テーマアーティファクトをテスト用にローカルで上書きするには、[Site Theme Builder のプロキシモード ](https://github.com/adobe/aem-site-theme-builder?tab=readme-ov-file#proxy) を使用します。
* テーマファイルをローカル開発サーバーから手動で提供し、ローカルサーバーアドレスと一致するよ `HtmlPageItemsConfig` に `prefixPath` を更新します。
* ライブ更新を確認するには、テスト中にブラウザーのキャッシュが無効になっていることを確認します。

ローカルフロントエンド開発について詳しくは、[Site Theme Builder ドキュメント ](https://github.com/adobe/aem-site-theme-builder) を参照してください。
