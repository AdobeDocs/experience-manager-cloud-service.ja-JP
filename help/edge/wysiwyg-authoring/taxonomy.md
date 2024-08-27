---
title: 分類データの管理
description: Edge Delivery ServicesサイトでAEMとタグを使用するための分類データを管理する方法を説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 81aacb0c616490eed4589cb8927ea1316ca1670e
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 7%

---


# 分類データの管理 {#managing-taxonomy-data}

Edge Delivery ServicesサイトでAEMとタグを使用するための分類データを管理する方法を説明します。

## はじめに {#introduction}

タグ付けは、ページを整理および管理するのに役立つ重要な機能です。 AEMの [ タグ付けコンソール ](/help/sites-cloud/administering/tags.md#tagging-console) を使用すると、タグの豊富な分類を作成してページを整理できます。

これらのタグは、作成者がコンテンツを整理する際に役立つだけでなく、読者にとっても役立ちます。 タグとその分類は、ページ上のコンポーネントで使用して、読者がコンテンツを移動しやすくすることができます。

ユニバーサルエディターは、タグの ID でのみ機能します。 コンテンツの分類ページを作成することにより、すべての言語のこれらのタグの説明をユニバーサルエディターに公開して、コンテンツのレンダリング時に情報を使用できるようにします。

## 分類ページの作成 {#creating}

分類は、[AEMの他のページ ](/help/sites-cloud/authoring/sites-console/creating-pages.md) と同様に作成されます。

1. [**Sites** コンソールに移動します。](/help/sites-cloud/authoring/sites-console/introduction.md)

1. 分類を作成する場所を選択します。

1. **作成**／**ページ**&#x200B;をタップまたはクリックします。

   ![ページを作成](assets/taxonomy/create-page.png)

1. **ページを作成** ウィザードの **テンプレート** タブで、**分類** テンプレートを選択し、「**次へ** をタップまたはクリックします。

   ![ 分類テンプレート ](assets/taxonomy/taxonomy-template.png)

1. **ページを作成** ウィザードの **プロパティ** タブで、ページに意味のある **タイトル** を指定し、**タグ** フィールドに [ タグピッカーを使用 ](/help/sites-cloud/authoring/sites-console/tags.md) して、分類に含めるタグまたは名前空間を選択します。

   ![ 分類プロパティ ](assets/taxonomy/create-page-wizard-properties.png)

1. 「**作成**」をタップまたはクリックします。

分類ページが作成されます。 **成功** ダイアログで、「**完了** ダイアログをタップまたはクリックしてメッセージを解除するか、「**開く [ をタップまたはクリックして、** ページエディター ](/help/sites-cloud/authoring/page-editor/introduction.md) でページを編集することができます。

次の手順で使用するために、分類ページの結果ページ名をメモしておきます。

## 分類ページの編集 {#editing}

AEMの他のページと同様に、分類ページの編集を開始します。

1. [**Sites** コンソールに移動します。](/help/sites-cloud/authoring/sites-console/introduction.md)

1. 編集する分類を選択します。

1. アクションバーの **編集** をタップまたはクリックします。

1. ページエディターが開き、分類が表示されます。

   * 分類ページは、ページエディターでは読み取り専用です。

   ![ 分類を編集 ](assets/taxonomy/edit-page.png)

1. ツールバーの **ページ情報** アイコンをタップまたはクリックして、「**プロパティを開く** を選択します。

   ![ プロパティを開く ](assets/taxonomy/open-properties.png)

1. **ページプロパティ** ウィンドウで、ページの名前を更新し、タグセレクターを使用して、分類に含まれるタグと名前空間を更新できます。

   ![ ページプロパティの編集 ](assets/taxonomy/edit-properties.png)

1. 「**保存して閉じる**」をタップまたはクリックします。

分類のコンテンツが選択したタグと名前空間から自動的に生成されるので、ページエディターに表示されるページは読み取り専用です。 分類のコンテンツを自動的に生成するためのフィルターの一種として機能します。 したがって、エディターでページを直接編集する必要はありません。

基になるタグと名前空間を更新すると、AEMによって分類ページのコンテンツが自動的に更新されます。 ただし、変更を加えた後で分類を [ 再公開 ](#publishing) して、その変更をユーザーが使用できるようにする必要があります。

## 分類の公開に関する paths.json の更新 {#paths-json}

Edge Delivery Servicesサイトの表形式のデータを管理して公開する [ 場合と同様に ](/help/edge/wysiwyg-authoring/tabular-data.md) 分類データを公開できるように、プロジェクトの `paths.json` ファイルを更新する必要があります。

1. GitHub でプロジェクトのルートを開きます。

1. `paths.json` ファイルをタップまたはクリックして詳細を開き、「**編集**」アイコンをタップまたはクリックします。

   ![paths.json file](assets/taxonomy/paths-json.png)

1. 行を追加して、新しい分類ページを `.json` リソースにマッピングします。

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/<taxonomy-page-name>:/<taxonomy-json-name>.json"
     ]
   }
   ```

   * 作成 `<taxonomy-page-name>` た [ 分類ページ ](#creating) の名前と一致する必要があります。
   * 任意の有効な名前を指定で `<taxonomy-json-name>` ます。

1. 「**変更をコミット…**」をクリックして、変更を `main` に保存します。

   * `main` にコミットするか、プロセスに従ってプルリクエストを作成します。

このプロセスは、分類ページごとに 1 回だけ実行する必要があります。 完了したら、分類を公開できます。

## 分類の公開 {#publishing}

分類は、公開されるまで、ユニバーサルエディターまたはユーザーは使用できません。

分類ページは、他のページと同様に、[ ツールバーの **クイックPublish** または **公開を管理** アイコンを使用 ](/help/sites-cloud/authoring/sites-console/publishing-pages.md) して公開されます。

分類ページは、次の操作を行うたびに再公開する必要があります。

* 分類ページを編集します。
* 分類ページに含まれるタグおよび名前空間を編集または追加します。

新しい分類ページを作成する場合は、まず [ プロジェクト内の `paths.json` ファイルへのマッピングを追加 ](#paths-json) する必要があります。

## 分類情報へのアクセス {#accessing}

分類が公開されると、その情報をユニバーサルエディターで活用して、ユーザーに表示できます。

以下のアドレスで、JSON データとして分類にアクセスできます。

`https://<branch>--<repository>--<owner>.hlx.page/<taxonomy-json-name>.json`

分類をプロジェクトの `paths.json` ファイルにマッピングする [ 際に定義した `<taxonomy-json-name>` を使用します。](#paths-json) 分類データは、次の例のように JSON データとして返されます。

```json
{
  "total": 3,
  "offset": 0,
  "limit": 3,
  "data": [
    {
      "tag": "default:",
      "title": "Standard Tags"
    },
    {
      "tag": "do-not-translate",
      "title": "Do Not Translate"
    },
    {
      "tag": "translate",
      "title": "Translate"
    }
  ],
  ":type": "sheet"
}
```

この JSON データは、分類を更新して再公開すると、自動的に更新されます。 アプリは、ユーザーのこの情報にプログラムでアクセスできます。

[ 複数の言語でタグを管理している場合 ](/help/sites-cloud/administering/tags.md#managing-tags-in-different-languages)、`sheet=` パラメーターの値として ISO2 言語コードを渡すことで、それらの言語にアクセスできます。
