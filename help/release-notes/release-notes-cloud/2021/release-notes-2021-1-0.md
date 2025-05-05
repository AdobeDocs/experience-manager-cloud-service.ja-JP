---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.1.0 リリースのリリースノート。'
description: "[!DNL Adobe Experience Manager] as a Cloud Service 2021.1.0 のリリースノート。"
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 92%

---


# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

[!DNL Experience Manager] as a Cloud Service の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2021.1.0 のリリース日は 2021 年 2 月 3 日です。
次回のリリース（2021.2.0）は、2021 年 2 月 25 日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[コンテンツフラグメント HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**：HTTP API を使用して、コンテンツフラグメントのバリエーションを追加、更新、削除する機能を追加します。

* **[コンテンツフラグメント配信用の GraphQL API](/help/headless/graphql-api/content-fragments.md)**：GraphQL 構文を使用してコンテンツフラグメントのクエリを実行する機能と、JSON 形式で出力するための、コンテンツフラグメントモデルに基づくスキーマが用意されました。

* **[GraphQL API リクエストの認証サポート](/help/headless/security/authentication.md)**：サーバー側 API のアクセストークンで GraphQL API リクエストを認証できるようになりました。

* リッチテキストを JSON 形式で出力する機能やロケールなど、GraphQL API からの JSON 出力が強化されました。

* コンテンツフラグメントモデルのネストのサポートにより、専用のコンテンツフラグメント参照データ型またはコンテンツフラグメント参照を使用して、ネストしたコンテンツフラグメント構造を複数行テキストフィールド内にインラインで作成できるようになりました。

* 「一意」、「必須」、「変換可能」など、コンテンツフラグメントモデルのデータ型で使用できる検証ルールが追加されました。

* コンテンツフラグメントモデルにタグ付けでき、タグ別またはパス別のポリシーを使用してフォルダー内でコンテンツフラグメントを作成できるようになりました。

* 公開アクションや、フラグメントのベースとなっているモデルの表示など、コンテンツフラグメントエディターの使いやすさが向上しました。

* コンテンツフラグメントエディターで JSON 出力を直接プレビューできるようになりました。


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] as a [!DNL Cloud Service] のスマートタグ機能が拡張されて、テキストベースのアセット内のキーワードやエンティティの識別をサポートするようになりました。テキストが識別され、インデックス作成され、メタデータとして使用できるようになるので、設定を行わなくても検索エクスペリエンスが向上します。詳しくは、[スマートタグ](/help/assets/smart-tags.md)を参照してください。

* MXF ファイル形式がサポートされるようになりました。詳しくは、[サポートされているファイル形式](/help/assets/file-format-support.md#video-formats)を参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品エクスペリエンス管理：アセットおよびエクスペリエンスフラグメント用の新しい「コマース」プロパティタブが追加されました。このタブでは、製品やカテゴリをアセットやエクスペリエンスフラグメントにリンクできます。また、このタブには、リンクされた製品やカテゴリのリアルタイムデータと、製品コンソールに詳細を表示するリンクが表示されます。

* 最新のCIF コアコンポーネント v1.7.0 を含んだCIF Venia 参照サイト 2021.02.02 をリリースしました。詳しくは、[CIF Venia 参照サイト ](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) を参照してください。

* CIF コアコンポーネント v1.7.0 をリリースしました。詳しくは、[CIF コアコンポーネント ](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) を参照してください。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2021.1.0 Cloud Manager のリリース日は 2021 年 1 月 14 日です。

### バグの修正 {#bug-fixes-cloud-manager}

* アセット実稼動インスタンスでは、**環境**&#x200B;の詳細ページに Brand Portal のステータスが&#x200B;*保留中*&#x200B;と表示され、ユーザーがアクションを実行できない場合があります。

* Cloud Manager から休止状態の解除をトリガーすると、解除が正常に開始された場合でも、エラーメッセージが表示されることがありました。

* 環境の作成または削除でまれにエラーが発生する問題に対処しました。

## コードリファクタリングツール {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] の新機能  {#what-is-new-crt}

* AIO-CLI プラグインの新しいバージョンがリリースされました。このプラグインの最新バージョンには、AEM Dispatcher コンバーターと Repository Modenizer のバグ修正が含まれ、新しいユーティリティインデックスコンバーターもサポートされています。このプラグインについて詳しくは、[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=ja#benefits) を参照してください。

* インデックスコンバーターは、顧客のカスタム OAK インデックス定義を AEM as a Cloud Service 互換の OAK インデックス定義に変換するために使用できるユーティリティです。詳しくは、[ インデックスコンバーター ](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) を参照してください。

* [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) にすべての OSGi 設定を含む個別のパッケージ `ui.config` を作成する新機能が追加されました。

### バグの修正 {#crt-bug-fixes}

* AEM Dispatcher コンバーターおよび Repository Modenizer ツールでいくつかのバグ修正が行われました。[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) および [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) を参照してください。

## AEM as a Cloud Service の基盤 {#aem-as-a-cloud-service-foundation}

### 新機能 {#what-is-new-foundation}

* 認証済みのサーバー間 API 呼び出し - 適切なアクセストークンを生成して、外部アプリケーションと AEM as a Cloud Service 環境の間で認証済みのサーバー間 API 呼び出しを行います。詳しくは、[こちらのドキュメント](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)や[チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=ja#authentication)を参照してください。

### SDK ビルドアナライザー {#sdk-build-analyzers}

AEM as a Cloud Service の SDK ビルドアナライザー Maven プラグインでは、依存関係の欠落など、Maven プロジェクトの問題を検出します。これを使用すると、ローカル開発中に、Cloud Manager でクラウド環境にデプロイする前に開発者が問題を見つけることができます。

このリリースでは、次の 2 つのアナライザーが新しく追加されました。

* repoinit アナライザー
* bundle-nativecode

詳しくは、[こちらのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja#developing)を参照してください。

## クラウド移行ツール {#code-transition-tools}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.2.2 のリリース日は 2021 年 2 月 1 日です。

### [!DNL Content Transfer Tool] の新機能 {#what-is-new-ctt}

* コンテンツ転送ツールに、新しい機能および UI であるユーザーマッピングツールが追加されました。この機能は、コンテンツ移行アクティビティの一環として、既存のユーザーおよびグループをそれぞれの Adobe Identity Management System ID に自動的にマッピングします。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja)を参照してください。
* コンテンツ転送ツールは、移行セットで参照されているすべてのグループとユーザーを子も含めて移行するようになりました。
* 移行セットの作成時に、`/etc` 下の特定のパスを選択できます。
