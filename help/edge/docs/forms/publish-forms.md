---
title: AEM Forms の Edge Delivery Services の公開
description: AEM Forms の Edge Delivery Services の公開
feature: Edge Delivery Services
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
role: Admin, Architect, Developer
source-git-commit: 4e6045aadd7d927851e431e2204cb2d56767a5a3
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 77%

---

# フォームを公開してデータの収集を開始

データ収集または送信のためにフォームをお客様と共有する準備が整ったら、公開するだけで、お客様がすぐにフォームを使用できるようになります。

![ドキュメントベースのオーサリングエコシステム](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## 前提条件

* [AEM Forms ボイラープレート](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)に基づく AEM プロジェクトがあるか、[既存の AEM プロジェクトに Adaptive Forms ブロックを追加している](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)
* フォームは完全にテスト済みで、使用する準備が整っている
* データを受け入れるように[スプレッドシートが設定](/help/edge/docs/forms/submit-forms.md)されている


## フォームの公開

+++ 1. スプレッドシートを公開

1. Microsoft SharePoint または Google Drive アカウントを開き、AEM Edge Delivery プロジェクトディレクトリに移動します。

1. フォームを含むスプレッドシートを開きます。例えば、「[ 問い合わせ ](/help/edge/assets/enquiry.xlsx)」フォームのMicrosoft Excel ワークブックなどです。

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用してシートをプレビューします。

   ![AEM Sidekick を使用してシートをプレビュー](/help/edge/assets/preview-form.png) します。

   プレビュー操作が正常に完了すると、スプレッドシートのコンテンツが JSON 形式に変換されます。プレビューページには、このコンテンツが構造化された表形式で表示されます。例えば、添付の画像は「お問い合わせ」フォームの内容を示しています。

   ![フォームのプレビューの JSON 形式](/help/edge/assets/forms-preview-json-format.png)

1. AEM Sidekick を使用してシートを公開します。次の節でフォームをレンダリングするために必要となるので、パブリッシュ URL を取得します。URL 形式は次のとおりです。


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form>.json
   ```

   * `<branch>` は、GitHub リポジトリのブランチを参照します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。

   例えば、プロジェクトのリポジトリの名前が「wefinance」で、「wkndform」というアカウントの下にあり、「main」ブランチとフォームを「inquiry」として使用している場合、URL は次のようになります。

   [https://main--wefinance--wkndform.aem.live/enquiry.json](https://main--wefinance--wkndform.aem.live/enquiry.json)

+++

+++ 2. Web ページにフォームを追加

Web ページに `<form>.json` を追加すると、顧客インタラクションが簡単になり、フォーム入力者が簡単にフォームに入力して送信できるようになります。


Web ページにフォームを追加するには、以下の手順に従います。

1. Microsoft SharePoint または Google Drive アカウントにアクセスし、`[AEM Edge Delivery project directory]` に移動します。

1. フォームを埋め込むドキュメントファイルを開きます。例えば、[inquiry-form.docx](/help/edge/assets/enquiry-form.docx) ファイルを開くことも、新しいドキュメントを作成することもできます。

1. ドキュメント内でフォームを挿入するセクションを特定し、これに応じてそのセクションに移動します。

1. 「Form」という名前のブロックをファイルに追加します。 例えば、プロジェクトのリポジトリの名前が「wefinance」の場合は、アカウント所有者の「wkndform」の下にあり、「main」ブランチを使用しています。

   | フォーム |
   |---|
   | [https://main--wefinance--wkndform.aem.live/enquiry.json](https://main--wefinance--wkndform.aem.live/enquiry.json) |

   ![「フォーム」という名前のブロックをファイルに追加](/help/edge/assets/enquiry-doc-to-embed-form.png)

   このブロックは、フォームが埋め込まれるプレースホルダーとして機能します。ブロックの 2 行目に、`<form>.json` ファイルの URL をハイパーリンクとして追加します。

   >[!IMPORTANT]
   >
   >
   > URL がプレーンテキストとして表示されるのではなく、ハイパーリンクとして書式設定されていることを確認します。

   開発またはテストの目的でプレビュー URL （.page URL）を使用し、実稼動ではパブリッシュ URL （.live）を使用します。

   例えば、プロジェクトのリポジトリの名前が「wefinance」の場合は、アカウント所有者の「wkndform」の下にあり、「main」ブランチを使用しています。

   プレビュー URL およびパブリッシュ URL の例を次に示します。

   **プレビュー URL**

   | フォーム |
   |---|
   | [https://main--wefinance--wkndform.aem.page/enquiry.json](https://main--wefinance--wkndform.aem.page/enquiry.json) |


   **パブリッシュ URL**

   | フォーム |
   |---|
   | [https://main--wefinance--wkndform.aem.live/enquiry.json](https://main--wefinance--wkndform.aem.live/enquiry.json) |

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用して web ページをプレビューします。これで、ページにフォームが表示されます。例えば、[お問い合わせスプレッドシート](/help/edge/assets/enquiry.xlsx)に基づくフォームは次のとおりです。


   ![EDS フォームのサンプル](/help/edge/assets/updated-form.png)

1. AEM Sidekick を使用してフォームを公開します。これで、お客様はフォームに入力して送信できます。

+++

## トラブルシューティング

+++ フォームにデータを送信できません。

次のメッセージのようなエラーが発生した場合は、スプレッドシートが[送信されたデータを受け入れる](/help/edge/docs/forms/submit-forms.md)ようにまだ設定されていないことを示します。

![フォーム送信時のエラー](/help/edge/assets/form-error.png)

+++


## 関連トピック

{{see-more-forms-eds}}
