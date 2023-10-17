---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service のコンテンツを作成するためにリッチテキストエディターを設定します。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service のコンテンツを作成するためにリッチテキストエディターを設定します。'
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '1876'
ht-degree: 100%

---

# リッチテキストエディターの設定 {#configure-the-rich-text-editor}

リッチテキストエディター（RTE）には、テキストコンテンツの編集に使用できる幅広い機能が用意されています。アイコン、選択ボックス、ツールバーおよびメニューを使用して、テキストを WYSIWYG で編集できます。管理者は RTE の設定をおこなって、オーサリングコンポーネント内で使用可能な機能を有効化、無効化および拡張できます。作成者が Web コンテンツの[オーサリングに RTE を使用する](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)方法を参照してください。

RTE の概念と設定に必要な手順を以下に示します。

| RTE の概念について | 必要な機能を有効にする | 個々の機能の設定 |
|---|---|---|
| [インターフェイスの理解](#understand-rte-ui) | [設定の場所の理解および設定](#understand-the-configuration-paths-and-locations) | [プラグインの設定](#enable-rte-functionalities-by-activating-plug-ins) |
| [編集モードの種類](#editingmodes) | [プラグインのアクティベーション](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [機能プロパティの設定](#aboutplugins) |
| [プラグインについて](#aboutplugins) | [RTE ツールバーの設定](#dialogfullscreen) | [貼り付けモードの設定](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## 作成者が使用できるユーザーインターフェイスを理解します。 {#understand-rte-ui}

RTE インターフェイスは、オーサリング環境に[レスポンシブデザイン](/help/sites-cloud/authoring/features/responsive-layout.md)を提供します。このインターフェイスは、タッチデバイスとデスクトップデバイスで使用できるように設計されています。

![リッチテキストエディターのツールバー](assets/rte-toolbar-full-screen-mode.png)

*図：使用可能なすべてのオプションが有効なリッチテキストエディターのツールバー*

ツールバーには、WYSIWYG オーサリング環境で使用できるオプションが用意されています。[!DNL Experience Manager] の管理者は、インターフェイスのツールバーで使用できるオプションを設定できます。[!DNL Experience Manager] では、包括的な編集オプションセットをデフォルトで使用できます。開発者は [!DNL Experience Manager] をカスタマイズして、さらに編集オプションを追加できます。

## 各種編集モード {#editingmodes}

[!DNL Experience Manager] では、コンポーネントの各種モードを使用して、テキストコンテンツを作成および編集できます。コンテンツをオーサリングおよび書式設定するためのツールバーオプションと、各種編集モードにおける RTE 対応コンポーネントのユーザーエクスペリエンスは、RTE 設定によって異なります。

| 編集モード | 編集領域 | 有効化が推奨される機能 |
|--- |--- |--- |
| インライン | 小規模な編集をすばやく行うのに適したインプレース編集で、ダイアログボックスを開かずに書式設定を行います。 | 最小限の RTE 機能。 |
| RTE フルスクリーン | ページ全体に広がる。 | 必要なすべての RTE 機能。 |
| ダイアログ | ダイアログボックスがページコンテンツの上部に表示されますが、ページ全体には広がりません。 | 慎重に有効化された機能。 |
| ダイアログフルスクリーン | フルスクリーンモードと同じ。RTE の横にダイアログのフィールドを含む。 | 必要なすべての RTE 機能。 |

>[!NOTE]
>
>インライン編集モードでは、ソース編集機能を使用できません。フルスクリーンモードでは画像をドラッグできません。その他の機能はすべて全モードで使用できます。

### インライン編集 {#inline-editing}

ページ内のコンテンツを編集するには、ゆっくりダブルクリックしてコンテンツを開きます。基本オプションを備えた、コンパクトなツールバーが表示されます。

![ツールバーの基本オプションを使用したインライン編集](assets/inline-editing-mode-basic-options.png)

*図：ツールバーの基本オプションを使用したインライン編集。*

### フルスクリーン編集 {#full-screen-editing}

[!DNL Experience Manager] コンポーネントをフルスクリーン表示で開くことができます。この表示にした場合は、ページコンテンツが隠され、使用可能なスクリーンが占有されます。フルスクリーン編集には最も多くの編集オプションがあるので、インライン編集の詳細版と考えてください。インライン編集モードの使用中にコンパクトツールバーから ![全画面表示で RTE を開くためのアイコン](assets/rte_fullscreen.png) をクリックして開くことができます。

ダイアログフルスクリーンモードでは、詳細な RTE ツールバーのほかに、ダイアログ内で使用可能なオプションとコンポーネントも提供されます。このモードは、他のコンポーネントと共に RTE を含むダイアログにのみ適用されます。

![フルスクリーンモードで編集する場合の詳細な RTE ツールバー](assets/rte-toolbar-full-screen-mode.png)

*図：フルスクリーンモードで編集する場合の詳細な RTE ツールバー。*

### ダイアログ編集 {#dialog-editing}

コンポーネントをダブルクリックすると、コンテンツ編集用のダイアログボックスが開きます。ダイアログボックスは、既存のページの上部に開きます。場合によっては、ダイアログがポップアップウィンドウとして開くこともあります。例えば、複数列から成るページレイアウト内の列の一部がテキストコンポーネントで、ダイアログに使用できる領域が少ない場合などです。

![ダイアログ編集モード](assets/dialog_editing_modetouchui.png)

*図：ダイアログ編集モード。*

## RTE プラグインと関連機能について {#aboutplugins}

この機能は、一連のプラグインを介して使用可能になります。各プラグインには以下が含まれます。

* `features` プロパティ

   * プラグインの基本機能をアクティベートまたはアクティベート解除するために使用します。
   * 標準化された手順を使用して設定します。

* 必要に応じて、さらなるプロパティやオプションに特別な設定が必要です。

RTE の基本機能は、該当するプラグインのノードにある `features` プロパティの値によって、アクティベートまたはアクティベート解除されます。

以下の表に、現在のプラグインを示します。

* API ドキュメントへのリンクを含むプラグイン ID。ID は、[プラグインをアクティベート](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin)するときにノード名として使用されます。
* `features` プロパティの許可されている値。
* プラグインが提供する機能の説明。

| プラグイン ID | 機能 | 説明 |
|--- |--- |--- |
| edit | `cut`、`copy`、`paste-default`、`paste-plaintext`、`paste-wordhtml` | [カット、コピーおよび 3 種類のペーストモード](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles)。 |
| findreplace | `find`、`replace` | 検索と置換。 |
| format | `bold`、`italic`、`underline` | [基本的なテキストの書式設定](configure-rich-text-editor-plug-ins.md#textstyles)。 |
| 画像 | `image` | 基本的な画像サポート（コンテンツまたはコンテンツファインダーからのドラッグ）。ブラウザーの種類に応じて、様々なサポート機能が提供されます |
| keys | - | この値を定義するには、[タブサイズ](configure-rich-text-editor-plug-ins.md#tabsize)を参照してください。 |
| justify | `justifyleft`、`justifycenter`、`justifyright` | 段落の整列。 |
| links | `modifylink`、`unlink`、`anchor` | [ハイパーリンクおよびアンカー](configure-rich-text-editor-plug-ins.md#linkstyles)。 |
| lists | `ordered`、`unordered`、`indent`、`outdent` | このプラグインは、[インデントとリスト](configure-rich-text-editor-plug-ins.md#indentmargin)（ネストされたリストを含む）の両方を制御します。 |
| misctools | `specialchars`、`sourceedit` | 各種ツールを使用して、[特殊文字](configure-rich-text-editor-plug-ins.md#spchar)の入力や HTML ソースの編集をおこなえます。また、独自のリストを定義する場合は、[特殊文字の範囲](configure-rich-text-editor-plug-ins.md#definerangechar)を追加できます。 |
| Paraformat | `paraformat` | `<h2>`デフォルトの段落形式は、段落、見出し 1、見出し 2 および見出し 3（`<p>`、`<h1>`、`<h3>`）です。[他の段落形式を追加](configure-rich-text-editor-plug-ins.md#paraformats)したり、リストを拡張したりできます。 |
| spellcheck | `checktext` | [言語ごとのスペルチェッカー](configure-rich-text-editor-plug-ins.md#adddict)。 |
| styles | `styles` | CSS クラスを使用したスタイル設定のサポート。テキストで使用するスタイルの範囲を独自に追加（または拡張）する場合は、[新しいテキストスタイルを追加](configure-rich-text-editor-plug-ins.md#textstyles)します。 |
| subsuperscript | `subscript`、`superscript` | 下付き文字や上付き文字を追加して基本的なフォーマットを拡張。 |
| table | `table`、`removetable`、`insertrow`、`removerow`、`insertcolumn`、`removecolumn`、`cellprops`、`mergecells`、`splitcell`、`selectrow`、`selectcolumns` | テーブル全体または個々のセルに独自のスタイルを追加する場合は、[テーブルスタイルの設定](configure-rich-text-editor-plug-ins.md#tablestyles)を参照してください。 |
| undo | `undo`、`redo` | [取り消しおよびやり直し](configure-rich-text-editor-plug-ins.md#undohistory)操作の履歴サイズ。 |

>[!NOTE]
>
>フルスクリーンプラグインは、ダイアログモードではサポートされません。`dialogFullScreen` 設定を使用して、フルスクリーンモード用のツールバーを設定します。

## 設定パスと設定の場所について {#understand-the-configuration-paths-and-locations}

作成者に提供する [RTE 編集のモードおよびインターフェイス](#editingmodes)によって、[RTE プラグインをアクティベート](configure-rich-text-editor-plug-ins.md#activateplugin)するときの設定詳細の場所が決まります。場所は次のとおりです。

* インラインモード：`cq:editConfig/cq:inplaceEditing`。
* フルスクリーンモード：`cq:editConfig/cq:inplaceEditing`。
* ダイアログモード：`cq:dialog`。
* フルスクリーンダイアログモード：`cq:dialog`。

>[!NOTE]
>
>`cq:inplaceEditing` の下のノードの名前を `config` にしないでください。`cq:inplaceEditing` ノードで、以下のプロパティを定義します。
>
>* **名前**：`configPath`
>* **型**：`String`
>* **値**：実際の設定を含むノードのパス
>
>RTE 設定ノードの名前を `config` にしないでください。この名前にすると、RTE 設定が管理者に対してのみ有効になり、グループ `content-author` のユーザーに対して有効になりません。

ダイアログ編集モードで適用する次のプロパティを設定します。

* `useFixedInlineToolbar`：RTE ツールバーは、フローティングではなく固定することができます。RTE ノードで定義されているこのブール型プロパティ sling:resourceType= `cq/gui/components/authoring/dialog/richtext` を `True` に設定します。このプロパティを `True` に設定すると、リッチテキストの編集が `foundation-contentloaded` イベントで開始されます。これを防ぐには、`customStart` プロパティを `True` に設定し、`rte-start` イベントを呼び出して RTE の編集を開始するようにします。このプロパティが `true` の場合、RTE はクリックで開始しなくなり、これがデフォルトの動作になります。

* `customStart`：RTE を開始するタイミングを `True` イベントの呼び出しによって制御するには、RTE ノードに定義されているこのブール値プロパティを `rte-start` に設定します。

* `rte-start`：このイベントを RTE の `contenteditable-div`（RTE の編集を開始するタイミング）で呼び出します。これは、`customStart` が `true` に設定されている場合にのみ機能します。

タッチ操作対応ダイアログで RTE を使用する場合は、問題を回避するために `useFixedInlineToolbar` プロパティを `true` に設定します。

## プラグインのアクティベートによる RTE 機能の有効化 {#enable-rte-functionalities-by-activating-plug-ins}

リッチテキストエディター（RTE）の各機能は一連のプラグインから使用でき、それぞれに features プロパティがあります。features プロパティを設定することで、各プラグインの様々な機能を有効化または無効化できます。

RTE プラグインの設定について詳しくは、[RTE プラグインをアクティベートして設定する方法](configure-rich-text-editor-plug-ins.md)を参照してください。

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

[コアコンポーネントのテキストコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=ja#the-text-component-and-the-rich-text-editor)を使用すると、テンプレートエディターのユーザーインターフェイスを使用して多数の RTE プラグインをコンテンツポリシーとして設定でき、技術的な設定が不要になります。コンテンツポリシーは、このドキュメントで説明するように RTE UI 設定と連携させることができます。詳しくは、[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md)および[コアコンポーネント開発者向けドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja)を参照してください。

>参照用として、デフォルトのテキストコンポーネント（標準インストールの一環として提供）が次の場所に用意されています。
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>独自のテキストコンポーネントを作成するには、上記のコンポーネントを直接編集するのではなく、コピーしてください。

## RTE ツールバーの設定 {#dialogfullscreen}

[!DNL Experience Manager] では、リッチテキストエディターのインターフェイスを編集モードごとに異なる設定にできます。デフォルト設定を以下に示します。これらの設定を必要に応じて上書きできます。作成者に提供するツールバー機能のみをカスタマイズします。すべてのツールバー設定を指定する必要はありません。

`dialogFullScreen` 用のツールバーを設定するには、次のサンプル設定を使用します。

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

インラインモードとフルスクリーンモードでは別のユーザーインターフェイス設定が使用されます。ツールバープロパティは、ツールバーのオプションを指定します。

例えば、オプション自体が 1 つの機能（例：`Bold`）である場合は、`PluginName#FeatureName` と指定されます（例：`links#modifylink`）。

オプションがポップオーバー（プラグインのいくつかの機能を含む）の場合は、`#PluginName` と指定されます（例：`#format`）。

オプションのグループの間の区切り文字（`|`）は、`-` で指定できます。

インラインまたはフルスクリーンモードのポップアップノードには、使用するポップオーバーのリストが含まれます。`popovers` ノードの下の各子ノードは、プラグインの名前を取って名付けられます（例：format）。プラグインの機能のリストが含まれるプロパティ「items」があります（例：format#bold）。

## RTE ユーザーインターフェイス設定とコンテンツポリシー {#rtecontentpolicies}

管理者は、上述のような設定を行わなくても、コンテンツポリシーを使用して RTE オプションを制御することができます。コンテンツポリシーでは、[編集可能テンプレート](/help/sites-cloud/authoring/features/templates.md)の一部として使用されるコンポーネントのデザインプロパティが定義されています。例えば、RTE を使用するテキストコンポーネントを編集可能テンプレートで使用する場合は、コンテンツポリシーの定義によって、太字オプションやいくつかの段落書式オプションが使用できるようになります。コンテンツポリシーは再利用可能であり、複数のテンプレートに対して適用できます。

RTE フローで使用可能なオプションに関するユーザーインターフェイス設定がコンテンツポリシーに影響します。

* ユーザーインターフェイス設定では、コンテンツポリシーで使用可能なオプションを定義します。
* RTE のユーザーインターフェイス設定が削除されたか、どの項目も有効にしていない場合、コンテンツポリシーではその設定ができません。
* 作成者は、ユーザーインターフェイス設定およびコンテンツポリシーによって使用可能となっている機能にのみアクセスできます。

例については、[テキストコアコンポーネントのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=ja#the-text-component-and-the-rich-text-editor)を参照してください。

## ツールバーアイコンとコマンドのマッピングのカスタマイズ {#iconstoolbar}

RTE ツールバーに表示される Coral アイコンと使用可能なコマンドとのマッピングをカスタマイズできます。Coral アイコンに加えて他のアイコンを使用することはできません。

1. `icons` の下に、`uiSettings/cui` という名前のノードを作成します。

1. そのノードの下に、各アイコンのノードを作成します。
1. 個々のアイコンノードで、Coral アイコンとそのアイコンにマッピングするコマンドを指定します。

以下に、`textItalic` という名前の Coral アイコンにコマンド「`Bold`」をマッピングするサンプルスニペットを示します。

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## 既知の制限事項 {#known-limitations}

[!DNL Experience Manager] RTE 機能には次の制限があります。

* RTE 機能は [!DNL Experience Manager] コンポーネントダイアログでのみサポートされます。RTE は、ウィザードまたは Foundation-forms ではサポートされていません。

* [!DNL Experience Manager] はハイブリッドデバイスでは機能しません。 <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* RTE 設定ノードの名前を `config` にしないでください。この名前にすると、RTE 設定が管理者に対してのみ有効になり、グループ `content-author` のユーザーに対して有効になりません。

* RTE は、インラインフレームまたは iframe へのコンテンツの埋め込みをサポートしていません。

## ベストプラクティスとヒント {#best-practices-and-tips}

* フローティングダイアログの場合は、ポップアップダイアログを表示しないプラグインのみを有効にします。ポップアップなしのプラグインはサイズが小さく、フローティングダイアログに最適です。
* `Paste` プラグインなど、大きめのポップアップがあるプラグインは、フルスクリーンダイアログモードまたはフルスクリーンモードでのみ有効にします。大きなポップアップがあるプラグインは、優れたオーサリング環境を提供するために、より多くのスクリーンスペースを必要とします。
* CoralUI3 RTE 用カスタムプラグインを使用する場合は、`rte.coralui3` ライブラリを使用してください。

>[!MORELIKETHIS]
>
>* [RTE プラグインの設定](configure-rich-text-editor-plug-ins.md)
>* [リッチテキストエディターをオーサリングに使用](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [RTE をアクセス可能なサイト用に設定](rte-accessible-content.md)
