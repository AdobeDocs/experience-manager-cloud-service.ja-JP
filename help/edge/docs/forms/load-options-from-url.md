---
title: URL からドロップダウン リスト オプションを読み込む
description: ドロップダウンリストのオプションは個別のスプレッドシートに含まれ、指定された URL を介してプライマリスプレッドシートに読み込まれます。
feature: Edge Delivery Services
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 3%

---


# URL からドロップダウンリストのオプションを読み込む

Formsには多くの場合、ユーザーが事前定義済みのオプションから選択するためのドロップダウンメニューが含まれています。 これらのオプションは通常、フォーム内で定義されますが、長いリストの管理は面倒な場合があります。 このガイドでは、URL を使用して別のスプレッドシートからドロップダウンオプションを読み込み、フォームのオーサリングを改善する方法について説明します。


ドロップダウンオプションを別のスプレッドシートから読み込む利点は次のとおりです。

* 管理のシンプル化：更新や追加を容易にするために、ドロップダウンオプションを一元化された場所で維持します。
* 効率の向上：長いオプションリストをフォーム定義内で手動で追加する必要がなくなります。




![ドロップダウンオプション](/help/forms/assets/drop-down-options.png)


この記事を最後まで読むと、以下の操作を実行できるようになります。

* [別のスプレッドシートでオプションを定義する](#define-options)
* [ドロップダウンリストのオプションを読み込む URL を追加](#add-url)

## 別のシートでオプションを定義する {#define-options}

別のスプレッドシートでのオプションの定義

1. スプレッドシートを作成します。
   1. Microsoft、SharePoint®GoogleのドライブでAEM プロジェクトフォルダーを見つけます。
   1. 新しいシートを追加します。 例えば、「shared-country」と指定します。
1. オプション列の定義：「オプション」と「値」の 2 列を追加します。
   * 「オプション」は、ドロップダウンメニューに表示するテキストを定義します。
   * 「値」は、ユーザーがオプションを選択したときに送信された値を定義します。

   >[!NOTE]
   >
   >オプションと値の両方が同じ場合は、「オプション」列のみ必須です。

1. スプレッドシートに入力します。「オプション」列（および必要に応じて「値」列）に国オプションを入力します。

   構造については、以下の例を参照してください。

   ![国のドロップダウン](/help/forms/assets/drop-down-country-options.png)

1. のプレビューと公開 `shared-country` を使用したシート [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   を表示する URL を参照してください。 `shared-country` シート : https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` は、URL に追加されるクエリパラメーターです。 このパラメーターは、に基づいてフィルタリングされた JSON を示します `shared-country` シート。 様々な国に関連する情報を含む JSON ファイルにリダイレクトされます。

## ドロップダウンリストのオプションを読み込む URL を追加{#add-url}

この `Options` のプロパティ `select` フィールドには URL を指定できます。 URL は、のオプションとして使用される JSON 配列を返します。 `Destination` ドロップダウンリスト。 ドロップダウンリストのオプションを読み込む URL を追加するには：

1. Microsoft、SharePoint®Google ドライブのAEM プロジェクトフォルダーに移動し、スプレッドシートを開きます。 また、フォームの新しいスプレッドシートを作成することもできます。
1. 次の URL をコピー `shared-country` シートを作成して、に貼り付ける `Options` 列： `Destination` フィールド。

   ![照会スプレッドシート](/help/forms/assets/drop-down-enquiry.png)

1. を使用したシートのプレビューとパブリッシュ [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![国のドロップダウン](/help/forms/assets/load-dropdown-options-form.png)

以下を参照してください [問い合わせスプレッドシート](/help/forms/assets/enquiry-options.xlsx) 読み込む URL を追加するドロップダウンリストオプション。

URL を読み込むフォーム定義に統合した後、ドロップダウンリストのオプションに `Destination` ドロップダウンが URL から表示されるようになります。

以下の URL を参照してください。この URL には、 `enquiry` 個別のシートに保存されたオプションを表示するフォーム：

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## 関連トピック

{{see-more-forms-eds}}


