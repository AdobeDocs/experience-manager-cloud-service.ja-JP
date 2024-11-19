---
title: スプレッドシートを使用した表形式データの管理
description: スプレッドシートを使用して、Edge Delivery Services を使用した AEM のサイトのメタデータやリダイレクトなど、様々な値の表形式データを管理する方法を説明します。
feature: Edge Delivery Services
exl-id: 26d4db90-3e4b-4957-bf21-343c76322cdc
role: Admin, Architect, Developer
source-git-commit: 4e4234c1aaf0a410cb419140e9e353348ce118c1
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 73%

---


# スプレッドシートを使用した表形式データの管理 {#tabular-data}

スプレッドシートを使用して、Edge Delivery Services を使用した AEM のサイトのメタデータやリダイレクトなど、様々な値の表形式データを管理する方法を説明します。

## ユースケース {#use-cases}

Edge Delivery Services を使用した AEM のサイトでは、キーと値のマッピングなど、表形式のデータのリストを維持する必要があります。これらは、メタデータやリダイレクトなど、様々な値のリストにすることができます。Edge Deliver Services を使用すると、スプレッドシートという直感的なツールを使用して、このような表形式のリストを管理できます。AEM は、これらのスプレッドシートを JSON ファイルに変換し、web サイトや web アプリケーションで容易に使用できるようにします。

一般的なユースケースを次に示します。

* [プレースホルダー](/help/edge/docs/placeholders.md)
* [メタデータ](/help/edge/docs/bulk-metadata.md)
* [ヘッダー](/help/edge/docs/custom-headers.md)
* [リダイレクト](/help/edge/docs/redirects.md)
* [設定](/help/edge/docs/setup-byo-cdn-push-invalidation.md)（CND 設定など）

