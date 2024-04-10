---
title: URL からドロップダウン リスト オプションを読み込む
description: ドロップダウンリストのオプションは個別のスプレッドシートに含まれ、指定された URL を介してプライマリスプレッドシートに読み込まれます。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 2%

---


# URL からドロップダウンリストのオプションを読み込む

Edge Delivery Servicesフォームでは、事前に定義された一連のオプションから値を選択できます。 フォーム作成者は次を使用します `select` 要素：選択肢のリストを提供します。
例： `enquiry` フォームには、国を選択するためのドロップダウンメニューが用意され、ユーザーは事前定義済みの様々な国から選択できます。 このリストは、コンマで区切られた国の長いリストで構成されていることがわかります。

![ドロップダウンオプション](/help/forms/assets/drop-down-options.png)

ドロップダウンメニューのオプションの長いリストをフォームの定義を含むシートに直接追加すると、面倒な場合があります。 これらのドロップダウンオプションを格納するシートを別途作成すると、プロセスを簡素化して効率化できます。 このシートは、構造化された形式に配置されたすべてのドロップダウンオプションの一元的なリポジトリとして機能します。 各オプションは独自の行にリストされ、管理と更新が容易になります。

URL を使用して別のスプレッドシートからオプションリストを読み込むことで、フォームのオーサリングプロセスを改善する方法を見てみましょう。

この記事を最後まで読むと、以下の操作を実行できるようになります。

* [別のスプレッドシートでオプションを定義する](#define-options)
* [ドロップダウンリストのオプションを読み込む URL を追加](#add-url)

## 別のシートでオプションを定義する {#define-options}

2 列のシートを作成します。`Option` および `Value`：オプションを定義します。

1. Microsoft、SharePoint®Google Drive フォルダーのAEM プロジェクトフォルダーに移動します。
2. という名前のシートを追加します `shared-country` Microsoft® SharePoint サイトまたはGoogle ドライブのフォルダー内で、次の情報を追加します。

   * **オプション**：ドロップダウンメニューのオプションの表示値を表します。
   * **値**：ユーザーがオプションを選択したときに送信された値を表します。

   >[!NOTE]
   >
   > ドロップダウンオプションの値とオプションが同じ場合、スプレッドシートには次の値のみを含めることができます **オプション** 列。

   新しいシートを追加しましょう。 [shared-country](/help/forms/assets/enquiry-options.xlsx) に表示されるオプション用 `Destination` のドロップダウンリスト `enquiry` フォーム。

   以下の図を参照してください。 `shared-country` スプレッドシート：

   ![国のドロップダウン](/help/forms/assets/drop-down-country-options.png)
3. のプレビューと公開 `shared-country` を使用したシート [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

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


