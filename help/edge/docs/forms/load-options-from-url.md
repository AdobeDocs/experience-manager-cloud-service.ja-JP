---
title: AEM Formsas a Cloud Service用Edge Delivery Servicesの URL または別のシートからドロップダウン リスト オプションを読み込む
description: ドロップダウンリストオプションは別個のスプレッドシートに含まれており、指定された URL を介してプライマリスプレッドシートに読み込まれます。
feature: Edge Delivery Services
exl-id: 5b0bc1b6-6e33-41f3-b7c1-4d997787b6cd
source-git-commit: 8730383d26c6f4fbe31a25a43d33bf314251d267
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 91%

---


# AEM Formsas a Cloud Service用Edge Delivery Servicesの URL または別のシートからのオプション

多くの場合、フォームには、ユーザーが定義済みのオプションから選択するドロップダウンメニューが含まれます。これらのオプションは通常、フォーム自体内で定義されますが、長いリストの管理は面倒な場合があります。このガイドでは、URL を使用して別のスプレッドシートからドロップダウンオプションを読み込んでフォームのオーサリングを改善する方法について概要を説明します。


別のスプレッドシートからドロップダウンオプションを読み込むことには、次のメリットがあります。

* 管理の簡素化：ドロップダウンオプションを一元的な場所に維持して、更新や追加を簡単にします。
* 効率の向上：フォーム定義内に長いオプションリストを手動で追加する必要がなくなります。




![ドロップダウンオプション](/help/forms/assets/drop-down-options.png)


この記事を最後まで読むと、以下の操作を実行できるようになります。

* [別個のスプレッドシートでオプションを定義する](#define-options)
* [ドロップダウンリストのオプションを読み込む URL を追加する](#add-url)

## 別個のシートでオプションを定義する {#define-options}

別のスプレッドシートでオプションを定義

1. 次のように、スプレッドシートを作成します。
   1. Microsoft® SharePoint または Google Drive で AEM プロジェクトフォルダーを見つけます。
   1. 新しいシートを追加します。例：「shared-country」。
1. オプション列を定義します。
「オプション」と「値」の 2 つの列を追加します。
   * 「オプション」では、ドロップダウンメニューに表示されるテキストを定義します。
   * 「値」では、ユーザーがオプションを選択したときに送信される値を定義します。

   >[!NOTE]
   >
   >オプションと値の両方が同じ場合は、「オプション」列のみが必要です。

1. スプレッドシートに入力します。
「オプション」列（必要に応じて「値」列）に国のオプションを入力します。

   構造について詳しくは、以下の例を参照してください。

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


