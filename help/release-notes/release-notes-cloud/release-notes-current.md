---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート'
translation-type: tm+mt
source-git-commit: 6c40641333f2297d7004d792e87f16a7cf081970
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 17%

---


# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

[!DNL Experience Manager] as a Cloud Service の一般的なリリースノートの概要を次に説明します。

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

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] は、スマートタグ機能を [!DNL Cloud Service] 拡張して、テキストベースのアセット内のキーワードとエンティティの識別をサポートしています。テキストを識別し、インデックスを作成し、メタデータとして使用できるようにして、設定を行うことなく検索体験を向上させます。 「[スマートタグ](/help/assets/smart-tags.md)」を参照してください。

* MXFファイル形式がサポートされるようになりました。 [サポートされているファイル形式](/help/assets/file-format-support.md#video-formats)を参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品エクスペリエンス管理：アセットおよびエクスペリエンスフラグメント用の新しい「コマース」プロパティタブ。 このタブでは、製品やカテゴリをアセットやエクスペリエンスフラグメントにリンクできます。 また、このタブには、リンクされた製品/カテゴリのリアルタイムデータと、製品コンソールに詳細を表示するリンクが表示されます。

* 最新のCIFコアコンポーネントバージョンv1.7.0が含まれるCIFベニアリファレンスサイト — 2021.02.02をリリースしました。詳細は、[CIFベニアリファレンスサイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02)を参照してください。

* CIF コアコンポーネント v1.7.0 をリリースしました。詳しくは、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0)を参照してください。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2021.2.0 Cloud Manager のリリース日は 2021 年 2 月 11 日です。

### 新機能 {#what-is-new-cloud-manager}

* Cloud Manager実稼働パイプラインに、カスタムUIテスト機能が含まれるようになりました。

* アセットのお客様は、Cloud Manager UIを使用してセルフサービスの方法でBrand Portalインスタンスをいつ、どこにデプロイするかを選択できるようになります。 アセットソリューションを使用する通常の（Sandbox以外の）プログラムの場合、Brand Portalを実稼働環境でプロビジョニングできるようになりました。 プロビジョニングは、実稼働環境で1回だけ実行できます。

* プロジェクトとサンドボックスの作成で使用されるAEMプロジェクトアーキタイプがバージョン25に更新されました。

* コードスキャン中に識別された非推奨のAPIのリストが絞り込まれ、最新Cloud ServiceのSDKリリースで非推奨となった追加のクラスとメソッドが含まれるようになりました。

* SonarQubeプロファイル（Cloud Manager用）が更新され、squid:S2142というSonarルールが削除されました。 これは、スレッド割り込みチェックと競合しなくなります。

* Cloud Manager UIは、ドメイン名を一時的に追加/更新できない可能性があるユーザーに通知します。関連付けられた環境には実行中のパイプラインが割り当てられているか、現在、承認手順を待機中です。

* sonarのプリフィックスが付いた顧客`pom.xml`ファイルに設定されたプロパティは、ビルドおよび品質スキャンの失敗を回避するために、動的に削除されるようになりました。

* Cloud Manager UIには、現在展開中のドメイン名でSSL証明書が使用されている場合、SSL証明書を一時的に選択できない可能性があるユーザーに通知されます。

* Cloud Serviceの互換性の問題をカバーするため、コード品質ルールが追加されました。

### バグ修正 {#bug-fixes-cloud-manager}

* ドメイン名に対するSSL証明書の一致で、大文字と小文字が区別されなくなりました。

* 証明書の秘密鍵が2048ビットの制限を満たさない場合に、適切なエラーメッセージが表示されるように、Cloud Manager UIからユーザーに通知されるようになりました。

* Cloud Manager UIには、現在デプロイ中のドメイン名でSSL証明書が使用されている場合、SSL証明書を一時的に選択できない可能性があるユーザーに通知されます。

* 場合によっては、内部の問題が原因で環境の削除が停止することがあります。

* 一部のパイプラインエラーは、誤ってパイプラインエラーとして報告されました。

## AEM FoundationとしてのCloud Service{#aem-as-a-cloud-service-foundation}

### 新機能 {#what-is-new-foundation}

* サーバー間認証API呼び出し — 適切なアクセストークンを生成して、認証済みのサーバー間API呼び出しを外部アプリケーションとAEMの間でCloud Service環境として行います。 詳しくは、[ドキュメント](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)を読むか、[チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)を参照してください。

### SDK ビルドアナライザー {#sdk-build-analyzers}

AEM as a Cloud Service の SDK ビルドアナライザー Maven プラグインでは、依存関係の欠落など、Maven プロジェクトの問題を検出します。これを使用すると、ローカル開発中に、Cloud Manager でクラウド環境にデプロイする前に開発者が問題を見つけることができます。

このリリースでは、2つの新しいアナライザーが追加されました。

* リポイント分析器
* bundle-nativecode

詳しくは、[ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja#developing)を参照してください。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt}

コンテンツ転送ツールv1.2.4のリリース日は2021年2月10日です。

### バグ修正 {#bug-fixes-ctt}

* 複数のユーザーをマッピングする際に、一部のユーザーのIMS IDが正しくマッピングされない問題を修正しました。 この問題が修正されました。

### リリース日 {#release-date-ctt-feb}

コンテンツ転送ツールv1.2.2のリリース日は2021年2月1日です。

### [!DNL Content Transfer Tool] の新機能 {#what-is-new-ctt}

* コンテンツ転送ツール — ユーザーマッピングツールに追加された新しい機能とUI。 この機能は、コンテンツ移行アクティビティの一環として、既存のユーザーとグループをAdobeのIdentity ManagementシステムIDに自動的にマッピングします。 詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)を参照してください。
* コンテンツ転送ツールは、移行セット内で参照されているすべてのグループとユーザーを子も含めて移行するようになりました。
* 移行セットの作成時に、`/etc`の下の特定のパスを選択できます。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

Best Practices Analyzer v2.1.0のリリース日は2021年2月11日です。

### [!DNL Best Practices Analyzer] の新機能 {#what-is-new-bpa}

* AEM FormsとAEM Formsの導入の使用を検出し、AEM Formsへの移行に関連する領域をCloud Serviceとして示す機能。
* カスタムコンポーネントとテンプレートの使用状況と数を検出し、レポートする機能。
* 使用するノードストアとデータストアの種類を検出する機能。
* Dynamic Mediaの使い方を検出する能力。
* 使用するJavaバージョンの検出機能。







