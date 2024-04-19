---
title: URL からのドロップダウンリストオプションの読み込み
description: ドロップダウンリストオプションは別個のスプレッドシートに含まれており、指定された URL を介してプライマリスプレッドシートに読み込まれます。
feature: Edge Delivery Services
exl-id: 5b0bc1b6-6e33-41f3-b7c1-4d997787b6cd
source-git-commit: e61ef529dc562862bd02d7767e45de3e2ec4983b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 59%

---

# URL からのドロップダウンリストオプションの読み込み

Formsには多くの場合、ユーザーが事前定義済みのオプションから選択するためのドロップダウンメニューが含まれています。 これらのオプションは通常、フォーム内で定義されますが、長いリストの管理は面倒な場合があります。 このガイドでは、URL を使用して別のスプレッドシートからドロップダウンオプションを読み込み、フォームのオーサリングを改善する方法について説明します。


ドロップダウンオプションを別のスプレッドシートから読み込む利点は次のとおりです。

* 管理のシンプル化：更新や追加を容易にするために、ドロップダウンオプションを一元化された場所で維持します。
* 効率の向上：長いオプションリストをフォーム定義内で手動で追加する必要がなくなります。




![ドロップダウンオプション](/help/forms/assets/drop-down-options.png)


この記事を最後まで読むと、以下の操作を実行できるようになります。

* [別個のスプレッドシートでオプションを定義する](#define-options)
* [ドロップダウンリストのオプションを読み込む URL を追加する](#add-url)

## 別個のシートでオプションを定義する {#define-options}

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

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用して、`shared-country` シートをプレビューし公開します。

   `shared-country` シートを表示する URL https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country を参照してください。


>[!NOTE]
>
> `?sheet=country` は、URL に追加されたクエリパラメーターです。このパラメーターは、`shared-country` シートに基づいてフィルタリングされた JSON を示します。様々な国に関連する情報を含んだ JSON ファイルにリダイレクトされます。

## ドロップダウンリストのオプションを読み込む URL を追加する{#add-url}

`select` フィールドの `Options` プロパティには URL を指定できます。その URL は、`Destination` ドロップダウンリストのオプションとして使用される JSON 配列を返します。ドロップダウンリストのオプションを読み込む URL を追加するには、次の手順に従います。

1. Microsoft® SharePoint または Google ドライブ上の AEM プロジェクトフォルダーに移動し、スプレッドシートを開きます。また、フォーム用の新しいスプレッドシートを作成することもできます。
1. `shared-country` シートの URL をコピーして、`Destination` フィールドの `Options` 列にペーストします。

   ![照会スプレッドシート](/help/forms/assets/drop-down-enquiry.png)

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用して、シートをプレビューし公開します。


   ![国のドロップダウン](/help/forms/assets/load-dropdown-options-form.png)

[照会スプレッドシート](/help/forms/assets/enquiry-options.xlsx)を参照して、ドロップダウンリストのオプションを読み込む URL を追加できます。

ドロップダウンリストのオプションを読み込む URL をフォーム定義に統合したら、`Destination` ドロップダウンのオプションが URL から表示されるようになります。

以下の URL を参照してください。別個のシートに保存されたオプションを表示する `enquiry` フォームが表示されます。

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## 関連トピック

{{see-more-forms-eds}}
