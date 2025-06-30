---
title: スタイルシステム
description: スタイルシステムを使用すると、テンプレート作成者がコンポーネントのコンテンツポリシーのスタイルクラスを定義し、コンテンツ作成者がページでのコンポーネントの編集時にそのスタイルクラスを選択できます。これらのスタイルは、1 つのコンポーネントの別の視覚的バリエーションとして使用することができるので、コンポーネントがより柔軟で扱いやすいものになります。
exl-id: 224928dd-e365-4f3e-91af-4d8d9f47efdd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: d2cd112de034ca6ea22590245fb480622acf258a
workflow-type: ht
source-wordcount: '1338'
ht-degree: 100%

---


# スタイルシステム {#style-system}

スタイルシステムを使用すると、テンプレート作成者がコンポーネントのコンテンツポリシーのスタイルクラスを定義し、コンテンツ作成者がページでのコンポーネントの編集時にそのスタイルクラスを選択できます。これらのスタイルは、1 つのコンポーネントの別の視覚的バリエーションとして使用することができるので、コンポーネントがより柔軟で扱いやすいものになります。

これにより、各スタイルのカスタムコンポーネントを開発したり、そのようなスタイル機能を有効にするためにコンポーネントダイアログをカスタマイズしたりする必要がなくなります。AEM のバックエンド開発を行わなくても、コンテンツ作成者のニーズに迅速かつ容易に適応できる再利用可能なコンポーネントの増加につながります。

>[!NOTE]
>
>スタイルシステムは、ページエディターで作成したページにのみ適用されます。
>
>[ユニバーサルエディター](/help/implementing/universal-editor/introduction.md)で作成され、[Edge Delivery Services](/help/edge/overview.md) で提供されるページのスタイル設定は、すべて GitHub プロジェクトを通じて行うことができます。

## ユースケース {#use-case}

テンプレート作成者には、コンテンツ作成者がコンポーネントを機能させる方法を設定する能力だけでなく、コンポーネントのいくつかの代替の視覚的バリエーションを設定する能力も必要です。

同様に、コンテンツ作成者には、コンテンツを構造化し、配置する能力だけでなく、それをどのように視覚的に表示するかを選択する能力も必要となります。

スタイルシステムでは、テンプレート作成者とコンテンツ作成者の両方の要件に対応する統一ソリューションを提供します。

* テンプレート作成者は、コンポーネントのコンテンツポリシーでスタイルクラスを定義できます。
* その後、コンテンツ作成者は、ページ上のコンポーネントの編集時にドロップダウンリストからこれらのクラスを選択し、対応するスタイルを適用できます。

スタイルクラスがコンポーネントの装飾ラッパー要素に挿入されるので、コンポーネント開発者は、CSS ルールを提供する以外にスタイルの処理に関与する必要がなくなります。

## 概要 {#overview}

スタイルシステムの使用は通常、次のように行われます。

1. Web デザイナーは 1 つのコンポーネントに対し様々な視覚的バリエーションを作成します。

1. HTML 開発者にはコンポーネントの HTML 出力と、実装する必要な視覚的バリエーションが提供されます。

1. HTML 開発者は各視覚的バリエーションに対応する CSS クラスを定義します。その CSS クラスが、コンポーネントをラップする要素に挿入されます。

1. HTML 開発者は視覚的バリエーションごとに対応する CSS コードを（オプションで JS コードも）実装し、それらは定義済みとなります。

1. AEM デベロッパーは、提供された CSS を（オプションで JS も）[クライアントライブラリ](/help/implementing/developing/introduction/clientlibs.md)に配置し、デプロイします。

1. AEM 開発者またはテンプレート作成者は、ページテンプレートを設定し、スタイル設定された各コンポーネントのポリシーを編集します。また、定義済みの CSS クラスを追加し、スタイルごとにわかりやすい名前を付け、組み合わせが可能なスタイルを示します。

1. 次に AEM ページ作成者は、ページエディターでコンポーネントのツールバーのスタイルメニューからデザイン済みのスタイルを選択できます。

AEM では、実際には最後の 3 つの手順のみが実行されます。つまり、必要な CSS と JavaScript のすべての開発は AEM なしで行うことができます。

実際にスタイルを実装するには、AEM にデプロイし、目的のテンプレートのコンポーネント内で選択する必要があるだけです。

次の図は、スタイルシステムのアーキテクチャを示しています。

![aem-style-system](/help/sites-cloud/authoring/assets/style-system-architecture.png)

## 使用方法 {#use}

