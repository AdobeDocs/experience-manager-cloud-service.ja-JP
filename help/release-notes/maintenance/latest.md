---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6fa6fc9015624bec9113a198285531a3bdd7e29c
workflow-type: ht
source-wordcount: '773'
ht-degree: 100%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 18175 {#release-18175}

2024年10月10日（PT）に公開された、メンテナンスリリース 18175 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 17964 でした。リリース 18099 は、問題が発生したことにより非公開になりました。

2024.10.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-18175}

* ASSETS-38322：AEM の HTTP リクエストイベントを有効化。
* ASSETS-41448：auth.ims バンドルを更新して、FI からグループへのマッピングをサポート。
* ASSETS-41684：OOB OSGI 設定を追加して、Assets、Foundation、Sites および Forms 用のグループマッピングへの FI を定義。
* ASSETS-43015：最新の auth.ims バンドルに更新。
* CQ-4356633：「コンテンツのみ」のツールチップに文字を追加。
* GRANITE-50948：リポジトリサービスを AEM に統合してリポジトリサービスをサポート。
* GRANITE-52454：サポートヘルパー 0.1.2 を追加。
* GRANITE-52454：サポートヘルパーのアップグレード、GRANITE-52454：AEMaaCS の最新リリースを使用するようにサポートヘルパーをアップグレード。
* GRANITE-53287：セキュリティ権限の統合テストバージョンを更新。
* GRANITE-53485：レプリケーション Azure Blob Storage のサービスプリンシパル認証をサポート。
* GRANITE-53514：Treeactivation をバージョン 1.0.26 にアップデート。
* GRANITE-53870：クイックスタートの最大 JVM バージョンチェックをスキップする内部メカニズムを作成。
* GRANITE-53914：アップデートされた Java 17 モジュールバージョンでのプラットフォームテストの失敗を修正。
* GRANITE-53966：コンテンツ配布に別のスレッドプールを使用。
* GRANITE-54006：Jackson を 2.17.2 にアップデート。
* GRANITE-54038：Creative Cloud エンタープライズ IMS クライアントを AEM IMS クライアント許可リストに追加。
* GRANITE-54054：com.adobe.granite.repository.impl.SystemUserValidation warnOnly の環境変数。
* GRANITE-54266：実稼動 SDK に検索サジェストサービスがない。
* GRANITE-54274：Firefly IMS クライアントを受け入れる。
* GRANITE-54300：Oak を最新のパブリックリリース（1.70.0）にアップデート。
* GUIDES-19069：aem guides アドオンの guidesPeerLinkIndex を追加。
* SITES-23584：Java 17 で基盤コンポーネントのテストが失敗する問題を修正。
* SKYOPS-69768：SlingModels で ResourceResolvers が逆シリアル化されない。
* SKYOPS-76378：i18n での ResourceBundle 登録／登録解除のスレッドの安全性を向上。
* SKYOPS-79285：Sling XSS を 2.4.2 にアップデート。
* SKYOPS-82383：コマンド実行記述子で「helm-values」convert-merge-analyse 結果を公開。
* SKYOPS-84810：RDE の起動時に「40-initialize-publish.sh」の実行をスキップする。
* SKYOPS-84951：可変コンテンツチェックサム生成コードを修正。
* SKYOPS-85335：org.apache.sling.jcr.repoinit を 1.1.52 にアップデート。
* SKYOPS-85336：Sling Commons Threads を 3.3.0 にアップデート。
* SKYOPS-86329：java 21 sdk サポート用のプラットフォームテストモジュールのバージョンをアップデート。

### 修正された問題 {#fixed-issues-18175}

* CNTBF-298：CC で書き出されたパッケージから jcr:uuid を削除。
* SKYOPS-83910：SKYOPS-82371 で見つかった同時実行の問題を修正。
* GRANITE-52876：com.adobe.granite.ui.content 0.8.1448 にアップデート。
* GUIDES-14445：ネイティブ PDF の生成が失敗し、Node.js の依存関係の取得に関連するエラーが発生する。
* GUIDES-16961：`<conref>` のタイトルが、web エディターのベースラインダッシュボードと翻訳ダッシュボードで解決されない。
* GUIDES-17283：「**topicmeta に追加されたメタデータを使用**」オプションを選択すると、メタデータプロパティがネイティブ PDF 出力のドキュメントのプロパティに反映されない。
* GUIDES-17793：公開済みコンテンツの一括アクティベーション中に、参照された PDF が&#x200B;**一括公開ダッシュボード**&#x200B;からアクティベートされない。

新しいガイド機能と強化されたガイド機能、および修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)をご覧ください。

### 既知の問題 {#known-issues-18175}

* FORMS-15818：コンポーネント記述子エントリ `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` が見つからないというステートメントがサーバーログに記録される。これらは無害なログステートメントです。

### 廃止された機能と API {#deprecated-18175}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

次に、最近廃止された機能や、廃止予定の機能の概要を示します。

#### JavaScript Use API {#javascript-use-api}

[JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) は、API を活用したコードのデバッグと保守に関する課題があったこと、Java の代替手段と比較してパフォーマンスの制限があったため、正式に廃止されました。

[Java Use API](https://experienceleague.adobe.com/ja/docs/experience-manager-htl/content/java-use-api) に移行する必要があります。これにより、パフォーマンスが向上し、デバッグが容易になり、長期サポートが強化されます。

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

アドビは現在 `com.day.cq.wcm.api` を更新中です。メソッドやクラスの一部は、現在のリリースでは `@Deprecated` としてマークされています。これらは今後のリリースで削除される予定です。推奨の代替案に切り替えることを検討してください。

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165：パブリック API の org.apache.jackrabbit.oak.plugins.blob を非推奨（廃止予定）。

### セキュリティ修正 {#security-18175}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。このメンテナンスリリースでは、特定された 2 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-18175}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
