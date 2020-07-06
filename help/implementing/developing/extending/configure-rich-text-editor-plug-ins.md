---
title: Configure the Rich Text Editor plug-ins in [!DNL Adobe Experience Manager].
description: リッチテキストエディタ [!DNL Adobe Experience Manager] ープラグインの設定について説明します。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 739dde6f9a6a7f4fe773e27e53f23a395f2881dc
workflow-type: tm+mt
source-wordcount: '4301'
ht-degree: 77%

---


# リッチテキストエディタープラグインの設定 {#configure-the-rich-text-editor-plug-ins}

リッチテキストエディター（RTE）の各機能は一連のプラグインを介して使用可能になり、それぞれに features プロパティがあります。features プロパティを設定することで、1 つ以上の RTE 機能を有効または無効にできます。この記事では、RTE プラグインの特殊な設定方法について説明します。

他の RTE 設定について詳しくは、[リッチテキストエディターの設定](/help/implementing/developing/extending/rich-text-editor.md)を参照してください。

>[!NOTE]
>
>CRXDE Lite を使用する場合は、「[!UICONTROL すべて保存]」オプションを使用して、変更を定期的に保存することをお勧めします。

## プラグインのアクティベートと features プロパティの設定 {#activateplugin}

プラグインをアクティベートするには、次の手順に従います。初めてプラグインを設定するときは、対応するノードが存在しないので、一部の手順のみ実行します。

By default, `format`, `link`, `list`, `justify`, and `control` plug-ins and all their features are enabled in RTE.

>[!NOTE]
>
>この記事では、重複を避けるために、それぞれの `rtePlugins` ノードを `<rtePlugins-node>` と表記しています。

1. CRXDE Lite を使用して、プロジェクトのテキストコンポーネントを見つけます。
1. RTE プラグインを設定する前に、`<rtePlugins-node>` の親ノードを作成します（親ノードがない場合）。

   * 親ノード（コンポーネントに応じる）：

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * 代替の設定ノード: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * 型：**jcr:primaryType** `cq:Widget`
   * いずれも以下のプロパティを持ちます。

      * **名前** `name`
      * **型** `String`
      * **値** `./text`


1. 設定するインターフェイスに応じて、ノード `<rtePlugins-node>` を作成します（まだ存在しない場合）。

   * **名前** `rtePlugins`
   * **型** `nt:unstructured`

1. この下に、アクティベートする各プラグインのノードを作成します。

   * **型** `nt:unstructured`
   * **名前** 必要なプラグインのプラグイン ID

プラグインをアクティベートしたら、次のガイドラインに従って `features` プロパティを設定します。

|  | すべての機能を有効化 | 一部の特定の機能を有効化。 | すべての機能を無効化. |
|---|---|---|---|
| 名前 | 機能 | 機能 | 機能 |
| 型 | String | `String` (複数文字列； タイプをに設定 `String` し、CRXDE Liteでクリック `Multi` します) | String |
| 値 | `*`（アスタリスク） | 1つ以上のフィーチャ値に設定します。 | - |

## findreplace プラグインの理解 {#findreplace}

`findreplace` プラグインには設定は必要ありません。すぐに使用できます。

置換機能を使用する場合は、検索文字列と同時に置換後の文字列も入力する必要があります。ただし、置換する前に「検索」をクリックして文字列を検索することはできます。「検索」をクリックした後に置換後の文字列を入力すると、検索がリセットされ、テキストの先頭から再開されます。

検索と置換ダイアログは、「検索」をクリックすると透明になり、「置換」をクリックすると不透明になります。この動作により、作成者は置き換えられるテキストを確認できます。 「すべてを置換」をクリックすると、ダイアログが閉じて、実行された置換の回数が表示されます。

## 貼り付けモードの設定 {#pastemodes}

RTE では、次の 3 つのいずれかのモードで、コンテンツを貼り付けることができます。

* **ブラウザーモード**：ブラウザーのデフォルトの貼り付け機能を使用して、テキストを貼り付けます。この方法は推奨されません。不要なマークアップが追加されることがあります。

* **プレーンテキストモード**：クリップボードの内容をプレーンテキストとして貼り付けます。It strips all elements of style and formatting from the copied content before inserting in [!DNL Experience Manager] component.

* **MS Word モード**：MS Word からテキスト（テーブルを含む）を書式付きでコピーして貼り付けます。Web ページや MS Excel など、他のソースからのテキストのコピー＆貼り付けはサポートされていないので、一部の書式しか保持されません。

