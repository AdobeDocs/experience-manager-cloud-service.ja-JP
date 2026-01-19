---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: be61c21e111e1655921325a35da6fa88545fb39f
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 19%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 23963 {#23963}

2026年1月19日（PT）に公開された、メンテナンスリリース 23963 の継続的な改善点を以下にまとめます。 前回のメンテナンスリリースは、リリース 23482 でした。

2026.1.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

>[!NOTE]
>
>リリース 23862 が非公開になりました。

### 機能強化 {#enhancements-23963}

* CQ-4361812:rest api で、オプションのパラメーター folderPath がサポートされるようになりました。 説明：新しい翻訳プロジェクトが API によって作成され、オプションの `folderPath` パラメーターで指定されたパス内に配置されます。それ以外の場合は、デフォルトでルートプロジェクトのパス `/content/projects` になります。
* FORMS-21960:forms-spa と同様に、インタラクティブ通信のローカルでのキャンバス編集がサポートされるようになりました。
* FORMS-22001:AEM Forms as a Cloud Serviceで大量の `/etc.clientlibs/toggles.json` リクエストを減らすためのガイダンスが追加されました。
* FORMS-22496：生の ResponseBody を呼び出しサービスで公開する。
* FORMS-22495:SetProperty ルールにプレースホルダープロパティを追加。
* FORMS-21925: UBS 脚注の書式設定：フォームの読み込み中に、フォーム内のすべての脚注を表示します。
* FORMS-20536：マッピングを使用せずに、ルールエディターの eventPayload で complete response のオプションを公開する。
* SITES-37199：注釈機能トリガー未検証の `authorizables.json` 呼び出しを使用したリポジトリのトラバーサルにより、パフォーマンスが低下する。
* SITES-37118：製品コックピットでのCommerce Optimizerのサポート。
* SITES-38029：変更イベントで MSM プッシュをトレースするためのログを追加します。
* SITES-37050：他の公開済みリソースから参照されるコンテンツフラグメントを非公開にできる、「強制非公開」のサポート。
* SITES-37142：コンテンツフラグメントのPATCHを使用してコンテンツフラグメントをチェックイン/チェックアウトできるようになりました。
* SITES-37613:CF API 権限エンドポイントでは、ユーザーがコンテンツフラグメントをチェックインできる場合はチェックイン、ユーザーがコンテンツフラグメントをチェックアウトできる場合はチェックアウトが返されます。
* SITES-37835：同じタイトルで、指定された名前がないコンテンツフラグメントを複数作成しようとすると、競合で失敗するのではなく、自動的に新しい名前が生成される。
* SITES-36823：ユニバーサルエディターを使用したEdge Delivery: インデックスのリバースマッピングの必要性をなくしました。
* SITES-34751：ユニバーサルエディターを使用したEdge Delivery：公開時（アーリーアクセス）に、サポートされていないファイルタイプとパスが制限を超えている場合に失敗します。
* SITES-37888：ユニバーサルエディターを使用したEdge Delivery: リンクのテキストの同義語として代替サフィックスを使用します。
* SITES-19850：ユニバーサルエディターを使用したEdge Delivery：スプレッドシートで複数のシートがサポートされるようになりました。
* SITES-32490：ユニバーサルエディターを使用したEdge Delivery: data-aue-component とユーザー定義の data-aue-label のサポートを、ブロックとデフォルトコンテンツに追加しました。
* SITES-37794：ユニバーサルエディターを使用したEdge Delivery：ページ作成ウィザードを簡素化します。
* SITES-36963:Workspace サポートのために、オーディエンス/セグメントエンドポイントを Target API v3 に移行します。

### 修正された問題 {#fixed-issues-23963}

* CQ-4361831:genai_dropdown_span が定義されていない問題を修正しました。
* CQ-4360895：同時更新中にプロジェクト内の不正確な翻訳ジョブステータス数が修正されました。
* CQ-4361599:2025.7 へのアップグレード後に、翻訳ジョブからコンテンツフラグメントがスキップされる問題を修正しました。
* CQ-4360747：固定繰り返し可能な翻訳ジョブで、空のペイロードとトリガーが頻繁に作成される（ScheduleRepeatTranslationProject の NullPointerException）。
* CQ-4359994：単一プロジェクトと多言語プロジェクトの destinationLanguage フィールドタイプの不整合が修正されました。
* FORMS-23557:Rhino の更新が原因で `*.js`Use API で正しくインスタンス化できない。
* SITES-38153:uuid ベースの参照の cf 公開参照プロバイダーを修正。
* SITES-37594：タグ機能によるモデルのパフォーマンスの向上。
* SITES-37337:FragmentCreateProcessor：ログにエラーの詳細を追加します。
* SITES-33666: コンテンツフラグメントエディターで「フラグメントの Json を印刷できません」というエラーメッセージがローカライズされていません。
* SITES-33675: コンテンツフラグメントエディター/関連コンテンツで「undefined」文字列をハードコードしました。
* SITES-30715: コンテンツフラグメントエディターで「一般」文字列がローカライズされていません。
* SITES-28592：コンテンツフラグメントモデルエディター/「モデルがロックされています」ダイアログで、ローカライズされていない文字列が表示される。
* SITES-977：文字列「タグ」および「コレクション」が、コンテンツフラグメントを編集ページでローカライズされていない。
* SITES-29699：コンテンツフラグメントエディターで、許可されているアセットのローカライズされていないタイプ。
* SITES-25240：ティーザーモーダル内のCall to action フィールドに、表示ラベルがない。
* SITES-24869：テンプレートエディター/セパレーター/ポリシーでツールヒントが切り詰められる。
* SITES-19313：テンプレートエディターでコンポーネントを削除されたテンプレートにドラッグ&amp;ドロップすると、エラーがローカライズされない。
* SITES-18103：ページエディター/ワークフローでローカライズされていない文字列。
* SITES-17501: テンプレートエディター/コンポーネントポリシーエディターでローカライズされていない文字列。
* SITES-15091：文字列が、エクスペリエンスフラグメントのテキストコンポーネントプロパティでローカライズされない。
* SITES-8113: 「Assets」文字列が、「ツール」メニューの「テンプレート」の「画像を選択」ダイアログでローカライズされない。
* SITES-37587:NPE が RolloutManagerImpl に設定されていると、実稼動環境でライブコピーの作成が失敗する。
* SITES-37335:cq タグに関連するコンソールでエラーを示すライブコピーページのプロパティ。
* SITES-36972：編集可能なツールバーに「ロールアウト」ボタンが表示されない。
* SITES-36570：チャンク化された「ライブコピーを作成」切替スイッチがアクティブ化されると、ライブコピーの作成に失敗します。
* SITES-36158：例外が原因でジョブが失敗し、ロールアウトが失敗する。
* SITES-35655：新しい CF エディターが、壊れた後にアクティブな継承を表示する。
* SITES-31425: サイトの「ワークフローを開始」にローカライズされていないエラーメッセージ `Error: {} field is required` 表示される。
* SITES-19802：ツールチップが、コアコンポーネントサイト/目次でローカライズされていない。
* SITES-36543：チェックアウトされたコンテンツフラグメントを管理者が編集できる問題を修正しました。
* SITES-36967：破損したコンテンツフラグメントのサムネールデータを生成しようとしたときに発生する NullPointerExceptions を修正しました。
* SITES-37791:`$` を含む文字列に対して FindAndReplace を呼び出すと失敗する問題を修正しました。
* SITES-37018：許可されていないテンプレートパスを含んだページをコピーする際に、空のエラーポップアップが表示される。
* SITES-36243：ユニバーサルエディターを使用したEdge Delivery:`sling:OrderedFolder` の公開中に 404 を修正しました。
* SITES-37684：ユニバーサルエディターを使用したEdge Delivery：多くのサイトが存在する環境でのパフォーマンス低下を修正しました。
* SITES-37840：ユニバーサルエディターを使用したEdge Delivery:Edge Deliveryのアクセストークンが古くなったことによる公開エラーを修正しました。
* SITES-37933：ユニバーサルエディターを使用したEdge Delivery：ローンチで削除されたリソースの公開エラーを修正（非公開）します。
* SITES-37870：ユニバーサルエディターを使用したEdge Delivery：複数フィールドのサポートを有効にしたカスタムページメタデータのレンダリングが壊れる問題を修正しました。
* SITES-37349：ユニバーサルエディターを使用したEdge Delivery：単一のリストアイテムを持つリストとして、単一のエントリを持つ複数のフィールドをレンダリングします。
* SITES-36148：ユニバーサルエディターを使用したEdge Delivery：複合マルチフィールド用の data-aue-label を修正しました。

### 既知の問題 {#known-issues-23963}

なし。

### 廃止された機能と API {#deprecated-23963}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-23963}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 23 個の脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-23963}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.88.0 | [Oak 1.88.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.30.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
