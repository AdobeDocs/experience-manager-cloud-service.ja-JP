---
title: CSV に書き出し
description: ページの情報をローカルシステムの CSV ファイルに書き出します
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# CSV に書き出し {#export-to-csv}

**CSV レポートの作成**&#x200B;では、ページの情報をローカルシステムの CSV ファイルに書き出すことができます。

* ダウンロードしたファイルの名前は `export.csv` になります。
* コンテンツは、選択するプロパティによって異なります。
* 書き出しのパスと深さを定義できます。

>[!NOTE]
>
>ブラウザーのダウンロード機能（およびデフォルトのダウンロード先）が使用されます。

**CSV の書き出しファイルを作成**&#x200B;ウィザードでは、次の要素を選択できます。

* 書き出すプロパティ
   * メタデータ
      * 名前
      * 変更済み
      * 公開済み
      * テンプレート
      * ワークフロー
   * 翻訳
      * 翻訳済み
   * Analytics
      * ページ表示
      * 個別訪問者数
      * ページ滞在時間
* 深さ
   * 親パス
   * 直属の子要素のみ
   * 追加の子のレベル
   * レベル

生成された `export.csv` ファイルは、Excel（または互換性のあるその他のアプリケーション）で開くことができます。

CSV の書き出しファイルを作成するには、次の手順を実行します。

1. **サイト**&#x200B;コンソールを開き、必要に応じて必要な場所まで移動します。
   * 「 **CSVレポートを作成** 」オプションは、サイトコンソール(リ **スト表示** )の閲覧時に使用できます。
   * これは、「作成」ドロップダウンメニ **ューの** 「オプション」です。

      ![CSVの作成オプション](/help/sites-cloud/authoring/assets/csv-create.png)

1. From the toolbar, select **Create** then **CSV Report** to open the wizard:

   ![CSVエクスポートオプション](/help/sites-cloud/authoring/assets/csv-options.png)

1. 書き出す必要があるプロパティを選択します。
1. 「**作成**」を選択します。
   ![ExcelでのCSVエクスポートの結果](/help/sites-cloud/authoring/assets/csv-example.png)
