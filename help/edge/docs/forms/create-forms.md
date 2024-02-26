---
title: AEM Forms Edge Delivery Service の概要
description: クラフトパーフェクトフォーム、高速！ ⚡ AEM Forms Edge Delivery ドキュメントベースのオーサリング=超高速で SEO に対応したフォームで、より幸せなユーザーと検索エンジンを実現。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 4a3ebcf7985253ebca24e90ab57ae7eaf3e924e9
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 1%

---


# AEM Forms Edge Delivery Service でのフォームの作成

今日のデジタル時代では、どの組織でも、使いやすいフォームを作成することが不可欠です。 AEM Forms Edge Delivery を使用すると、Word やGoogle Docs などの使い慣れたツールを使用してフォームを作成できます。

これらのフォームは、Microsoft Excel またはGoogleシートファイルに直接データを送信します。Googleシート、Microsoft Excel、Microsoft Sharepoint の活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

AEM Forms Edge Delivery は、フォームを簡単に作成して、取り込んだデータを取り込み、保存するのに役立つフォームブロックを提供します。 AEM EDS プロジェクトにフォームブロックを含めて、フォームの作成を開始できます。 では、開始しましょう。


## 前提条件

開始する前に、次の手順が完了していることを確認します。

* AEMボイラープレートを使用して Edge Delivery Service(EDS)GitHub プロジェクトを設定し、対応する GitHub リポジトリのクローンをローカルマシンに作成します。 詳しくは、 [開発者向けチュートリアル](https://www.aem.live/developer/tutorial) 」を参照してください。 このドキュメントでは、Edge Delivery Service(EDS) プロジェクトのローカルフォルダーを `[EDS Project repository]` .
* のクローン [Forms Block リポジトリ](https://github.com/adobe/afb) ローカルマシン上にある。 EDS Web ページ上でフォームをレンダリングするコードを含みます。 このドキュメントでは、Formsブロックリポジトリのローカルフォルダーを `[Forms Block repository]`.
* Google Sheet またはMicrosoft SharePointへのアクセス権があることを確認します。


## フォームの作成

+++ 手順 1:Edge Delivery Service(EDS) プロジェクトにフォームブロックを追加します。

The `Form block` には、EDS サイトにフォームを追加する機能が含まれています。 このブロックは、AEMボイラープレートを使用して作成されたプロジェクトに含まれていません。 フォームブロックを Edge Delivery Service プロジェクトに含めるには：

1. 次に移動： `[Forms Block repository]/blocks` ローカルマシン上のフォルダーにコピーし、 `form` フォルダー。

1. 次に移動： `[EDS Project repository]/blocks/` ローカルマシン上のフォルダーにコピーし、 `form` フォルダー。

1. チェックイン： `form` フォルダーおよび基になるファイルを、GitHub の Edge Delivery Service プロジェクトに追加します。

   Form ブロックが GitHub の EDS プロジェクトリポジトリに追加されます。 GitHub のビルドに失敗しないことを確認します。

   * 「モジュール「../../scripts/lib-franklin.js」へのパスを解決できません」というエラーが発生した場合は、 `[EDS Project]/blocks/forms/form.js` ファイル。 import 文で、 `lib-franklin.js` ファイルに `aem.js` ファイル。

   * リントエラーが発生した場合は、それらを無視してください。 リンクチェックを回避するには、 `[EDS Project]\package.json` ファイルを作成し、次の「lint」スクリプトを更新します： `"lint": "npm run lint:js && npm run lint:css"` から `"lint": "echo 'skipping linting for now'"`. ファイルを保存し、GitHub プロジェクトにコミットします。

これで、フォームを作成して、サイトに追加できます。

+++

+++ 手順 2:Microsoft Excel またはGoogleシートを使用してフォームを作成する。

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

+++ 手順 3:Edge Delivery Service(EDS) ページを使用してフォームをプレビューします。


これまで、フォームブロックを EDS プロジェクトに追加し、フォームの構造を準備しました。 次に、フォームをプレビューします。

1. Microsoft SharePointまたはGoogle Drive アカウントに移動し、AEM Edge Delivery プロジェクトディレクトリを開きます。

1. ドキュメントファイルを開き、フォームを埋め込みます。 例えば、インデックスファイルを開きます。 また、新しいドキュメントファイルを作成することもできます。

1. フォームを追加するドキュメント内の目的の場所に移動します。

1. 以下に示すように、「Form」という名前のブロックをファイルに追加します。

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   2 番目の行に、前の節で記録した URL をハイパーリンクとして含めます。 開発やテストの目的ではプレビュー URL(.page URL) を、実稼動環境では公開 URL(.live) を使用します。

   >[!IMPORTANT]
   >
   >
   > URL がプレーンテキストとして表示されるのではなく、ハイパーリンクされていることを確認します。


1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、ページをプレビューします。 これで、ページにフォームが表示されます。

   例えば、次に、 [お問い合わせスプレッドシート](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![EDS フォームのサンプル](/help/edge/assets/eds-form.png)

   次に、フォームに入力して送信ボタンをクリックすると、スプレッドシートがまだデータを受け入れるように設定されていないので、次のようなエラーが発生します。

   ![フォーム送信エラー](/help/edge/assets/form-error.png)

+++


## 次の手順

[スプレッドシートを準備する](/help/edge/docs/forms/submit-forms.md) フォーム送信時にデータの受け入れを開始する



## 詳細を表示する

* [フォームフィールドのプロパティ](/help/edge/docs/forms/eds-form-field-properties)
* [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
* [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
* [サイトページにフォームを発行する](/help/edge/docs/forms/publish-eds-forms.md)
* [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
* [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)
