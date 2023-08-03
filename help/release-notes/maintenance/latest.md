---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: acaed9eed20e8134574fd326e23ac68130ac019b
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 11%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 12874 {#release-12874}

2023 年 8 月 2 日に公開されたメンテナンスリリース12874の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 12790 からのアップデートです。

2023.8.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-12874}

- インデックス定義の新しいバージョン： `/oak:index/damAssetLucene-9`
- ASSETS-18351：安全でないファセットに切り替え、検索パフォーマンスを向上させます。
- ASSETS-17896：インデックスから機能ベクトルを削除します。スマートタグに基づいた類似検索
- ASSETS-8715：プロパティ「jcr:content/metadata/dam:status」に null check または not null check を追加します。
- GRANITE-45138：予測されたタグのダイナミックブーストプロパティからプロパティインデックスを削除します。
- ASSETS-17614:Scene7 ID をインデックス付きのプロパティとして追加します（null check および null check not null check enabled）。
- ASSETS-14516: 「新規 UI」ごみ箱機能のプロパティをインデックスに追加します。
- ASSETS-16270：結合されたタイトルプロパティをインデックスに追加します（並べ替えで使用）。
- ASSETS-24478:（顧客インデックスデータの分析に基づいて）インデックスから 5 つの潜在的に大きなプロパティを削除します。
- ASSETS-3383：タグ「assetsOmnisearch」を追加します。

AEMリリース12874以降には、damAssetLucene インデックス (damAssetLucene-9) の新しいバージョンが含まれています。 最もレスポンシブな検索エクスペリエンスを提供するために、damAssetLucene-9 では、Oak クエリの結果ファセットの動作を変更し、基になる検索インデックス（「安全でない」モードと呼ばれる）で返されるファセット数のアクセス制御を評価しなくなりました。

したがって、現在のユーザーがアクセスできないアセットを含むファセット数の値がユーザーに表示される場合があります。 これにより、ユーザーはアセットへのアクセス、ダウンロード、読み取りを実行できず、また、アセットの存在に関する詳細情報を取得できません。

以前の動作が必要な場合は、 [コンテンツの検索とインデックス作成](/help/operations/indexing.md) 以前の「統計」ファセットモードで damAssetLucene-9 インデックスのカスタムバージョンを作成する場合。

### 修正された問題 {#fixed-issues-12874}

- ASSETS-24379:ReplicateOnModifyListener を改善しました。
- ASSETS-25794：起動時に高価なクエリが実行される原因となっていた S7ConfigResolverImpl の問題を解決しました。
- ASSETS-25473：レプリケーション権限を持たないユーザーにクイック公開オプションが表示されるバグを修正しました。
- ASSETS-24803：ビューア機能の XSS の脆弱性に対処しました。
- ASSETS-25489：誤ったサフィックスでスマート切り抜きがダウンロードされる問題を修正しました。
- ASSETS-25435：動的レンディションのダウンロードで WidthxHeight フィールドが見つからないエラーを修正しました。
- ASSETS-25741：視覚的なアスタリスク (`*`) 記号（「基本」タブセクションの必須の「幅」編集フィールド）。
- ASSETS-25759：コントラストの大きい黒/白のモードで、ドロップダウン要素にフォーカスが見えるようになりました。
- ASSETS-25749：キーボードの Tab を使用して移動する際に、フォーカスがビデオの下の複数のコントロールに移動せず、アクセスできなくなる問題を修正しました。
- ASSETS-26074：非ビデオアセットの名前の上限である 127 文字を復元しました。
- ASSETS-21428：メタデータスキーマエディターの複数行フィールドが次のフィールドと重なる問題を修正しました。
- ASSETS-21989:302 応答および 401 応答で CORS ヘッダーが上書きされ、リモート DAM ログインができない問題を修正しました。
- ASSETS-22603：アセットダウンロードレポートを表示する際の列名と値に影響する問題を修正しました。
- ASSETS-23120：リソースリゾルバーの漏洩に関連する AssetSetLastModifiedProcess の問題を修正しました。
- ASSETS-24938：アセットフォルダーのプロパティダイアログの「保存」ボタンが「保存して閉じる」と同じように動作する問題を修正しました。
- ASSETS-25456：アセットの名前が長いと、アセットのプロパティエディターでアクションをクリックできない問題を修正しました。
- ASSETS-25832：フルアクセスフォルダーのアセットを読み取り専用アクセスフォルダーに関連付ける際の問題を修正しました。
- ASSETS-25397：新しい UI で名前が変更されたアセットの新しい名前が検索結果に反映されない問題を修正しました。
- ASSETS-26102:CI Hub コネクタからのアップロードが妨げられる可能性がある問題を修正しました。
- ASSETS-26172：永続的な Sling ジョブノードに保存される一括読み込みの進行状況ログコンテンツのサイズを縮小しました。
- ASSETS-26292:Java API の非推奨（廃止予定）の AssetManager createOrUpdateAsset() および createOrReplaceAsset() メソッド
- ASSETS-26399：コレクションをBrand Portalに公開できなかった問題を修正しました。
- ASSETS-26533:Indesign Server 統合で、長時間の処理リクエストのタイムアウトが発生する問題を修正しました。
- ASSETS-26549：アセットのリスト表示で、アップロードされたすべてのアセットに対して「外部ユーザー」が最後に変更されたユーザーとして表示されていた問題を修正しました。
- ASSETS-26551：作成者で削除されたアセットが非公開にならない問題を解決しました。
- ASSETS-26571：アセットレポートページで、失敗したレポートジョブがリストに複数存在する場合に、ページの読み込みに失敗する問題を修正しました。
- ASSETS-26147:window.top.opener が設定されているが window.opener が設定されていない場合に、統合シェルが iframe を/ui にリダイレクトしようとする問題を修正しました。
- ASSETS-26576:Dropboxーの読み込みで、間違ったフォルダー階層が作成されていた問題を修正しました。
- ASSETS-26671：一括読み込みで DCIM フォルダー内のファイルを含めることができなかった問題を修正しました。
- ASSETS-26700：パブリックフォルダーのプロパティページを変更なしで保存すると、3 つの不要なグループが作成される問題を修正しました。
- CQ-4353449：読み取り専用のタグ付け権限を持つユーザーが、タグ付け UI を使用してタグを作成できる問題を修正しました。
- GRANITE-46601：クイックスタート SDK が JDK 11.0.20 で起動できなかった問題を修正しました。
- SKYOPS-33168:CM 開発者コンソールで、拡張子のないアセット名の/content/dam を読み込めなかった問題を修正しました。
- SKYOPS-61484: RDEProvider サービスで、置換されていない${sling.home} トークンが結合された OSGi 設定で保持される問題を修正しました。
- 様々なセキュリティ、アクセシビリティ、ローカライゼーションの修正

### 既知の問題 {#known-issues-12874}

- GRANITE-46851：コンテンツ配布のテスト接続が機能しない

### 組み込みテクノロジー {#embedded-tech-12874}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
