---
title: マークダウン
description: コンテンツフラグメントエディターがページオーサリングとヘッドレス配信の両方にマークダウン構文を使用して、コンテンツを簡単に作成する仕組みを説明します。
feature: Content Fragments
role: User
exl-id: 4e9b076e-7429-466b-bb53-2164da379650
source-git-commit: 34574fdc7f246499bd238fef388671d2287e62bc
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 68%

---

# マークダウン {#markdown}

コンテンツフラグメントの編集者は、[オーサリング](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#authoring-your-content)の際、ページオーサリングとヘッドレス配信の両方で、*マークダウン*&#x200B;構文を使用してコンテンツを簡単に記述できます。

![Markdown エディター](/help/sites-cloud/administering/content-fragments/assets/cfm-markdown-01.png)

以下を定義できます。

* [見出し表記](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md#heading-notation)
* [段落と改行](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [リンク](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md#links)
* [画像](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md#images)
* [ブロック引用](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md#block-quotes)
* [リスト](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md#lists)
* [強調](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md#emphasis)
* [コードブロック](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md#code-blocks)
* [バックスラッシュエスケープ](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md#backslash-escapes)

## 見出し表記 {#heading-notation}

ヘッダーを作成するには、見出しの前にハッシュタグ (#) を配置します。 H1 には 1 つのハッシュタグ (#)、H2 には 2 つのハッシュタグ (##) が使用されます。 最大 6 個のハッシュタグを使用できます。 次に例を示します。

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

必要に応じて、H1 を作成するには、テキストに等号で下線を付け、マイナス記号で下線を付けて H2 を作成します。 次に例を示します。

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落と改行 {#paragraphs-and-line-breaks}

段落は、1 つ以上の空白行で区切られた、1 つ以上の連続したテキスト行です。 空白行とは、スペースやタブ以外を含まない行です。 通常の段落はスペースまたはタブでインデントされません。

改行するには、行の末尾に 2 つ以上のスペースを付けてからリターンします。

## リンク {#links}

インラインリンクと参照リンクを作成できます。

どちらのスタイルでも、リンクテキストはブラケット `[]` で囲みます。

インラインリンクの例を次に示します。

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

参照リンクの構文は次のとおりです。

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 画像 {#images}

画像の構文はリンクと似ています。インライン画像と参照画像を作成できます。

例えば、インライン画像の構文は次のようになります。

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

構文の内容は次のとおりです。

* 感嘆符：! 。
* 1 組のブラケットが後に続き、その中に画像の alt 属性テキストが含まれています。
* 1 組の丸括弧が後に続き、その中に画像の URL またはパスが含まれています。さらに、title 属性を二重引用符または一重引用符で囲んで指定することもできます。

参照スタイルの画像の構文は次のとおりです。

    `![Alt text][id]`

「id」は、定義された画像参照の名前です。画像参照は、次のようにリンク参照と同じ構文を使用して定義されます。

    `[id]: url/to/image "Optional title attribute"`

## ブロック引用 {#block-quotes}

テキストの前に > 記号を追加すると、テキストを引用できます。 次に例を示します。

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

ネストされたブロック引用符を使用できます。 次に例を示します。

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## リスト {#lists}

順序付きと順序なし両方のリストを作成できます。

順序なしリストを作成するには、* 記号をリストの項目の前に付けます。次に例を示します。

    `* item in list`

    `* item in list`

    `* item in list`

順序付きリストを作成するには、リスト内の各項目の前に数字とピリオドを 1 つ追加します。 次に例を示します。

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 強調 {#emphasis}

斜体または太字のスタイルをテキストに追加できます。

次のように斜体を追加できます。

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

次のようにテキストを太字にすることができます。

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

コードの範囲を示すには、バッククォート（&grave;）で囲みます。書式設定済みのコードブロックとは異なり、コード span は通常の段落内のコードを示します。

次に例を示します。

    ``Use the `printf()` function.``

## コードブロック {#code-blocks}

コードブロックは、通常、ソースコードを説明するために使用されます。 コードブロックを作成するには、タブを使用してコードをインデントするか、少なくとも 4 つのスペースを使用します。 次に例を示します。

    `This is a normal paragraph.`

        `This is a code block.`

## バックスラッシュエスケープ {#backslash-escapes}

書式設定構文で特殊な意味を持つリテラル文字を表示するには、バックスラッシュエスケープを使用します。例えば、ある単語を（HTML の &lt;em> タグではなく）リテラルアスタリスクで囲みたい場合は、次のようにアスタリスクの前にバックスラッシュを使用します。

    `\\*literal asterisks\\*`

バックスラッシュエスケープは次の文字に使用できます。

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
