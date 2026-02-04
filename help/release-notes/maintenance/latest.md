---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f01a98604e045c48ab7167122aee3b2468db6d52
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 24%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 24288 {#24288}

2026年2月4日に公開された、メンテナンスリリース 24288 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 23963 でした。

2026.2.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

>[!NOTE]
>
>リリース 24222 が非公開になりました。

### 機能強化 {#enhancements-24288}

* CNTBF-604：新しい contentbackflow バンドルリリースを作成します。
* CQ-4361592：プロジェクトの作成と更新で TypeHint のサポートを追加。
* CQ-4362198:AEMと Granite の最新のパッケージ翻訳。
* GRANITE-36205：内部Oak リリースバージョンを最新に更新します。
* GRANITE-59211:OPTEL:nonce サポートとセルフサービス設定を追加。
* GRANITE-62166：移行バンドルを更新して、移行ツールから移行状態を再利用します。
* GRANITE-62598：コンテンツパッケージフィルターから除外する冗長プロパティを削除しました。
* GRANITE-62684:skyline-ops を通じて、クライアントソケットタイムアウトを設定可能にします。
* GRANITE-62702:Sling Discovery を、オンライン移行用のスタンドアロン実装に置き換えます。
* GRANITE-62763:ASSETS ロータリーに基づいて、Guava 非推奨（廃止予定）の例外リストを更新しました。
* GRANITE-62771：新しい非推奨（廃止予定）の Commons-Lang 依存関係が導入されると、クイックスタートビルドに失敗します。
* GRANITE-62987:Felix web コンソールをバージョン 5.0.18 に更新します。
* GRANITE-63339:Azure migration-state BLOB のリースメカニズムを改善しました。
* GRANITE-63343:workflow.core に、最新バージョンの Sling API バンドルのサポートを追加。
* GRANITE-63799:OIDC 認証バンドルバージョンを向上しました。
* GRANITE-63821:JCRVLT-831/JCRVLT-839 を修正する filevault リリースへのクイックスタートの更新。
* GRANITE-63827：クイックスタートをOakの最新の公開リリース（1.90.0）に更新します。
* GRANITE-63888：クイックスタートを Jackrabbit 2.22.3 に更新します。
* GRANITE-64030：式言語バリデーターの許可リストにキーワードとパターンを追加します。
* GRANITE-64050：外部製品機能を非表示にするために、非表示の設定フォルダーを許可します。
* SITES-30452:ASO を使用したコンテンツ API - タイトルと説明の提案。
* SITES-38099：より新しいバージョンの健全性チェックを使用するように `testing-model.txt` を更新します。
* SKYOPS-43616:Dispatcher リポジトリで Jenkins 資格情報を Vault に移行します。
* SKYOPS-108584: 0.6.0 から 0.6.10 へのバンプ ファクト ツール
* SKYOPS-115691:CORS フィルターバンドルをアップグレードして、プリフライトリクエストに Vary Origin ヘッダーを追加します。
* SKYOPS-123094：クイックスタートで Apache HTTP コンポーネントを更新します。
* SKYOPS-123236: レプリケーションパッケージに `rep:cugPolicy` を含めます。
* SKYOPS-123240：クイックスタートの CRXDE 依存関係を更新します。
* SKYOPS-123247：クイックスタートの Sling XSS バンドルを更新します。
* SKYOPS-123250：クイックスタートの Sling セキュリティバンドルを更新します。
* SKYOPS-123327:AEM-CS SDKには Java 21 が必要です。
* SKYOPS-125574:Quickstart で netcentric AC Tool バンドルを更新します。
* SKYOPS-126150: スレッドダンプ生成スクリプトの top コマンドを改善しました。

### 修正された問題 {#fixed-issues-24288}

* FORMS-23687：デフォルト値なしで contains ルールが使用された場合の SSV 検証エラーを修正。
* GRANITE-48472:「ユーザー設定を編集」タブでパスワードを変更する際に、「エラーをローカライズ」が発生する。
* GRANITE-50286:User Management モーダルのステータス列にあるレイアウトの問題を修正。
* GRANITE-52301: Localize セキュリティグループのセッション文字列に対する変更をコミットできません。
* GRANITE-52920: セキュリティでユーザーを作成する際に、ローカル化エラーが発生する新しいユーザーを作成する。
* GRANITE-54654：セキュリティAdobe IMS設定チェックダイアログで、文字列をローカライズします。
* GRANITE-56371：セキュリティ Trust Store の間違ったデータ形式を修正。
* GRANITE-62717：非 ASCII 文字を使用した JSafe パスワード処理の暗号化キーストアをアップグレードしました。
* GRANITE-62789：コンテンツ配布での再試行モードをサポートしないように messaging-client を更新します。
* GRANITE-62824：ユーザーエディターで「グループ」タブにアクセスする際の `NullPointerException` ラーを修正。
* GRANITE-63080:`org.slf4j.spi` のインポートを `slf4j 2.x` と互換性のあるものにします。
* GRANITE-63210：パブリッシュの起動時に Dispatcher の無効化を修正するように、配布コアを更新します。
* GRANITE-63293：最初のオーサリング後に、必須のアスタリスクが失われる必須のパスフィールドを修正。
* GRANITE-63360：複数のパスが選択されている場合に表示される誤った情報を修正します。
* SITES-36242:GraphQLで正規表現を実行するように絞り込んで、Dispatcher のフィルターバイパスを修正します。
* SITES-40122：コンテンツ配布 ImsService とのEdge Delivery統合の修正。
* SKYOPS-84379:RDE による適切な機能切り替えピックアップには、最新の FACT ツールを使用してください。
* SKYOPS-121216：更新を Jackson 2.20.0 ライブラリに戻す。

#### AEM ガイド {#guides-24288}

* GUIDES-38198：コンテキストメニューの「MathMLを編集」オプションを使用してインライン MathMLの式を更新する場合、更新された値は、ページが更新されるまで反映されません。
* GUIDES-38276:Assets UI のバージョン履歴パネルからバージョンラベルを削除できない。
* GUIDES-36641:AEM Sites出力を生成する際に、キーワードを含むマップタイトルと `<ph>` の要素を含むトピックタイトルが、公開された出力に含まれません。
* GUIDES-37837：トピックまたはマップを保存しようとすると、「ファイルの保存に失敗しました」エラーが発生して、特にアセット処理に負荷の高いタスクやバックグラウンドで実行されている翻訳ワークフローで操作が失敗することがあります。
* GUIDES-27774：壊れたリストレポートに、現在のマップの範囲内で正しく解決された外部リンク、有効な `keyrefs`、キーワードが誤って含まれています。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-24288}

