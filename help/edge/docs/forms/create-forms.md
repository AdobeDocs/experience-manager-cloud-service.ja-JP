---
title: アダプティブフォームブロックを使用したフォームの作成
description: AEM Forms の Edge Delivery Services の基本について学びます。完璧なフォームを素早く作成しましょう。AEM Forms Edge Delivery ドキュメントベースのオーサリング = 超高速かつ SEO に対応したフォームで、高い顧客満足度と検索エンジンを実現します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: 67416999d068af6350748d610e7c1c7b1d991bc4
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 97%

---

# アダプティブフォームブロックを使用したフォームの作成

>[!VIDEO](https://video.tv.adobe.com/v/3427881?quality=12&learn=on)

AEM Forms Edge Delivery には、アダプティブフォームブロックと呼ばれるブロックが用意されており、フォームを簡単に作成して、キャプチャしたデータを保存するのに役立ちます。 [アダプティブフォームブロックで事前設定された新しい AEM プロジェクトを作成](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) するか、[アダプティブフォームブロックを既存の AEM プロジェクトに追加](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)できます。

これらのフォームは、Microsoft Excel または Google Sheets ファイルに直接データを送信します。これにより、Google Sheets、Microsoft Excel、Microsoft SharePoint の活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

![ドキュメントベースのオーサリングエコシステム](/help/edge/assets/document-based-authoring-workflow-create-form.png)


## 前提条件

開始する前に、次の手順が完了していることを確認してください。

* [AEM Forms ボイラープレートを使用した AEM プロジェクト](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)を設定するか、[アダプティブフォームブロックを既存の AEM プロジェクトに追加](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)して、ローカルマシン上に対応する GitHub リポジトリのクローンを作成します。
<!--In this document, the local folder of your Edge Delivery Services (EDS) project is referred as `[EDS Project repository]`.  -->
* Google Sheets または Microsoft SharePoint へのアクセス権があることを確認します。 Microsoft SharePoint をコンテンツソースとして設定するには、[SharePoint の使用方法](https://www.aem.live/docs/setup-customer-sharepoint)を参照してください。



## フォームの作成

<!--
+++ Step 1: Add the Adaptive Forms Block to your Edge Delivery Services (EDS) project.

The Adaptive  empowers users to create forms for an Edge Delivery Service Site. However, this block isn't included in the default AEM boilerplate (used to create an Edge Delivery Services project). To seamlessly integrate the Adaptive Forms Block into your Edge Delivery Services project:

1. **Clone the Adaptive Forms Block repository**: Clone the [Adaptive Forms Block repository](https://github.com/adobe-rnd/form-block) on your local machine. It contains the code to render the form on an EDS webpage. In this document, the local folder of your Forms Block repository is referred as `[Adaptive Forms Block repository]`.
2. **Locate the Adaptive Forms Block Repository:** Access the [Adaptive Forms Block repository]/blocks/src folder and copy its content. 

3. on your local machine and copy the `form` folder. 
4. **Paste the Adaptive Forms Block's code into your EDS Project:**
Navigate to the [EDS Project repository]/blocks/ folder on your local machine and create a 'form' folder. Paste the `[Adaptive Forms Block repository]/blocks/src content`, copied in perevious step to the `[EDS Project repository]/blocks/form` folder.
1. **Commit Changes to GitHub:** Check in the `[EDS Project repository]/blocks/form` folder and its underlying files to your Edge Delivery Services project on GitHub.

After completing these steps, the Adaptive Forms Block is successfully added to your Edge Delivery Services (EDS) project repository on GitHub. You can now create and add forms to a EDS Sites page.
 

**Troubleshooting GitHub build issues**

Ensure a smooth GitHub build process by addressing potential issues:

* **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file.

* **Handle Linting Errors:**
    Should you come across any linting errors, you can bypass them. Open the [EDS Project]/package.json file and modify the "lint" script from "lint": "npm run lint:js && npm run lint:css" to "lint": "echo 'skipping linting for now'". Save the file and commit the changes to your GitHub project. -->

+++ 手順 1：Microsoft Excel または Google Sheets を使用してフォームを作成します。

複雑なプロセスを進める代わりに、スプレッドシートを使用してフォームを簡単に作成できます。 フォーム構造を構成する行と列を定義できます。 各行は、個々の[フォームフィールド](/help/edge/docs/forms/form-components.md#available-components)を表し、列ヘッダーは対応する[フィールドプロパティ](/help/edge/docs/forms/form-components.md#components-properties)を定義します。

例えば、行が[お問い合わせ](/help/edge/assets/enquiry.xlsx)スプレッドシートのフィールドの概要を示し、列ヘッダーがそのプロパティを定義する次のスプレッドシートを考えてみましょう。

![照会スプレッドシート](/help/edge/assets/enquiry-form-spreadsheet.png)

フォームの作成を続行するには、以下の手順を実行します。

1. Microsoft SharePoint または Google Drive の AEM Edge Delivery プロジェクトフォルダーにアクセスします。

1. AEM Edge Delivery プロジェクトディレクトリ内の任意の場所で、Microsoft Excel ワークブックまたは Google シートを作成します。 例えば、Google Drive の AEM Edge Delivery プロジェクトディレクトリに `enquiry` という名前のスプレッドシートを作成します。

   <!-- ![Sample Content on Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)-->

1. [プロジェクトに指定された設定に従って](https://www.aem.live/docs/setup-customer-sharepoint)、シートが適切な AEM ユーザー（`forms@adobe.com` など）と共有されていることを確認します。 ユーザにシートの編集権限を付与します。

1. 作成したスプレッドシートを開き、デフォルトのシートの名前を「shared-aem」に変更します。

   ![デフォルトのシート名を「shared-default」に変更](/help/edge/assets/rename-sheet-to-shared-default.png)

   >[!IMPORTANT]
   >
   >**フォームを作成するシートには、名前の付け方に制限があります。 シート名として使用できるのは `helix-default` と `shared-aem` のみです。**

1. フォームフィールドを追加するには、行と列のヘッダーを「shared-aem」シートに挿入します。各行は、[フォームフィールド](/help/edge/docs/forms/form-components.md#available-components)を表し、列ヘッダーが対応するフィールドの[プロパティ](/help/edge/docs/forms/form-components.md#components-properties)を定義する必要があります。


   すぐに開始するには、[照会スプレッドシート](/help/edge/assets/enquiry.xlsx)の内容を、お使いのスプレッドシートにコピーすることを検討してください。 内容をコピーした後、スプレッドシートを保存します。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用してシートをプレビューします。

   ![AEM Sidekick を使用してシートをプレビュー](/help/edge/assets/preview-form.png)

   プレビュー時に、新しいブラウザータブにシートの内容が JSON 形式で表示されます。 プレビュー URL を取り込む必要があります。これは、次のセクションでフォームをレンダリングする際に必要です。 URL 形式は次のとおりです。


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form-path>/<form-file-name>.json
   ```

   * `<branch>` は、GitHub リポジトリのブランチを参照します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。

   例えば、プロジェクトのリポジトリの名前が「wefinance」で、アカウント「wkndform」の下にあり、「main」分岐を使用している場合、URL は次のようになります。

`https://main--wefinance--wkndform.aem.page/enquiry.json`
&lt;!--(https://main--wefinance--wkndform.aem.page/enquiry.json)-->


+++

+++ 手順 2：Edge Delivery Services ページを使用してフォームをプレビュー。


ここまでで、フォームの構造の準備が整いました。 フォームをプレビューする手順は次のとおりです。

1. Microsoft SharePoint または Google Drive アカウントを開き、AEM Edge Delivery プロジェクトディレクトリに移動します。



1. フォームを埋め込むドキュメントファイル（インデックスファイルなど）を開きます。 または、[新しいドキュメントを作成](/help/edge/assets/enquiry-form.docx)することもできます。

1. フォームを追加するドキュメント内の目的の場所に移動します。

1. フォームをレンダリングするフォームブロックを作成します。 挿入／テーブルを選択し、1 列 2 行のテーブルを作成します。 テーブルに「Form」という名前を付け、2 行目にプレビュー URL をペーストします。 以下に示すように、URL がプレーンテキストではなく、ハイパーリンクとして書式設定されていることを確認します。

   | フォーム |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |


   ![アダプティブフォームブロックを web ページに追加](/help/edge/assets/enquiry-doc-to-embed-form.png)

   このブロックは、フォームが埋め込まれるプレースホルダーとして機能します。 ブロックの 2 行目に、`<form>.json` ファイルのプレビュー URL をハイパーリンクとして追加します。

   >[!IMPORTANT]
   >
   >
   > URL がプレーンテキストとして表示されるのではなく、ハイパーリンクとして書式設定されていることを確認します。


1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用してドキュメントをプレビューします。 これで、ページにフォームが表示されます。 例えば、[照会スプレッドシート](/help/edge/assets/enquiry-form.docx)に基づくフォームは次のとおりです。


   [![EDS フォームのサンプル](/help/edge/assets/updated-form.png)](https://main--wefinance--wkndform.aem.page/enquiry-form)

   ここで、フォームに入力して送信ボタンをクリックすると、スプレッドシートがまだデータを受け入れるように設定されていないので、次のようなエラーが発生します。

   ![フォーム送信時のエラー](/help/edge/assets/form-error.png)

+++


## 次の手順

フォーム送信時にデータの受け入れを開始できるように[スプレッドシートを準備](/help/edge/docs/forms/submit-forms.md)します。


## 関連トピック

{{see-more-forms-eds}}
