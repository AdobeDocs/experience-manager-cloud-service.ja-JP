---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 09c52e32e6ffff2c69fb24f28e99a65477b434ec
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 15%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 27083 {#release-27083}

2026年7月15日に公開されたメンテナンスリリース 27083の継続的な改善の概要を以下に示します。 以前のメンテナンスリリースはリリース 26908でした。

2026.7.0機能のアクティベーションは、このメンテナンスリリースの完全な機能セットを提供します。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-27083}

* 翻訳設定を削除するCQ-4354303:Added機能。
* FORMS-23746:InvokeDDXとAsset Uploadのワークフローステップ間でデータタイプが一致しないため、それらを順番に使用できません。
* FORMS-24585：プロビジョニングが簡単なAEP Connector。
* FORMS-25250:ConvertPdf サービスが導入されました。
* FORMS-26044:AF1およびコアコンポーネントベースのフォームにアップロードするための添付ファイルのウイルス/マルウェアスキャンを追加しました。
* GRANITE-69298: `cqPageContent-5`と`graphqlConfig-3`個のインデックスを追加します。
* SITES-42563: ユニバーサルエディターを使用したEdge Delivery：ユニバーサルエディターとSites管理者（早期アクセス）で公開エラーが表示されます。
* SITES-42792:「ツール」/「一般」/「ローンチ」のフィルターパネルの「ローンチSourceのパスを選択」プレースホルダーが切り捨てられています。
* SITES-43178: AEM: ローカライズされた時間フォーマットには、ツール/サイト/ローンチのAM/PMが含まれます。
* SITES-44344: コンテンツ API:MSM/言語コピーを親サイトの一部として扱います。
* SITES-44598：エディターヘッダーバーにプリフライトボタンを表示します。
* SITES-44676：コンテンツフラグメントの検索結果に、各フラグメントのメタデータスキーマ IDが含まれるようになりました。
* SITES-44767: コンテンツフラグメントのデフォルトのメタデータスキーマを追加しました。
* SITES-45651: API仕様のOpenAPI コンテンツフラグメントの例を修正しました。
* SITES-45664：フィルター可能なメタデータプロパティを取得するための新しいGET `/cf/metadata/schemas` エンドポイントを追加しました。
* SITES-45725: Content API：リクエスト相関フィルターを追加して、Oak トラバーサル SLO アラートを有効にします。
* SITES-45817: ユニバーサルエディターを使用したEdge Delivery：公開中（早期アクセス）にエッジ配信の役割と権限を確認できます。
* SITES-45842: ユニバーサルエディター付きEdge Delivery：読み取り専用およびレビュー/コメント用のユニバーサルエディターのインストルメントを保持します。
* SITES-45848: ユニバーサルエディターを使用したEdge Delivery：公開前に`json-ld`を検証します。
* SITES-46768: ユニバーサルエディターを使用したEdge Delivery：サイト作成ウィザードでサイト作成の問題を表示します。

### 修正された問題 {#fixed-issues-27083}