なし。

### 廃止された機能と API {#deprecated-24288}

* AEMSRE-2896：カスタマイズされた logmanager 設定処理を修正しました。
* GRANITE-62802：非推奨（廃止予定）の `commons-lang` 依存関係を `granite.auth.saml` から削除します。
* GRANITE-62805：非推奨（廃止予定）の `commons-lang` 依存関係を `granite.httpcache.core` から削除します。
* GRANITE-62864：非推奨（廃止予定）の `commons-lang` 依存関係を `granite.jobs.async` から削除します。
* GRANITE-62865：非推奨（廃止予定）の `commons-lang` 依存関係を `granite.replication.core` から削除します。
* GRANITE-62868：非推奨（廃止予定）の `commons-lang` 依存関係を `granite.rest.api` から削除します。
* GRANITE-62895：非推奨（廃止予定）の `commons-lang` 依存関係を `translation.connector.msft.core` から削除します。
* GRANITE-63069:`com.adobe.granite.httpcache.core` を非推奨（廃止予定）にする。
* GRANITE-63179：非推奨（廃止予定）の `commons-lang` 依存関係を `cq-workflow-impl` から削除します。
* GRANITE-63180：非推奨（廃止予定）の `commons.lang` エクスポートをバンドルから削除 `cq-mailer` ます。
* SKYOPS-123329:AEM Ethos デプロイメントの Java 11 サポートを終了し、`commons-lang3` を更新します。
* SKYOPS-124983:AEM起動スクリプトから非推奨の `nashorn.args` を削除します。

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-24288}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 10 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-24288}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.30.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
