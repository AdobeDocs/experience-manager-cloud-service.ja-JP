---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 478b77488f46ae2566ffe5276ad26834371612aa
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 30%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 26125 {#release-26125}

2026年5月20日（PT）に公開されたメンテナンスリリース 26125の継続的な改善の概要を以下に示します。 以前のメンテナンスリリースはリリース 25892でした。

2026.5.0機能のアクティベーションは、このメンテナンスリリースの完全な機能セットを提供します。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-26125}

* ASSETS-56957: OpenAPIを使用したDynamic Mediaでのビデオのマルチオーディオトラックとマルチキャプションのアップロードのサポートを追加しました。
* ASSETS-58563: AEM AssetsにAdobe Commerce統合を追加しました。
* ASSETS-65603：アセット数を減らす設定を可能にすることで、タッチ UIでのフォルダーリストパフォーマンスを改善しました。
* ASSETS-66032:IP制限のあるクラウドストレージを使用する環境で、Assets Bulk Importに高度なネットワークプロキシのサポートを追加しました。
* CQ-4363346：サンプルガイドラインのダウンロード、JSON、PDF、DOCX形式のガイドラインファイルのアップロード、既存のガイドラインの削除をサポートし、翻訳ガイドライン UIを強化しました。
* GRANITE-67514：変換ジョブの失敗や、顧客がデプロイしたバンドルとの競合を防ぐために、内部キャッシングライブラリバンドルを分離しました。
* SITES-42076：実験：Content APIにMCP プリミティブとしてページの一括検索および置換操作を追加しました。
* SITES-42835：実験的：Content API以外で作成されたAEM Forms ページに、移行やスキーマの変更を必要とせずに、AEM Sites Content API経由でアクセスできるようになりました。
* SITES-44265: Content APIに安定したレプリケートされたページ識別子を追加しました。これは、ページの移動後も有効であり、古い参照404 エラーを防ぎます。

### 修正された問題 {#fixed-issues-26125}

* ASSETS-36208:Dynamic Mediaが無効になっている場合に、フォルダープロパティに画像プロファイルが表示されない問題を修正しました。
* ASSETS-63240：追加モードで一括マルチセレクトのリレート操作を修正し、Assets コンソールに戻る代わりに空白ページにユーザーを残しました。
* ASSETS-65076:Externalizer APIに渡される誤ったプロトコル値を修正しました。これにより、Sling リクエストビルダーを使用する際にエラーが発生しました。
* ASSETS-66102：下流の統合でエラーが発生する原因となる、誤った`repo:version`値を報告するAdobe I/O Runtime アセット公開イベントを修正しました。
* ASSETS-66226：承認ステータスが大文字と小文字が混在した値で保存されている場合に、削除時に配信層からアセットが削除されない問題を修正しました。
* ASSETS-66669：統合シェルが有効になっている場合に、Touch UIの検索結果ページの「ホーム」ボタンが起動画面に移動しない問題を修正しました。
* ASSETS-66683：アップロード失敗によってトリガーされるOpenAPIを使用したDynamic Mediaで、バックログが作成され、アセットの承認ワークフローが中断する問題を修正しました。
* ASSETS-67113: MIME タイプ `image/svg+xml`でフィルタリングする際にSVG アセットを無視する一括読み込みを修正しました。
* CQ-4363355: GenAI翻訳コネクタの翻訳要求が、ハードコードされた静的URLにより、誤った地域エンドポイントにルーティングされる問題を修正しました。
* CQ-4363466: カスタム設定の解決を使用するサードパーティの翻訳コネクタに影響する、クラウド設定のパス解決エラーを修正しました。
* SITES-44186：一部の顧客に対する作成者のページエディターのイベント処理の破損に関するメタタグの挿入を修正しました。

### 既知の問題 {#known-issues-26125}

なし。

### 廃止された機能と API {#deprecated-26125}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-26125}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースは19の脆弱性に対応し、堅牢なシステム保護への取り組みを強化します。

### 組み込みテクノロジー {#embedded-tech-26125}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 2.0.0 | [Oak 2.0.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.0.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.30.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
