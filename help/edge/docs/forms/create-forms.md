---
title: AEM Forms Edge Delivery Service の概要。 フォームを作成します。
description: クラフトパーフェクトフォーム、高速！ ⚡ AEM Forms Edge Delivery ドキュメントベースのオーサリング=超高速で SEO に対応したフォームで、より幸せなユーザーと検索エンジンを実現。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 68b60d33e6ccfe27452cfea76603e4d7d29f0c6e
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---


# アダプティブフォームブロックを使用したフォームの作成

今日のデジタル時代では、どの組織でも、使いやすいフォームを作成することが不可欠です。 AEM Forms Edge Delivery を使用すると、Word やGoogle Docs などの使い慣れたツールを使用してフォームを作成できます。

これらのフォームは、Microsoft Excel またはGoogleシートファイルに直接データを送信します。Googleシート、Microsoft Excel、Microsoft Sharepoint の活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

![ドキュメントベースのオーサリングエコシステム](/help/edge/assets/document-based-authoring.png)

AEM Forms Edge Delivery には、アダプティブフォームブロックと呼ばれるブロックが用意されており、これを使用すると、キャプチャしたデータを取得して保存するためのフォームを簡単に作成することができます。 アダプティブフォームブロックをAEM EDS プロジェクトに含めて、フォームの作成を開始できます。 では、開始しましょう。


## 前提条件

開始する前に、次の手順が完了していることを確認します。

