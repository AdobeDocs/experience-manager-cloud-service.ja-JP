---
title: Markdown
description: オーサリング中に、コンテンツフラグメントエディターは Markdown 構文を使用してユーザーがコンテンツを簡単に記述できるようにします。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Markdown{#markdown}

When you are [authoring](/help/assets/content-fragments/content-fragments-variations.md#authoring-your-content), the content fragment editor uses *markdown* syntax to allow you to easily write content:

![MarkDown Editor](/help/assets/content-fragments/assets/cfm-markdown-01.png)

次を定義できます。

* [見出し表記](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [段落と改行](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [リンク](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [画像](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [ブロック引用](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [リスト](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [強調](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [コードブロック](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [バックスラッシュエスケープ](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## 見出し表記 {#heading-notation}

ハッシュタグ（#）を前に付けて見出しを作成します。H1 には 1 つのハッシュタグ（#）、H2 には 2 つのハッシュタグ（##）のように使用します。最大で 6 個のハッシュタグを使用できます。次に例を示します。

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

オプションで、テキストに等号で下線を付けて H1、マイナス符号で下線を付けて H2 を作成することもできます。次に例を示します。

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落と改行 {#paragraphs-and-line-breaks}

段落とは、1 つ以上の空白行によって区切られている、1 つ以上の連続したテキスト行です。空白行とは、スペースまたはタブしか含まれていない行です。通常の段落は、スペースやタブでインデントしないでください。

改行するには、行の末尾に 2 つ以上のスペースを付けてからリターンします。

## リンク {#links}

インラインリンクと参照リンクを作成できます。

In both styles, the link text is delimited by square brackets `[]`.

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

* 感嘆符：!;
* 続いて角括弧が続き、画像のalt属性テキストが含まれます。
* 括弧の後に続き、画像のURLまたはパス、および二重引用符または一重引用符で囲まれたオプションのtitle属性が含まれます。

参照スタイルの画像の構文は次のとおりです。

    `![Alt text][id]`

ここで「id」は、定義された画像参照の名前です。 画像参照は、次のようにリンク参照と同じ構文を使用して定義されます。

    `[id]: url/to/image "Optional title attribute"`

## ブロック引用 {#block-quotes}

テキストを引用するときは、テキストの先頭に > 記号を付けます。次に例を示します。

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

ブロック引用はネストできます。次に例を示します。

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## リスト {#lists}

順序付きと順序なし両方のリストを作成できます。

順不同リストを作成するには、&amp;ast；を使用します。記号を追加します。 次に例を示します。

    `* item in list`

    `* item in list`

    `* item in list`

順序付きリストを作成するには、数字の後にピリオドを付けて、リストの項目の前に付けます。次に例を示します。

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

コードの範囲を示すには、バッククォート（`）で囲みます。事前に書式設定されたコードブロックとは異なり、コード範囲は通常の段落内のコードを示します。

次に例を示します。

    ``Use the `printf()` function.``

## コードブロック {#code-blocks}

コードブロックは通常はソースコードを示すために使用されます。コードブロックを作成するには、1 個のタブまたは少なくとも 4 個分のスペースを使用してコードをインデントします。次に例を示します。

    `This is a normal paragraph.`

        `This is a code block.`

## バックスラッシュエスケープ {#backslash-escapes}

書式設定構文で特殊な意味を持つリテラル文字を表示するには、バックスラッシュエスケープを使用します。例えば、単語をリテラルアスタリスクで囲む場合（HTML &lt;em>タグの代わりに）、次のようにアスタリスクの前に円記号を使用できます。

    `\\*literal asterisks\\*`

バックスラッシュエスケープは次の文字に使用できます。

    `\ backslash`

    ` バッククォート

    `* asterisk`

    `_ underscore`

    `{} curly braces`

    `[] square brackets`

    `() parentheses`

    `# hash mark`

    `+ plus sign`

    `- minus sign (hyphen)`

    `. dot`
