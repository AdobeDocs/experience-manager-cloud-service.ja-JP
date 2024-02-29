---
title: AEM FormsEdge Delivery Servicesフォームの公開
description: AEM FormsEdge Delivery Servicesフォームの公開
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 39bb45b285fcd938d44b9748aa8559b89a3636b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 1%

---


# フォームを発行する

データの収集や送信を目的として顧客とフォームを共有する準備が整ったら、そのフォームを発行するだけで、顧客がすぐに使用できるようになります。

## 前提条件

* The [Github の EDS プロジェクトでフォームブロックが有効になっています](/help/edge/docs/forms/create-forms.md).
* フォームは完全にテスト済みで、使用する準備が整っています。
* お使いの [スプレッドシートが設定されました](/help/edge/docs/forms/submit-forms.md) をクリックしてデータを受け入れます。

## フォームを発行する

フォームを発行するには：

1. Microsoft SharePointまたはGoogle Drive アカウントにアクセスし、 `[AEM Edge Delivery project directory]`.

1. フォームを埋め込むドキュメントファイルを開きます。 例えば、インデックスファイルを開いたり、新しいドキュメントを作成したりできます。

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

1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、ページをプレビューします。 これで、ページにフォームが表示されます。 例えば、次に、 [照会スプレッドシート](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![EDS フォームのサンプル](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   これで、顧客はフォームに入力して送信できます。

## トラブルシューティング

+++ データをフォームに送信できません

次のメッセージに似たエラーが発生した場合は、送信されたデータを受け入れるようにスプレッドシートが設定されていないことを示します。

![フォーム送信エラー](/help/edge/assets/form-error.png)

+++


## 詳細を表示する

* [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
* [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
* [サイトページにフォームを発行する](/help/edge/docs/forms/publish-eds-forms.md)
* [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
* [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)