* CQ-4364078：言語コピーによるエクスペリエンスフラグメント内の内部リンクの書き換えを修正しました。
* CQ-4364077: OakState0001の競合による言語コピー作成の破損を修正しました。
* CQ-4363949：更新専用翻訳で参照されている変更されていないエクスペリエンスフラグメントが誤って再追加される問題を修正しました。
* CQ-4363942: タグ UI:「言語を追加」ドロップダウンで、JCRに永続化されているにもかかわらず表示されなかった非掲載ロケールが表示されるようになりました。
* CQ-4363527:Agentic Method &amp; Providerの言語コピーウィジェット UIの不具合を修正しました。
* FORMS-25979: AEM Forms アドオンのUnderscore.js ライブラリ（1.13.6 → 1.13.8以降）をアップグレードしました。
* FORMS-18969:AEM Forms テーマでフォームのプレビューを更新できない問題を修正しました。
* FORMS-25184：コアコンポーネントベースのフォーム（AF v2）のデータソースサイドパネルでデータバインディングインジケーターが見つからない問題を修正しました。
* FORMS-18721:AEM Forms テーマがベースクライアントライブラリを更新できない問題を修正しました。
* FORMS-19235:Forms Managerで機密情報を公開する可能性があるアプリケーションエラーを修正しました。
* FORMS-25369：テーマのコピーで、クライアントライブラリのベースメタデータからclientlibの依存関係が引き継がれない問題を修正しました。
* FORMS-25372：埋め込み事前入力エラーとJSON マージの問題が埋め込みアダプティブ Formsに影響する問題を修正しました。
* FORMS-24853：アダプティブFormsの手書き署名コンポーネント（基盤コンポーネント）のタブ付けの問題を修正しました。
* SITES-41928: Contexthub + Unified Shellの重複により、エディターでコンポーネントメニューにアクセスできなくなります。
* SITES-46579: Content API: RelationshipServiceの言語コピークエリでリポジトリのトラバーサルを修正 – インデックスを定義してクエリを書き換えます。
* SITES-44192: Forms/Content API: Content APIは、`cq:conf`ではなく`sling:configRef`を使用しているEDS フォームに対して404を返します。
* SITES-29367: GraphQL：誤った`cqPageLucene` インデックスのカスタマイズからModelManagerを保護します。
* SITES-46521: クエリ内のコンテンツ API: `jcr:path`がクエリトラバーサルを引き起こしています。
* SITES-46784: GraphQL: ModelManagerのモデルは重複を排除する必要があります。
* SITES-46304: Content API: Content API ページの検索で`/content/campaigns`がサイレントに除外されます。
* SITES-46769: GraphQL：大きなコンテンツフラグメントモデルを持つリクエストごとのDataCacheがOOMの例外につながります。
* SITES-46570: コンテンツ API: テンプレートクエリでインデックスパス（）オペランドを使用して、インデックスプッシュダウンを行います。
* SITES-24497：繰り返し使用するランドマークに対して個別のラベルが提供されるようになり、支援テクノロジーがそれらのラベルを区別できるようになりました。
* SITES-24525：モーダルボタンに割り当てられた間違った見出し役割を修正しました – スクリーンリーダーがボタンとしてアナウンスするようになりました。
* SITES-24703: リストボックスポップアップボタンのフォーカスインジケーターが完全に表示され、クリップされなくなりました。
* SITES-25217：情報アイコンが拡大され、ターゲットサイズの最小要件を満たしました。
* SITES-25263: タイムワープ日付フィールドのaria-haspopup値を修正して、スクリーンリーダーが正しく通知するようにしました。
* SITES-25308: デモグラフィックツールバーボタンのフォーカスインジケーターのコントラストを上げて、WCAGの最小値を満たします。
* SITES-25318：デモグラフィックツールバーの入力フィールドのテキストコントラストを改善しました。
* SITES-25364：入力指示がチェックボックスにプログラムでリンクされるようになったため、支援技術が一緒にアナウンスするようになりました。
* SITES-25377: フィルターフィールドにフォーカスが適用されたときに、Assetsのサイドレールがコンテンツを再読み込みしなくなりました。
* SITES-40752：サイドパネルコンポーネントリストのキーボードナビゲーションを改善しました。
* SITES-41121：スクリーンリーダーが、コンポーネント名と共に非表示のグループラベルをアナウンスするのを防止しました。
* SITES-43802：挿入コンポーネントモーダル内に表示されていた偽の「false」文字列を削除しました。
* SITES-46720: Page-Properties ラジオは、2026.05以降のアップデート（SDK ≥ 26353）後に保存済みの選択範囲を失います。値はクライアントサイドでクリアされます。
* SITES-46680：カスタムコードでSling サーブレットのマッピングが原因で、CF Launchを作成できません。
* SITES-46327:「ソースページのライブデータを継承」オプションを有効にしてローンチを作成する場合、ソースページのエクスペリエンスフラグメントが継承されず、一部のリンクも壊れています。
* SITES-45969:「新しいテンプレート」+「サブページを含める」を使用すると、ローンチプロモーション時に子ページが削除される。
* SITES-45723: SITES-44245の修正でローンチが壊れる：empty-genericFrom ガードは、正当なローンチ参照の書き換えを抑制します。
* SITES-45689：断続的なMSM ロールアウト エラー – &quot;Source パスなし&quot; &amp; AccessDeniedException。
* SITES-44918: IDの代わりにINで表示されるインドネシア語コード。
* SITES-41427：ライブコピーが存在しない場合、XF ロールアウトが成功したことを報告しますが、サイレントで失敗します。適切な処理または自動作成をリクエストします
* SITES-36149：プロモーション後にローンチでライブシンクを使用したコンポーネントの複製。
* SITES-25970：コンポーネント UIのロールアウトダイアログがカットされる。
* SITES-30707：ローカライゼーションをサポートするために、コンテンツフラグメントエディターでハードコードされた「一般」ラベルを修正しました。
* SITES-44228: uuidで参照されている参照コンテンツフラグメントを削除すると、参照フラグメントが調整されない問題を修正しました。
* SITES-45171：公開リクエストでアクティベーションのリクエスト ワークフローが誤ってトリガーされる問題を修正しました。
* SITES-46303：不要なカード移行の試みを避けるために、バージョンの取得を修正しました。
* SITES-46713：ユーザーがカードの移行に必要な削除権限を持っていない場合にPATCHの操作が失敗する問題を修正しました。
* SITES-46590: タイムラインで以前のバージョンに戻しても、Assets管理ビューでアセットカードのサムネールが更新されないリグレッションを修正しました。
* SITES-47292：ユニバーサルエディターを使用したEdge Delivery：ページメタデータ内の結合タグのレンダリングを修正します。

### 既知の問題 {#known-issues-27083}

なし。

### 廃止された機能と API {#deprecated-27083}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-27083}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 18 個の脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-27083}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 2.2.0 | [Oak 2.2.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.2.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.67 | [Apache Httpd 2.4.67](https://apache.googlesource.com/httpd/+/refs/tags/2.4.67/CHANGES) |
| Dispatcher | 2.0.274 |  |
| AEM コアコンポーネント | 2.31.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
| Java 21 | 21.0.11 | [JDK 21.0.11](https://www.oracle.com/java/technologies/javase/21-0-11-relnotes.html) |
