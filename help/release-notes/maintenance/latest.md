---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: ea7e027b5247b64e78da1d14e4e602f39a37e4bd
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 27%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 18099 {#release-18099}

2024年10月9日（PT）に公開された、メンテナンスリリース 18099 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 17964 でした。

2024.10.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-18099}

* ASSETS-43015：最新の auth.ims バンドルに更新します。
* ASSETS-41684:src/main/features/docker/ethos/base-ims-oauth.jsonを更新します。
* ASSETS-38322:AEMの http リクエストイベントを有効化。
* ASSETS-41684: OOB OSGI 設定を追加して、Assets、Foundation、Sites およびForms用のグループマッピングに対して FI を定義します。
* ASSETS-41448：グループマッピングに対する FI をサポートするように、auth.ims バンドルを更新します。
* CQ-4356633:「コンテンツのみ」のツールチップに文字を追加。
* SITES-23584：基盤コンポーネントテストが Java 17 で失敗する。
* GUIDES-19069:aem guides アドオンの guidesPeerLinkIndex を追加。
* GRANITE-54300：Oak を最新のパブリックリリース（1.70.0）に更新します。
* GRANITE-54274:Firefly IMS クライアントを受け入れます。
* GRANITE-36205：内部の Oak リリースバージョンを最新に更新します。
* GRANITE-45298：低い権限を持つユーザーは、JS を使用せずに XSS 形式で悪意のあるフォームを作成することで、RCE を取得できます。
* GRANITE-54266：実稼動 SDK に検索 Suggestor サービスがない。
* GRANITE-50948 - リポジトリサービスをAEMに統合ローカル開発用に別のリポジトリサービスを追加します。
* GRANITE-53966：コンテンツ配布に別のスレッドプールを使用する。
* GRANITE-53514:Treeactivation 1.0.26。
* GRANITE-54054:com.adobe.granite.repository.impl.SystemUserValidation warnOnly の環境変数。
* GRANITE-50948：リポジトリサービスをAEMに統合リポジトリサービスをサポート。
* GRANITE-52454：サポートヘルパー 0.1.2 の追加
* GRANITE-53514:Treeactivation 1.0.26。
* GRANITE-54038:Creative Cloudのエンタープライズ IMS クライアントをAEM 許可リストに加える IMS クライアントに追加します。
* GRANITE-36205：内部の Oak リリースバージョンを最新に更新します。
* GRANITE-53485: レプリケーション Azure Blob Storage のサービスプリンシパル認証をサポートします。
* GRANITE-54006:Jackson を 2.17.2 に更新します。
* GRANITE-53287: セキュリティ権限の統合テストバージョンを更新しています。
* GRANITE-53914:Java 17 でモジュールバージョンを更新した場合、プラットフォームテストが失敗します。
* GRANITE-53870：クイックスタートの最大 JVM バージョン数のチェックをスキップする内部メカニズムを作成します。
* GRANITE-52454：サポートヘルパーのアップグレード AEMaaCS の最新リリースを使用するためのサポートヘルパーのアップグレード GRANITE-52454。
* SKYOPS-85335:org.apache.sling.jcr.repoinit を 1.1.52 に更新します。
* SKYOPS-85336:Sling Commons Threadsを 3.3.0 に更新します。
* SKYOPS-76378:i18n での ResourceBundle 登録/登録解除のスレッドの安全性を向上しました。
* SKYOPS-84951：可変コンテンツチェックサム生成コードが正しくありません。
* SKYOPS-82383: &#39;helm-values&#39; convert-merge-analyze の結果をコマンド実行記述子に公開します。
* SKYOPS-86329:java 21 sdk サポートのプラットフォームテストモジュールのバージョンを更新しています。
* SKYOPS-69768: SlingModels は ResourceResolvers を逆シリアル化しません。
* SKYOPS-84810: RDE の起動時に&quot;40-initialize-publish.sh&quot;の実行をスキップします。
* SKYOPS-79285:Sling XSS を 2.4.2 に更新する

### 修正された問題 {#fixed-issues-18099}

* CNTBF-298: CC で書き出されたパッケージから jcr:uuid を削除します。
* SKYOPS-83910:SKYOPS-82371 で見つかった同時実行の問題を修正しました。
* GRANITE-52876:com.adobe.granite.ui.content 0.8.1448 を更新します。
* GRANITE-53088:SITES-11992 の修正によって発生したリグレッション。
* GUIDES-14445：ネイティブPDFの生成が失敗し、Node.js の依存関係の取得に関連するエラーが発生します。
* GUIDES-16961:`<conref>` のタイトルが、web エディターのベースラインダッシュボードと翻訳ダッシュボードで解決されない。
* GUIDES-17283:「**topicmeta に追加されたメタデータを使用**」オプションを選択すると、メタデータプロパティがネイティブPDF出力のドキュメントのプロパティに反映されません。
* GUIDES-17793：公開済みコンテンツの一括アクティベーション中に、参照されたPDFが **一括Publish ダッシュボード** からアクティベートされない。

リリースで修正された新機能および機能強化ガイドの機能と問題について詳しくは、[Experience Manager Guides リリースロードマップ ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap) を参照してください。

### 既知の問題 {#known-issues-18099}

* FORMS - 15818：コンポーネント記述子エントリ `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` が見つからないというステートメントがサーバーログに記録される。これらは無害なログステートメントです。

### 廃止された機能と API {#deprecated-18099}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

次に、最近非推奨（廃止予定）になった機能や、廃止予定の機能の概要を示します。

#### JavaScriptの使用 API {#javascript-use-api}

[JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) は、API を活用したコードのデバッグと保守に関する課題があったこと、Java の代替手段と比較してパフォーマンスの制限があったため、正式に廃止されました。

パフォーマンスの向上、デバッグの容易さ、長期サポートの強化を実現する [Java Use API](https://experienceleague.adobe.com/en/docs/experience-manager-htl/content/java-use-api) に移行する必要があります。

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

Adobeでは現在、`com.day.cq.wcm.api` のアップデートを行っています。 メソッドやクラスの一部は、現在のリリースでは `@Deprecated` としてマークされています。 これらは今後のリリースで削除される予定です。 推奨の代替案に切り替えることを検討してください。

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165：パブリック API の org.apache.jackrabbit.oak.plugins.blob を非推奨（廃止予定）にします。

### セキュリティ修正 {#security-18099}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 2 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-18099}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
