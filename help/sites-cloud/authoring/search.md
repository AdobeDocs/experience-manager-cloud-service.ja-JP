---
title: 検索
description: 包括的な検索で、より迅速にコンテンツを見つけます。
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 100%

---

# 検索 {#search-feature}

AEM のオーサー環境は、リソースタイプに応じて、コンテンツを検索するための様々なメカニズムを提供します。

## 検索の基本 {#search-basics}

検索は上部のツールバーから使用できます。

![検索アイコン](/help/sites-cloud/authoring/assets/search-icon.png)

検索レールでは、次の操作を実行できます。

* 特定のキーワード、パス、タグを検索する
* リソース固有の条件（変更日、ページのステータス、ファイルサイズなど）に基づいてフィルターする
* 上記の条件に基づいて、[保存済みの検索結果](#saved-searches)を定義して使用する

>[!NOTE]
>
>検索レールが表示されていれば、ホットキー `/`（スラッシュ）を使用して検索を呼び出すこともできます。

## 検索とフィルター {#search-and-filter}

リソースを検索およびフィルターするには、次のようにします。

1. （ツールバーの虫眼鏡アイコンを使用して）**検索**&#x200B;を開き、検索語を入力します。候補が表示され、その中から選択できます。

   ![検索語句](/help/sites-cloud/authoring/assets/search-term.png)

   デフォルトでは、検索結果は現在の場所（コンソールと関連するリソースタイプ）に限定されます。

   ![検索場所](/help/sites-cloud/authoring/assets/search-term-location.png)

1. 必要に応じて、場所フィルターを削除（削除するフィルターで「**X**」を選択）し、すべてのコンソール／リソースタイプを検索できます。
1. 検索結果は、コンソールや関連するリソースタイプに基づいてグループ化されて表示されます。

   特定のリソースを選択してアクションをさらに実行するか、必要なリソースタイプ（「**すべてのサイトを表示**」など）を選択してドリルダウンできます。

   ![検索結果](/help/sites-cloud/authoring/assets/search-results.png)

1. さらにドリルダウンするには、レール記号（左上）を選択して&#x200B;**フィルターおよびオプション**&#x200B;サイドパネルを開きます。

   ![レールボタン](/help/sites-cloud/authoring/assets/rail-button.png)

   検索には、リソースタイプに従って、検索／フィルター条件の定義済みの選択項目が表示されます。

   サイドパネルでは、次の要素を選択できます。

   * 保存済みの検索結果
   * 検索ディレクトリ
   * タグ
   * 検索基準（変更日、公開ステータス、ライブコピーのステータスなど）

   >[!NOTE]
   >
   >検索条件は、次の場合に変わる可能性があります。
   >
   >* 選択したリソースタイプによって。例えば、アセットとコミュニティの条件はわかりやすく細分化されています。
   >* 検索フォームのインスタンスを（AEM 内の場所に適切なように）カスタマイズできる場合。

<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![検索サイドパネル](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 検索用語を追加することもできます。

1. **検索**&#x200B;を閉じるには **X**（右上）を使用します。

>[!NOTE]
>
>検索結果で項目を選択すると、検索条件が保持されます。
>
>検索結果ページの項目を選択する際に、ブラウザーの戻るボタンを使用した後で検索ページに戻ると、検索条件が保持されます。

## 保存済みの検索結果 {#saved-searches}

様々なファセットで検索するだけでなく、特定の検索設定を保存して、後で取得して使用することもできます。

1. 検索条件を定義して、「**保存**」を選択します。

   ![検索の保存](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 名前を割り当ててから、「**保存**」を使用して確認します。

   ![名前を付けて検索を保存](/help/sites-cloud/authoring/assets/search-save-name.png)

1. 保存済みの検索は、次回検索パネルにアクセスするときにセレクターで選択できます。

   ![保存済みの検索結果](/help/sites-cloud/authoring/assets/saved-searches.png)

1. 保存すると、次の操作を実行できます。

   * （保存済みの検索結果の名前に対して）**x** を使用して、新しいクエリを開始する（保存済みの検索結果自体は削除されません）。
   * **保存済みの検索を編集**&#x200B;し、検索条件を変更して、もう一度&#x200B;**保存**&#x200B;する。

保存済みの検索結果を変更するには、保存済みの検索結果を選択して、検索パネルの下部にある「**保存済みの検索を編集**」をクリックします。

![保存済みの検索結果の変更](/help/sites-cloud/authoring/assets/saved-searches-modify.png)
