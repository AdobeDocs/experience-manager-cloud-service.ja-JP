---
title: AEM Forms Edge Delivery Service の概要
description: クラフトパーフェクトフォーム、高速！ ⚡ AEM Forms Edge Delivery ドキュメントベースのオーサリング=超高速で SEO に対応したフォームで、より幸せなユーザーと検索エンジンを実現。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f37a99cd5cbfb745cb591e3be2a46a5f52139cb2
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---


# AEM Forms Edge Delivery Service でのフォームの作成

今日のデジタル時代では、どの組織でも、使いやすいフォームを作成することが不可欠です。 AEM Forms Edge Delivery を使用すると、Word やGoogle Docs などの使い慣れたツールを使用してフォームを作成できます。

これらのフォームは、Microsoft Excel またはGoogleシートファイルに直接データを送信します。Googleシート、Microsoft Excel、Microsoft Sharepoint の活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

## 前提条件

* GitHub アカウントを持っている。
* Google Sheet またはMicrosoft SharePointにアクセスできます。
* Git、HTML、CSS および JavaScript の基本を理解します。
* ローカル開発用に Node と NPM がインストールされている。

## 事前準備

* Edge Delivery Service(EDS) プロジェクトをセットアップして複製します。 詳しくは、 [開発者向けチュートリアル](https://www.aem.live/developer/tutorial) 」を参照してください。
* のクローン [Forms Block リポジトリ](https://github.com/adobe/afb). これには、フォームのレンダリングに必要な Form ブロックが含まれます。

![Edge Delivery Formsの概要](/help/edge/assets/getting-started-with-eds-forms.png)

## Edge Delivery Service(EDS) プロジェクトにフォームブロックを追加する {#add-forms-block-to-an-eds-project}

AEM Forms Edge Delivery には、取り込んだデータを取り込んで保存するフォームを簡単に作成できるフォームブロックが含まれています。 フォームブロックを Edge Delivery Service プロジェクトに含めるには：

1. ローカル開発環境の Edge Delivery Service(EDS) プロジェクトフォルダーに移動します。


   ```Shell
   cd [EDS Project folder]
   ```

1. という名前のフォルダーを作成します。 `form` EDS プロジェクトディレクトリの下にある。 例えば、EDS プロジェクトのディレクトリの下に、 `Portal`、という名前のフォルダーを作成します。 `form`.

   ```Shell
   mkdir form
   ```


1. 次を追加： [Forms Block](https://github.com/adobe/afb/tree/main/blocks/form) ファイルを「form」フォルダーに保存します。

   ```shell
   cp -R <source:path of the form block> <destination: path of the form folder created in the previous step>
   
   For example
   
   cp -R Documents/afb/blocks/form Documents/portal/blocks/
   ```

1. 「form」フォルダーとその下にあるファイルを、GitHub の Edge Delivery Service プロジェクトにチェックインします。

   ```Shell
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   これで、EDS フォームをレンダリングする準備が整いました。

   >[!NOTE]
   >
   > * プルリクエスト/eds プロジェクトのビルドに失敗し、 `franklin-lib.js` ファイルを参照するには、 `aem.js` の代わりにファイル `franklin-lib.js` ファイル。
   > * リントエラーが発生した場合は、それらを無視してください。 リンティングチェックを回避するには、package.json ファイルに移動し、次の場所から「lint」スクリプトを更新します。 `"lint": "npm run lint:js && npm run lint:css"` から `"lint": "echo 'skipping linting for now'"`. 次に、変更を package.json ファイルにコミットします。

## Microsoft Excel またはGoogleシートを使用したフォームの作成 {#create-a-form-for-an-eds-project}

Web サイト開発者がフォームを作成し、Web サイトの訪問者から収集する情報を選択することが役立つ場合。 作成者は複雑なプロセスではなく、スプレッドシートを使用してフォームを簡単に設定できます。 適切な列ヘッダーを追加し、フォームブロックを使用して Web サイトに表示する必要があります。 フォームを作成するには：

1. Microsoft SharePointまたはGoogle Drive のAEM Edge Delivery プロジェクトディレクトリの下の任意の場所で、Microsoft Excel ワークブックまたはGoogleシートを作成します。

1. AEMユーザー（例： ）を確認します。 `helix@adobe.com`) がプロジェクト用に設定され、シートの編集権限を持ちます。

1. 作成したブックを開き、既定のシートの名前を&quot;shared-default&quot;に変更します。

   ![既定のシートの名前を&quot;shared-default&quot;に変更](/help/edge/assets/rename-sheet-to-helix-default.png)

1. の内容をコピーします。 [お問い合わせスプレッドシート](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) を独自のスプレッドシートに追加します。

   ![お問い合わせスプレッドシート](/help/edge/assets/contact-us-form-spreadsheet.png)

1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、シートをプレビューおよびパブリッシュします。

   プレビューと公開時に、ブラウザーが新しいタブを開き、シートの内容が JSON 形式で表示されます。 後でフォームをレンダリングする際に必要になるので、ライブ URL を必ずメモしておきます。

   URL の形式は次の通りです。

   ```shell
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

## Edge Delivery Service(EDS) ページを使用してフォームをプレビューする {#add-a-form-to-your-eds-page}

これまで、EDS プロジェクトのフォームブロックを有効にし、フォームの構造を準備しました。 次に、フォームを EDS ページに含めてレンダリングします。

1. Microsoft SharePointまたはGoogle Drive のAEM Edge Delivery プロジェクトディレクトリに移動します。

1. フォームをページに追加するには、ドキュメントファイルに対応するを開きます。 例えば、インデックスファイルを開きます。

1. フォームを追加するドキュメント内の目的の場所に移動します。

1. 以下に示すように、「Form」という名前のブロックをファイルに追加します。

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   2 行目には、前の節で説明した URL をハイパーリンクとして含めます。

1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、ページをプレビューおよび公開します。 フォームがレンダリングされます。

   例えば、次に、 [お問い合わせスプレッドシート](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![お問い合わせ（EDS フォーム）](/help/edge/assets/eds-form.png)

   フォームブロックは、フォームをレンダリングしますが、データを受け入れる準備はまだできていません。 送信ボタンをクリックすると、次のようなエラーが発生します。

   ![フォーム送信エラー](/help/edge/assets/form-error.png)

   [データを受け入れるシートを準備します](/help/edge/docs/forms/submit-forms.md). データを受け入れるために、データを準備した後にシートに送信できます。


## 詳細を表示する

* [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
* [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
* [サイトページにフォームを発行する](/help/edge/docs/forms/publish-eds-forms.md)
* [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
* [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)