### RTE ツールバーで使用可能な貼り付けオプションの設定  {#configure-paste-options-available-on-the-rte-toolbar}

これらの 3 つのアイコンのいくつか、またはすべてを RTE ツールバーに表示できます（どのアイコンも表示しないという選択も可能です）。

* **[!UICONTROL 貼り付け（Ctrl + V）]**：事前設定によって、3 つの貼り付けモードのいずれかに対応付けることができます。

* **[!UICONTROL テキストとして貼り付け]**：プレーンテキストモード機能を提供します。

* **[!UICONTROL Word から貼り付け]**：MS Word モード機能を提供します。

必須アイコンを表示するように RTE を設定するには、以下の手順に従います。

1. 例えば、`/apps/<myProject>/components/text` コンポーネントに移動します。
1. `rtePlugins/edit` ノードに移動します。このノードが存在しない場合は、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `features` ノードの `edit` プロパティを作成し、1 つ以上の機能を追加します。すべての変更を保存します。

### 貼り付け（Ctrl + V）アイコンとショートカットの動作の設定 {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

以下の手順に従って、**[!UICONTROL 貼り付け（Ctrl + V）]**&#x200B;アイコンの動作を事前設定できます。また、この設定では、作成者がコンテンツの貼り付けに使用するキーボードショートカット Ctrl + V の動作も定義します。

この設定では、以下の 3 つの使用方法を定義できます。

* ブラウザーのデフォルトの貼り付け機能を使用して、テキストを貼り付けます。この方法は推奨されません。不要なマークアップが追加されることがあります。下の `browser` を使用して設定します。

* クリップボードの内容をプレーンテキストとして貼り付けます。It strips all elements of style and formatting from the copied content before inserting in [!DNL Experience Manager] component. 下の `plaintext` を使用して設定します。

* MS Word からテキスト（テーブルを含む）を書式付きでコピーして貼り付けます。Web ページや MS Excel など、他のソースからのテキストのコピー＆貼り付けはサポートされていないので、一部の書式しか保持されません。下の `wordhtml` を使用して設定します。

1. コンポーネント内で、`<rtePlugins-node>/edit` ノードに移動します。ノードが存在しない場合は、ノードを作成します。 詳しくは、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `edit` ノード内で、次の詳細情報を使用してプロパティを作成します。

   * **名前** `defaultPasteMode`
   * **型** `String`
   * **値** は、、、またはの各 `browser``plaintext``wordhtml` モードの必要な貼り付けモードの1つです。

### コンテンツの貼り付け時に使用可能な書式の設定 {#pasteformats}

The paste-as-Microsoft-Word (`paste-wordhtml`) mode can be further configured so that you can explicitly allow a few styles when pasting in [!DNL Experience Manager] from another program, such as [!DNL Microsoft Word].

For example, if only bold formats and lists should be allowed when pasting in [!DNL Experience Manager], you can filter out the other formats. これは、設定可能な貼り付けフィルタリングと呼ばれ、次の両方に対して実行できます。

