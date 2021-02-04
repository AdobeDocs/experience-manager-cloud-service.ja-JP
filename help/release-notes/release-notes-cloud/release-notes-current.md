---
title: Cloud Serviceとしての [!DNL Adobe Experience Manager] の最新のリリースノートです。
description: Cloud Serviceとしての [!DNL Adobe Experience Manager] の最新のリリースノートです。
translation-type: tm+mt
source-git-commit: 135fe0d4172af12f091268e9ffc45295e6645fd7
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 8%

---


# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

次の節では、[!DNL Experience Manager]の一般的なリリースノートをCloud Serviceとしてまとめています。

## リリース日 {#release-date}

Cloud Service2021.1.0の[!DNL Adobe Experience Manager]のリリース日は2021年2月3日です。
次のリリース(2021.2.0)は、2021年2月25日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### ヘッドレスコンテンツ管理 {#headless}

* **[GraphQL API for Content Fragment配信](/help/assets/content-fragments/graphql-api-content-fragments.md)**:GraphQL構文を使用したコンテンツフラグメントのクエリ、およびコンテンツフラグメントモデルに基づくスキーマ（JSON形式で出力）

* **[GraphQL APIリクエストの認証サポート](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:GraphQL APIリクエストをサーバ側APIのアクセストークンで認証できる機能。

* **[RemotePageコンポーネント](/help/implementing/developing/hybrid/remote-page.md)**:を使用して、AEM内の外部SPAを表示および編集するためのサポートを追加しました。

* **[AEM内での外部SPAの編集](/help/implementing/developing/hybrid/editing-external-spa.md)**:スタンドアロンのシングルページアプリをAEMインスタンスにアップロードする機能、編集可能なコンテンツセクションの追加、オーサリングを有効にする機能が追加されました。

* JSON形式やロケールでリッチテキストを出力する機能など、GraphQL APIからのJSON出力の強化。

* コンテンツフラグメントモデルのネストをサポートし、ネストされたコンテンツフラグメント構造を作成できます。このためには、専用のコンテンツフラグメント参照データ型またはコンテンツフラグメント参照を複数行テキストフィールド内にインラインで作成します。

* 「一意」、「必須」、「変換可能」など、コンテンツフラグメントモデルのデータ型で使用できる追加の検証ルールです。

* コンテンツフラグメントモデルにタグ付けし、タグまたはパスによるポリシーを持つフォルダー内でコンテンツフラグメントを作成できます。

* コンテンツフラグメントエディターでの使い勝手の向上（公開アクションや、フラグメントが基づくモデルの表示など）。

* コンテンツフラグメントエディターでJSON出力を直接プレビューできる機能。

### プログレッシブWebアプリ(PWA) {#pwa}

* [プログレッシブWeb App(PWA)版の](/help/sites-cloud/authoring/features/enable-pwa.md)  サイトは、簡単な設定でプロジェクトレベルで有効にできるようになりました。

## [!DNL Adobe Experience Manager Assets] として  [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] は、スマートタグ機能を [!DNL Cloud Service] 拡張して、テキストベースのアセット内のキーワードとエンティティの識別をサポートしています。テキストを識別し、インデックスを作成し、メタデータとして使用できるようにして、設定を行うことなく検索体験を向上させます。 「[スマートタグ](/help/assets/smart-tags.md)」を参照してください。

* MXFファイル形式がサポートされるようになりました。 [サポートされているファイル形式](/help/assets/file-format-support.md#video-formats)を参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品エクスペリエンス管理：アセットおよびエクスペリエンスフラグメント用の新しい「コマース」プロパティタブ。 このタブでは、製品やカテゴリをアセットやエクスペリエンスフラグメントにリンクできます。 また、このタブには、リンクされた製品/カテゴリのリアルタイムデータと、製品コンソールに詳細を表示するリンクが表示されます。

* 最新のCIFコアコンポーネントバージョンv1.7.0が含まれるCIFベニアリファレンスサイト — 2021.02.02をリリースしました。詳細は、[CIFベニアリファレンスサイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02)を参照してください。

* CIF コアコンポーネント v1.7.0 をリリースしました。詳しくは、「[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0)」を参照してください。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEMのCloud ManagerのCloud Service2021.1.0のリリース日は2021年1月14日です。

### バグ修正 {#bug-fixes-cloud-manager}

* アセット実稼動インスタンスでは、場合によっては、環境&#x200B;**ユーザー**&#x200B;の詳細ページにブランドポータルのステータスが&#x200B;*保留*&#x200B;として表示されます。ユーザーは何も操作を行えません。

* Cloud Managerから非休止状態をトリガーすると、非休止状態が正常に開始された場合でも、エラーメッセージが表示されることがありました。

* 環境の作成または削除でエラーが発生した場合は、まれに対処しました。

## AEM FoundationとしてのCloud Service{#aem-as-a-cloud-service-foundation}

### 新機能 {#what-is-new-foundation}

* サーバー間認証API呼び出し — 適切なアクセストークンを生成して、認証済みのサーバー間API呼び出しを外部アプリケーションとAEMの間でCloud Service環境として行います。 詳しくは、[ドキュメント](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)を読むか、[チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)を参照してください。

### SDKビルドアナライザー{#sdk-build-analyzers}

Cloud ServiceSDKビルドアナライザーMavenプラグインとしてのAEMは、Mavenプロジェクト内の問題（依存関係の欠落など）を検出します。 開発者は、ローカル開発中に問題を発見し、Cloud Managerを使用してCloud環境に展開する前に、問題を発見できます。

このリリースでは、2つの新しいアナライザーが追加されました。

* リポイント分析器
* bundle-nativecode

詳しくは、[ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)を参照してください。

## クラウド移行ツール {#code-transition-tools}

### リリース日 {#release-date-ctt}

コンテンツ転送ツールv1.2.2のリリース日は2021年2月1日です。

### [!DNL Content Transfer Tool] の新機能 {#what-is-new-ctt}

* コンテンツ転送ツール — ユーザーマッピングツールに追加された新しい機能とUI。 この機能は、コンテンツ移行アクティビティの一環として、既存のユーザーとグループをAdobeのIdentity ManagementシステムIDに自動的にマッピングします。 詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)を参照してください。
* コンテンツ転送ツールは、移行セット内で参照されているすべてのグループとユーザーを子も含めて移行するようになりました。
* 移行セットの作成時に、`/etc`の下の特定のパスを選択できます。
