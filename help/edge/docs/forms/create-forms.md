---
title: AEM Forms Edge Delivery Service の概要。 フォームを作成します。
description: クラフトパーフェクトフォーム、高速！ ⚡ AEM Forms Edge Delivery ドキュメントベースのオーサリング=超高速で SEO に対応したフォームで、より幸せなユーザーと検索エンジンを実現。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: f4cf79e2cd71a390741987cfcf034e6eed02432d
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 1%

---

# アダプティブFormsブロックを使用したフォームの作成

>[!VIDEO](https://video.tv.adobe.com/v/3427881?quality=12&learn=on)

AEM Forms Edge Delivery には、アダプティブFormsブロックと呼ばれるブロックが用意されており、これを使用すると、フォームを簡単に作成して、取り込んだデータを取り込み、保存することができます。 以下が可能です。 [アダプティブFormsブロックで事前設定された新しいAEMプロジェクトを作成する](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) または [アダプティブFormsブロックを既存のAEMプロジェクトに追加する](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project).

これらのフォームは、Microsoft Excel またはGoogleシートファイルに直接データを送信します。これにより、Googleシート、Microsoft Excel、Microsoft SharePointの活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

![ドキュメントベースのオーサリングエコシステム](/help/edge/assets/document-based-authoring-workflow-create-form.png)


## 前提条件

開始する前に、次の手順が完了していることを確認します。

* を設定します。 [AEM Forms BoilerPlate を使用したAEMプロジェクト](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) または [アダプティブFormsブロックを既存のAEMプロジェクトに追加しました。](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) 対応する GitHub リポジトリをローカルマシンに複製します。
このドキュメントでは、Edge Delivery Services(EDS) プロジェクトのローカルフォルダーを `[EDS Project repository]`.
* Google Sheet またはMicrosoft SharePointへのアクセス権があることを確認します。 Microsoft SharePointをコンテンツソースとして設定するには、 [SharePointの使用方法](https://www.aem.live/docs/setup-customer-SharePoint).



## フォームの作成

<!-- 

+++ Step 1: Add the Adaptive Forms Block to your Edge Delivery Services (EDS) project.

The Adaptive  empowers users to create forms for an Edge Delivery Service Site. However, this block isn't included in the default AEM boilerplate (used to create an Edge Delivery Services project). To seamlessly integrate the Adaptive Forms Block into your Edge Delivery Services project:

1. **Clone the Adaptive Forms Block repository**: Clone the [Adaptive Forms Block repository](https://github.com/adobe-rnd/form-block) on your local machine. It contains the code to render the form on an EDS webpage. In this document, the local folder of your Forms Block repository is referred as `[Adaptive Forms Block repository]`.
1. **Locate the Adaptive Forms Block Repository:** Access the [Adaptive Forms Block repository]/blocks/src folder and copy its content. 

1. on your local machine and copy the `form` folder. 
1. **Paste the Adaptive Forms Block's code into your EDS Project:**
Navigate to the [EDS Project repository]/blocks/ folder on your local machine and create a 'form' folder. Paste the `[Adaptive Forms Block repository]/blocks/src content`, copied in perevious step to the `[EDS Project repository]/blocks/form` folder.
1. **Commit Changes to GitHub:** Check in the `[EDS Project repository]/blocks/form` folder and its underlying files to your Edge Delivery Services project on GitHub.

After completing these steps, the Adaptive Forms Block is successfully added to your Edge Delivery Services (EDS) project repository on GitHub. You can now create and add forms to a EDS Sites page.
 

**Troubleshooting GitHub build issues**

Ensure a smooth GitHub build process by addressing potential issues:

* **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file.

* **Handle Linting Errors:**
    Should you come across any linting errors, you can bypass them. Open the [EDS Project]/package.json file and modify the "lint" script from "lint": "npm run lint:js && npm run lint:css" to "lint": "echo 'skipping linting for now'". Save the file and commit the changes to your GitHub project.

+++

-->

+++ 手順 1:Microsoft Excel またはGoogleシートを使用してフォームを作成する。

複雑なプロセスを進める代わりに、スプレッドシートを使用してフォームを簡単に作成できます。 フォーム構造を構成する行と列を定義できます。 各行は、個々の [フォームフィールド](/help/edge/docs/forms/form-components.md#available-components) 列ヘッダーは、対応する [フィールドプロパティ](/help/edge/docs/forms/form-components.md#components-properties).

例えば、行が `enquiry` フォームヘッダーと列ヘッダーは、プロパティを定義します。

![照会スプレッドシート](/help/edge/assets/enquiry-form-spreadsheet.png)

フォームの作成を続行するには：

1. Microsoft SharePointまたはGoogle Drive のAEM Edge Delivery プロジェクトフォルダーにアクセスします。

1. AEM Edge Delivery プロジェクトディレクトリ内の任意の場所で、Microsoft Excel ワークブックまたはGoogleシートを作成します。 例えば、 `enquiry` (Google Drive のAEM Edge Delivery プロジェクトディレクトリ )

   ![Google Drive のサンプルコンテンツ](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

1. シートが適切なAEMユーザー ( 例： `helix@adobe.com`) [プロジェクトに指定された設定に従って](https://www.aem.live/docs/setup-customer-SharePoint). ユーザにシートの編集権限を付与します。

1. 作成したスプレッドシートを開き、デフォルトのシートの名前を「shared-default」に変更します。

   ![既定のシートの名前を&quot;shared-default&quot;に変更](/help/edge/assets/rename-sheet-to-shared-default.png)

1. フォームフィールドを追加するには、行と列のヘッダーを「shared-default」シートに挿入します。 各行は、 [フォームフィールド](/help/edge/docs/forms/form-components.md#available-components)を作成し、対応するフィールドを定義する列ヘッダーを含めます。 [プロパティ](/help/edge/docs/forms/form-components.md#components-properties).


   すぐに開始するには、 [照会スプレッドシート](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0) をスプレッドシートに追加します。 内容をコピーした後、スプレッドシートを保存します。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、シートをプレビューします。

   ![AEM Sidekickを使用してシートをプレビュー](/help/edge/assets/preview-form.png)

   プレビュー時に、新しいブラウザタブにシートのコンテンツが JSON 形式で表示されます。 プレビュー URL を取り込む必要があります。これは、次のセクションでフォームをレンダリングする際に必要なものです。 URL 形式は次のとおりです。


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form-path>/<form-file-name>.json
   ```

   * `<branch>` は、GitHub リポジトリのブランチを参照します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。

   例えば、プロジェクトのリポジトリの名前が「portal」の場合、リポジトリは「wkndforms」アカウントの下に配置され、「main」ブランチを使用している場合、URL は次のようになります。

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ 手順 2:Edge Delivery Services(EDS) ページを使用してフォームをプレビューする。


これまでは、フォームの構造を準備しています。 次に、フォームをプレビューします。

1. Microsoft SharePointまたはGoogle Drive アカウントを開き、 AEM Edge Delivery プロジェクトディレクトリに移動します。



1. フォームを埋め込むドキュメントファイル（インデックスファイルなど）を開きます。 または、新しいドキュメントを作成できます。

1. フォームを追加するドキュメント内の目的の場所に移動します。

1. フォームをレンダリングするフォームブロックを作成する場合。 挿入/テーブルを選択し、1 列 2 行のテーブルを作成します。 テーブルに「Form」という名前を付け、2 行目にプレビュー URL を貼り付けます。 URL がプレーンテキストではなく、ハイパーリンクとしてフォーマットされていることを確認します（下図を参照）。

   | フォーム |
   |---|
   | [https://main—wefinance—wkndforms.hlx.live/inquiry.json](https://main--wefinance--wkndforms.hlx.live/enquiry.json) |


   ![アダプティブFormsブロックを Web ページに追加する](/help/edge/assets/add-adaptive-forms-block.png)

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


## 関連トピック

{{see-more-forms-eds}}