* [テキスト](#pastemodes)
* [リンク](#linkstyles)

リンクに関しては、自動的に承認されるプロトコルも定義できます。

To configure which formats are allowed when pasting text into [!DNL Experience Manager] from another program:

1. コンポーネント内で、ノード `<rtePlugins-node>/edit` に移動します。ノードが存在しない場合は、ノードを作成します。 詳しくは、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `edit` ノードの下に、HTML 貼り付けルールを格納するノードを作成します。

   * **名前** `htmlPasteRules`
   * **型** `nt:unstructured`

1. `htmlPasteRules` の下に、使用可能な基本書式の詳細を格納するノードを作成します。

   * **名前** `allowBasics`
   * **型** `nt:unstructured`

1. 受け入れられる個々の書式を制御するには、以下のうち 1 つまたは複数のプロパティを `allowBasics` ノードで作成します。

   * **名前** `bold`
   * **名前** `italic`
   * **名前** `underline`
   * **名前** `anchor`（リンクと名前付きアンカーの両方に対応）
   * **名前** `image`

   プロパティの&#x200B;**型**&#x200B;はすべて `Boolean` なので、該当する&#x200B;**値**&#x200B;では、チェックマークを付けるか外すことで、機能を有効または無効にできます。

   >[!NOTE]
   >
   >明示的に定義されていない場合は、デフォルト値である true が使用され、書式が承認されます。

1. その他の様々なプロパティやノードを使用して、その他の書式も定義でき、`htmlPasteRules` ノードに適用できます。

| プロパティ | 型 | 説明 |
|--- |--- |--- |
| `allowBlockTags` | `String` | 使用可能なブロックタグのリストを定義します。ヘッドライン(h1、h2、h3)、段落(p)、リスト(ol、ul)、テーブル(table)など、使用できるブロックタグがいくつかあります。 |
| `fallbackBlockTag` | `String` | Defines the block tag used for any blocks having a block tag not included in `allowBlockTags`. 通常は十分で `p` す。 |
| `table` | `nt:unstructured` | テーブルを貼り付けるときの動作を定義します。このノードには、テーブルの貼り付けを許可するかどうかを定義するプロパティ allow（型は Boolean）が必要です。allowがfalseに設定されている場合、貼り付けられたテーブルコンテンツの処理方法を定義するには、プロパティignoreMode（タイプString）を指定する必要があります。 ignoreModeの有効な値は、テーブルの内容 `remove` を削除し、テーブルのセルを段落 `paragraph` に変換することです。 |
| `list` | `nt:unstructured` | リストを貼り付けるときの動作を定義します。リストの貼り付けを許可するかどうかを定義するプロパティ `allow`（型は Boolean）が必要です。If `allow` is set to `false`, specify the property `ignoreMode` (type `String`) to define how to handle any list content pasted. ignoreModeの有効な値は、リストの内容 `remove` を削除し、リスト項目 `paragraph` を段落に変換することです。 |

有効な `htmlPasteRules` 構造の例を以下に示します。

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. すべての変更を保存します。

## テキストスタイルの設定 {#textstyles}

スタイルを適用して、テキストの外観を部分的に変更できます。スタイルは、CSS スタイルシートに事前定義する CSS クラスに基づきます。スタイル設定したコンテンツは、CSS クラスを参照する `span` 属性を使用して `class` タグで囲まれます。次に例を示します。

`<span class=monospaced>Monospaced Text Here</span>`

スタイルプラグインを初めて有効にしたときは、使用可能なデフォルトのスタイルがありません。ポップアップリストは空です。スタイルを使用できるようにするには、次の操作をおこないます。

* 「スタイル」ドロップダウンセレクターを有効にします。
* スタイルシートの場所を1つ以上指定します。
* スタイルポップアップリストから選択できる個々のスタイルを指定します。

後で再設定する場合は、別のスタイルを追加する場合は、説明に従って新しいスタイルシートを参照し、追加のスタイルを指定します。

>[!NOTE]
>
>[テーブルやテーブルセル](configure-rich-text-editor-plug-ins.md#tablestyles)のスタイルを定義することもできます。これらの設定には別の手順が必要となります。

### 「スタイル」ドロップダウンセレクターリストの有効化{#styleselectorlist}

これをおこなうには、スタイルプラグインを有効にします。

1. コンポーネント内で、ノード `<rtePlugins-node>/styles` に移動します。ノードが存在しない場合は、ノードを作成します。 詳しくは、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `features` ノードで `styles` プロパティを作成します。

   * **名前** `features`
   * **型** `String`
   * **値** `*`（アスタリスク）

1. すべての変更を保存します。

>[!NOTE]
>
>スタイルプラグインが有効になると、編集ダイアログに「スタイル」ドロップダウンリストが表示されます。ただし、スタイルが設定されていないので、リストは空です。

### スタイルシートの場所の指定 {#locationofstylesheet}

次に、参照するスタイルシートの場所を指定します。

1. テキストコンポーネントのルートノードに移動します（例：`/apps/<myProject>/components/text`）。
1. `externalStyleSheets` の親ノードに、`<rtePlugins-node>` プロパティを追加します。

   * **名前** `externalStyleSheets`
   * **型** `String[]`（複数文字列。CRXDE で「**複数**」をクリック）
   * **値** 使用する各スタイルシートのパスとファイル名。リポジトリパスを使用します。

   >[!NOTE]
   >
   >参照先のスタイルシートは後から追加できます。

1. すべての変更を保存します。

ダイアログ（クラシックUI）でRTEを使用する場合、リッチテキストの編集用に最適化されたスタイルシートを指定できます。 技術的な制限により、CSSコンテキストはエディターで失われるので、このコンテキストをエミュレートしてWYSIWYGの操作性を向上させることができます。

リッチテキストエディターは、コンテナDOM要素を使用します。IDは、表示や編集に対して異なるスタイル `CQrte` を提供する、次のようなIDを持ちます。

```css
#CQ td {
// defines the style for viewing
 }
```

```css
#CQrte td {
 // defines the style for editing
 }
```

### ポップアップリストで使用可能なスタイルの指定 {#stylesindropdown}

1. コンポーネント定義内で、「[スタイル](#styleselectorlist)」ドロップダウンセレクターの有効化で作成したように、ノード `<rtePlugins-node>/styles` に移動します。
1. Under the node `styles`, create a node (also called `styles`) to hold the list being made available:

   * **名前** `styles`
   * **型** `cq:WidgetCollection`

1. Create a node under the `styles` node to represent an individual style:

   * **名前** 実際のスタイルに適した名前を指定可能
   * **型** `nt:unstructured`

1. CSS クラスを参照する `cssName` プロパティをこのノードに追加します。

   * **名前** `cssName`
   * **型** `String`
   * **値** CSS クラスの名前（先頭に &quot;.&quot; を付けない。例、`.cssClass` ではなく `cssClass`）

1. `text` プロパティを同じノードに追加します。これは、選択ボックスに表示されるテキストを定義します。

   * **名前** `text`
   * **型** `String`
   * **値** スタイルの説明。この説明は、「スタイル」ドロップダウン選択ボックスに表示されます。

1. 変更内容を保存します。

   必要な各スタイルについて上記の手順を繰り返します。

### 日本語で最適な単語分割をするための RTE の設定 {#jpwordwrap}

Authors using [!DNL Experience Manager] to author Japanese language content can apply a style to characters to avoid line break where a break is not required. これにより、作成者は文を目的の位置で区切ることができます。この機能のスタイルは、CSS スタイルシートに事前定義する CSS クラスに基づいています。

作成者が日本語のテキストに適用できるスタイルを作成するには、次の手順に従います。

1. stylesノードの下にノードを作成します。 See [specify a style](#stylesindropdown).
   * 名前：`jpn-word-wrap`
   * 型：`nt:unstructure`

1. CSS クラスを参照する `cssName` プロパティをノードに追加します。このクラス名は日本語のワードラップ機能のための予約名です。
   * 名前：`cssName`
   * 型：`String`
   * 値：`jpn-word-wrap`（先行の `.` なし）

1. プロパティテキストを同じノードに追加します。値は、スタイルを選択するときに作成者に表示されるスタイルの名前です。
   * 名前：`text`
*型： 
`String`
   * 値：`Japanese word-wrap`

1. スタイルシートを作成し、パスを指定します。 [スタイルシートの場所を指定](#locationofstylesheet)を参照してください。スタイルシートに次のコンテンツを追加します。必要に応じて背景色を変更してください。

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![日本語の折り返し機能を作成者が使用できるスタイルシート](assets/rte_jpwordwrap_stylesheet.jpg)

## 段落書式の設定 {#paraformats}

RTE で作成したテキストは、ブロックタグ（デフォルトでは `<p>` タグ）内に配置されます。`paraformat` プラグインを有効にすることで、ドロップダウン選択リストを使用して、段落に割り当てることができる追加のブロックタグを指定します。段落書式は、正しいブロックタグを割り当てることにより、段落の種類を特定します。作成者は、書式セレクターを使用して書式を選択し、割り当てることができます。ブロックタグとしては、例えば、標準段落 &lt;p> や見出し &lt;h1>、&lt;h2> などがあります。

>[!CAUTION]
>
>このプラグインは、リストやテーブルなど複雑な構造を持つコンテンツには適していません。

>[!NOTE]
>
>If a block tag, for example an `<hr>` tag, can&#39;t be assigned to a paragraph, it is not a valid use case for a `paraformat` plug-in.

段落書式プラグインを初めて有効にしたときは、使用可能なデフォルトの段落書式はありません。ポップアップリストは空です。作成者に段落書式を設定するには、次の手順を実行します。

* Enable the [!UICONTROL Format] pop-up selector list.
* ポップアップメニューから段落書式として選択できるブロックタグを指定します。

後で再設定する場合は、別の形式を追加する場合は、手順の該当部分のみに従います。

### 「フォーマット」ドロップダウンセレクターの有効化{#formatselectorlist}

プラグインを有効にするには、次の `paraformat` 手順に従います。

1. コンポーネント内で、ノード `<rtePlugins-node>/paraformat` に移動します。ノードが存在しない場合は、ノードを作成します。 詳しくは、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `features` ノードで `paraformat` プロパティを作成します。

   * **名前** `features`
   * **型** `String`
   * **値** `*`（アスタリスク）

>[!NOTE]
>
>プラグインをそれ以上設定しない場合、有効になるデフォルトの形式は、段落( `<p>`)、見出し1 ( `<h1>`)、見出し2 ( `<h2>`)、見出し3 ( `<h3>`)です。

>[!CAUTION]
>
>RTE の段落書式を設定する際に、書式オプションとしての段落タグ &lt;p> を削除しないでください。`<p>` タグが削除されると、追加書式を設定したとしても、コンテンツ作成者が「[!UICONTROL 段落書式]」オプションを選択できなくなります。

### 使用可能な段落書式の指定 {#paraformatsindropdown}

段落書式は次の方法で選択できます。

1. コンポーネント定義内で、[「フォーマット」ドロップダウンセレクターの有効化](#styleselectorlist)で作成したように、`<rtePlugins-node>/paraformat` ノードに移動します。
1. Under the `paraformat` node create a node, to hold the list of formats:

   * **名前** `formats`
   * **型** `cq:WidgetCollection`

1. Create a node under the `formats` node, this holds details for an individual format:

   * **名前** 実際の書式に適した名前（myparagraph、myheading1 など）を指定可能です。
   * **型** `nt:unstructured`

1. このノードに、使用するブロックタグを定義するプロパティを追加します。

   * **名前** `tag`
   * **型** `String`
   * **値**：p、h1、h2 など、形式のブロックタグ。

      区切りの山括弧を入力する必要はありません。

1. 同じノードに、説明テキストをドロップダウンリストに表示するための別のプロパティを追加します。

   * **名前** `description`
   * **型** `String`
   * **値** この書式の説明テキスト。例えば、段落、見出し 1、見出し 2 など。このテキストは「フォーマット」選択リストに表示されます。

1. 変更内容を保存します。

   必要な各書式について上記の手順を繰り返します。

>[!CAUTION]
カスタム書式を定義すると、デフォルトの書式（`<p>`、`<h1>`、`<h2>`、`<h3>`）は削除されます。`<p>` 書式はデフォルトの書式なので再作成してください。

## 特殊文字の設定 {#spchar}

In a standard [!DNL Experience Manager] installation, when the `misctools` plug-in is enabled for special characters (`specialchars`) a default selection is immediately available for use; for example, the copyright and trademark symbols.

RTEを設定して、選択した文字を利用できるようにします。 はっきりした文字を定義するか、シーケンス全体を定義することで指定します。

>[!CAUTION]
特殊文字を追加すると、デフォルトの選択よりも優先されます。 必要に応じて、選択した文字を再定義します。

### 単一文字の定義 {#definesinglechar}

1. コンポーネント内で、ノード `<rtePlugins-node>/misctools` に移動します。ノードが存在しない場合は、ノードを作成します。 詳しくは、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `features` ノードで `misctools` プロパティを作成します。

   * **名前** `features`
   * **型** `String[]`
   * **値** `specialchars`

          （このプラグインに関してすべての機能を適用する場合は `String / *`）

1. `misctools` の下に、特殊文字の設定を格納するノードを作成します。

   * **名前** `specialCharsConfig`
   * **型** `nt:unstructured`

1. `specialCharsConfig` の下に、文字のリストを格納する別のノードを作成します。

   * **名前** `chars`
   * **型** `nt:unstructured`

1. Under `chars` add a node to hold an individual character definition:

   * **名前** 文字を反映する名前（half など）を指定可能
   * **型** `nt:unstructured`

1. このノードに、以下のプロパティを追加します。

   * **名前** `entity`
   * **型** `String`
   * **値** 必要な文字の HTML 表現。分数 2 分の 1 を表す場合は `&189;` など。

1. 変更内容を保存します。

CRXDE でプロパティを保存すると、HTML 表現された文字が表示されます。下の例を参照してください。上記の手順を繰り返して、より多くの特殊文字を使用できるようにします。

![CRXDE で、RTE ツールバーで使用可能にする 1 文字を追加します。](assets/chlimage_1-106.png "CRXDE で、RTE ツールバーで使用可能にする 1 文字を追加します。")

### 文字範囲の定義 {#definerangechar}

1. [単一文字の定義](#definesinglechar)の手順 1～3 を使用します。
1. Under `chars` add a node to hold the definition of the character range:

   * **名前** 文字範囲を反映する名前（pencils など）を指定可能
   * **型** `nt:unstructured`

1. このノード（特殊文字の範囲に従って命名）の下に、次の 2 つのプロパティを追加します。

   * **名前** `rangeStart`

      **型** `Long`
      **値** 範囲内の最初の文字の [Unicode](https://unicode.org/) 表現（10 進数）

   * **名前** `rangeEnd`

      **型** `Long`
      **値** 範囲内の最後の文字の [Unicode](https://unicode.org/) 表現（10 進数）

1. 変更内容を保存します。

   例えば、9998 ～ 10000 の範囲を定義すると、次の文字が作成されます。

   ![CRXDE で、RTE で使用可能な文字の範囲を定義します。](assets/chlimage_1-107.png)

   *図：CRXDE で、RTE で使用可能な文字の範囲を定義します。*

   ![RTE で使用できる特殊文字は、ポップアップウィンドウで作成者に表示されます。](assets/rtepencil.png "RTE で使用できる特殊文字は、ポップアップウィンドウで作成者に表示されます。")

## テーブルスタイルの設定 {#tablestyles}

スタイルは一般的に、テキストに適用されますが、テーブルやいくつかのテーブルセルに適用できるスタイルもあります。こうしたスタイルは、セルのプロパティまたはテーブルのプロパティダイアログの「スタイル」セレクターボックスから使用できます。スタイルは、標準のテーブルコンポーネントではなく、テキストコンポーネント（または派生コンポーネント）内のテーブルを編集するときに使用できます。

>[!NOTE]
テーブルとセルのスタイルはクラシック UI 用にのみ定義できます。

>[!NOTE]
RTE コンポーネント内または RTE コンポーネントからのテーブルのコピーおよび貼り付けはブラウザーに依存します。デフォルトでは一部のブラウザーしかサポートされていません。結果はテーブルの構造やブラウザーに応じて様々です。例えば、クラシック UI とタッチ UI の Mozilla Firefox で、RTE コンポーネント内でテーブルをコピーして貼り付ける場合、テーブルのレイアウトは保存されません。

1. コンポーネント内で、以下のノードに移動します。`<rtePlugins-node>/table`ノードが存在しない場合は、ノードを作成します。 詳しくは、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `features` ノードで `table` プロパティを作成します。

   * **名前** `features`
   * **型** `String`
   * **値** `*`

   >[!NOTE]
   テーブルの機能をすべて有効にはしない場合は、`features` プロパティを次のように作成します。
   * **型** `String[]`

   * **値** 必要に応じて、以下のいずれかまたは両方：
      * `table`：スタイルを含むテーブルのプロパティの編集を許可する場合。
      * `cellprops`：スタイルを含むセルのプロパティの編集を許可する場合。


1. 参照する CSS スタイルシートの場所を定義します。これは、[テキストのスタイル](#textstyles)を定義する場合と同じなので、[スタイルシートの場所の指定](#locationofstylesheet)を参照してください。他のスタイルを定義済みであれば、場所は定義されている可能性があります。
1. Under the `table` node create the following nodes as required:

   * テーブル全体のスタイルを定義するには（**[!UICONTROL テーブルのプロパティ]**&#x200B;の下）：

      * **名前** `tableStyles`
      * **型** `cq:WidgetCollection`
   * To define styles for the individual cells (available under **[!UICONTROL Cell properties]**),

      * **名前** `cellStyles`
      * **型** `cq:WidgetCollection`


1. Create a node (under the `tableStyles` or `cellStyles` node as appropriate) to represent an individual style,

   * **名前** 名前を指定できますが、スタイルが反映されている必要があります。
   * **型** `nt:unstructured`

1. このノードで、以下のプロパティを作成します。

   * 参照されるCSSスタイルを定義するには、次の手順を実行します。

      * **名前** `cssName`
      * **型** `String`
      * **値** CSS クラスの名前（先頭の `.` を除く。例、`.cssClass` ではなく `cssClass`）
   * ポップアップセレクターに表示する説明テキストを定義するには、次の手順を実行します。

      * **名前** `text`
      * **型** `String`
      * **値** 選択リストに表示するテキスト


1. すべての変更を保存します。

必要な各スタイルについて上記の手順を繰り返します。

### アクセシビリティ向上のためにテーブル内に非表示のヘッダーを設定 {#hiddenheader}

列ヘッダーの目的が他の列との関係性によって暗示される場合に、目に見えるテキストを列ヘッダーに含まないデータテーブルを作成することがあります。その場合は、ヘッダーセル内に非表示の内部テキストを指定し、様々な補助を必要とするユーザーがスクリーンリーダーやその他補助テクノロジーを利用して列の目的を理解できるようにする必要があります。

このようなシナリオでアクセシビリティを向上させるために、RTE は非表示のヘッダーセルをサポートします。また、テーブルの非表示のヘッダーに関連する設定が用意されています。これらの設定を使用すると、編集モードやプレビューモードで非表示のヘッダーに CSS スタイルを適用できます。作成者が編集モードで非表示のヘッダーを特定できるように、コードに次のパラメーターを追加してください。

* `hiddenHeaderEditingCSS`：RTE が編集されたときに、非表示のヘッダーセルに適用されている CSS クラスの名前を指定します。
* `hiddenHeaderEditingStyle`：RTE が編集されたときに、非表示のヘッダーセルに適用されているスタイル文字列を指定します。

コードに CSS とスタイル文字列の両方を指定すると、CSS がスタイル文字列に優先され、スタイル文字列によって加えられたすべての設定の変更が上書きされることがあります。

作成者がプレビューモードで非表示のヘッダーに CSS を適用できるように、コードに次のパラメーターを追加してください。

* `hiddenHeaderClassName`：プレビューモードで非表示のヘッダーセルに適用される CSS クラスの名前を指定します。
* `hiddenHeaderStyle`：プレビューモードで非表示のヘッダーセルに適用されているスタイル文字列を指定します。

コードに CSS とスタイル文字列の両方を指定すると、CSS がスタイル文字列に優先され、スタイル文字列によって加えられたすべての設定の変更が上書きされることがあります。

## スペルチェッカー用の辞書の追加 {#adddict}

スペルチェックプラグインがアクティベートされると、RTE ではそれぞれ該当する言語の辞書を使用します。その後、サブツリーの言語プロパティを取得するか、URL から言語を抽出することによって、Web サイトの言語に従って辞書が選択されます。例えば、`/en/` ブランチは英語としてチェックされ、`/de/` ブランチはドイツ語としてチェックされます。

>[!NOTE]
インストールされていない言語に関してチェックを試みると、「スペルチェックできませんでした。」というメッセージが表示されます。

標準のExperience Managerインストールには、次の辞書が含まれます。

* アメリカ英語（en_us）
* イギリス英語（en_gb）

>[!NOTE]
The standard dictionaries are located at `/libs/cq/spellchecker/dictionaries`, along with the appropriate ReadMe files. これらのファイルを修正しないでください。

必要に応じて辞書を追加するには、次の手順に従います。

1. ページ [https://extensions.openoffice.org/](https://extensions.openoffice.org/) に移動します。
1. 必要な言語を選択して、スペル定義を含む ZIP ファイルをダウンロードします。アーカイブの内容をファイルシステム上に抽出します。

   >[!CAUTION]
   OpenOffice.org v2.0.1 以前の `MySpell` 形式の辞書のみがサポートされています。辞書は現在アーカイブファイルなので、ダウンロード後にアーカイブを確認することをお勧めします。

1. .aff ファイルと .dic ファイルを見つけます。ファイル名は小文字のままにします。例えば、`de_de.aff` と `de_de.dic` です。
1. `/apps/cq/spellchecker/dictionaries` のリポジトリ内に .aff ファイルと .dic ファイルを読み込みます。

>[!NOTE]
RTE スペルチェッカーは、オンデマンドで使用できます。テキストの入力を開始しても自動的に実行されません。
スペルチェッカーを実行するには、ツールバーの「スペルチェッカー」ボタンをタップまたはクリックします。RTE は、単語のスペルをチェックし、スペルミスした単語をハイライト表示します。
スペルチェッカーが提案した変更を組み込むと、テキストの状態が変更され、スペルミスした単語はハイライト表示されなくなります。スペルチェッカーを実行するには、「スペルチェッカー」ボタンをもう一度タップまたはクリックします。

## 取り消しおよびやり直し操作の履歴サイズの設定 {#undohistory}

RTE では、以前の編集を取り消す、またはやり直すことができます。デフォルトでは、50 回分の編集が履歴に保存されます。この値は必要に応じて設定できます。

1. コンポーネント内で、以下のノードに移動します。`<rtePlugins-node>/undo`これらのノードが存在しない場合は作成します。詳しくは、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `undo` ノードで、以下のプロパティを作成します。

   * **名前** `maxUndoSteps`
   * **型** `Long`
   * **値** 履歴に保存する取り消しステップ数。デフォルトは 50 です。元に戻す／やり直しを完全に無効にする場合、`0` を使用します。

1. 変更内容を保存します。

## タブサイズの設定 {#tabsize}

任意のテキスト内でタブ文字を押すと、事前に定義済みの数のスペースが挿入されます。デフォルトでは、これはノーブレークスペース 3 個とスペース 1 個です。

タブサイズを定義するには、次のようにします。

1. コンポーネント内で、ノード `<rtePlugins-node>/keys` に移動します。ノードが存在しない場合は、ノードを作成します。 詳しくは、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `keys` ノードで、以下のプロパティを作成します。

   * **名前** `tabSize`
   * **型** `String`
   * **値** タブに使用するスペース文字の数.

1. 変更内容を保存します。

## インデントの余白の設定 {#indentmargin}

インデントが有効なとき（デフォルト）は、インデントのサイズを定義できます。

>[!NOTE]
このインデントサイズは、テキストの段落（ブロック）のみに適用されます。実際のリストのインデントには影響しません。

1. コンポーネント内で、以下のノードに移動します。`<rtePlugins-node>/lists`これらのノードが存在しない場合は作成します。詳しくは、[プラグインのアクティベート](#activateplugin)を参照してください。
1. `lists` ノードで、`identSize` パラメーターを作成します。

   * **名前**：`identSize`
   * **型**：`Long`
   * **値**：インデントの余白に必要なピクセル数.

## 編集可能な領域の高さの設定 {#editablespace}

コンポーネントダイアログ内に表示される編集可能なスペースの高さを定義できます。 この設定は、ダイアログでRTEを使用する場合にのみ適用されます。 この設定では、ダイアログウィンドウの高さは変更されません。

1. In the `../items/text` node, in the dialog definition for the component, create a property:

   * **名前** `height`
   * **型** `Long`
   * **値** 編集キャンバスの高さ（ピクセル単位）.

1. 変更内容を保存します。

## リンクのスタイルとプロトコルの設定 {#linkstyles}

でリンクを追加する場合 [!DNL Experience Manager]、使用するCSSスタイルと、自動的に受け入れるプロトコルを定義できます。 To configure how links are added in [!DNL Experience Manager] from another program, define the HTML rules.

1. CRXDE Lite を使用して、プロジェクトのテキストコンポーネントを見つけます。
1. Create a node at the same level as `<rtePlugins-node>`, that is, create the node under the parent node of `<rtePlugins-node>`:

   * **名前** `htmlRules`
   * **型** `nt:unstructured`

   >[!NOTE]
   `../items/text` ノードは次のプロパティを持ちます。
   * **名前** `xtype`
   * **型** `String`
   * **値** `richtext`

   The location of the `../items/text` node can vary, depending on the structure of your dialog. との2つの例があ `/apps/myProject>/components/text/dialog/items/text` り `/apps/<myProject>/components/text/dialog/items/panel/items/text`ます。

1. Under `htmlRules`, create a node.

   * **名前** `links`
   * **型** `nt:unstructured`

1. `links` ノードの下で、必要に応じてプロパティを定義します。

   * 内部リンクの CSS スタイル：

      * **名前** `cssInternal`
      * **型** `String`
      * **値** CSS クラスの名前（先頭に &quot;.&quot; を付けない。例、`.cssClass` ではなく `cssClass`）
   * 外部リンクの CSS スタイル：

      * **名前** `cssExternal`
      * **型** `String`
      * **値** CSS クラスの名前（先頭に &quot;.&quot; を付けない。例、`.cssClass` ではなく `cssClass`）
   * 有効な **[!UICONTROL プロトコルの配列]** ( `https://`、 `https://`、 `file://`、 `mailto:`、など)

      * **名前** `protocols`
      * **型** `String[]`
      * **値** 1 つまたは複数のプロトコル
   * **defaultProtocol**（型が **String** のプロパティ）：ユーザーが明示的に指定しなかった場合に使用されるプロトコル。

      * **名前** `defaultProtocol`
      * **型** `String`
      * **値** 1 つまたは複数のデフォルトプロトコル
   * リンクのターゲット属性の処理方法の定義。 ノードの作成：

      * **名前** `targetConfig`
      * **型** `nt:unstructured`

      `targetConfig` ノード上：必要なプロパティを定義します。

      * ターゲットモードを指定：

         * **名前** `mode`
         * **Type** `String`)
         * **値**：

            * `auto`：自動ターゲットが選択されたことを意味する

               （外部リンクの `targetExternal` プロパティまたは内部リンクの `targetInternal` プロパティで指定）。

            * `manual`：このコンテキストでは使用不可
            * `blank`：このコンテキストでは使用不可
      * 内部リンクのターゲット：

         * **名前** `targetInternal`
         * **型** `String`
         * **値** 内部リンクのターゲット（モードが `auto` の場合にのみ使用）
      * 外部リンクのターゲット：

         * **名前** `targetExternal`
         * **型** `String`
         * **値** 外部リンクのターゲット（モードが `auto` の場合にのみ使用）








1. すべての変更を保存します。
