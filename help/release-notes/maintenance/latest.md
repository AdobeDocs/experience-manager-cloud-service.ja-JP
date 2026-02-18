---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a58225edb8ca49db9743db6c9c5b08c786fa0144
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 27%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 24464 {#release-24464}

2026年2月17日に公開された、メンテナンスリリース 24464 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 24288 でした。

2026.2.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-24464}

* AEMARCH-264:RequestEntity に基づく条件付きリクエストの検証のサポートを追加しました。
* AEMARCH-269:OpenAPI 実装用の JavaEE 検証 API を公開します。
* AEMARCH-276:RequestEntity を通じて i18n のサポートを提供します。
* ASSETS-10995：ダウンロード zip でアセット数の制限を設定します。
* ASSETS-50788:Asset Metadata GET API を使用するように検索 API を更新してください。
* ASSETS-50946：メタデータGET API を使用してリクエスト本文を JCR メタデータにマッピングします。
* ASSETS-55866：前の処理が完了するまで、同じアセットに対して新しいリクエストを送信しないでください。
* ASSETS-60300：非同期ジョブコンテキストと結果を取得する API を提供する。
* ASSETS-60574：最新バージョンの Sling API バンドルのサポートを追加。
* ASSETS-61049: メタデータマネージャーバンドルの開発を続行します。
* ASSETS-61692：検索 Open API でデフォルトでセマンティック検索を実行します。
* ASSETS-61696：アセットビューの BAM ルートと MFE ラッパー。
* ASSETS-61854:GenStudio ソリューションをアクティベーション/非アクティブ化メッセージで送信する。
* ASSETS-61973：プロンプトを管理するための API をAEMで作成する。
* ASSETS-62182:c2pa-manifest レンディションのAsset Compute イベントハンドラー。
* ASSETS-62311：検索回帰の問題。
* ASSETS-62413:JSON のすべてのレイヤーで customModifier フィールドのサポートを追加。
* ASSETS-62432：結合フォルダー削除 API PR。
* ASSETS-62540：クイックスタートの ui タッチ操作向けバージョンを強化しました。
* ASSETS-62622:MatchQuery で検索モードを処理します。
* ASSETS-62671:MatchQuery startsWith 演算子を修正。
* ASSETS-62780：フォルダー API の機能トグルを追加。
* ASSETS-62988:「レンディション」タブで c2pa マニフェストレンディションを表示しないようにします。
* ASSETS-63336:AEMから DM へのテンプレート同期は、DAM の名前空間メタデータに対してのみ行われる必要があります。
* ASSETS-63375：アセットのアップロードに実験的な OpenAPI を機能トグルの背後に配置する。
* ASSETS-63453：すべてのユーザーがオムニサーチ設定を読み取れるようにします。
* GRANITE-63744：非同期ジョブを Sling ジョブに接続できるようにします。
* GRANITE-64567:SKU 検索のセマンティック検索を自動的に無効にします。
* GUIDES-41187：ガイドの使用向けにヘッダーを追加する。
* SITES-30452:ASO - タイトルと説明の提案を含むコンテンツ API
* SITES-33116：パスの検証を修正。
* SITES-34234：ページエディター：コンテンツツリーの状態を保持します。

### 修正された問題 {#fixed-issues-24464}

* ASSETS-43198：アセットの有効期限通知メールが、ユーザーの言語の環境設定に違反する。
* ASSETS-51840：アセット処理の改善。
* ASSETS-52061：保存した検索条件を選択した後で戻って移動できません。
* ASSETS-53155：アセットコンテンツの改善。
* ASSETS-53745:Dynamic Media のダウンロードフローでは、web プリセットを選択する前に、元のアセットの選択を解除する必要があります。
* ASSETS-54260:Asset コンテンツの修正。
* ASSETS-54787：アセットコンテンツの改善。
* ASSETS-57391：アセットのコンテンツのアップデート。
* ASSETS-59213:cq-dynamicmedia-core は、非推奨の commons-lang ライブラリに依存しています。
* ASSETS-59214:cq-scene7-imaging は非推奨の commons-lang ライブラリに依存しています。
* ASSETS-59546:cq-remotedam-client-core は、非推奨（廃止予定）の commons-lang ライブラリに依存します。
* ASSETS-59703:cq-dam-core は、非推奨（廃止予定）の commons-lang ライブラリに依存します。
* ASSETS-59705:cq-dam-handler は、非推奨の commons-lang ライブラリに依存します。
* ASSETS-59707:cq-dam-indesign は、非推奨（廃止予定）の commons-lang ライブラリに依存します。
* ASSETS-59709:cq-scene7-core は非推奨の commons-lang ライブラリに依存します。
* ASSETS-59929：フィールドに改行文字が含まれている場合、メタデータ書き出しからの CSV が機能しなくなる。
* ASSETS-60241：フォルダー名を変更すると、非同期移動ジョブが失敗する。
* ASSETS-61134:pom ファイルから comparisonVersion タグを削除します。
* ASSETS-61309：コンテンツフラグメントの移動/コピーで、内部参照が更新されなくなりました。
* ASSETS-61730：直接バイナリアクセスではアセットのエンコーディングが適用される必要がある場合にリダイレクトします。
* ASSETS-62358:Assets レポートの CSV で、コンテンツパスに破損した値が表示される。
* ASSETS-62610:Assets UI で「Adobe Stock ライセンス」ボタンが無効になる。
* ASSETS-62613:`downloadasset`/`saveas` の NPE。
* ASSETS-62656:Assets以外での検索で、オムニサーチのAI 検索インジケーターが正しく表示されない。
* GRANITE-55387：引用符で囲まれた単語を修正すると、単語全体が削除される。
* GRANITE-61240:lazycontainer.js に格納された XSS を介した RCE。
* GRANITE-64101:ES に変換された OOTB インデックスが、再起動時に Lucene に戻されました。
* SITES-24530：検索モーダルで閉じる/削除ボタンのタッチターゲットが十分な大きさではない。
* SITES-31425：開始ワークフローでローカライズされていないエラーメッセージが表示される。

### 既知の問題 {#known-issues-24464}

なし。

### 廃止された機能と API {#deprecated-24464}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-24464}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 14 個の脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-24464}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.30.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

