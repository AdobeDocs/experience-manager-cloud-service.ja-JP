---
title: AEM FormsEdge Delivery Servicesフォームの公開
description: AEM FormsEdge Delivery Servicesフォームの公開
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 2%

---

# フォームを発行する

データの収集や送信を目的として顧客とフォームを共有する準備が整ったら、そのフォームを発行するだけで、顧客がすぐに使用できるようになります。

![ドキュメントベースのオーサリングエコシステム](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## 前提条件

* The [アダプティブFormsブロックが GitHub の EDS プロジェクトで有効になっています](/help/edge/docs/forms/create-forms.md).
* フォームは完全にテスト済みで、使用する準備が整っています。
* お使いの [スプレッドシートが設定されました](/help/edge/docs/forms/submit-forms.md) をクリックしてデータを受け入れます。

## フォームを発行する

+++ 1.スプレッドシートを公開します。

1. Microsoft SharePointまたはGoogle Drive アカウントを開き、 AEM Edge Delivery プロジェクトディレクトリに移動します。

1. フォームを含むスプレッドシートを開きます。 例えば、 `enquiry` Microsoft Excel ブックから

1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、シートをプレビューします。

   ![AEM Sidekickを使用してシートをプレビュー](/help/edge/assets/preview-form.png)

   プレビュー操作が正常に完了すると、スプレッドシートコンテンツは JSON 形式に変換されます。 次に、プレビューページで、このコンテンツが構造化された表形式で表示されます。 例えば、付属の画像は、「問い合わせ」形式の内容を示します。

   ![Forms Preview JSON 形式](/help/edge/assets/forms-preview-json-format.png)

1. AEM Sidekickを使用してシートをパブリッシュします。 次のセクションでフォームをレンダリングする際に必要になるので、必ずパブリッシュ URL を取り込んでください。 URL 形式は次のとおりです。


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` は、GitHub リポジトリのブランチを参照します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。

   例えば、プロジェクトのリポジトリの名前が「portal」の場合、リポジトリは「wkndforms」アカウントの下に配置され、「main」ブランチを使用している場合、URL は次のようになります。

   `https://main--portal--wkndforms.hlx.page/enquiry.json`

+++

+++ 2. Web ページにフォームを追加する

次を追加： `<form>.json` 顧客とのやり取りを容易にする web ページに追加し、フォーム入力者が容易にフォームを入力して送信できるようにします。


フォームを Web ページに追加するには、次の手順を実行します。

1. Microsoft SharePointまたはGoogle Drive アカウントにアクセスし、 `[AEM Edge Delivery project directory]`.

1. フォームを埋め込むドキュメントファイルを開きます。 例えば、 `index.docx` ファイル、または新しいドキュメントを作成します。

1. ドキュメント内でフォームを挿入するセクションを指定し、それに応じてそのセクションに移動します。

1. 以下に示す例のように、「Form」という名前のブロックをファイルに追加します。

   | フォーム |
   |---|
   | [https://main—portal—wkndforms.hlx.live/inquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   このブロックは、フォームが埋め込まれるプレースホルダーとして機能します。 ブロックの 2 行目に、 `<form>.json` ファイルをハイパーリンクとして保存します。

   >[!IMPORTANT]
   >
   >
   > URL がプレーンテキストで表示されるのではなく、ハイパーリンクとしてフォーマットされていることを確認します。

   開発やテストの目的ではプレビュー URL(.page URL) を、実稼動環境では公開 URL(.live) を使用します。 プレビューおよび公開 URL の例を次に示します。

   **プレビュー URL**
| フォーム | |—| | [https://main—portal—wkndforms.hlx.page/inquiry.json](https://main--portal--wkndforms.hlx.page/enquiry.json)  |


   **公開 URL**
| フォーム | |—| | [https://main—portal—wkndforms.hlx.live/inquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json)  |

1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) :web ページをプレビューします。 これで、ページにフォームが表示されます。 例えば、次に、 [照会スプレッドシート](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![EDS フォームのサンプル](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

1. 「AEM Sidekick」を使用して、フォームを発行します。 これで、顧客はフォームに入力して送信できます。

+++

## トラブルシューティング

+++ データをフォームに送信できません

次のメッセージに似たエラーが発生した場合は、スプレッドシートが [提出を受諾](/help/edge/docs/forms/submit-forms.md) データをまだ取得しています。

![フォーム送信エラー](/help/edge/assets/form-error.png)

+++




## 詳細を表示する