* AEMボイラープレートを使用して Edge Delivery Service(EDS)GitHub プロジェクトを設定し、対応する GitHub リポジトリのクローンをローカルマシンに作成します。 詳しくは、 [開発者向けチュートリアル](https://www.aem.live/developer/tutorial) 」を参照してください。 このドキュメントでは、Edge Delivery Service(EDS) プロジェクトのローカルフォルダーを `[EDS Project repository]` .
* Google Sheet またはMicrosoft SharePointへのアクセス権があることを確認します。 Microsoft SharePointをコンテンツソースとして設定するには、 [SharePoint の使用方法](https://www.aem.live/docs/setup-customer-sharepoint)



## フォームの作成

+++ 手順 1：アダプティブフォームブロックを Edge Delivery Service(EDS) プロジェクトに追加します。

アダプティブを使用すると、ユーザーはエッジ配信サービスサイトのフォームを作成できます。 ただし、このブロックは、デフォルトのAEMボイラープレート（Edge Delivery Service プロジェクトの作成に使用）には含まれていません。 アダプティブフォームブロックを Edge 配信サービスプロジェクトにシームレスに統合するには、次の手順を実行します。

1. **アダプティブフォームブロックリポジトリの複製**：を複製します。 [アダプティブフォームブロックリポジトリ](https://github.com/adobe/afb) ローカルマシン上にある。 EDS Web ページ上でフォームをレンダリングするコードを含みます。 このドキュメントでは、Formsブロックリポジトリのローカルフォルダーを `[Adaptive Form block repository]`.
1. **アダプティブフォームブロックリポジトリを探します。** 次にアクセス： [アダプティブフォームブロックリポジトリ]/blocks フォルダーをローカルマシン上に置き、 `form` フォルダー。
1. **アダプティブフォームブロックを EDS プロジェクトに貼り付けます。**
次に移動： [EDS プロジェクトリポジトリ]/blocks/フォルダーをローカルマシンに貼り付け、フォームフォルダーを貼り付けます。
1. **変更を GitHub にコミット：** フォームフォルダーとその基になるファイルを、GitHub の Edge Delivery Service プロジェクトにチェックインします。

これらの手順を完了すると、アダプティブフォームブロックが GitHub の Edge Delivery Service(EDS) プロジェクトリポジトリに正常に追加されます。 EDS サイトページにフォームを作成し、追加できるようになりました。


**GitHub ビルドの問題のトラブルシューティング**

潜在的な問題に対処し、GitHub のビルドプロセスをスムーズに進めます。

* **モジュールパスの解決エラー：**
「モジュール「../../scripts/lib-franklin.js」へのパスを解決できません」というエラーが発生した場合は、 [EDS プロジェクト]/blocks/forms/form.jsファイルを参照してください。 lib-franklin.js ファイルを aem.js ファイルに置き換えて、import 文を更新します。

* **リントエラーを処理：**
リントエラーが発生した場合は、それらを回避できます。 を開きます。 [EDS プロジェクト]/package.jsonファイルを編集し、&quot;lint&quot;スクリプトを&quot;lint&quot;: &quot;npm run lint:js &amp;&amp; npm run lint:css&quot;から&quot;lint&quot;: &quot;echo &#39;今すぐのリントをスキップ&#39;&quot;に変更します。 ファイルを保存し、変更を GitHub プロジェクトにコミットします。



+++

+++ 手順 2:Microsoft Excel またはGoogleシートを使用してフォームを作成する。

複雑なプロセスを進める代わりに、スプレッドシートを使用してフォームを簡単に作成できます。 まず、行と列のヘッダーをスプレッドシートに追加します。スプレッドシートの各行はフォームフィールドを表し、各列ヘッダーは対応するフィールドのプロパティを定義します。

例えば、行が `enquiry` フォームヘッダーと列ヘッダーは、プロパティを定義します。

![照会スプレッドシート](/help/edge/assets/enquiry-form-spreadsheet.png)

フォームの作成を続行するには：

1. Microsoft SharePointまたはGoogle Drive のAEM Edge Delivery プロジェクトフォルダーにアクセスします。

1. AEM Edge Delivery プロジェクトディレクトリ内の任意の場所で、Microsoft Excel ワークブックまたはGoogleシートを作成します。 例えば、 `enquiry` (Google Drive のAEM Edge Delivery プロジェクトディレクトリ )

1. シートが適切なAEMユーザー ( 例： `helix@adobe.com`) [プロジェクトに指定された設定に従って](https://www.aem.live/docs/setup-customer-sharepoint). ユーザにシートの編集権限を付与します。

1. 作成したスプレッドシートを開き、デフォルトのシートの名前を「shared-default」に変更します。

   ![既定のシートの名前を&quot;shared-default&quot;に変更](/help/edge/assets/rename-sheet-to-shared-default.png)

1. フォームフィールドを追加するには、行と列のヘッダーを「shared-default」シートに挿入します。 各行は、 [フォームフィールド](/help/edge/docs/forms/form-components.md)を作成し、対応するフィールドを定義する列ヘッダーを含めます。 [プロパティ](/help/edge/docs/forms/eds-form-field-properties).

   すぐに開始するには、 [照会スプレッドシート](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0) をスプレッドシートに追加します。 内容をコピーした後、スプレッドシートを保存します。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、シートをプレビューします。

   ![AEM Sidekickを使用してシートをプレビュー](/help/edge/assets/preview-form.png)

   プレビュー時に、新しいブラウザタブにシートのコンテンツが JSON 形式で表示されます。 プレビュー URL を取り込む必要があります。これは、次のセクションでフォームをレンダリングする際に必要なものです。 URL 形式は次のとおりです。


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` は、GitHub リポジトリのブランチを参照します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。

   例えば、プロジェクトのリポジトリの名前が「portal」の場合、リポジトリは「wkndforms」アカウントの下に配置され、「main」ブランチを使用している場合、URL は次のようになります。

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ 手順 3:Edge Delivery Service(EDS) ページを使用してフォームをプレビューします。


これまで、アダプティブフォームブロックを EDS プロジェクトに追加し、フォームの構造を準備しました。 次に、フォームをプレビューします。

1. **プロジェクトディレクトリにアクセスする：** Microsoft SharePointまたはGoogle Drive アカウントを開き、 AEM Edge Delivery プロジェクトディレクトリに移動します。

1. **フォームをドキュメントに埋め込む：** フォームを埋め込むドキュメントファイル（インデックスファイルなど）を開きます。 または、新しいドキュメントを作成できます。

1. **目的の場所に移動します。** フォームを追加するドキュメント内の目的の場所に移動します。

1. **アダプティブフォームブロックを追加します。** 次の図に示すように、ファイルに「Form」という名前のブロックを挿入します。

   | フォーム |
   |---|
   | [https://main—portal—wkndforms.hlx.live/inquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   このブロックは、フォームが埋め込まれるプレースホルダーとして機能します。 ブロックの 2 行目に、 `<form>.json` ファイルをハイパーリンクとして保存します。

   >[!IMPORTANT]
   >
   >
   > URL がプレーンテキストで表示されるのではなく、ハイパーリンクとしてフォーマットされていることを確認します。


1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックしてドキュメントをプレビューします。 これで、ページにフォームが表示されます。 例えば、次に、 [照会スプレッドシート](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![EDS フォームのサンプル](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   次に、フォームに入力して送信ボタンをクリックすると、スプレッドシートがまだデータを受け入れるように設定されていないので、次のようなエラーが発生します。

   ![フォーム送信エラー](/help/edge/assets/form-error.png)

+++


## 次の手順

[スプレッドシートを準備する](/help/edge/docs/forms/submit-forms.md) フォーム送信時にデータの受け入れを開始する



## 詳細を表示する

* [フォームコンポーネント](/help/edge/docs/forms/form-components.md)
* [フォームフィールドのプロパティ](/help/edge/docs/forms/eds-form-field-properties)
* [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
* [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
* [サイトページにフォームを発行する](/help/edge/docs/forms/publish-eds-forms.md)
* [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
* [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)
