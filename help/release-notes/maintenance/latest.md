---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 0dab7428d8ae5ec4c11a88ff310fad649a365868
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 20%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 13665 {#release-13665}

2023 年 9 月 27 日に公開されたメンテナンスリリース13665の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、リリース13420に代わるものです。

2023.10.0機能のアクティベーションは、このメンテナンスリリースの完全な機能セットを提供します。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-13665}

* コンテンツフラグメント API で様々な改善がおこなわれました。
* ASSETS-26713:Assets ダッシュボード：新しい Experience UI ダッシュボードが、タッチ UI からアクセスできるようになりました。
* SITES-11206：コンテンツフラグメント：コンテンツフラグメントの検索 API。
* SITES-11262：コンテンツフラグメント：新しいコンテンツフラグメントエディターに切り替えるためのボタン。
* SITES-15447：コアコンポーネント：バージョン2.23.4のリリース。

### 修正された問題 {#fixed-issues-13665}

* 各種翻訳関連アップデート。
* CQ-4354428：ワークフロー：インボックスでタスクを完了できません。
* SITES-9733：コンテンツフラグメント：コンテンツフラグメント参照パネルのアセット参照に 0（ゼロ）の参照が表示される。
* SITES-14561：コンテンツフラグメント：マークアップの変換のHTMLが修正され、向上しました。
* SITES-14882：コンテンツフラグメント：コンテンツフラグメントを編集し、「保存」または「閉じる」ボタンをクリックせずにタブを閉じると、値が保存されます。
* SITES-15167：コンテンツフラグメント：無効なペイロードを含むバリエーションにパッチを適用しても、400 が返されず、500 が返される。
* SITES-15514：コンテンツフラグメント：RTE 内のテーブルの Markdown 出力の形式が正しくありません。
* SITES-15661：コンテンツフラグメント：一意の制約を使用せず、フラグメント API の参照フィールドで項目を並べ替えてください。
* SITES-15730:Screens:Screens チャネルプレビュー機能がダッシュボードで機能しない。
* SITES-15995：コンテンツフラグメント：モデルとフラグメントの長いテキストフィールドの両方の MIME タイプがハードコードされます。
* SITES-16074：コンテンツフラグメント：文字列でないフィールドにタグを付ける[] は JCR から取得できません。
* SITES-16084：コンテンツフラグメント： CFHomeCardModelImpl にターゲットナビゲーターがありません。
* SITES-14773：エクスペリエンスフラグメント：リンク参照がエクスペリエンスフラグメント内で更新されない。
* SITES-14899：エクスペリエンスフラグメント：Target の XF バリエーション用に作成された複数のオファー。
* SITES-8590:GraphQL：永続化されたクエリでの変数のエンコードの問題。
* SITES-9224:GraphQL:GraphQLServlet の「Writer has already been closed」例外。
* SITES-14800:GraphQL：変数を使用した永続化されたGraphQLクエリの例外。
* SITES-15586:GraphQL：永続化されたクエリで null 値でフィルタリングされた問題。
* SITES-15622:GraphQL：数値およびブールパラメーターを持つ永続クエリに関する問題。
* SITES-15654:GraphQL：同じ名前の和集合とプロパティに関する問題。
* SITES-15267：ローンチ：ローンチ設定を変更する前に変更されたローンチページがプロモーションで選択されません。
* SITES-15406：ローンチ：ローンチページを追加できません。
* SITES-15427：ローンチ：「現在のページとサブページを昇格」スコープの動作に一貫性がありません。
* SITES-15429：ローンチ：ローンチの昇格中に削除されたページのオーサリング。
* SITES-15462：ローンチ：自動昇格プロセスにより、昇格範囲外のページが公開されます。
* SITES-15815：ローンチ：ローンチからページを削除すると、ローンチが正常に昇格されません。
* SITES-15223：ページエディター：タブレットサイズエミュレーターでコンポーネントのサイズを変更できない。
* SITES-15463：ページテンプレート：テンプレートを公開できません。

### 既知の問題 {#known-issues-13665}

なし

### 組み込みテクノロジー {#embedded-tech-13665}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