この機能のデモを行うために、コアコンポーネントの[タイトルコンポーネント](https://www.adobe.com/go/aem_cmp_title_v2_jp)の [WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja) による実装を例として使用します。

次の[コンテンツ作成者として](#as-a-content-author)節と[テンプレート作成者として](#as-a-template-author)節では、WKND のスタイルシステムを使用してスタイルシステムの機能をテストする方法について説明します。

スタイルシステムを独自のコンポーネントに使用する場合は、次の手順に従います。

1. [概要](#overview)の節の説明に従って、クライアントライブラリとして CSS をインストールします。
1. コンテンツ作成者が使用できる CSS クラスを設定します（[テンプレート作成者として](#as-a-template-author)の節を参照）。
1. コンテンツ作成者は、「[コンテンツ作成者として](#as-a-content-author)」の節で説明されるようにスタイルを使用できます。

### コンテンツ作成者として {#as-a-content-author}

1. WKND プロジェクトをインストールした後、WKND の英語のマスターホームページ（`http://<host>:<port>/sites.html/content/wknd/language-masters/en`）に移動し、ページを編集します。
1. ページの下方の&#x200B;**タイトル**&#x200B;コンポーネントを選択します。

   ![作成者にとってのスタイルシステム](/help/sites-cloud/authoring/assets/style-system-author1.png)

1. **リスト**&#x200B;コンポーネントのツールバーで「**スタイル**」ボタンを選択してスタイルメニューを開き、コンポーネントの外観を変更します。

   ![スタイルの選択](/help/sites-cloud/authoring/assets/style-system-author2.png)

   >[!NOTE]
   >
   >この例では、**カラー**&#x200B;スタイル（**黒**、**白**、**グレー**）は相互排他的ですが、**スタイル**&#x200B;オプション（**アンダーライン**、**右揃え**、**最小間隔**）は組み合わせることができます。これは、[テンプレート作成者としてテンプレートで設定可能](#as-a-template-author)です。

### テンプレート作成者として {#as-a-template-author}

1. WKND の英語版マスターホームページ（`http://<host>:<port>/sites.html/content/wknd/language-masters/en`）の編集時に、**ページ情報／テンプレートの編集**&#x200B;でページのテンプレートを編集します。

   ![テンプレートを編集](/help/sites-cloud/authoring/assets/style-system-edit-template.png)

1. コンポーネントの「**ポリシー**」ボタンをタップまたはクリックして、**タイトル**&#x200B;コンポーネントのポリシーを編集します。

   ![ポリシーを編集](/help/sites-cloud/authoring/assets/style-system-edit-policy.png)

1. プロパティの「スタイル」タブで、スタイルがどのように設定されているかを確認できます。

   ![プロパティの編集](/help/sites-cloud/authoring/assets/style-system-properties.png)

   * **グループ名：**&#x200B;スタイルは、コンポーネントのスタイルの設定時にコンテンツ作成者に表示されるスタイルメニュー内にまとめてグループ化できます。
   * **スタイルは結合できません：**&#x200B;そのグループ内の複数のスタイルを一度に選択できます。
   * **スタイル名：**&#x200B;コンポーネントのスタイルの設定時に、コンテンツ作成者に表示されるスタイルの説明。
   * **CSS クラス：**&#x200B;スタイルと関連付けられている CSS クラスの実際の名前。

   ドラッグハンドルを使用すると、グループの順序とグループ内のスタイルを調整できます。 追加アイコンまたは削除アイコンを使用すると、グループやグループ内のスタイルを追加したり削除したりできます。

>[!CAUTION]
>
>コンポーネントポリシーのスタイルプロパティとして設定されている CSS クラスと、必要な JavaScript を動作可能にするには、[クライアントライブラリ](/help/implementing/developing/introduction/clientlibs.md)としてデプロイする必要があります。

## セットアップ {#setup}

コアコンポーネントのバージョン 2 以降はスタイルシステムを完全に活用できるので、追加の設定は不要です。

以下の手順は、独自のカスタムコンポーネントに対してスタイルシステムを有効にする場合、または[編集ダイアログのオプションの「スタイル」タブを有効にする](#enable-styles-tab-edit)場合にのみ必要です。

### デザインダイアログの「スタイル」タブを有効にする {#enable-styles-tab-design}

コンポーネントが AEM のスタイルシステムと連動し、デザインダイアログに「スタイル」タブが表示されるようにするには、コンポーネント開発者がコンポーネントに次の設定を行って「スタイル」タブを組み込む必要があります。

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>これは、[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) を介して[オーバーレイ](/help/implementing/developing/introduction/overlays.md)を使用します。

コンポーネントが設定されると、すべての編集可能なコンポーネントを自動的にラップする装飾要素に、ページ作成者が設定したスタイルが AEM により自動的に挿入されます。コンポーネント自体で必要な操作はこれで終わりです。

### 編集ダイアログの「スタイル」タブを有効にする {#enable-styles-tab-edit}

編集ダイアログの「スタイル」タブもオプションで使用できます。「デザインダイアログ」タブとは異なり、編集ダイアログのタブは、スタイルシステムが機能するのに必須ではなく、コンテンツ作成者がスタイルを設定するためのオプションの代替インターフェイスです。

編集ダイアログのタブは、デザインダイアログのタブと同様の方法で組み込むことができます。

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>これは、[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) を介して[オーバーレイ](/help/implementing/developing/introduction/overlays.md)を使用します。

>[!NOTE]
>
>編集ダイアログの「スタイル」タブは、デフォルトでは有効になっていません。

### 要素名を持つスタイル {#styles-with-element-names}

開発者は `cq:styleElements` 文字列配列プロパティを使用して、コンポーネントのスタイルに使用できる要素名のリストを設定することもできます。その後、テンプレート作成者はデザインダイアログのポリシーの「スタイル」タブで、各スタイルに設定する要素名を選択することもできます。これにより、ラッパー要素の要素名が設定されます。

このプロパティは `cq:Component` ノードに設定されます。次に例を示します。

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>組み合わせ可能なスタイルには要素名を定義しないでください。 複数の要素名を定義する場合の、優先順位は次のようになります。
>
>1. HTL（`data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`）が他のすべての要素よりも優先されます。
>1. 次に、複数のアクティブなスタイルの中で、コンポーネントのポリシーで設定されたスタイルのリストの最初のスタイルが優先されます。
>1. 最後に、コンポーネントの `cq:htmlTag` または `cq:tagName` がフォールバック値と見なされます。
>

スタイル名を定義するこの機能は、レイアウトコンテナやコンテンツフラグメントコンポーネントなどの一般的なコンポーネントに意味を追加できます。

例えば、レイアウトコンテナに `<main>`、`<aside>`、`<nav>` などのセマンティクスを指定できます。
