---
title: AEM Forms Edge Delivery Service の概要
description: クラフトパーフェクトフォーム、高速！ ⚡ AEM Forms Edge Delivery ドキュメントベースのオーサリング=超高速で SEO に対応したフォームで、より幸せなユーザーと検索エンジンを実現。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 7b497791c70fd588b7e8c9a94caa218189d3153a
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 2%

---


# AEM Forms Edge Delivery Service でのフォームの作成

今日のデジタル時代では、どの組織でも、使いやすいフォームを作成することが不可欠です。 AEM Forms Edge Delivery を使用すると、Word やGoogle Docs などの使い慣れたツールを使用してフォームを作成できます。

これらのフォームは、Microsoft Excel またはGoogleシートファイルに直接データを送信します。Googleシート、Microsoft Excel、Microsoft Sharepoint の活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

## 前提条件

* 既に GitHub アカウントを持っています。
* Google Sheet またはMicrosoft SharePointにアクセスできます。
* Git、HTML、CSS および JavaScript の基本を理解します。
* ローカル開発用に Node と NPM がインストールされている。

## 事前準備

* Edge Delivery Service(EDS) プロジェクトをセットアップして複製します。 詳しくは、 [開発者向けチュートリアル](https://www.aem.live/developer/tutorial) 」を参照してください。
* のクローン [Forms Block リポジトリ](https://github.com/adobe/afb).

  ![Edge Delivery Formsの概要](/help/edge/assets/getting-started-with-eds-forms.png)


## フォームの作成


+++ 手順 1:Edge Delivery Service(EDS) プロジェクトにフォームブロックを追加します。

AEM Forms Edge Delivery には、取り込んだデータを取り込んで保存するフォームを簡単に作成できるフォームブロックが含まれています。 フォームブロックを Edge Delivery Service プロジェクトに含めるには：

1. に移動します。 `[cloned Forms Block repository folder]`/blocks/.

1. をコピーします。 `forms` フォルダー `[Cloned EDS Project repository folder]\blocks` フォルダー。

1. 「form」フォルダーとその下にあるファイルを、GitHub の Edge Delivery Service プロジェクトにチェックインします。

   ```Shell
   cd ..
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   Form ブロックが EDS プロジェクトに追加されます。 これで、フォームを作成して、サイトに追加できます。

   >[!NOTE]
   >
   > * 「モジュール「../../scripts/lib-franklin.js」へのパスを解決できません」というエラーが発生した場合は、 `[EDS Project]/blocks/forms/form.js` ファイル。 import 文で、 `lib-franklin.js` ファイルに `aem.js` ファイル。
   > * リントエラーが発生した場合は、それらを無視してください。 リンクチェックを回避するには、 `[EDS Project]\package.json` ファイルを作成し、次の「lint」スクリプトを更新します： `"lint": "npm run lint:js && npm run lint:css"` から `"lint": "echo 'skipping linting for now'"`. ファイルを保存し、GitHub プロジェクトにコミットします。

+++

+++ 手順 2:Microsoft Excel またはGoogleシートを使用してフォームを作成する


複雑なプロセスの代わりに、スプレッドシートを使用して簡単にフォームを作成できます。 まず、行と列のヘッダーをスプレッドシートに追加します。各行でフォームフィールドが定義され、各列ヘッダーで対応するフォームフィールドのプロパティが定義されます。

例えば、次のスプレッドシートでは、行が `contact us` フォームおよび列ヘッダーは、対応するフィールドのプロパティを定義します。

![お問い合わせスプレッドシート](/help/edge/assets/contact-us-form-spreadsheet.png)

フォームを作成するには：

1. Microsoft SharePointまたはGoogle Drive のAEM Edge Delivery プロジェクトフォルダーを開きます。

1. AEM Edge Delivery プロジェクトディレクトリの下の任意の場所で、Microsoft Excel ワークブックまたはGoogleシートを作成します。 例えば、 `contact-us` (Google Drive のAEM Edge Delivery プロジェクトディレクトリ )

1. シートがAEMユーザーと共有されていることを確認します ( 例： `helix@adobe.com`) [プロジェクト用に設定](https://www.aem.live/docs/setup-customer-sharepoint) およびユーザーはシートの編集権限を持っています。

1. 作成したスプレッドシートを開き、デフォルトのシートの名前を「shared-default」に変更します。

   ![既定のシートの名前を&quot;shared-default&quot;に変更](/help/edge/assets/rename-sheet-to-shared-default.png)

1. フォームのフィールドを追加するには、行と列のヘッダーを `shared-default` シート。各行でフォームフィールドが定義され、各列ヘッダーで [プロパティ](/help/edge/docs/forms/eds-form-field-properties)) をクリックします。

   すばやく開始するには、 [お問い合わせスプレッドシート](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) をスプレッドシートに追加します。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)

1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、シートをプレビューおよびパブリッシュします。

   ![AEM Sidekickを使用してシートをプレビューおよびパブリッシュします。](/help/edge/assets/preview-form.png)

   プレビューと公開時に、ブラウザーが新しいタブを開き、シートの内容が JSON 形式で表示されます。 後でフォームをレンダリングする際に必要になるので、ライブ URL を必ずメモしておきます。

   URL の形式は次の通りです。

   ```JSON
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

+++

+++ 手順 3:Edge Delivery Service(EDS) ページを使用してフォームをプレビューする


これまで、EDS プロジェクトのフォームブロックを有効にし、フォームの構造を準備しました。 次に、フォームをプレビューします。

1. Microsoft SharePointまたはGoogle Drive アカウントに移動し、AEM Edge Delivery プロジェクトディレクトリを開きます。

1. ドキュメントファイルを開き、フォームを埋め込みます。 例えば、インデックスファイルを開きます。 新しいファイルを作成することもできます。

1. フォームを追加するドキュメント内の目的の場所に移動します。

1. 以下に示すように、「Form」という名前のブロックをファイルに追加します。

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   2 行目には、前の節で説明した URL をハイパーリンクとして含めます。 プレビュー URL(.page URL) または公開 URL(.live) を使用できます。 プレビュー URL は、フォームの構築またはテスト時に使用し、実稼動用に発行 URL を使用できます。

   >[!IMPORTANT]
   >
   >
   > URL がプレーンテキストとして言及されていないことを確認します。 ハイパーリンクとして追加する必要があります。

1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、ページをプレビューします。 これで、ページにフォームが表示されます。 例えば、次に、 [お問い合わせスプレッドシート](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![EDS フォームのサンプル](/help/edge/assets/eds-form.png)

   次に、フォームに入力して送信ボタンをクリックすると、スプレッドシートがまだデータを受け入れるように設定されていないので、次のようなエラーが発生します。

   ![フォーム送信エラー](/help/edge/assets/form-error.png)

+++


## 次の手順

次の手順は、 [データを受け入れるためのスプレッドシートの準備](/help/edge/docs/forms/submit-forms.md).



## 詳細を表示する

* [フォームフィールドのプロパティ](/help/edge/docs/forms/eds-form-field-properties)
* [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
* [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
* [サイトページにフォームを発行する](/help/edge/docs/forms/publish-eds-forms.md)
* [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
* [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)
