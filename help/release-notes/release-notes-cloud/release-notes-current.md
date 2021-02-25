---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート'
translation-type: tm+mt
source-git-commit: ad80ea25abf06fd18dd781641f215e134a18a037
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 11%

---


# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

[!DNL Experience Manager] as a Cloud Service の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

Cloud Service2021.2.0の[!DNL Adobe Experience Manager]のリリース日は2021年2月25日です。
次のリリース(2021.3.0)は、2021年3月25日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### ヘッドレスコンテンツ管理 {#headless}

* **[GraphQL API for Content Fragment配信](/help/assets/content-fragments/graphql-api-content-fragments.md)**:GraphQL構文を使用したコンテンツフラグメントのクエリ、およびコンテンツフラグメントモデルに基づくスキーマ（JSON形式で出力）

* **[GraphQL APIリクエストの認証サポート](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:GraphQL APIリクエストをアクセストークンで認証し、サーバ側APIを使用できる。

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

## [!DNL Assets] の新機能 {#what-is-new-assets}

* アセットは[!DNL Experience Manager Assets Brand Portal]を使用してソースにできます。 新しいマーケティングキャンペーン、フォトシュート、プロジェクトに関して、エージェンシーユーザーからアセットをソース化するのに役立ちます。

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

## [!DNL Assets] {#bug-fixes-assets}のバグ修正

* 名前の競合を解決した後に既存のアセットの新しいバージョンを作成すると、元のアセットのメタデータが上書きされます。 （CQ-4313594）
* 注釈テキストが長いアセットを印刷すると、空白がある場合でも、注釈テキストはトリミングされます。 （CQ-4314101）

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2021.2.0 Cloud Manager のリリース日は 2021 年 2 月 11 日です。

### 新機能 {#what-is-new-cloud-manager}


* アセットのお客様は、Cloud Manager UIを使用してセルフサービスの方法でBrand Portalインスタンスをいつ、どこにデプロイするかを選択できるようになります。 アセットソリューションを使用する通常の（Sandbox以外の）プログラムの場合、Brand Portalを実稼働環境でプロビジョニングできるようになりました。 プロビジョニングは、実稼働環境で1回だけ実行できます。

* プロジェクトとサンドボックスの作成で使用されるAEMプロジェクトアーキタイプがバージョン25に更新されました。

* コードスキャン中に特定された非推奨のAPIのリストが絞り込まれ、最新Cloud ServiceのSDKリリースで非推奨となった追加のクラスとメソッドが含まれるようになりました。

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

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt}

コンテンツ転送ツールv1.2.4のリリース日は2021年2月10日です。

### バグ修正 {#bug-fixes-ctt}

* 複数のユーザーをマッピングする際に、一部のユーザーのIMS IDが正しくマッピングされない問題を修正しました。 この問題が修正されました。

### リリース日 {#release-date-ctt-feb}

コンテンツ転送ツールv1.2.2のリリース日は2021年2月1日です。

### コンテンツ転送ツールの新機能{#what-is-new-ctt}

* コンテンツ転送ツール — ユーザーマッピングツールに追加された新しい機能とUI。 この機能は、コンテンツ移行アクティビティの一環として、既存のユーザーとグループをAdobeのIdentity ManagementシステムIDに自動的にマッピングします。
詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)を参照してください。
* コンテンツ転送ツールは、移行セット内で参照されているすべてのグループとユーザーを子も含めて移行するようになりました。
* 移行セットの作成時に、`/etc`の下の特定のパスを選択できます。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

Best Practices Analyzer v2.1.2のリリース日は2021年2月19日です。

### ベストプラクティスアナライザの新機能{#what-is-new-bpa}

* AEM FormsとAEM Formsの導入の使用を検出し、AEM Formsへの移行に関連する領域をCloud Serviceとして示す機能。
* カスタムコンポーネントとテンプレートの使用状況と数を検出し、レポートする機能。
* 使用するノードストアとデータストアの種類を検出する機能。
* Dynamic Mediaの使い方を検出する能力。
* 使用するJavaバージョンの検出機能。

## コードリファクタリングツール {#code-refactoring-tools}

### コードリファクタリングツールの新機能{#what-is-new-crt}

* AIO-CLIプラグインの新しいバージョンがリリースされました。 このプラグインの最新バージョンには、リポジトリの最新化機能に関するいくつかのバグ修正が含まれています。
このプラグインの詳細については、[統合エクスペリエンス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)を参照してください。

### バグ修正 {#bug-fixes-crt}

* リポジトリの最新化で行われたいくつかのバグ修正。
[GitHubリソースを参照：aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)を参照してください。