さらに、任意の構造の[スプレッドシートを作成](#own-spreadsheet)して、独自の目的でマッピングを保存できます。

このドキュメントでは、リダイレクトの例を使用して、このようなスプレッドシートの作成方法を説明します。各ユースケースについて詳しくは、Edge Delivery Services ドキュメントのリンク済みのトピックを参照してください。

>[!TIP]
>
>スプレッドシートの一般的な Edge Delivery Services の操作方法について詳しくは、[スプレッドシートと JSON](/help/edge/developer/spreadsheets.md) のドキュメントを参照してください。

>[!TIP]
>
>スプレッドシートは、表形式のデータの管理にのみ使用する必要があります。構造化データを保存する場合、[AEM のヘッドレス機能を確認してください。](/help/headless/introduction.md)

## 前提条件 {#prerequisites}

Edge Delivery Services を使用した AEM プロジェクトでスプレッドシートを使ってマッピングを作成するには、最新のサイトテンプレートを使用してサイトを作成しておく必要があります。

詳しくは、[Edge Delivery Servicesを使用したWYSIWYG オーサリングの開発者向けスタートガイド ](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) を参照してください。

## スプレッドシートの作成 {#spreadsheet}

この例では、Edge Delivery Services を使用した AEM のサイトでのリダイレクトを管理するスプレッドシートを作成します。作成する[その他のスプレッドシートタイプ](#other)にも同じ手順を適用します。

1. AEM as a Cloud Service のオーサリングインスタンスにログインし、**Sites** コンソールに移動し、スプレッドシートが必要なサイトのルートに移動します。**作成**／**ページ**&#x200B;をタップまたはクリックします。

   ![ページを作成](assets/tabular-data/tabular-data-create-page.png)

1. ページ作成ウィザードの「**テンプレート**」タブで、**リダイレクト**&#x200B;テンプレートをタップまたはクリックして選択し、「**次へ**」をタップまたはクリックします。

   ![テンプレートを選択](assets/tabular-data/tabular-data-create-page-teamplate-redirects.png)

1. ウィザードの「**プロパティ**」タブに、リダイレクトスプレッドシートのデフォルト値が表示されます。「**作成**」をタップまたはクリックします。

   * **タイトル** - この値はそのままにします。
   * **列** - リダイレクトに必要な最小限の列が事前入力されています。
      * **ソース** - リダイレクトするページ
      * **宛先** - リダイレクト先のページ

   ![スプレッドシートのプロパティ](assets/tabular-data/tabular-data-create-page-properties-redirects.png)

1. **成功**&#x200B;ダイアログで、「**開く**」をタップまたはクリックします。

   ![成功ダイアログ](assets/tabular-data/tabular-data-success.png)

1. 新しいタブが開き、事前定義済みの「**ソース**」および「**宛先**」の列を含むスプレッドシートがエディターに読み込まれます。リダイレクトを定義するには、「**ソース**」列の空の行をタップまたはクリックします。スプレッドシートを編集すると、変更内容は自動的に保存されます。

   ![スプレッドシートを編集](assets/tabular-data/tabular-data-edit-redirects.png)

   * **ソース**&#x200B;は web サイトのドメインに対して相対的なものなので、相対パスのみが含まれます。
   * **宛先**&#x200B;は、別の web サイトにリダイレクトする場合は完全修飾 URL、独自の web サイト内でリダイレクトする場合は相対パスにすることができます。
   * Tab キーを使用して、フォーカスを次のセルに移動します。
   * エディターは、必要に応じて、新しい行をスプレッドシートに追加します。
   * 行を削除または移動するには、各行の末尾にある「**削除**」アイコンと、各行の先頭にあるドラッグハンドルを使用します。

## スプレッドシート・データのインポート {#importing}

AEM ページエディターでのスプレッドシートの編集に加えて、CSV ファイルからデータを読み込むこともできます。

1. AEMでスプレッドシートを編集する際に、画面の左上にある **アップロード** ボタンをタップまたはクリックします。
1. ドロップダウンで、データの読み込み方法を選択します。
   * **ドキュメントを置換**：スプレッドシート全体のコンテンツを、アップロードする CSV ファイルのコンテンツに置き換えます。
   * **ドキュメントに追加**：アップロードする CSV ファイルのデータを既存のスプレッドシートコンテンツに追加します。
1. 開いたダイアログで、CSV ファイルを選択して「**開く** をタップまたはクリックします。

読み込みが処理されると、ダイアログが開きます。 完了すると、CSV ファイルのデータがスプレッドシートのコンテンツに追加または置き換えられます。 列の不一致などのエラーが発生した場合は、CSV ファイルを修正できるようにレポートされます。

>[!NOTE]
>
>* CSV ファイルの見出しは、スプレッドシートの列と完全に一致する必要があります。
>* CSV 全体を読み込んでも、列見出しは変更されず、コンテンツ行のみが変更されます。
>* 列を更新する必要がある場合は、CSV のインポートを実行する前に、AEM ページエディターで更新を行う必要があります。
>* CSV ファイルの読み込みサイズは 10 MB 以下にする必要があります。

選択した `mode` に応じて、次のような CSV および cURL コマンドを使用して、スプレッドシートに `create`、`replace` または `append` を付けることもできます。

```text
curl --request POST \
  --url http://<aem-instance>/bin/asynccommand \
  --header 'content-type: multipart/form-data' \
  --form file=@/path/to/your.csv \
  --form spreadsheetPath=/content/<your-site>/<your-spreadsheet> \
  --form 'spreadsheetTitle=Your Spreadsheet' \
  --form cmd=spreadsheetImport \
  --form operation=asyncSpreadsheetImport \
  --form _charset_=utf-8 \
  --form mode=append
```

この呼び出しにより、ジョブ ID に関する情報を含むHTMLページが返されます。

```text
Message | Job(Id:2024/9/18/15/27/5cb0cacc-585d-4176-b018-b684ad2dfd02_90) created successfully. Please check status at Async Job Status Navigation.
```

[**ジョブ** コンソールを使用 ](/help/operations/asynchronous-jobs.md) して、ジョブのステータスを表示したり、返された ID を使用してジョブをクエリしたりできます。

```text
https://<aem-instance>/bin/asynccommand?optype=JOBINF&jobid=2024/10/24/14/1/8da63f9e-066b-4134-95c9-21a9c57836a5_1
```

## スプレッドシートの paths.json の公開 {#paths-json}

AEM でスプレッドシートのデータを公開するには、さらにプロジェクトの `paths.json` ファイルを更新する必要があります。

1. GitHub でプロジェクトのルートを開きます。

1. `paths.json` ファイルをタップまたはクリックして詳細を開き、「**編集**」アイコンをタップまたはクリックします。

   ![paths.json file](assets/tabular-data/tabular-data-paths-json.png)

1. 新しいスプレッドシートを `redirects.json` リソースにマップする行を追加します。

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/redirects:/redirects.json"
     ]
   }
   ```

   >[!NOTE]
   >
   >この `paths.json` エントリは、表形式のデータを使用してリダイレクトを作成する例に基づいています。 作成するスプレッドシートの [ タイプ ](#other) に適したパスを必ず更新してください。

1. 「**変更をコミット…**」をクリックして、変更を `main` に保存します。

   * `main` にコミットするか、プロセスに従ってプルリクエストを作成します。

1. リダイレクトの定義が完了し、パスマッピングを更新したら、**Sites** コンソールに戻ります。

1. コンソールで作成したリダイレクトスプレッドシートをタップまたはクリックして選択し、アクションバーの「**クイック公開**」をタップまたはクリックして、スプレッドシートを公開します。

   ![Sites コンソールでのスプレッドシートの選択](assets/tabular-data/tabular-data-select-publish.png)

1. **クイック公開**&#x200B;ダイアログで、「**公開**」をタップまたはクリックします。

   ![公開の確認](assets/tabular-data/tabular-data-quick-publish.png)

1. バナーで公開を確認します。

   ![バナーによる公開の確認](assets/tabular-data/tabular-data-publish-banner.png)

リダイレクトスプレッドシートが公開され、公にアクセスできるようになりました。

>[!TIP]
>
>Edge Delivery Servicesマッピングについて詳しくは、「パスのパスマッピング [ のドキュメントを参照してください。](/help/edge/wysiwyg-authoring/path-mapping.md)

## その他のスプレッドシートタイプ {#other}

リダイレクトスプレッドシートの作成方法がわかったので、他の標準的なスプレッドシートタイプを作成できます。

* プレースホルダー
* メタデータ
* ヘッダー
* 設定
* [分類](/help/edge/wysiwyg-authoring/taxonomy.md)

「[スプレッドシートを作成](#spreadsheet)」および「[paths.json を更新](#paths-json)」セクションと同じ手順に従い、適切なテンプレートを選択して、`paths.json` ファイルを適切に更新します。

「[設定](https://www.aem.live/docs/configuration)」、「[ヘッダー](https://www.aem.live/docs/custom-headers)」、「[メタデータ](https://www.aem.live/docs/bulk-metadata)」については、デフォルトの場所に公開するためのマッピングを必ず追加してください。

* 設定：`/.helix/config.json`
* ヘッダー：`/.helix/headers.json`
* メタデータ：`/metadata.json`
* 分類：詳しくは、分類データの管理 [ ドキュメントを参照し ](/help/edge/wysiwyg-authoring/taxonomy.md) ください。

また、任意の列を含む[独自のスプレッドシートを作成](#own-spreadsheet)して、独自に使用することもできます。

>[!NOTE]
>
>Edge Delivery Services プロジェクトで AEM as a Cloud Service のインデックス作成を管理するために、スプレッドシートを作成する必要はありません。
>
>独自のインデックスを作成する場合は、[このドキュメントに従って](https://www.aem.live/developer/indexing#setting-up-more-index-configurations)、独自の `helix-query.yaml` ファイルを作成してください。

## 独自のスプレッドシートの作成 {#own-spreadsheet}

1. 「[スプレッドシートの作成](#spreadsheet)」セクションと同じ手順に従います。

1. テンプレートを選択する際に、「**スプレッドシート**」を選択します。

1. ウィザードの「**プロパティ**」タブを使用して、独自の列を追加できます。

   ![独自の列を追加](assets/tabular-data/tabular-data-own-spreadsheet.png)

   * 「**列**」セクションで、「**追加**」をタップまたはクリックして新しい列を追加します。
   * 列の名前を指定します。
   * 列を削除または再編成するには、「**削除**」アイコンおよびドラッグハンドルアイコンを使用します。

1. リダイレクトスプレッドシートの指示に従って、スプレッドシートを作成し、公開します。

1. リダイレクトスプレッドシートの指示に従って、マッピングを `paths.json` ファイルに追加します。

